# NextGen Healthcare (nextgen-healthcare)

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

NextGen Healthcare is a United States ambulatory electronic health record (EHR/EMR) and practice-management vendor serving outpatient specialties and community health through its NextGen Enterprise and NextGen Office platforms and the Mirth Connect interoperability engine. Its developer surface is standards-driven: 21st Century Cures Act-certified HL7 FHIR APIs for patient access and provider apps, a SMART App Launch API, and a Bulk FHIR (Flat FHIR) API delivering USCDI data, alongside an 800+ route JSON RESTful Enterprise API family. Both NextGen Enterprise and NextGen Office expose live FHIR service base URLs with SMART-on-FHIR OAuth2, coded against the US Core / USCDIv1 implementation guides.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/nextgen-healthcare/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/nextgen-healthcare/refs/heads/main/apis.yml)

## Tags

- Healthcare
- United States
- EHR
- EMR
- FHIR
- HL7
- Interoperability
- SMART on FHIR
- USCDI
- Bulk FHIR
- Patient Access
- 21st Century Cures

## Timestamps

- **Created:** 2026-07-24
- **Modified:** 2026-07-24

## APIs

### NextGen Enterprise Patient Access FHIR API

HL7 FHIR API for the NextGen Enterprise EHR, certified under the 21st Century Cures Act Patient Access criteria, in FHIR R4 (4.0.1) and legacy DSTU2, authenticated with SMART-on-FHIR OAuth2. The live R4 CapabilityStatement advertises 28 US Core resource types.

- **Human URL:** [https://www.nextgen.com/api/nge-fhir-r4](https://www.nextgen.com/api/nge-fhir-r4)
- **Base URL:** `https://fhir.nextgen.com/nge/prod/fhir-api-r4/fhir/r4/`

#### Properties

- [CapabilityStatement](fhir/nextgen-enterprise-r4-capabilitystatement.json)
- [SMART Configuration](fhir/nextgen-enterprise-r4-smart-configuration.json)
- [Documentation](https://www.nextgen.com/api/nge-fhir-r4)
- [API Reference](https://www.nextgen.com/api/regulatory-nge)

### NextGen Enterprise API

An extensive collection of JSON-based RESTful APIs (800+ routes) powering provider-organization apps on the NextGen Enterprise platform (v5.9.0+), authenticated with OAuth2 and Global Service Account (GSA) auth. Route-level docs and sandbox access are gated behind the NextGen API onboarding form.

- **Human URL:** [https://www.nextgen.com/api/enterprise-uscdi-documentation](https://www.nextgen.com/api/enterprise-uscdi-documentation)

#### Properties

- [Documentation](https://www.nextgen.com/api/enterprise-uscdi-documentation)
- [Getting Started](https://www.nextgen.com/api-on-boarding)

### NextGen Office FHIR R4 API

HL7 FHIR R4 (4.0.1) Patient Access API for the cloud-based NextGen Office (formerly MediTouch) EHR, coded against the US Core specification and exposing read-only USCDIv1 data. A downloadable Swagger 2.0 definition (45 paths) is published, and the live R4 CapabilityStatement advertises 26 US Core resource types.

- **Human URL:** [https://www.nextgen.com/api/regulatory-ngo](https://www.nextgen.com/api/regulatory-ngo)
- **Base URL:** `https://fhir.meditouchehr.com/api/fhir/r4`

#### Properties

- [OpenAPI](openapi/nextgen-office-fhir-r4-openapi.yaml)
- [CapabilityStatement](fhir/nextgen-office-r4-capabilitystatement.json)
- [SMART Configuration](fhir/nextgen-office-r4-smart-configuration.json)
- [OpenID Configuration](fhir/nextgen-office-openid-configuration.json)

### NextGen Office Bulk FHIR R4 API

Bulk FHIR (Flat FHIR) R4 API for the NextGen Office EHR, 21st Century Cures compliant, enabling authorized vendors to export USCDIv1 data for multiple patients. A downloadable OpenAPI 3.0.0 definition (5 paths) is published.

- **Human URL:** [https://www.nextgen.com/api/regulatory-ngo](https://www.nextgen.com/api/regulatory-ngo)
- **Base URL:** `https://fhir.meditouchehr.com/api/bulkfhir/r4`

#### Properties

- [OpenAPI](openapi/nextgen-office-bulk-fhir-r4-openapi.yml)
- [Documentation](https://www.nextgen.com/api/regulatory-ngo)

### NextGen Office FHIR R3 API

HL7 FHIR STU3 (R3) API for the NextGen Office EHR with C-CDA support, authenticated with SMART App Launch / OpenID Connect OAuth2 via Keycloak.

- **Human URL:** [https://www.nextgen.com/api/regulatory-ngo](https://www.nextgen.com/api/regulatory-ngo)
- **Base URL:** `https://fhir.meditouchehr.com/api/fhir/`

#### Properties

- [Documentation](https://www.nextgen.com/api/regulatory-ngo)

## Common Properties

- [Website](https://www.nextgen.com/)
- [Developer Portal](https://www.nextgen.com/developer-program)
- [Portal](https://developer.nextgen.com/)
- [Documentation](https://www.nextgen.com/api)
- [Marketplace](https://www.nextgen.com/marketplace)
- [GitHub Organization](https://github.com/NextGenHealthcare)
- [LinkedIn](https://www.linkedin.com/company/nextgen-healthcare-information-systems)
- [Blog](https://www.nextgen.com/blog)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
