---
name: Trigger SAP Emarsys external events for real-time automation
description: Register an external event, fire it for a contact with personalization data to start an Automation Centre program or triggered email, and understand why a 200 OK does not mean anything ran.
api: openapi/emarsys-events-openapi.yml
operations:
  - createExternalEvent
  - listExternalEvents
  - QueryExternalEvent
  - updateExternalEvent
  - listUsesOfExternalEvent
  - triggerExternalEvents
  - triggerWishlistUpdate
  - deleteExternalEvent
---

# Trigger SAP Emarsys external events

External events are how your systems drive Emarsys in real time — an abandoned
cart, an order shipped, a password reset. Emarsys is the **consumer** here; your
system is the producer. (Emarsys has no general customer-facing webhook product
in the other direction — see `asyncapi/emarsys-webhooks.yml`.)

## 1. Register the event

`createExternalEvent` — `POST /v2/event`. Returns an `eventId`.

Existing events: `listExternalEvents` (`GET /v2/event/`) and
`QueryExternalEvent` (`GET /v2/event/{eventId}`). Note the capital Q in the
operationId — that is what the published spec says.

## 2. Wire it up in the Emarsys UI

Registration alone does nothing. Someone must attach the event to a **triggered
email campaign** or an **Automation Centre program** inside Emarsys. Verify with
`listUsesOfExternalEvent` (`GET /v2/event/{eventId}/usages`) before you rely on
it in production — an event with no usages is a silent no-op.

## 3. Fire it

`triggerExternalEvents` — `POST /v2/event/{eventId}/trigger`.

The body identifies the contact (by `key_id` + key value, same identifier model
as `skills/emarsys-import-and-update-contacts.md`) and carries the
personalization data the campaign will render — order number, product list, cart
total.

There is a purpose-built variant for wishlist changes:
`triggerWishlistUpdate` (`POST /v2/wishlist/update`).

## 4. Do not trust the 200

This is the single most important thing about this endpoint, and it is a
documented behaviour change, not a bug:

> Since **September 2020**, every Emarsys client receives `200 OK` regardless of
> whether an automated program or email campaign was actually triggered by the
> event.

Accounts **without** the Interactions (RTI) feature may still see HTTP 400 reply
code `5005` — "No program or campaign is triggered" — but accounts **with** it
get a clean 200 even when the linked program was deleted.

So:

- A 200 confirms **receipt**, not **effect**.
- Confirm effect out of band — `listUsesOfExternalEvent` at deploy time, and
  delivery reporting (`queryDeliveryStatus`,
  `queryEmailResponseMetricsAndDeliverability`) after the fact.
- Alert on *absence* of downstream sends, not on trigger errors. Trigger errors
  will not fire.

## 5. Retries

No idempotency key exists on this API. A retried trigger can send the customer a
second email. Treat a timeout as unknown and check delivery reporting rather than
re-firing blind.

## Rate

1000 requests per minute per API user. Real-time event traffic is exactly the
workload that hits this ceiling — spread it across API users if you need more
headroom, and watch `X-Ratelimit-Remaining`.
