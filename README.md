# Sift (sift)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Sift is a digital trust and safety platform that uses machine learning to detect and prevent online fraud and abuse - payment fraud, account takeover, account abuse, content abuse, and promotion abuse. Applications stream user events to the Sift Events API, retrieve real-time risk Sift Scores (0-100) per abuse type, and act on them through the Decisions API, automated Workflows, verification (OTP), and PSP merchant risk management.

## Access Model (Honest Summary)

- **Public, documented REST API** over HTTPS at `https://api.sift.com`. Interactive docs at [developers.sift.com](https://developers.sift.com/docs).
- **Authentication is by API key.** Ingestion APIs (Events, Score, Labels) accept the key either as `$api_key` in the JSON body or via HTTP Basic auth (API key as username, empty password). The account-scoped APIs (Decisions, Workflows, PSP Merchant Management) use HTTP Basic auth **and** require your numeric Account ID in the path. No OAuth.
- **Not self-serve / not free.** Sift is a commercial B2B platform. You need a Sift account, and API credentials are provisioned during a sales-led onboarding. Pricing is custom (contact sales) and is **not** published as public rate cards.
- **REST only - no public WebSocket API.** Decision notifications are delivered outbound via webhooks; there is no documented `wss://` streaming surface.
- **Versioning is per API.** The Events, Score, and Labels APIs are on `v205`; Decisions, Workflows, and PSP Merchant Management are on `v3`; Verification is on `v1`.

This entry is grounded in Sift's live public developer documentation and its officially maintained client libraries (Python, Ruby, Java, Node, PHP). Sift does not publish a single machine-readable OpenAPI definition; the `openapi/sift-openapi.yml` here is **modeled by API Evangelist** from those documented endpoints. Request/response schemas are representative where Sift documents examples rather than full JSON Schemas - see `review.yml` for the confirmed-vs-modeled breakdown.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/sift/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/sift/refs/heads/main/apis.yml)

## Tags

- Fraud Detection
- Fraud Prevention
- Risk
- Trust and Safety
- Machine Learning
- Payment Fraud
- Account Takeover
- Chargebacks
- Digital Trust

## Timestamps

- **Created:** 2026-07-12
- **Modified:** 2026-07-12

## APIs

### Sift Events API

Streams user activity - account creation, logins, orders, transactions, content, chargebacks, and more - to Sift's machine learning models via `POST /v205/events`. Supports both reserved event types (prefixed with `$`) and custom events, and can return a real-time Sift Score inline with `return_score=true`.

- **Human URL:** [https://developers.sift.com/docs/curl/events-api/overview](https://developers.sift.com/docs/curl/events-api/overview)
- **Base URL:** `https://api.sift.com`

#### Tags

- Events
- Fraud Detection
- Machine Learning

#### Properties

- [Documentation](https://developers.sift.com/docs/curl/events-api/overview)
- [API Reference](https://developers.sift.com/docs/curl/apis-overview)
- [OpenAPI](openapi/sift-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/sift.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/sift.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Sift Score API

Retrieves a user's real-time Sift Score (0-100, higher is riskier) per abuse type - `payment_abuse`, `account_abuse`, `account_takeover`, `content_abuse`, and `promotion_abuse` - along with reason codes. Includes synchronous score endpoints that fetch the latest score or rescore a user on demand.

- **Human URL:** [https://developers.sift.com/docs/curl/score-api/overview](https://developers.sift.com/docs/curl/score-api/overview)
- **Base URL:** `https://api.sift.com`

#### Tags

- Risk
- Score
- Fraud Detection

#### Properties

- [Documentation](https://developers.sift.com/docs/curl/score-api/overview)
- [OpenAPI](openapi/sift-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/sift.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/sift.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Sift Decisions API

Applies and retrieves decisions (accept, watch, block) against Sift entities - users, orders, sessions, and content - scoped to an account. Decisions record the outcome of manual or automated review, feed Sift's models, and trigger downstream webhooks. The modern replacement for the legacy Labels API.

- **Human URL:** [https://developers.sift.com/docs/curl/decisions-api/overview](https://developers.sift.com/docs/curl/decisions-api/overview)
- **Base URL:** `https://api.sift.com`

#### Tags

- Decisions
- Trust and Safety
- Workflow

#### Properties

- [Documentation](https://developers.sift.com/docs/curl/decisions-api/overview)
- [OpenAPI](openapi/sift-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/sift.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/sift.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Sift Workflow Status API

Retrieves the status and results of a Sift Workflow run by `run_id`, including the decisions a workflow applied to an entity. Workflows automate scoring, routing, and decisioning based on Sift Scores and business rules.

- **Human URL:** [https://developers.sift.com/docs/curl/workflows-api/workflow-decisions](https://developers.sift.com/docs/curl/workflows-api/workflow-decisions)
- **Base URL:** `https://api.sift.com`

#### Tags

- Workflow
- Automation
- Decisions

#### Properties

- [Documentation](https://developers.sift.com/docs/curl/workflows-api/workflow-decisions)
- [OpenAPI](openapi/sift-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/sift.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/sift.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Sift Labels API

Legacy API for labeling a user as good or bad for a given abuse type to train Sift's models via `POST` and `DELETE /v205/users/{user_id}/labels`. Sift recommends the Decisions API for new integrations; Labels remain documented for backfilling historical fraud outcomes.

- **Human URL:** [https://developers.sift.com/docs/curl/labels-api/overview](https://developers.sift.com/docs/curl/labels-api/overview)
- **Base URL:** `https://api.sift.com`

#### Tags

- Labels
- Training
- Legacy

#### Properties

- [Documentation](https://developers.sift.com/docs/curl/labels-api/overview)
- [OpenAPI](openapi/sift-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/sift.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/sift.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Sift Verification API

Step-up verification for high-risk actions. Sends, resends, and checks one-time passcodes (OTP) via `POST /v1/verification/send`, `/resend`, and `/check` to confirm a user's identity and mitigate account takeover.

- **Human URL:** [https://developers.sift.com/docs/curl/verification-api/overview](https://developers.sift.com/docs/curl/verification-api/overview)
- **Base URL:** `https://api.sift.com`

#### Tags

- Verification
- OTP
- Account Takeover

#### Properties

- [Documentation](https://developers.sift.com/docs/curl/verification-api/overview)
- [OpenAPI](openapi/sift-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/sift.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/sift.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Sift PSP Merchant Management API

For payment service providers and marketplaces - create, update, list, and retrieve sub-merchant profiles under an account so Sift can monitor merchant onboarding and transaction risk across a payments portfolio.

- **Human URL:** [https://developers.sift.com/docs/curl/psp-merchant-management-api/overview](https://developers.sift.com/docs/curl/psp-merchant-management-api/overview)
- **Base URL:** `https://api.sift.com`

#### Tags

- PSP
- Payment Fraud
- Merchant Risk

#### Properties

- [Documentation](https://developers.sift.com/docs/curl/psp-merchant-management-api/overview)
- [OpenAPI](openapi/sift-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/sift.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/sift.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Domain Security](security/sift-domain-security.yml)
- [Authentication](authentication/sift-authentication.yml)
- [GitHub Organization](https://github.com/SiftScience)
- [LinkedIn](https://www.linkedin.com/company/sift-science)
- [Website](https://sift.com)
- [Documentation](https://developers.sift.com/docs)
- [Plans](plans/sift-plans-pricing.yml)
- [Rate Limits](rate-limits/sift-rate-limits.yml)
- [Fin Ops](finops/sift-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
