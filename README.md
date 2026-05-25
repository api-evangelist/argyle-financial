# Argyle (argyle-financial)

Argyle is a consumer-permissioned employment and income data platform. The REST API and Link SDK let lenders, mortgage originators, background-check firms, gig marketplaces, and government benefits programs verify a worker's identity, employment, income, paystubs, deposits, shifts, gigs, and ratings directly from the source payroll, gig, and banking systems. Argyle covers approximately 90% of the U.S. workforce and is used by partners including Checkr, NFM Lending, Regional Finance, and LMCU, with loan-origination integrations into Encompass, nCino, Empower, and Byte.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/argyle-financial/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Consuming
- **Access:** 3rd-Party

## Tags

- Employment Data
- Income Verification
- Payroll
- Identity Verification
- Financial Data
- Banking
- Gig Economy
- Mortgage
- Lending
- Background Checks

## Timestamps

- **Created:** 2026-05-25
- **Modified:** 2026-05-25

## APIs

| API | Surface | OpenAPI |
|---|---|---|
| Argyle Users API | `/users`, `/user-tokens` | [openapi/argyle-users-openapi.yml](openapi/argyle-users-openapi.yml) |
| Argyle Invites API | `/invites` | [openapi/argyle-invites-openapi.yml](openapi/argyle-invites-openapi.yml) |
| Argyle Accounts API | `/accounts` | [openapi/argyle-accounts-openapi.yml](openapi/argyle-accounts-openapi.yml) |
| Argyle Items API | `/items`, `/item-filters`, `/employer-search` | [openapi/argyle-items-openapi.yml](openapi/argyle-items-openapi.yml) |
| Argyle Identities API | `/identities` | [openapi/argyle-identities-openapi.yml](openapi/argyle-identities-openapi.yml) |
| Argyle Employments API | `/employments` | [openapi/argyle-employments-openapi.yml](openapi/argyle-employments-openapi.yml) |
| Argyle Paystubs API | `/paystubs` | [openapi/argyle-paystubs-openapi.yml](openapi/argyle-paystubs-openapi.yml) |
| Argyle Payroll Documents API | `/payroll-documents` | [openapi/argyle-payroll-documents-openapi.yml](openapi/argyle-payroll-documents-openapi.yml) |
| Argyle Deposit Destinations API | `/deposit-destinations` | [openapi/argyle-deposit-destinations-openapi.yml](openapi/argyle-deposit-destinations-openapi.yml) |
| Argyle Shifts API | `/shifts` | [openapi/argyle-shifts-openapi.yml](openapi/argyle-shifts-openapi.yml) |
| Argyle Gigs API | `/gigs` | [openapi/argyle-gigs-openapi.yml](openapi/argyle-gigs-openapi.yml) |
| Argyle Vehicles API | `/vehicles` | [openapi/argyle-vehicles-openapi.yml](openapi/argyle-vehicles-openapi.yml) |
| Argyle Ratings API | `/ratings` | [openapi/argyle-ratings-openapi.yml](openapi/argyle-ratings-openapi.yml) |
| Argyle Reports API | `/reports` | [openapi/argyle-reports-openapi.yml](openapi/argyle-reports-openapi.yml) |
| Argyle User Uploads API | `/user-uploads` | [openapi/argyle-user-uploads-openapi.yml](openapi/argyle-user-uploads-openapi.yml) |
| Argyle User Forms API | `/user-forms` | [openapi/argyle-user-forms-openapi.yml](openapi/argyle-user-forms-openapi.yml) |
| Argyle Verifications API | `/verifications` | [openapi/argyle-verifications-openapi.yml](openapi/argyle-verifications-openapi.yml) |
| Argyle Verifications Partners API | `/verifications` (partner-scoped) | [openapi/argyle-verifications-partners-openapi.yml](openapi/argyle-verifications-partners-openapi.yml) |
| Argyle Banking API | `/connect-url`, `/banking-reports`, `/bank-accounts`, `/financial-institutions` | (no public OpenAPI artifact yet — see docs) |
| Argyle Receipts API | `/receipts` | [openapi/argyle-receipts-openapi.yml](openapi/argyle-receipts-openapi.yml) |

**Production base URL:** `https://api.argyle.com/v2`
**Sandbox base URL:** `https://api-sandbox.argyle.com/v2`
**Authentication:** HTTP Basic with `api_key_id` / `api_key_secret` pairs issued through Argyle Console
**Rate limit:** 50 requests per second per integration

## Naftiko Capabilities

