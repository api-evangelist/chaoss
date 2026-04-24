# CHAOSS (chaoss)

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
