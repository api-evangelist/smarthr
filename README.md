# SmartHR (smarthr)

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
