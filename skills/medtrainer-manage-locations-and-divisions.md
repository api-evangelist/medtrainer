---
name: medtrainer-manage-locations-and-divisions
description: Create and update MedTrainer locations and divisions, including the difference between full-replace PUT and partial PATCH.
api: MedTrainer Public API
base_url: https://api.medtrainer.com
generated: '2026-08-25'
method: generated
source: openapi/medtrainer-public-api-openapi.json
operations:
  - searchLocations
  - getLocation
  - createLocation
  - updateLocation
  - patchLocation
  - searchDivisions
  - getDivision
  - createDivision
  - updateDivision
  - patchDivision
---

# Manage MedTrainer locations and divisions

Creates and edits the organisational structure practitioners are attached to. **This skill
writes.**

## Divisions

- **List** — `GET /api/v1/divisions` (`searchDivisions`), `_elements=id,name,locations`.
- **Read** — `GET /api/v1/divisions/{divisionId}` (`getDivision`).
- **Create** — `POST /api/v1/divisions` (`createDivision`) with a `DivisionCreateRequest`.
  A 201 returns an `OperationOutcome` carrying the new `DIV-` id in `issue[0].details.id`.
- **Replace** — `PUT /api/v1/divisions/{divisionId}` (`updateDivision`) with a
  `DivisionUpdateRequest`. This is a **full replace**: omitted fields are not preserved.
- **Patch** — `PATCH /api/v1/divisions/{divisionId}` (`patchDivision`) to change a subset.
  Prefer PATCH unless you are deliberately rewriting the whole record.

## Locations

- **List** — `GET /api/v1/locations` (`searchLocations`), `_elements=id,name,division`.
- **Read** — `GET /api/v1/locations/{publicId}` (`getLocation`).
- **Create** — `POST /api/v1/locations` (`createLocation`) with a `LocationCreateRequest`:
  `name`, `addressLine`, `city`, `state`, `zipCode`, `phoneNumber`, `fax`, `email`, `sendEmail`,
  `enabledCredentialing`, and the parent `division`.
- **Replace** — `PUT /api/v1/locations/{publicId}` (`updateLocation`), full replace.
- **Patch** — `PATCH /api/v1/locations/{publicId}` (`patchLocation`), partial.

Set `enabledCredentialing` deliberately: it controls whether the location participates in
MedTrainer credentialing workflows.

## Ordering

Create the **division before** the locations that belong to it — `Location.division` needs an
existing `DIV-` id, and `Division.locations[]` references `LOC-` ids.

## Guardrails

- **There is no delete.** The API publishes no `DELETE` for locations or divisions and no
  archive/deactivate/restore operation. A location or division created through the API can only be
  removed by a human in the MedTrainer platform.
- **No idempotency keys.** A timed-out or 5xx `POST` may or may not have created the record —
  re-run `searchLocations` / `searchDivisions` to check before retrying.
- **PUT is destructive.** `updateLocation` and `updateDivision` replace the whole resource. Read the
  current record first (`getLocation` / `getDivision`), merge your change into it, and send the
  merged body — or use PATCH.
- **429 carries no `Retry-After`.** Back off exponentially.
