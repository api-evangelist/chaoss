---
name: chaoss-collectoss-authenticate
description: Obtain and maintain an authenticated session against a self-hosted CollectOSS instance using its OAuth 2.0 authorization code flow.
api: CollectOSS REST API
provider: CHAOSS
providerId: chaoss
generated: '2026-09-05'
method: generated
source: >-
  Grounded in https://docs.collectoss.org/en/latest/login.html and the login operations in
  openapi/chaoss-collectoss-openapi.yml. Every operationId below was grepped from that contract.
operations:
  - Generate User Session Token
  - Refresh User Session Token
---

# Authenticate against a CollectOSS instance

## Before you start

There is no CHAOSS-operated CollectOSS server and no central identity provider. **Every CollectOSS
deployment is its own OAuth authorization server.** You need the base URL of the specific instance
you are calling; the documentation writes it as `https://collectoss.example.com`. Substitute the
real host everywhere below.

## Prerequisites (human steps — an agent cannot do these)

1. Register a user account on the target instance: **Login → Register**.
2. Open **your username → Profile → Applications**.
3. Create an application with a name and a redirect URL that the *user's browser* can reach.
4. Record the **Application ID** and the **Client Secret**.

For local testing the docs allow `http://127.0.0.1/` or `http://localho.st` as the redirect host,
and warn that the authorization server does not check that the redirect URL is reachable.

If the instance sits behind Nginx or Apache, the operator must set
`proxy_set_header X-Forwarded-Proto $scheme;` or the flow will not complete.

## Step 1 — send the user to the authorization server

The flow **must be started by an explicit user action**. The documentation is direct about this:
your application "must not request initial authorization on the user's behalf, and must not
automatically redirect the user to the authorization server."

```
GET https://collectoss.example.com/user/authorize
  ?client_id=<Application ID>
  &response_type=code
  &state=<your opaque value>
```

## Step 2 — receive the temporary code

The user approves on a verification page and is redirected back:

```
https://your.app/redirect?code=<temporary code>&state=<your value>
```

Compare `state` to what you sent. **Exchange the code immediately.** It is one-time use and valid
for seconds only; the docs forbid storing it for any longer than the exchange takes.

## Step 3 — exchange the code (`Generate User Session Token`)

```
POST https://collectoss.example.com/api/unstable/user/session/generate
  ?code=<temporary code>
  &grant_type=code
Authorization: Client <Client Secret>
```

Note the arguments go on the **query string**, not in a form body — this is a deviation from
RFC 6749 §4.1.3.

Success returns `status: "Validated"` plus `username`, `access_token`, `refresh_token`,
`token_type` and `expires` (seconds until the access token dies).

## Step 4 — call the API

Both credentials go in **one** header, comma-separated:

```
Authorization: Client <Client Secret>, Bearer <User Session Token>
```

This is not RFC 7235 credential syntax. Most generated SDKs assume a single scheme per header and
will need a manual override.

## Step 5 — refresh (`Refresh User Session Token`)

```
POST https://collectoss.example.com/api/unstable/user/session/refresh
  ?refresh_token=<refresh token>
  &grant_type=refresh_token
Authorization: Client <Client Secret>
```

**This call is destructive and has no undo.** If the returned bearer token differs from your current
one, the old bearer token *and* the old refresh token are both invalid. Persist the new pair before
doing anything else — there is no token-revocation or token-recovery endpoint in the contract, so
losing this response means restarting the whole flow with fresh user intent.

A refresh token may only be used by the application that issued it.

## Error handling — read the body, not the status code

Both token operations return **HTTP 200 on failure** with the reason in a `status` string:

| `status` | Meaning | What to do |
| --- | --- | --- |
| `Validated` | Success | Continue |
| `Invalid grant type` | Wrong `grant_type` for this endpoint | Use `code` on generate, `refresh_token` on refresh |
| `Invalid authorization code` | Code expired or already used | Restart the flow from Step 1 |
| `Invalid user` | No such account on this instance | The user must register on this instance |
| `Invalid refresh token` | Token rotated or revoked | Restart the flow from Step 1 |
| `Invalid application` | Refresh token belongs to another app | Use the issuing app's client secret |

Never treat `HTTP 200` as success on these two operations. Check `status` first.

## What is not available

There are **no OAuth scopes**. Authorization is all-or-nothing per Client Application, so you cannot
request least privilege. See `scopes/chaoss-scopes.yml`.
