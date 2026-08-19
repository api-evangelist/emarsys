---
name: Load custom objects into SAP Emarsys Relational Data (RDS)
description: Insert, update, upsert, replace, query and delete records in Emarsys Relational Data tables — the custom-object layer for purchase, product and loyalty data that lives outside the /api/v2 path space.
api: openapi/emarsys-relational-data-openapi.yml
operations:
  - queryRecordsInRdsTable
  - insertRecordsIntoRdsTable
  - updateRecordsInRdsTable
  - replaceRdsTable
  - upsertRecordsInRdsTable
  - deleteRecordsFromRdsTable
---

# Load custom objects into SAP Emarsys Relational Data

Contacts hold flat, account-defined fields. Anything with cardinality — orders,
line items, loyalty balances, product catalogues — belongs in **Relational Data
(RDS)**.

RDS is the one part of the Emarsys surface that does **not** live under
`/api/v2`. The path space is:

```
/rds/connections/{connectionName}/tables/{tableName}/records
```

It is also the only Swagger 2.0 document in the Core API set that carries real
request/response schemas (7 definitions rather than the shared single "Default
Response" envelope every other batch uses) — so this is the one place the
published contract will actually tell you the shape of a payload.

## Pick the right write verb

| Intent | Operation | Method |
|---|---|---|
| Add new records | `insertRecordsIntoRdsTable` | `POST .../records` |
| Patch existing records | `updateRecordsInRdsTable` | `PATCH .../records` |
| Insert-or-update | `upsertRecordsInRdsTable` | `POST .../records/upsert` |
| Swap the whole table | `replaceRdsTable` | `PUT .../records` |
| Remove records | `deleteRecordsFromRdsTable` | `POST .../records/remove` |

**`replaceRdsTable` replaces the entire table.** It is a `PUT`, it is
idempotent in the HTTP sense, and it will happily wipe a live table if you point
it at the wrong `tableName`. Read the table first with `queryRecordsInRdsTable`
(`GET .../records`) and confirm the row count before you replace anything. There
is no sandbox and no undo.

Prefer `upsertRecordsInRdsTable` for routine synchronisation — it is the only
write here with natural retry-safety, since re-sending the same keyed records
converges rather than duplicating. The rest of this API has no idempotency-key
mechanism at all (`conventions/emarsys-conventions.yml`).

## Connections and tables

`connectionName` and `tableName` are both path parameters and both are
provisioned per account. There is no create-table operation in the published API
— tables are defined in the Emarsys application first, then loaded through this
API.

## Errors

Same envelope as the rest of the Core API: check `replyCode`, not just the HTTP
status. The Relational Data error messages were rewritten by Emarsys on
2024-04-02 and are catalogued in `errors/emarsys-error-codes.yml`.

## Volume

Bulk loads are exactly the workload that hits the **1000 requests per minute per
API user** ceiling and the **10 MB payload** cap. Batch records into fewer, larger
requests up to 10 MB rather than fanning out, and back off on `429` — there is no
`Retry-After` header to tell you how long.
