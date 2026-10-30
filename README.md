# MedTrainer

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

MedTrainer is a healthcare workforce compliance software company that consolidates learning management, credentialing and provider enrollment, document and policy management, incident reporting, safety plans, contract management and exclusion/sanction monitoring into a single all-in-one platform for medical practices, ambulatory surgery centers, urgent care, behavioral health, dental groups, community health centers and long-term care organizations. The company publishes a MedTrainer Public API at api.medtrainer.com, documented with an OpenAPI 3.1 definition rendered through Redoc, that lets external integrations search and manage the core provider directory — locations, divisions, departments, positions, practitioner categories and practitioners. The API is notable for being FHIR-aligned: resource payloads use HL7 FHIR shapes and the application/fhir+json media type, searches return FHIR Bundle envelopes with FHIR search parameters (_count, _page, _elements), and every error is returned as a FHIR OperationOutcome. Access is customer-gated behind an API key generated from the platform Organization settings, and the wider platform authenticates against an Auth0-backed OpenID Connect provider at auth.medtrainer.com.

**Areas:** Company · Healthcare · Compliance · Credentialing · LMS · Provider Directory · FHIR · HL7 · Training · Risk Management · Software-as-a-Service

## MedTrainer on APIs.io

Everything profiled for MedTrainer is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/medtrainer/](https://apis.io/providers/medtrainer/)** — or go straight to one of the APIs or properties below.

### APIs (6)

- [MedTrainer Departments API](https://apis.io/apis/medtrainer/medtrainer-departments-api/) — Public department lookup endpoints
- [MedTrainer Divisions API](https://apis.io/apis/medtrainer/medtrainer-divisions-api/) — Public division lookup and mutation endpoints
- [MedTrainer Locations API](https://apis.io/apis/medtrainer/medtrainer-locations-api/) — Public location lookup and mutation endpoints
- [MedTrainer Positions API](https://apis.io/apis/medtrainer/medtrainer-positions-api/) — Public position lookup endpoints
- [MedTrainer Practitioner Categories API](https://apis.io/apis/medtrainer/medtrainer-practitioner-categories-api/) — Public practitioner category lookup endpoints
- [MedTrainer Practitioners API](https://apis.io/apis/medtrainer/medtrainer-practitioners-api/) — Public practitioner lookup, search, and mutation endpoints

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [MedTrainer MCP Server (WordPress MCP Adapter)](https://apis.io/servers/medtrainer/medtrainer-mcp-server-wordpress-mcp-adapter/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Medtrainer Public Api Overlay](https://apis.io/overlays/medtrainer/medtrainer-public-api-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Medtrainer Authentication](https://apis.io/security/medtrainer/medtrainer-authentication/)
- [Medtrainer Domain Security](https://apis.io/security/medtrainer/medtrainer-domain-security/)
- [Medtrainer Vulnerability Disclosure](https://apis.io/security/medtrainer/medtrainer-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Medtrainer Scopes](https://apis.io/scopes/medtrainer/medtrainer-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Medtrainer Plans Pricing](https://apis.io/plans/medtrainer/medtrainer-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Medtrainer Rate Limits](https://apis.io/rate-limits/medtrainer/medtrainer-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://medtrainer.com/)
- [Documentation](https://api.medtrainer.com/docs)
- [Getting started](https://api.medtrainer.com/docs#section/Getting-started)
- [API reference](https://api.medtrainer.com/docs)
- [Pricing](https://medtrainer.com/pricing/)
- [Sign up](https://medtrainer.com/demo/)
- [Support](https://support.medtrainer.com/)
- [Blog](https://medtrainer.com/blog/)
- [Security](https://medtrainer.com/security/)
- [Terms of service](https://medtrainer.com/terms/)
- [Privacy policy](https://medtrainer.com/privacy/)

## API Evangelist rating

**Kin Score 55.9** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 50.2 |
| Contract governance | 18.2 |
| Operational transparency | 10.5 |
| Developer ergonomics | 58.9 |
| Access clarity | 84.2 |

**Agent readiness 44.9** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | platform (partial credit) |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 41.4** — Health

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/medtrainer/](https://apis.io/providers/medtrainer/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for MedTrainer: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/medtrainer/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
