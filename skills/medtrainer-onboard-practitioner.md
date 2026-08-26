---
name: medtrainer-onboard-practitioner
description: Create a practitioner in the MedTrainer provider directory and attach them to the correct location, division, department and position.
api: MedTrainer Public API
base_url: https://api.medtrainer.com
generated: '2026-08-25'
method: generated
source: openapi/medtrainer-public-api-openapi.json
operations:
  - searchLocations
  - searchDivisions
  - searchDepartments
  - searchPositions
  - searchPractitionerCategories
  - searchPractitioners
  - createPractitioner
  - getPractitioner
---

# Onboard a practitioner into MedTrainer

Adds a new practitioner (provider/employee) to the MedTrainer directory with the right
organisational attachments. **This skill writes personal health-workforce data — read the
guardrails at the bottom before running it.**

## Before you start

- Authenticate with `X-API-Key: <key>` on every request. An API key is created in the MedTrainer
  platform under **Organization → Organization Management → API keys manager**, and starts in
  **Inactive** status — it must be switched to **Active** before it will work.
- All responses are `application/fhir+json`. Errors are FHIR `OperationOutcome` documents; read
  `issue[0].details.text`.

## Steps

1. **Check the practitioner does not already exist.** `GET /api/v1/practitioner` (`searchPractitioners`)
   with `_count` and `_page`, narrowing the returned fields with
   `_elements=id,name,telecom.email`. There is no create-if-absent operation and no idempotency
   key, so this search is the only duplicate protection available.
2. **Resolve the location.** `GET /api/v1/locations` (`searchLocations`) with
   `_elements=id,name`. Keep the `LOC-` prefixed `id`.
3. **Resolve the division.** `GET /api/v1/divisions` (`searchDivisions`) with
   `_elements=id,name,locations`. Keep the `DIV-` prefixed `id`.
4. **Resolve the department.** `GET /api/v1/departments` (`searchDepartments`). Keep the `DEPT-` id.
5. **Resolve the position.** `GET /api/v1/position` (`searchPositions`) with
   `_elements=id,name,clinical` — `clinical` tells you whether the position is a clinical role.
   Keep the `POS-` id.
6. **Resolve the practitioner category if you need one.** `GET /api/v1/practitioner-categories`
   (`searchPractitionerCategories`). Note that the Practitioner resource does not carry a category
   reference field, so this lookup is informational only.
7. **Create the practitioner.** `POST /api/v1/practitioner` (`createPractitioner`) with a
   `PractitionerWriteRequest` body: `name`, `telecom`, `address`, `birthDate` (format `MM/DD/YYYY`),
   plus `position`, `departments[]`, `locations[]` and `divisions[]` carrying the ids you resolved.
   `extension.user.userType` must be one of `admin`, `super_admin`, `student`;
   `extension.provider.npiNumber` carries the NPI.
   A 201 returns an `OperationOutcome` with `severity: information` and the new public id in
   `issue[0].details.id`.
8. **Read the record back.** `GET /api/v1/practitioner/{publicId}` (`getPractitioner`) using that
   id, and confirm the attachments landed.

## Error handling

| Status | `issue[].code` | What to do |
|---|---|---|
| 400 | `invalid` | Malformed JSON or a payload the backing service rejected. Do not retry unchanged. |
| 401 | `login` | Key missing, invalid, revoked, or still Inactive. |
| 422 | `invalid` | Field validation failed — read `details.text` for the field. |
| 429 | `throttled` | Rate limited. **No `Retry-After` header is returned**; back off exponentially. |
| 500 | `exception` | Server error. See the retry warning below. |
| 502 | `invalid` | Public-id resolver unavailable; retry with backoff. |

## Guardrails — read before writing

- **The practitioner record is PII.** It carries legal name, home and mailing address, personal
  phone, email, birth date, birth place and NPI. Handle it as healthcare workforce personal data.
- **This action cannot be undone through the API.** MedTrainer publishes no `DELETE` operation for
  practitioners, and no cancel, void, archive or restore operation. Once `createPractitioner`
  succeeds, removing the record requires a human in the MedTrainer platform UI.
- **Retries can duplicate.** There is no `Idempotency-Key` support. If `POST /api/v1/practitioner`
  times out or returns 500/502, DO NOT blindly retry — re-run step 1 first to see whether the
  record was in fact created.
- **Get human confirmation before creating.** Given the two points above, an agent should treat
  `createPractitioner` as an irreversible write and confirm with a person first.
