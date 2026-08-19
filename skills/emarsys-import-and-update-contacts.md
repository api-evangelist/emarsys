---
name: Import and update SAP Emarsys contacts
description: Resolve Emarsys field ids, then create or update contacts in batches without duplicating people, and read the result correctly despite Emarsys returning failures inside HTTP 200.
api: openapi/emarsys-contacts-openapi.yml
operations:
  - listAvailableFields
  - createContacts
  - updateContacts
  - getContactId
  - getContactData
  - verifyContactInternalIdentifiers
---

# Import and update SAP Emarsys contacts

Use this when you need to push people into Emarsys or refresh their attributes.

## Before anything else: resolve field ids

An Emarsys contact has **no fixed attribute set**. Every attribute is a numeric
**field id** defined per account, and contact payloads use those ids as JSON
object keys — `"3": "jane@example.com"`, not `"email": "..."`.

1. Call `listAvailableFields` (`GET /v2/field/translate/{languageId}`, use `en`).
2. Build a name → id map and cache it. Do not hardcode ids beyond the defaults
   (`1` first name, `2` last name, `3` email); custom fields differ per account.

## Authenticate

Every v2 call carries an `X-WSSE` header (`UsernameToken` with `Username`,
`PasswordDigest`, `Nonce`, `Created`). The digest is
`base64(sha1(nonce + ISO8601 timestamp + secret))` and must be **recomputed per
request**. `Created` must be within **five minutes** of Emarsys server time or the
request is rejected. See `conventions/emarsys-conventions.yml`.

WSSE is deprecated with a final sunset at the **end of 2026** — if you are
building new, use the OAuth 2.0 / OIDC v3 surface instead. See
`lifecycle/emarsys-lifecycle.yml`.

## Choose the identifier before you write

Pick one indexed field as `key_id` and keep it stable for the whole integration.
Email (`3`) is the usual choice. A custom field can only be used as `key_id` if
Emarsys has indexed it for your account — raise a support ticket first.

## Create

`createContacts` — `POST /v2/contact`

- Body carries `key_id` plus a `contacts` array of field-id-keyed objects.
- For a **single** contact the body is flat: `{"key_id": "3", "3": "...", "1": "..."}`.
- Hard limits: **1000 contacts per call** and **10 MB payload**. Exceeding the
  batch returns HTTP 400 reply code `1000`.

## Update

`updateContacts` — `PUT /v2/contact/` with the same shape. Use this rather than
create when the person may already exist; Emarsys does **not** deduplicate a
create for you.

## Read the response properly — this is the part that bites

There is **no idempotency key** on this API. A retried create can double-write.
Worse, Emarsys returns application-level failures **inside HTTP 200 responses**.
The envelope is:

```json
{ "replyCode": 0, "replyText": "OK", "data": { } }
```

- `replyCode: 0` is the only success signal. **Never treat 2xx as success.**
- `replyCode 2008` inside a 200 means *no contact found* for that identifier.
- `replyCode 2010` inside a 200 means *more than one contact matched* — your key
  field is not unique and you must fix the data before writing.
- Key on the **(HTTP status, replyCode)** pair; the same replyCode is reused
  across statuses. Full registry: `errors/emarsys-error-codes.yml` (353 codes).

## Recover from a partial batch

Because retries are not idempotent, reconcile instead of blindly re-sending:

- `getContactId` (`GET /v2/contact/query/?{keyId}={keyValue}`) maps an external
  key to the internal Emarsys id.
- `verifyContactInternalIdentifiers` (`POST /v2/contact/checkids`) confirms which
  internal ids exist.
- `getContactData` (`POST /v2/contact/getdata`) reads back the field values you
  believe you wrote.

## Pace yourself

1000 requests per minute **per API user** (not per account). Watch
`X-RateLimit-Limit`, `X-Ratelimit-Remaining` and `X-RateLimit-Reset`; on `429`
back off — there is no `Retry-After`. See `rate-limits/emarsys-rate-limits.yml`.
