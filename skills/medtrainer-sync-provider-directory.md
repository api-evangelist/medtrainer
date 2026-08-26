---
name: medtrainer-sync-provider-directory
description: Read the full MedTrainer provider directory — locations, divisions, departments, positions, practitioner categories and practitioners — with FHIR Bundle pagination.
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
  - getLocation
  - getDivision
  - getPractitioner
---

# Sync the MedTrainer provider directory

Pulls a read-only snapshot of the MedTrainer directory into an external system. **Read-only — this
skill performs no writes.**

## Pagination contract

Every search operation uses FHIR search-control parameters, not limit/offset and not cursors:

- `_count` — page size, integer ≥ 1, default `20`.
- `_page` — **1-based** page number, integer ≥ 1, default `1`.
- `_elements` — comma-separated field selector.

Responses are FHIR `Bundle` envelopes. Follow the absolute URLs in `link[]` (they include scheme
and host) rather than incrementing `_page` yourself. **Unknown `_elements` selectors are silently
ignored** — they are preserved in the pagination links but dropped when the resource is built, and
no warning issue is returned, so verify the fields you asked for actually came back.

## Steps

1. **Reference vocabularies first** (small, read-only, cache them):
   - `GET /api/v1/position` (`searchPositions`) — `_elements=id,name,clinical`
   - `GET /api/v1/departments` (`searchDepartments`) — `_elements=id,name`
   - `GET /api/v1/practitioner-categories` (`searchPractitionerCategories`) — `_elements=id,name`
2. **Organisational structure**:
   - `GET /api/v1/divisions` (`searchDivisions`) — `_elements=id,name,locations`. Division
     `locations[]` entries are `DivisionLocationReference` objects whose `reference` field holds a
     location id and **may be null**.
   - `GET /api/v1/locations` (`searchLocations`) — `_elements=id,name,division`. Locations can
     nest: `locations[]` on a Location holds child location ids.
3. **Practitioners** — `GET /api/v1/practitioner` (`searchPractitioners`). Omitting `_elements`
   returns the full public resource including PII. Prefer an explicit narrow selector, e.g.
   `_elements=id,name,position,locations,extension.user.status`. Nested selectors are supported:
   `telecom.email`, `telecom.homePhone`, `address.city`, `extension.user.status`,
   `extension.user.statusReason`, `extension.user.userType`, `extension.provider.npiNumber`.
4. **Detail fetches** where you need one record: `getLocation`, `getDivision`, `getPractitioner`
   by `{publicId}`.

## Joining the graph

Ids are prefixed and opaque: `LOC-`, `DIV-`, `POS-`, `DEPT-`, `PCAT-`, `PRAC-`. Practitioner links
out to Position (`position.id`), Departments (`departments[].id`), Locations (`locations[].id`) and
Divisions (`divisions[].id`). See `data-model/medtrainer-data-model.yml`.

## Limits and cautions

- **No incremental sync.** No resource carries a created/updated timestamp, ETag or version field,
  and no search parameter filters by modification date. Every sync is a full re-read.
- **Rate limits are enforced but unpublished.** Any operation can return 429 with
  `issue[].code = "throttled"` and no `Retry-After`. Pace conservatively and back off exponentially.
- **Practitioner data is PII.** Request only the `_elements` you need and store accordingly.
