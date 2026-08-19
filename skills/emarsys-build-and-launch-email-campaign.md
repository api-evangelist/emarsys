---
name: Build, test and launch an SAP Emarsys email campaign
description: Create an email campaign, point it at a contact list or segment, preview and test-send it safely, launch it, and then poll for delivery status and response metrics.
api: openapi/emarsys-email-campaigns-openapi.yml
operations:
  - createEmailCampaign
  - listEmailCampaigns
  - getEmailCampaignData
  - getEmailCampaignLanguages
  - getEmailCampaignCategories
  - updateEmailCampaignRecipientSource
  - previewEmailCampaignContents
  - sendTestEmail
  - launchEmailCampaign
  - stopEmailCampaign
  - queryDeliveryStatus
  - queryEmailResponseMetricsAndDeliverability
  - getEmailResponseMetricsAndDeliverabilityResults
---

# Build, test and launch an SAP Emarsys email campaign

There is **no sandbox account** on Emarsys — one production host, one credential,
live data (`sandbox/emarsys-sandbox.yml`). Your safety boundary is the send path,
not the environment, so follow this order exactly.

## 1. Gather the campaign's vocabulary

- `getEmailCampaignLanguages` (`GET /v2/language`)
- `getEmailCampaignCategories` (`GET /v2/emailcategory`)

Both return account-scoped ids you must reference when creating the campaign.

## 2. Create the campaign

`createEmailCampaign` — `POST /v2/email`. Returns the `emailId` everything else
keys on.

Related, if you are working from something that exists:
`listEmailCampaigns` (`GET /v2/email/`) and `getEmailCampaignData`
(`GET /v2/email/{emailId}/`).

## 3. Point it at an audience

`updateEmailCampaignRecipientSource` — `POST /v2/email/{emailId}/updatesource`.

The recipient source is either a **contact list** (static, built with
`createContactList` + `addContactsToContactList`) or a **segment** (dynamic,
`createSegment`). Confirm the size first with `countContactsInSegment` or
`countContactsInContactLict` (the misspelling is what the published spec ships) —
this is the last cheap moment to notice you are about to mail the wrong 400,000
people.

## 4. Prove the content renders — never skip this

- `previewEmailCampaignContents` — `POST /v2/email/{emailId}/preview`. Renders for
  a specific contact. Sends nothing.
- `sendTestEmail` — `POST /v2/email/{emailId}/sendtestmail`. Delivers to a
  nominated test address instead of the recipient source.

For multi-language campaigns, `finalizeMultilanguageEmailCampaign`
(`POST /v2/email/{emailId}/finalize`) before launching.

## 5. Launch

`launchEmailCampaign` — `POST /v2/email/{emailId}/launch`.

This is **irreversible for messages already dispatched**. There is no idempotency
key on this API, so a retried launch is a genuinely dangerous operation — treat a
timeout as "unknown", not as "failed", and reconcile with
`listEmailCampaignLaunches` (`POST /v2/email/getlaunchesofemail`) before ever
re-calling launch.

`stopEmailCampaign` (`POST /v2/email/{emailId}/stop`) halts an in-flight launch.
Know this call before you need it.

To send to addresses that are not contacts, use
`launchEmailCampaignVirtualContacts` (`POST /v2/email/{emailId}/broadcast`).

## 6. Measure — submit, then poll

Reporting on this API is asynchronous:

- `queryDeliveryStatus` — `POST /v2/email/getdeliverystatus`.
- `queryEmailResponseMetricsAndDeliverability` — `POST /v2/email/responses`
  returns a **`queryId`**.
- `getEmailResponseMetricsAndDeliverabilityResults` —
  `GET /v2/email/{queryId}/responses` retrieves the result once ready.

Per-contact delivery detail lives on a separate OpenAPI 3 service with bearer JWT
auth: `openapi/emarsys-email-reporting-api-openapi.yml` (max 90-day window).

Do **not** use `trendreporting` — it is marked `deprecated` in the published spec.

## Errors

Check `replyCode` on every response; Emarsys returns failures inside HTTP 200.
Launch-specific failures have their own code family — see
`errors/emarsys-error-codes.yml` and the Email Status and Error Codes guide.
