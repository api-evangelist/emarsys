# SAP Emarsys

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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

SAP Emarsys (formerly Emarsys, acquired by SAP in 2020 and now marketed as part of SAP Engagement Cloud) is an omnichannel customer engagement and marketing automation platform used by retail and consumer brands to run personalized email, SMS, mobile, web and ads campaigns from a unified customer data layer with AI-driven segmentation. The developer surface is the Emarsys Core API — 23 published endpoint batches covering contacts and custom contact fields, static contact lists and rule-based segments, email campaign creation, preview, test-send, launch and stop, delivery status and response-metric reporting, external event triggers that start Automation Centre programs, media assets, tracked links, account and API-user administration, and the Relational Data Store (RDS) custom-object layer for purchase and product data. A separately published SMS Partner API lets SMS aggregators integrate with the Emarsys SMS channel. Authentication is the legacy X-WSSE UsernameToken header, which SAP Emarsys has deprecated with a final sunset at the end of 2026 in favour of OAuth 2.0 client credentials / OpenID Connect on the v3 surface. Rate limiting is 1000 requests per minute per API user with published X-RateLimit-* headers, and errors are returned as a proprietary replyCode/replyText/data envelope that can carry failures inside HTTP 200 responses.

**Areas:** Marketing Automation · Customer Engagement · Email Marketing · Omnichannel · Customer Data Platform · SAP · Segmentation · SMS · Marketing Analytics · Retail · Personalization · Campaign Management

## SAP Emarsys on APIs.io

