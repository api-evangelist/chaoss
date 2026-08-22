# CHAOSS (chaoss)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

CHAOSS (Community Health Analytics in Open Source Software) is a Linux Foundation project that develops metrics, methodologies, software, and practitioner guides for measuring and improving open source community health and sustainability. It produces a metrics catalog organized into focus areas (Common, DEI, Risk, Value, Evolution) and metrics models, along with open source software (Augur, 8Knot, GrimoireLab) that ingests data from Git, GitHub, GitLab, mailing lists, and other community platforms to compute the metrics. CHAOSS-aligned SaaS services such as OSS Compass and Bitergia Analytics also expose the metrics for adopters who do not want to host the software themselves.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/chaoss/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Producer
- **Access:** Open Source
- **x-type:** opensource

## Tags

- Analytics, Community Health, DEI, Linux Foundation, Metrics, Observability, Open Source, Risk, Sustainability

## Timestamps

- **Created:** 2026-03-16
- **Modified:** 2026-04-23

## APIs

### CHAOSS Augur REST API

Augur is a CHAOSS reference implementation that collects data from GitHub, GitLab, mailing lists, and other community sources, and exposes a REST API for querying CHAOSS-aligned metrics on repositories, contributors, issues, pull requests, releases, and more. The API powers downstream analytics tools and dashboards including 8Knot.

**Human URL:** [https://oss-augur.readthedocs.io/](https://oss-augur.readthedocs.io/)
**Base URL:** `https://ai.chaoss.io/api`

#### Tags

- Augur, Community Health, Metrics, REST

#### Properties

- [Documentation](https://oss-augur.readthedocs.io/)
- [GitHub Repository](https://github.com/chaoss/augur)
- [API Reference](https://oss-augur.readthedocs.io/en/dev/rest-api/api.html)

### CHAOSS Metrics Catalog

The CHAOSS Metrics catalog is a community-maintained, structured reference of community-health metrics organized into focus areas (Common, DEI, Risk, Value, Evolution) plus metrics models that compose them. The catalog is openly licensed and published on the CHAOSS website and the chaoss/metrics GitHub repository, and is consumed by Augur, GrimoireLab, OSS Compass, Bitergia Analytics, and other implementations.

**Human URL:** [https://chaoss.community/metrics/](https://chaoss.community/metrics/)

#### Tags

- Catalog, Documentation, Metrics, Models

#### Properties

- [Documentation](https://chaoss.community/kbtopic/all-metrics/)
- [Metrics Models GitHub](https://github.com/chaoss/wg-metrics-models)
- [Community Repository](https://github.com/chaoss/community)

### CHAOSS GrimoireLab

GrimoireLab is an open source platform for software development analytics. It pulls data from 30+ data sources (Git, GitHub, GitLab, mailing lists, IRC, Slack, Jira, Bugzilla, etc.) and provides a Python toolkit (Perceval, Sortinghat, GrimoireELK) plus a Kibana-based dashboard, exposing CHAOSS metrics for community health analysis.

**Human URL:** [https://chaoss.github.io/grimoirelab/](https://chaoss.github.io/grimoirelab/)

#### Tags

- Analytics, Data Pipeline, GrimoireLab, Kibana, Metrics

#### Properties

- [Documentation](https://chaoss.github.io/grimoirelab/)
- [GitHub Repository](https://github.com/chaoss/grimoirelab)

### CHAOSS 8Knot Dashboard

8Knot is an open source community analytics dashboard built on top of Augur that provides ready-made visualizations of CHAOSS metrics for stakeholders evaluating open source project health.

**Human URL:** [https://github.com/oss-aspen/8knot](https://github.com/oss-aspen/8knot)

#### Tags

- Dashboard, Visualization

#### Properties

- [Documentation](https://github.com/oss-aspen/8knot)
- [GitHub Repository](https://github.com/oss-aspen/8knot)

## Common Properties

- [Website](https://chaoss.community/)
- [Documentation](https://chaoss.community/kbtopic/all-metrics/)
- [GitHub](https://github.com/chaoss)
- [Working Groups](https://chaoss.community/working-groups/)
- [Events](https://chaoss.community/events/)
- [Blog](https://chaoss.community/news-blog/)
- [Practitioner Guides](https://chaoss.community/practitioner-guides/)
- [Parent Organization (Linux Foundation)](https://www.linuxfoundation.org/)
- [Getting Started](https://chaoss.community/get-started/)
- [Community](https://chaoss.community/participate/)
- [Slack](https://chaoss.community/connect/)
- [YouTube](https://www.youtube.com/c/CHAOSScommunity)
- [LinkedIn](https://www.linkedin.com/company/chaoss-community/)
- [X](https://x.com/chaossproj)

## Features

Community Health Metrics, Metrics Models, DEI Metrics, Risk Metrics, Value Metrics, Evolution Metrics, Common Metrics, Open Source Software, Practitioner Guides, Working Groups, Reference Implementations, REST API (Augur), Data Pipeline (GrimoireLab), Dashboards (8Knot, Bitergia), SaaS Adopter Services

## Use Cases

Open Source Project Health Assessment, Contributor Sustainability Analysis, DEI in Open Source Communities, Open Source Risk and Security Assessment, Open Source Investment ROI, Funding Impact Measurement, Community Onboarding Improvement, Foundation-Level Reporting, OSPO Health Reporting, Maintainer Burnout Detection

## Tools

Augur, GrimoireLab, 8Knot, Bitergia Analytics, OSS Compass, Cauldron, Sortinghat, Perceval, GrimoireELK

## Working Groups

Common Metrics, DEI Metrics, Risk Metrics, Value Metrics, Evolution Metrics, Software (Augur and GrimoireLab), Education, Practitioner Guides

## Integrations

GitHub, GitLab, Bitbucket, Git, Mailing Lists, Jira, Bugzilla, Discourse, Slack, IRC, Stack Exchange, Meetup, Linux Foundation, CNCF, Apache Software Foundation, OpenSSF

## Maintainers

**FN:** Kin Lane

**Email:** info@apievangelist.com
