---
name: chaoss-collectoss-compare-repo-group
description: Compare the repositories inside one CollectOSS repo group — an organization or ecosystem — to rank activity, contributor load and risk across a portfolio.
api: CollectOSS REST API
provider: CHAOSS
providerId: chaoss
generated: '2026-09-05'
method: generated
source: >-
  Grounded in openapi/chaoss-collectoss-openapi.yml. Every operationId below was grepped from that
  contract.
operations:
  - Get All Repo Groups
  - Get Repos in Repo Group
  - Get Top Insights
  - Aggregate Summary (Repo Group)
  - Annual Commit Count Ranked by Repo in Repo Group (Repo Group)
  - Annual Lines of Code Ranked by Repo in Repo Group (Repo Group)
  - Top Committers (Repo Group)
  - Contributors (Repo Group)
  - New Contributors (Repo Group)
  - Issue Backlog (Repo Group)
  - Issue Throughput (Repo Group)
  - License Coverage (Repo Group)
  - License Declared (Repo Group)
  - CII Best Practices Badge (Repo Group)
  - Stars Count (Repo Group)
---

# Compare repositories across a repo group

A **repo group** is CollectOSS's portfolio unit — usually a GitHub or GitLab organization, or a
curated ecosystem. The documentation's own example is a group named "Rails" of type
"GitHub Organization". Groups are created by the operator with `collectoss db add-repo-groups`.

## Step 1 — find the group

```
GET /api/unstable/repo-groups                              # Get All Repo Groups
GET /api/unstable/repo-groups/{repo_group_id}/repos        # Get Repos in Repo Group
```

`Get All Repo Groups` returns `repo_group_id`, `rg_name`, `rg_description`, `rg_type`, `rg_website`
and collection metadata. As with `repo_id`, **`repo_group_id` is instance-local** — never treat it
as a global identifier.

## Step 2 — group-level aggregates

Every repository metric has a `(Repo Group)` twin under `/repo-groups/:repo_group_id/`. The useful
portfolio ones:

| Operation | Path |
| --- | --- |
| `Contributors (Repo Group)` | `/repo-groups/:repo_group_id/contributors` |
| `New Contributors (Repo Group)` | `/repo-groups/:repo_group_id/contributors-new` |
| `Issue Backlog (Repo Group)` | `/repo-groups/:repo_group_id/issue-backlog` |
| `Issue Throughput (Repo Group)` | `/repo-groups/:repo_group_id/issue-throughput` |
| `License Coverage (Repo Group)` | `/repo-groups/:repo_group_id/license-coverage` |
| `License Declared (Repo Group)` | `/repo-groups/:repo_group_id/license-declared` |
| `CII Best Practices Badge (Repo Group)` | `/repo-groups/:repo_group_id/cii-best-practices-badge` |
| `Stars Count (Repo Group)` | `/repo-groups/:repo_group_id/stars-count` |

## Step 3 — rankings (experimental — label them as such)

| Operation | Path |
| --- | --- |
| `Annual Commit Count Ranked by Repo in Repo Group (Repo Group)` | `/repo-groups/:repo_group_id/annual-commit-count-ranked-by-repo-in-repo-group` |
| `Annual Lines of Code Ranked by Repo in Repo Group (Repo Group)` | `/repo-groups/:repo_group_id/annual-lines-of-code-count-ranked-by-repo-in-repo-group` |
| `Top Committers (Repo Group)` | `/repo-groups/:repo_group_id/top-committers` |
| `Aggregate Summary (Repo Group)` | `/repo-groups/:repo_group_id/aggregate-summary` |

All four are tagged **`experimental`** in the contract. Their definitions are not stable — carry that
caveat into anything you report.

## Step 4 — insights

```
GET /api/unstable/repo-groups/{repo_group_id}/top-insights     # Get Top Insights
```

Returns machine-generated summarizations produced during collection, not computed at read time.

## Routing trap you must handle

Twelve operations are mounted under a prefix that contradicts their own path parameter. Eleven
repo-scoped metrics live under the **`/repo-groups/`** prefix while taking `:repo_id`:

- `/repo-groups/:repo_id/languages`
- `/repo-groups/:repo_id/license-count`
- `/repo-groups/:repo_id/open-issues-count`
- `/repo-groups/:repo_id/abandoned-issues`
- `/repo-groups/:repo_id/issue-duration`
- `/repo-groups/:repo_id/pull-requests-new`
- `/repo-groups/:repo_id/lines-changed-by-author`
- the four `/repo-groups/:repo_id/annual-*-ranked-by-*-repo-in-repo-group` variants

And `/repos/:repo_group_id/releases` inverts it the other way. **Do not route on the path prefix** —
read the parameter name. Sending a `repo_group_id` where a `repo_id` is expected will silently
return the wrong thing.

Three operationIds are also duplicated across the 137 operations ("Number of Releases (Repo)",
"Open Issues Count (Repo Group)", "New Contributor Counts Stacked Bar Chart (shows actions)"), so do
not key a client on operationId alone.

## Rules

- No pagination anywhere. A large group returns everything at once.
- Read the `status` field in the body; HTTP 200 is not proof of success.
- No rate-limit headers exist — self-throttle.
- Use `begin_date` / `end_date` / `period` as **query** parameters even though the contract types
  them `in: path`.