Everything profiled for SAP Emarsys is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/emarsys/](https://apis.io/providers/emarsys/)** — or go straight to one of the APIs or properties below.

### APIs (30)

- [SAP Emarsys Ac API](https://apis.io/apis/emarsys/emarsys-ac-api/) — The Ac API from SAP Emarsys — 2 operation(s) for ac.
- [SAP Emarsys Administrator API](https://apis.io/apis/emarsys/emarsys-administrator-api/) — The Administrator API from SAP Emarsys — 7 operation(s) for administrator.
- [SAP Emarsys Blocklist API](https://apis.io/apis/emarsys/emarsys-blocklist-api/) — The Blocklist API from SAP Emarsys — 1 operation(s) for blocklist.
- [SAP Emarsys Campaigns API](https://apis.io/apis/emarsys/emarsys-campaigns-api/) — The Campaigns API from SAP Emarsys — 1 operation(s) for campaigns.
- [SAP Emarsys Client Configuration API](https://apis.io/apis/emarsys/emarsys-client-configuration-api/) — The Client Configuration API from SAP Emarsys — 1 operation(s) for client configuration.
- [SAP Emarsys Client Configuration Test API](https://apis.io/apis/emarsys/emarsys-client-configuration-test-api/) — The Client Configuration Test API from SAP Emarsys — 1 operation(s) for client configuration test.
- [SAP Emarsys Condition API](https://apis.io/apis/emarsys/emarsys-condition-api/) — The Condition API from SAP Emarsys — 1 operation(s) for condition.
- [SAP Emarsys Contact API](https://apis.io/apis/emarsys/emarsys-contact-api/) — The Contact API from SAP Emarsys — 10 operation(s) for contact.
- [SAP Emarsys Delivery Reports API](https://apis.io/apis/emarsys/emarsys-delivery-reports-api/) — The Delivery Reports API from SAP Emarsys — 1 operation(s) for delivery reports.
- [SAP Emarsys Email API](https://apis.io/apis/emarsys/emarsys-email-api/) — The Email API from SAP Emarsys — 34 operation(s) for email.
- [SAP Emarsys Emailcategory API](https://apis.io/apis/emarsys/emarsys-emailcategory-api/) — The Emailcategory API from SAP Emarsys — 1 operation(s) for emailcategory.
- [SAP Emarsys Event API](https://apis.io/apis/emarsys/emarsys-event-api/) — The Event API from SAP Emarsys — 6 operation(s) for event.
- [SAP Emarsys Export API](https://apis.io/apis/emarsys/emarsys-export-api/) — The Export API from SAP Emarsys — 3 operation(s) for export.
- [SAP Emarsys Field API](https://apis.io/apis/emarsys/emarsys-field-api/) — The Field API from SAP Emarsys — 5 operation(s) for field.
- [SAP Emarsys File API](https://apis.io/apis/emarsys/emarsys-file-api/) — The File API from SAP Emarsys — 4 operation(s) for file.
- [SAP Emarsys Filter API](https://apis.io/apis/emarsys/emarsys-filter-api/) — The Filter API from SAP Emarsys — 10 operation(s) for filter.
- [SAP Emarsys Folder API](https://apis.io/apis/emarsys/emarsys-folder-api/) — The Folder API from SAP Emarsys — 1 operation(s) for folder.
- [SAP Emarsys Form API](https://apis.io/apis/emarsys/emarsys-form-api/) — The Form API from SAP Emarsys — 2 operation(s) for form.
- [SAP Emarsys Https: API](https://apis.io/apis/emarsys/emarsys-https-api/) — The Https: API from SAP Emarsys — 1 operation(s) for https:.
- [SAP Emarsys Inbound Messages API](https://apis.io/apis/emarsys/emarsys-inbound-messages-api/) — The inbound-messages API from SAP Emarsys — 1 operation(s) for inbound-messages.
- [SAP Emarsys Keyring API](https://apis.io/apis/emarsys/emarsys-keyring-api/) — The Keyring API from SAP Emarsys — 2 operation(s) for keyring.
- [SAP Emarsys Language API](https://apis.io/apis/emarsys/emarsys-language-api/) — The Language API from SAP Emarsys — 1 operation(s) for language.
- [SAP Emarsys Outbound Message Sending API](https://apis.io/apis/emarsys/emarsys-outbound-message-sending-api/) — The Outbound Message Sending API from SAP Emarsys — 1 operation(s) for outbound message sending.
- [SAP Emarsys Programresource API](https://apis.io/apis/emarsys/emarsys-programresource-api/) — The Programresource API from SAP Emarsys — 1 operation(s) for programresource.
- [SAP Emarsys Rds API](https://apis.io/apis/emarsys/emarsys-rds-api/) — The Rds API from SAP Emarsys — 3 operation(s) for rds.
- [SAP Emarsys Settings API](https://apis.io/apis/emarsys/emarsys-settings-api/) — The Settings API from SAP Emarsys — 9 operation(s) for settings.
- [SAP Emarsys Source API](https://apis.io/apis/emarsys/emarsys-source-api/) — The Source API from SAP Emarsys — 2 operation(s) for source.
- [SAP Emarsys Trendreporting API](https://apis.io/apis/emarsys/emarsys-trendreporting-api/) — The Trendreporting API from SAP Emarsys — 1 operation(s) for trendreporting.
- [SAP Emarsys Wishlist API](https://apis.io/apis/emarsys/emarsys-wishlist-api/) — The Wishlist API from SAP Emarsys — 1 operation(s) for wishlist.
- [SAP Emarsys Contact List API](https://apis.io/apis/emarsys/emarsys-contact-list-api/) — The Contact List API from SAP Emarsys — 10 operation(s) for contact list.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Emarsys Webhooks](https://apis.io/asyncapis/emarsys/emarsys-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [emarsys](https://apis.io/servers/emarsys/emarsys/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Emarsys Agentic Access](https://apis.io/agentic-access/emarsys/emarsys-agentic-access/)

#### Collections (25)

Postman and Open Collection request collections.

- [Emarsys Core API - Accounts endpoint batch](https://apis.io/collections/emarsys/open-emarsys-accounts/)
- [Emarsys Core API - Auto-import profiles endpoint batch](https://apis.io/collections/emarsys/open-emarsys-auto-import-profiles/)
- [Bulk Response Summary](https://apis.io/collections/emarsys/open-emarsys-bulk-response-summary/)
- [Emarsys Core API - Conditional text rules endpoint batch](https://apis.io/collections/emarsys/open-emarsys-conditional-text-rules/)
- [Emarsys Core API - Contact and email data endpoint batch](https://apis.io/collections/emarsys/open-emarsys-contact-and-email-data/)
- [Emarsys Core API - Contact lists endpoint batch](https://apis.io/collections/emarsys/open-emarsys-contact-lists/)
- [Emarsys Core API - Contact sources endpoint batch](https://apis.io/collections/emarsys/open-emarsys-contact-sources/)
- [Emarsys Core API - Contacts endpoint batch](https://apis.io/collections/emarsys/open-emarsys-contacts/)
- [Emarsys Core API - Email campaign lifecycle endpoint batch](https://apis.io/collections/emarsys/open-emarsys-email-campaign-lifecycle/)
- [Emarsys Core API - Email campaigns endpoint batch](https://apis.io/collections/emarsys/open-emarsys-email-campaigns/)
- [Email Reporting API](https://apis.io/collections/emarsys/open-emarsys-email-reporting-api/)
- [Emarsys Core API - Email templates endpoint batch](https://apis.io/collections/emarsys/open-emarsys-email-templates/)
- [Emarsys Core API - Events endpoint batch](https://apis.io/collections/emarsys/open-emarsys-events/)
- [Emarsys Core API - External Content endpoint batch](https://apis.io/collections/emarsys/open-emarsys-external-content/)
- [Emarsys Core API - Fields endpoint batch](https://apis.io/collections/emarsys/open-emarsys-fields/)
- [Emarsys Core API - Forms endpoint batch](https://apis.io/collections/emarsys/open-emarsys-forms/)
- [Emarsys Core API - Keys endpoint batch](https://apis.io/collections/emarsys/open-emarsys-keys/)
- [Emarsys Core API - Media Database endpoint batch](https://apis.io/collections/emarsys/open-emarsys-media-database/)
- [Emarsys Core API - Programs endpoint batch](https://apis.io/collections/emarsys/open-emarsys-programs/)
- [Emarsys Core API - Relational Data endpoint batch](https://apis.io/collections/emarsys/open-emarsys-relational-data/)
- [Emarsys Core API - Sections endpoint batch](https://apis.io/collections/emarsys/open-emarsys-sections/)
- [Emarsys Core API - Segments endpoint batch](https://apis.io/collections/emarsys/open-emarsys-segments/)
- [Provider callbacks](https://apis.io/collections/emarsys/open-emarsys-sms-partner-callbacks/)
- [SAP Emarsys SMS Partner Service](https://apis.io/collections/emarsys/open-emarsys-sms-partner-service/)
- [Emarsys Core API - Tracked links endpoint batch](https://apis.io/collections/emarsys/open-emarsys-tracked-links/)

#### Overlays (25)

OpenAPI overlays, including conversational phrasing for each operation.

- [Emarsys Accounts Overlay](https://apis.io/overlays/emarsys/emarsys-accounts-overlay/)
- [Emarsys Auto Import Profiles Overlay](https://apis.io/overlays/emarsys/emarsys-auto-import-profiles-overlay/)
- [Emarsys Bulk Response Summary Overlay](https://apis.io/overlays/emarsys/emarsys-bulk-response-summary-overlay/)
- [Emarsys Conditional Text Rules Overlay](https://apis.io/overlays/emarsys/emarsys-conditional-text-rules-overlay/)
- [Emarsys Contact And Email Data Overlay](https://apis.io/overlays/emarsys/emarsys-contact-and-email-data-overlay/)
- [Emarsys Contact Lists Overlay](https://apis.io/overlays/emarsys/emarsys-contact-lists-overlay/)
- [Emarsys Contact Sources Overlay](https://apis.io/overlays/emarsys/emarsys-contact-sources-overlay/)
- [Emarsys Contacts Overlay](https://apis.io/overlays/emarsys/emarsys-contacts-overlay/)
- [Emarsys Email Campaign Lifecycle Overlay](https://apis.io/overlays/emarsys/emarsys-email-campaign-lifecycle-overlay/)
- [Emarsys Email Campaigns Overlay](https://apis.io/overlays/emarsys/emarsys-email-campaigns-overlay/)
- [Emarsys Email Reporting Api Overlay](https://apis.io/overlays/emarsys/emarsys-email-reporting-api-overlay/)
- [Emarsys Email Templates Overlay](https://apis.io/overlays/emarsys/emarsys-email-templates-overlay/)
- [Emarsys Events Overlay](https://apis.io/overlays/emarsys/emarsys-events-overlay/)
- [Emarsys External Content Overlay](https://apis.io/overlays/emarsys/emarsys-external-content-overlay/)
- [Emarsys Fields Overlay](https://apis.io/overlays/emarsys/emarsys-fields-overlay/)
- [Emarsys Forms Overlay](https://apis.io/overlays/emarsys/emarsys-forms-overlay/)
- [Emarsys Keys Overlay](https://apis.io/overlays/emarsys/emarsys-keys-overlay/)
- [Emarsys Media Database Overlay](https://apis.io/overlays/emarsys/emarsys-media-database-overlay/)
- [Emarsys Programs Overlay](https://apis.io/overlays/emarsys/emarsys-programs-overlay/)
- [Emarsys Relational Data Overlay](https://apis.io/overlays/emarsys/emarsys-relational-data-overlay/)
- [Emarsys Sections Overlay](https://apis.io/overlays/emarsys/emarsys-sections-overlay/)
- [Emarsys Segments Overlay](https://apis.io/overlays/emarsys/emarsys-segments-overlay/)
- [Emarsys Sms Partner Callbacks Overlay](https://apis.io/overlays/emarsys/emarsys-sms-partner-callbacks-overlay/)
- [Emarsys Sms Partner Service Overlay](https://apis.io/overlays/emarsys/emarsys-sms-partner-service-overlay/)
- [Emarsys Tracked Links Overlay](https://apis.io/overlays/emarsys/emarsys-tracked-links-overlay/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Emarsys Authentication](https://apis.io/security/emarsys/emarsys-authentication/)
- [Emarsys Domain Security](https://apis.io/security/emarsys/emarsys-domain-security/)
- [Emarsys Trust Center](https://apis.io/security/emarsys/emarsys-trust-center/)
- [Emarsys Vulnerability Disclosure](https://apis.io/security/emarsys/emarsys-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Emarsys Scopes](https://apis.io/scopes/emarsys/emarsys-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Emarsys Plans Pricing](https://apis.io/plans/emarsys/emarsys-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Emarsys Rate Limits](https://apis.io/rate-limits/emarsys/emarsys-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://emarsys.com)
- [Documentation](https://dev.emarsys.com/)
- [Getting started](https://dev.emarsys.com/docs/emarsys-core-api-guides/tv7m82af5d5hn-1-prerequisites)
- [API reference](https://dev.emarsys.com/docs/core-api-reference)
- [Pricing](https://emarsys.com/request-pricing/)
- [Support](https://emarsys.com/contact-us/)
- [Blog](https://emarsys.com/learn/blog/)
- [Security](https://www.sap.com/report-a-vulnerability)
- [Compliance](https://www.sap.com/about/trust-center/certification-compliance.html)
- [Terms of service](https://emarsys.com/legal-notice/)
- [Privacy policy](https://emarsys.com/privacy-statement/)
- [GitHub](https://github.com/emartech)
- [Status](https://status.emarsys.com)

## API Evangelist rating

**Kin Score 66.5** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 78.6 |
| Contract quality | 55.8 |
| Contract governance | 4.5 |
| Operational transparency | 73.7 |
| Developer ergonomics | 70.8 |
| Access clarity | 53.9 |

**Agent readiness 35.9** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 48.3** — Telecommunications

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/emarsys/](https://apis.io/providers/emarsys/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for SAP Emarsys: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/emarsys/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
