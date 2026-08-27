---
name: delete-dsp-content-safely
description: >-
  Remove content from DSP-API without destroying an archive. DSP draws a hard line between DELETE
  (soft, retained, the IRI still resolves) and ERASE (permanent, irrecoverable, stated in capitals
  by the provider). It also publishes a family of can-delete pre-flight checks that let you rehearse
  the decision. This skill is the order of operations.
api: university-of-basel:dsp-api
base_url: https://api.dasch.swiss
auth: bearer JWT required for every write; the can-delete checks are mostly anonymous
generated: '2026-08-27'
method: generated
source: >-
  Grounded in operationIds verified present in openapi/*.yml in this repository, and in
  https://docs.dasch.swiss/latest/DSP-API/03-endpoints/api-v2/editing-resources/ and
  https://docs.dasch.swiss/latest/DSP-API/03-endpoints/api-admin/users/.
operations:
  - postV2Authentication
  - getV2ResourcesCandelete
  - getV2OntologiesCandeleteclassResourceclassiri
  - getV2OntologiesCandeletepropertyPropertyiri
  - getV2OntologiesCandeleteontologyOntologyiri
  - postV2OntologiesCandeletecardinalities
  - getAdminListsCandeleteP1
  - postV2ResourcesDelete
  - postV2ValuesDelete
  - postV2ResourcesErase
  - postV2ValuesErase
  - deleteV2Authentication
---

# Delete DSP content safely

## The distinction that matters

| Verb | What happens | Reversible? |
|---|---|---|
| `delete` | The object is **marked** deleted. Triples are retained. IRI and ARK still resolve, returning a `knora-base:DeletedResource` with `deleteDate`. It disappears from search. | Data survives, but **no un-delete route is published** for resources or values. Treat it as one-way through the API. |
| `erase` | The object and all its versions are **removed from the triplestore**. The contract's own words: "This will permanently and irrecoverably remove the project and all its assets." | **No.** Never. |
| admin user / group `delete` | Sets `status` to `false`. The record is retained. | **Yes** — set `status` back to `true`. This is the only documented reversal in the estate. |

## 1. Authenticate

`postV2Authentication` — `POST /v2/authentication` with
`{"identifier_type": "email", "password": "..."}`. Keep the returned `token` and send it as
`Authorization: Bearer <token>`. Call `deleteV2Authentication` (`DELETE /v2/authentication`) when
you are done; it invalidates the token server-side.

## 2. Rehearse — always

DSP publishes real pre-flight checks. They perform no write. Run the one that matches:

- `getV2ResourcesCandelete` — `GET /v2/resources/candelete`
- `getV2OntologiesCandeleteclassResourceclassiri` — `GET /v2/ontologies/candeleteclass/{resourceClassIri}`
- `getV2OntologiesCandeletepropertyPropertyiri` — `GET /v2/ontologies/candeleteproperty/{propertyIri}`
- `getV2OntologiesCandeleteontologyOntologyiri` — `GET /v2/ontologies/candeleteontology/{ontologyIri}`
- `postV2OntologiesCandeletecardinalities` — `POST /v2/ontologies/candeletecardinalities`
- `getAdminListsCandeleteP1` — `GET /admin/lists/candelete/{listIri}`

An ontology entity generally cannot be deleted while data uses it, which is exactly what these
answer. There is **no** dry-run for create or update — only for delete.

## 3. Read the current lastModificationDate

Every mutation body carries `knora-api:lastModificationDate` as an `xsd:dateTimeStamp`. It must be
the value you just read. If someone wrote in between, you get `409 EditConflictException` — which is
the system doing its job. Re-read, then re-issue. There is no `Idempotency-Key` header in this API;
this timestamp is the only concurrency guard.

## 4. Soft-delete

`postV2ResourcesDelete` — `POST /v2/resources/delete`, body:

```json
{
  "@id": "http://rdfh.ch/0001/a-thing",
  "@type": "anything:Thing",
  "knora-api:lastModificationDate": {
    "@type": "xsd:dateTimeStamp",
    "@value": "2019-02-05T17:05:35.776747Z"
  },
  "knora-api:deleteComment": "This resource was created by mistake.",
  "@context": { "knora-api": "http://api.knora.org/ontology/knora-api/v2#" }
}
```

`knora-api:deleteComment` is optional and you should always supply it — it is the only explanation a
future reader gets. `knora-api:deleteDate` is optional and defaults to now.

`postV2ValuesDelete` — `POST /v2/values/delete` is the same pattern for a single value, and needs
the resource id and type, the property, and the value's id and type.

## 5. Stop before erase

`postV2ResourcesErase`, `postV2ValuesErase`, `postV2ValuesErasehistory` and
`DELETE /admin/projects/shortcode/{shortcode}/erase` are permanent. They require SystemAdmin (or
ProjectAdmin) and they are the operations an autonomous agent must never take on its own. Escalate
to a human, name the exact object, and quote the `candelete` result.

## Verify

After a soft-delete, `GET` the IRI again. A correct result is a **200** carrying
`"knora-api:isDeleted": true` and `@type: knora-api:DeletedResource`, not a 404. If you get a 404
you had the wrong IRI to begin with.
