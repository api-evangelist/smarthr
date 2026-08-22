# SmartHR (smarthr)

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

SmartHR is a leading Japanese cloud HR, labor, and personnel management SaaS (smarthr.jp). Its public developer API is a **per-tenant REST API**: every customer accesses it at their own subdomain, `https://{tenant}.smarthr.jp/api`, with all resources under a `/v1` path (for example `GET /v1/crews`). There is no single shared API host - the OpenAPI in this repo models the tenant as a server variable rather than a fabricated fixed host.

**Access model (be honest up front):**

- **Per-tenant host** - `https://{tenant}.smarthr.jp/api`, where `{tenant}` is the customer's SmartHR subdomain. A separate Sandbox environment is offered for testing.
- **Auth** - a per-tenant **access token** issued from the SmartHR admin console (OAuth2 access tokens are used for registered apps), passed as `Authorization: Bearer ACCESS_TOKEN`. HTTP Basic with the token as the username (`curl -u ACCESS_TOKEN`) is also accepted.
- **Region** - Japan. The API reference and most documentation are in Japanese.
- **Transport** - request/response REST over HTTPS, plus outbound **webhooks** for change notifications. No WebSocket API is documented.
- **Rate limits** - 5,000 requests/hour and 10 requests/second per access token; 50,000 requests/minute per subdomain.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/smarthr/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/smarthr/refs/heads/main/apis.yml)

## Grounding and fidelity

The six API groups below, the per-tenant base host, and the `/v1` paths are grounded against SmartHR's published API-overview documentation and the endpoint paths in the community Go SDK ([ktsujichan/smarthr-sdk-go](https://github.com/ktsujichan/smarthr-sdk-go)). Request/response property shapes are representative and modeled from the documented object semantics. SmartHR's official API reference documents **additional real resources** (dependents, bank accounts, payrolls, positions/job titles, tags, companies) that are intentionally **not modeled** here rather than guessed - see `review.yml` for the confirmed-vs-not-modeled breakdown.

## Tags

- HR
- Human Resources
- HRIS
- Labor Management
- Payroll
- Japan
- Employees
- Personnel
- Onboarding
- SaaS

## Timestamps

- **Created:** 2026-07-12
- **Modified:** 2026-07-12

## APIs

### SmartHR Crews API

List, create, get, update, delete, and invite employee ("crew") records - the core personnel objects in SmartHR - with pagination, sorting, and filtering by employment status.

- **Human URL:** [https://developer.smarthr.jp/api](https://developer.smarthr.jp/api)
- **Base URL:** `https://{tenant}.smarthr.jp/api`

#### Tags

- Crews
- Employees
- Personnel

#### Properties

- [Documentation](https://developer.smarthr.jp/api/about_api)
- [API Reference](https://developer.smarthr.jp/api)
- [OpenAPI](openapi/smarthr-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/smarthr.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/smarthr.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### SmartHR Departments API

Manage the organizational departments that crews belong to - create, list, get, update, and delete departments, including parent/child hierarchy and display ordering.

- **Human URL:** [https://developer.smarthr.jp/api](https://developer.smarthr.jp/api)
- **Base URL:** `https://{tenant}.smarthr.jp/api`

#### Tags

- Departments
- Organization

#### Properties

- [API Reference](https://developer.smarthr.jp/api)
- [OpenAPI](openapi/smarthr-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/smarthr.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/smarthr.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### SmartHR Employment Types API

Manage employment type master data (full-time, part-time, contract, and custom types) - create, list, get, update, and delete employment types referenced by crew records.

- **Human URL:** [https://developer.smarthr.jp/api](https://developer.smarthr.jp/api)
- **Base URL:** `https://{tenant}.smarthr.jp/api`

#### Tags

- Employment Types
- Master Data

#### Properties

- [API Reference](https://developer.smarthr.jp/api)
- [OpenAPI](openapi/smarthr-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/smarthr.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/smarthr.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### SmartHR Custom Field Templates API

Define and manage the custom field templates that attach additional, organization-specific fields to crew records - text, number, date, enum, and file field types with choice elements.

- **Human URL:** [https://developer.smarthr.jp/api](https://developer.smarthr.jp/api)
- **Base URL:** `https://{tenant}.smarthr.jp/api`

#### Tags

- Custom Fields
- Templates

#### Properties

- [API Reference](https://developer.smarthr.jp/api)
- [OpenAPI](openapi/smarthr-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/smarthr.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/smarthr.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### SmartHR Business Establishments API

List the business establishments (jigyosho) registered for the tenant, used for social insurance and labor administration filings.

- **Human URL:** [https://developer.smarthr.jp/api](https://developer.smarthr.jp/api)
- **Base URL:** `https://{tenant}.smarthr.jp/api`

#### Tags

- Business Establishments
- Social Insurance

#### Properties

- [API Reference](https://developer.smarthr.jp/api)
- [OpenAPI](openapi/smarthr-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/smarthr.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/smarthr.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### SmartHR Webhooks API

Create, list, get, update, and delete webhook subscriptions so external systems are notified when crews and other records change - for example to auto-provision cloud accounts at onboarding.

- **Human URL:** [https://developer.smarthr.jp/api/about_webhook](https://developer.smarthr.jp/api/about_webhook)
- **Base URL:** `https://{tenant}.smarthr.jp/api`

#### Tags

- Webhooks
- Events
- Notifications

#### Properties

- [Documentation](https://developer.smarthr.jp/api/about_webhook)
- [API Reference](https://developer.smarthr.jp/api)
- [OpenAPI](openapi/smarthr-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/smarthr.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/smarthr.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Domain Security](security/smarthr-domain-security.yml)
- [Authentication](authentication/smarthr-authentication.yml)
- [GitHub Organization](https://github.com/kufu)
- [LinkedIn](https://www.linkedin.com/company/smarthr)
- [Website](https://smarthr.jp/)
- [Documentation](https://developer.smarthr.jp/)
- [Plans](plans/smarthr-plans-pricing.yml)
- [Rate Limits](rate-limits/smarthr-rate-limits.yml)
- [Fin Ops](finops/smarthr-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
