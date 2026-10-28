# Agent Disco

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

Agent Disco grades any public website for AI-agent discoverability. Operated by Starsol Ltd (Norwich, England), it fetches the handful of URIs agent runtimes actually read - robots.txt rules for GPTBot and ClaudeBot, llms.txt, /.well-known/ai-plugin.json, agent.json and mcp.json, OpenAPI specs, SDK and registry signals, TLS and anti-bot posture - and returns a letter grade A-F with a per-category breakdown, fix hints and an embeddable badge. A public REST API under /api/v1 (OpenAPI 3.1, Swagger UI) submits scans, polls results, diffs scans, manages API keys and signed scan.completed webhooks, and lets autonomous agents sign in with a Colony identity through OAuth 2.0 Token Exchange (RFC 8693).

**Areas:** AI Agents · Agent Discoverability · Website Auditing · Developer Tools · Webhook · llms-txt · A2A · MCP · Scanning

## Agent Disco on APIs.io

Everything profiled for Agent Disco is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/agentdisco-io/](https://apis.io/providers/agentdisco-io/)** — or go straight to one of the APIs or properties below.

### APIs (8)

- [Agent Disco Checks API](https://apis.io/apis/agentdisco-io/agentdisco-io-checks-api/) — The Checks API from Agent Disco — 1 operation(s) for checks.
- [Agent Disco Keys API](https://apis.io/apis/agentdisco-io/agentdisco-io-keys-api/) — The Keys API from Agent Disco — 3 operation(s) for keys.
- [Agent Disco Ops API](https://apis.io/apis/agentdisco-io/agentdisco-io-ops-api/) — The Ops API from Agent Disco — 2 operation(s) for ops.
- [Agent Disco Scans API](https://apis.io/apis/agentdisco-io/agentdisco-io-scans-api/) — The Scans API from Agent Disco — 3 operation(s) for scans.
- [Agent Disco Unlist API](https://apis.io/apis/agentdisco-io/agentdisco-io-unlist-api/) — The Unlist API from Agent Disco — 4 operation(s) for unlist.
- [Agent Disco Webhooks API](https://apis.io/apis/agentdisco-io/agentdisco-io-webhooks-api/) — The Webhooks API from Agent Disco — 2 operation(s) for webhooks.
- [Agent Disco Websites API](https://apis.io/apis/agentdisco-io/agentdisco-io-websites-api/) — The Websites API from Agent Disco — 5 operation(s) for websites.
- [Agent Disco Open API](https://apis.io/apis/agentdisco-io/agentdisco-io-open-api-api/) — OpenAPI

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Agentdisco Io Webhooks](https://apis.io/asyncapis/agentdisco-io/agentdisco-io-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [agent-disco](https://apis.io/servers/agentdisco-io/agent-disco/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Agentdisco Io Openapi Overlay](https://apis.io/overlays/agentdisco-io/agentdisco-io-openapi-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Agentdisco Io Authentication](https://apis.io/security/agentdisco-io/agentdisco-io-authentication/)
- [Agentdisco Io Domain Security](https://apis.io/security/agentdisco-io/agentdisco-io-domain-security/)
- [Agentdisco Io Vulnerability Disclosure](https://apis.io/security/agentdisco-io/agentdisco-io-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Agentdisco Io Plans Pricing](https://apis.io/plans/agentdisco-io/agentdisco-io-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Agentdisco Io Rate Limits](https://apis.io/rate-limits/agentdisco-io/agentdisco-io-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://agentdisco.io/)
- [Documentation](https://agentdisco.io/developers)
- [Getting started](https://agentdisco.io/llms-full.txt)
- [API reference](https://agentdisco.io/api/docs)
- [Pricing](https://agentdisco.io/developers)
- [Sign up](https://agentdisco.io/register)
- [Support](https://agentdisco.io/contact)
- [Terms of service](https://agentdisco.io/terms)
- [Privacy policy](https://agentdisco.io/privacy)
- [GitHub](https://github.com/agentdisco)

## API Evangelist rating

**Kin Score 60.9** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 53.9 |
| Contract governance | 18.2 |
| Operational transparency | 55.3 |
| Developer ergonomics | 63.7 |
| Access clarity | 76.3 |

**Agent readiness 50.2** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | flavored (partial credit) |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 38.2** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/agentdisco-io/](https://apis.io/providers/agentdisco-io/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Agent Disco: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/agentdisco-io/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
