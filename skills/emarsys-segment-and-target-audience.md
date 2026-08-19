---
name: Build an SAP Emarsys audience with segments and contact lists
description: Choose between a static contact list and a dynamic segment, build either one, evaluate it asynchronously, and check membership before you spend a send on it.
api: openapi/emarsys-segments-openapi.yml
operations:
  - createSegment
  - listSegments
  - updateContactCriteriaInSegment
  - getSegmentContactCriteria
  - countContactsInSegment
  - lookUpContactInSegment
  - runContactSegmentSingle
  - pollStatusContactSegmentSingle
  - runContactSegmentBatch
  - pollStatusContactSegmentBatch
  - createContactList
  - listContactLists
  - addContactsToContactList
  - fetchContactsInContactList
  - countContactsInContactLict
  - removeContactsFromContactList
---

# Build an SAP Emarsys audience

Emarsys has two audience primitives and they behave completely differently.

| | Contact list | Segment |
|---|---|---|
| URL space | `/v2/contactlist` | `/v2/filter` (yes — "filter", not "segment") |
| Membership | explicit, you add and remove people | rule-based, re-evaluated on run |
| Spec | `openapi/emarsys-contact-lists-openapi.yml` | `openapi/emarsys-segments-openapi.yml` |

## Static: contact lists

1. `createContactList` — `POST /v2/contactlist`.
2. `addContactsToContactList` — `POST /v2/contactlist/{listId}/add`.
3. `countContactsInContactLict` — `GET /v2/contactlist/{listId}/count`.
   (The operationId really is spelled `Lict` in the published spec. Use it
   verbatim; do not "correct" it.)
4. `fetchContactsInContactList` — `GET /v2/contactlist/{contactlistId}/contactIds`.

Housekeeping: `renameContactList`, `replaceContactList`,
`removeContactsFromContactList`, `deleteContactList`.

**Do not use** `listContactsInContactList` or `getContactDataInContactList` —
both are marked `deprecated` in the spec and were superseded by
`fetchContactsInContactList` in December 2023.

## Dynamic: segments

1. `createSegment` — `PUT /v2/filter` (a PUT, not a POST). Returns `segmentId`.
2. `updateContactCriteriaInSegment` — `PUT /v2/filter/{segmentId}/contact_criteria`
   to change the rules; `getSegmentContactCriteria` to read them back.
3. `listSegments` — `GET /v2/filter/{segmentId}`.

### Evaluating a segment is asynchronous — submit then poll

For many contacts:

- `runContactSegmentBatch` — `POST /v2/filter/{segmentId}/runs` → returns `runId`
- `pollStatusContactSegmentBatch` — `GET /v2/filter/runs/{runId}`

For one contact:

- `runContactSegmentSingle` — `POST /v2/filter/{segmentId}/single_runs` → `runId`
- `pollStatusContactSegmentSingle` — `GET /v2/filter/single_runs/{runId}`

Poll with backoff; you are inside a 1000-request-per-minute budget shared with
everything else your API user does.

### Cheap membership checks

- `countContactsInSegment` — `GET /v2/filter/{segmentId}/contacts/count`
- `lookUpContactInSegment` — `GET /v2/filter/{segmentId}/contacts/{contactId}`

Always run the count before wiring a segment into
`updateEmailCampaignRecipientSource`. There is no sandbox to catch a bad rule.

## Gotcha: deleting a segment is a GET

`deleteSegment` is `GET /v2/filter/{segmentId}/delete`. Emarsys states its
resources "do not necessarily map to the standard HTTP methods", so a GET here is
destructive. Never treat GET as safe on this API, and never let a crawler or a
speculative prefetch loose on it.
