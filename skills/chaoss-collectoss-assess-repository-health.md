---
name: chaoss-collectoss-assess-repository-health
description: Produce a CHAOSS-aligned community health profile for one repository from a CollectOSS instance, covering the Evolution, Risk and Value focus areas.
api: CollectOSS REST API
provider: CHAOSS
providerId: chaoss
generated: '2026-09-05'
method: generated
source: >-
  Grounded in openapi/chaoss-collectoss-openapi.yml. Every operationId below was grepped from that
  contract; metric semantics come from https://www.chaoss.community/kb-metrics-and-metrics-models/.
operations:
  - Get Repo by Owner and Repo Name
  - Code Changes (Repo)
  - Code Changes Lines (Repo)
  - Contributors (Repo)
  - New Contributors (Repo)
  - Committers (Repo)
  - Issue Backlog (Repo)
  - Issue Throughput (Repo)
  - Issue Response Time (Repo)
  - Closed Issue Resolution Duration (Repo)
  - Reviews (Repo)
  - Review Duration (Repo)
  - Reviews Accepted (Repo)
  - Reviews Declined (Repo)
  - License Coverage (Repo)
  - License Declared (Repo)
  - CII Best Practices Badge (Repo)
  - Fork Count (Repo)
  - Stars Count (Repo)
  - Watchers Count (Repo)
  - Project Languages (repo)
  - Total Lines (repo)
  - File Complexity (repo)
---

# Assess a repository's community health

## Step 0 — resolve the identifier. Do not skip this.

`repo_id` is assigned by the local PostgreSQL instance. **It is not portable** — `repo_id` 21996 on
one CollectOSS deployment is a different repository on another. Always resolve first:

```
GET /api/unstable/owner/{owner}/repo/{repo}      # Get Repo by Owner and Repo Name
```

If the repository is not tracked on this instance, nothing below will return data. The operator adds
repositories through the CLI (`collectoss db add-repos`), not through the API.

## Step 1 — Evolution (how the work is going)

Pick a `begin_date` / `end_date` window and a `period` bucket, and call:

| Operation | Path | Tells you |
| --- | --- | --- |
| `Code Changes (Repo)` | `/repos/:repo_id/code-changes` | Commit volume over time |
| `Code Changes Lines (Repo)` | `/repos/:repo_id/code-changes-lines` | Lines added/removed |
| `Contributors (Repo)` | `/repos/:repo_id/contributors` | Who is active |
| `New Contributors (Repo)` | `/repos/:repo_id/contributors-new` | Whether the funnel is filling |
| `Committers (Repo)` | `/repos/:repo_id/committers` | Commit-bearing contributor count |
| `Issue Backlog (Repo)` | `/repos/:repo_id/issue-backlog` | Open issue debt |
| `Issue Throughput (Repo)` | `/repos/:repo_id/issue-throughput` | Closed vs opened |
| `Issue Response Time (Repo)` | `/repos/:repo_id/issues-maintainer-response-duration` | Maintainer responsiveness |
| `Closed Issue Resolution Duration (Repo)` | `/repos/:repo_id/issues-closed-resolution-duration` | Time to close |
| `Reviews (Repo)` / `Review Duration (Repo)` | `/repos/:repo_id/reviews`, `/review-duration` | Review load and latency |
| `Reviews Accepted (Repo)` / `Reviews Declined (Repo)` | `/repos/:repo_id/reviews-accepted`, `/reviews-declined` | Review outcomes |

**Contract trap:** the spec declares `period`, `begin_date` and `end_date` as `in: path` even though
only `repo_id` appears in the path template. Send them as **query parameters**. A generator that
follows the contract literally builds an unusable URL.

## Step 2 — Risk

| Operation | Path |
| --- | --- |
| `License Coverage (Repo)` | `/repos/:repo_id/license-coverage` |
| `License Declared (Repo)` | `/repos/:repo_id/license-declared` |
| `CII Best Practices Badge (Repo)` | `/repos/:repo_id/cii-best-practices-badge` |
| `Fork Count (Repo)` | `/repos/:repo_id/fork-count` |

`CII Best Practices Badge (Repo)` returns the OpenSSF Best Practices badge level — a standard
CollectOSS reads rather than defines.

## Step 3 — Value and complexity

- `Stars Count (Repo)` → `/repos/:repo_id/stars-count`
- `Watchers Count (Repo)` → `/repos/:repo_id/watchers-count`
- `Project Languages (repo)` → `/complexity/project_languages`
- `Total Lines (repo)` → `/complexity/project_lines`
- `File Complexity (repo)` → `/complexity/project_file_complexity`

The `/complexity/*` operations take `repo_id` as a **query** parameter (correctly declared, unlike
the metric endpoints above).

## Rules to apply throughout

- **Read the body, not the status code.** Seven of the nine catalogued failure modes come back as
  HTTP 200 with a `status` string. See `errors/chaoss-problem-types.yml`.
- **There is no pagination.** Nothing you call here pages, and `Get All Repos` returns every tracked
  repository in a single array. Cap response size client-side.
- **There are no rate-limit headers and no 429** in the contract. Throttle yourself; the instance
  operator has not told you what it can take.
- **Avoid the `experimental` tag** for anything reportable. 26 operations — Aggregate Summary, the
  annual-count rankings, Pull Request Acceptance Rate, Abandoned Issues, Top Committers — are tagged
  `experimental` in the contract and their definitions are not stable.
- **Contributor responses include `name` and `email`.** That is personal data harvested from public
  forges. Do not cache or re-publish it without a reason.
- **Everything sits under `/api/unstable/`.** The provider is telling you in the URL that the
  interface is not stabilised.

## What you cannot do here

There is no operation that writes a health assessment back, no webhook to subscribe to for changes,
and no event stream. This is a read-only pull.
