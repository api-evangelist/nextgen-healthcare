---
name: Run a NextGen Office Bulk FHIR export
description: Create a patient Group and run an asynchronous Bulk FHIR ($export) job to pull USCDIv1 data for a population, then poll for and download the output.
api: openapi/nextgen-office-bulk-fhir-r4-openapi.yml
operations: [createGroup, getGroup, groupExport, pollJobStatus, deleteJob]
auth: SMART Backend Services OAuth2 (client_credentials, bearer JWT)
---

# Run a NextGen Office Bulk FHIR export

Export USCDIv1 data for a population of patients from NextGen Office using the 21st Century
Cures-compliant Bulk FHIR (Flat FHIR) API. Base URL: `https://fhir.meditouchehr.com/api/bulkfhir/r4`.

## Prerequisites
- A registered backend app with a `system/*.rs` (or granular `system/[Resource].rs`) scope.
- An OAuth2 access token from the Keycloak token endpoint
  (`https://idp-prod.prod.ngo.nextgenaws.net/auth/realms/nextgen/protocol/openid-connect/token`)
  via `client_credentials`. Send it as `Authorization: Bearer <token>` on every call.

## Steps
1. **Create the cohort** — call `createGroup` (`POST /bulkfhir/r4/Group`) with a FHIR Group
   describing the patient membership. Capture the returned Group `id`.
2. **(Optional) Verify** — call `getGroup` (`GET /bulkfhir/r4/Group/{id}`) to confirm the Group.
3. **Kick off the export** — call `groupExport` (`GET /bulkfhir/r4/Group/{id}/$export`) with
   `Prefer: respond-async`. A `202 Accepted` returns a `Content-Location` URL for the job.
4. **Poll** — call `pollJobStatus` (`GET /bulkfhir/r4/$export-poll-status`) against the job.
   While processing you get `202` with `X-Progress` / `Retry-After`; on completion a `200`
   returns a manifest of `output[]` NDJSON file URLs. Respect `Retry-After` between polls.
5. **Download** — fetch each NDJSON file in the completed manifest.
6. **Clean up** — call `deleteJob` (`DELETE /bulkfhir/r4/$export-poll-status`) to release the job.

## Rules
- Errors come back as FHIR `OperationOutcome` (`application/fhir+json`); read
  `issue[].code` / `issue[].diagnostics`. `401` = token problem, `403` = missing scope,
  `400` = bad request. See `errors/nextgen-healthcare-problem-types.yml`.
- This is protected US health data — only request the minimum `system/` scopes needed and
  handle all output under HIPAA controls.
