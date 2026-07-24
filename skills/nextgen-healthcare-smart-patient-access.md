---
name: Read patient records via SMART-on-FHIR patient access
description: Authorize a patient-facing app with SMART App Launch, obtain a patient-scoped token, and read USCDI clinical resources from the NextGen FHIR R4 Patient Access API.
api: openapi/nextgen-office-fhir-r4-openapi.yaml
operations: ['GET /fhir/r4/Patient/{id}', 'GET /fhir/r4/Condition', 'GET /fhir/r4/Observation', 'GET /fhir/r4/AllergyIntolerance', 'GET /fhir/r4/MedicationRequest']
auth: SMART-on-FHIR OAuth2 (authorization_code + PKCE)
---

# Read patient records via SMART-on-FHIR patient access

Retrieve a patient's USCDI clinical data from NextGen using the standard SMART App Launch flow.
The Office R4 Patient Access base URL is `https://fhir.meditouchehr.com/api/fhir/r4`; the Enterprise
R4 base URL is `https://fhir.nextgen.com/nge/prod/fhir-api-r4/fhir/r4`. The published R4 Swagger is
read-only (search + read) per US Core resource and declares no operationIds, so address operations
by path + method.

## Steps
1. **Discover** — GET `/.well-known/smart-configuration` on the FHIR base URL to read the
   `authorization_endpoint`, `token_endpoint`, and `scopes_supported`.
2. **Authorize** — send the user to the `authorization_endpoint` with `response_type=code`,
   PKCE (`code_challenge`, `S256`), and scopes such as `launch/patient openid fhirUser
   offline_access patient/Patient.rs patient/Observation.rs patient/Condition.rs`.
3. **Token** — exchange the `code` at the `token_endpoint` for an access token; the token
   response includes the `patient` context id. Use `Authorization: Bearer <token>` thereafter.
4. **Read the patient** — GET `/fhir/r4/Patient/{id}` using the `patient` id from step 3.
5. **Search clinical resources** — GET `/fhir/r4/Condition?patient={id}`,
   `/fhir/r4/Observation?patient={id}&category=laboratory`,
   `/fhir/r4/AllergyIntolerance?patient={id}`, `/fhir/r4/MedicationRequest?patient={id}`.
   Each returns a FHIR searchset `Bundle`; follow `link[relation=next]` for paging.

## Rules
- Request only the granular `patient/[Resource].rs` scopes you need (SMART v2 granular scopes are
  advertised). See `scopes/nextgen-healthcare-scopes.yml`.
- Errors are FHIR `OperationOutcome`; `401` = expired/invalid token (refresh with
  `offline_access`), `403` = scope not granted. See `conventions/nextgen-healthcare-conventions.yml`.