- [capabilities/voie-workflow.yaml](capabilities/voie-workflow.yaml) — combined VOIE workflow (create user, issue token, order verification, retrieve, generate report)
- [capabilities/payroll-data-pull.yaml](capabilities/payroll-data-pull.yaml) — identities, employments, paystubs, payroll documents for a connected user
- [capabilities/gig-worker-coverage.yaml](capabilities/gig-worker-coverage.yaml) — gigs, shifts, vehicles, and ratings for gig-economy users

## Other Artifacts

- [rules/argyle-rules.yml](rules/argyle-rules.yml) — Argyle API conventions and Spectral-friendly rules
- [vocabulary/argyle-financial-vocabulary.yml](vocabulary/argyle-financial-vocabulary.yml) — domain vocabulary
- [json-ld/argyle-financial-context.jsonld](json-ld/argyle-financial-context.jsonld) — JSON-LD context mapping core entities to schema.org
- [json-schema/argyle-paystub-schema.json](json-schema/argyle-paystub-schema.json), [argyle-identity-schema.json](json-schema/argyle-identity-schema.json), [argyle-verification-schema.json](json-schema/argyle-verification-schema.json)
- [json-structure/argyle-financial-structure.json](json-structure/argyle-financial-structure.json) — entity graph and webhook catalog
- [examples/](examples/) — request / response examples for create user, order verification, list paystubs
- [plans/argyle-financial-plans-pricing.yml](plans/argyle-financial-plans-pricing.yml) — API Commons Plans 0.1
- [rate-limits/argyle-financial-rate-limits.yml](rate-limits/argyle-financial-rate-limits.yml) — API Commons Rate Limits 0.1
- [finops/argyle-financial-finops.yml](finops/argyle-financial-finops.yml) — FinOps Framework / FOCUS 1.3 mapping

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/argylesystems)
- [GitHub Organization](https://github.com/argyle-systems)
- [Website](https://www.argyle.com/)
- [Developer Portal](https://docs.argyle.com/)
- [Documentation](https://docs.argyle.com/api-guide/overview)
- [Postman Collection](https://docs.argyle.com/api-guide/postman)
- [Webhooks](https://docs.argyle.com/api-guide/webhooks)
- [Sandbox](https://docs.argyle.com/overview/sandbox-testing)
- [Sign Up](https://console.argyle.com/sign-up)
- [Login](https://console.argyle.com/)
- [Link SDK](https://docs.argyle.com/link/overview)
- [Web Link SDK](https://docs.argyle.com/link/initialization/web)
- [Mobile SDKs](https://docs.argyle.com/link/initialization/mobile-sdks)
- [Hosted Link](https://docs.argyle.com/link/initialization/hosted-link)
- [Changelog](https://changelog.argyle.com/)
- [Trust Center](https://trustcenter.argyle.com/)
- [Blog](https://www.argyle.com/blog)
- [Pricing](https://www.argyle.com/pricing)
- [Customers](https://www.argyle.com/customers)
- [Errors](https://docs.argyle.com/api-reference/account-connection-errors)
- [Data Security](https://docs.argyle.com/overview/data-security)

## Features

- Consumer-permissioned payroll-direct VOI / VOE verifications
- Combined VOIE workflow in a single API call
- Direct-from-bank VOA and VOAI through the Banking API
- Document processing path for W-2, 1099, and paystub uploads with OCR and authenticity checks
- Fannie Mae Day 1 Certainty reps-and-warrants relief
- Freddie Mac Asset and Income Modeler (AIM) eligibility
- Coverage of ~90% of the U.S. workforce across payroll, gig, and banking sources
- Hosted Link flow plus Web, iOS, Android, React Native, and Flutter SDKs
- Reports endpoint that emits underwriter-ready PDF and JSON deliverables
- Webhook-driven event model covering accounts, paystubs, documents, gigs, shifts, verifications
- Encompass, nCino, Empower, and Byte LOS/POS plugins
- Ocrolus integration for document authenticity
- Console no-code tooling for flow configuration and member management
- 50 RPS documented platform rate limit
- Sandbox at api-sandbox.argyle.com with synthetic payroll, gig, and banking data

## SDKs

- [argyle-link-ios](https://github.com/argyle-systems/argyle-link-ios) — Swift
- [argyle-link-android](https://github.com/argyle-systems/argyle-link-android) — Kotlin
- [argyle-link-react-native](https://github.com/argyle-systems/argyle-link-react-native) — Kotlin / JS
- [argyle-link-flutter](https://github.com/argyle-systems/argyle-link-flutter) — Dart

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
