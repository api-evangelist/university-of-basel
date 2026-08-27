---
name: search-humanities-research-data
description: >-
  Search DaSCH humanities research data anonymously — full text, label search, and Gravsearch graph
  queries — then pull the resource, its links, its version history, its IIIF manifest or its TEI
  rendering. All operations in this skill are marked "Publicly accessible" in the DSP-API contract
  and need no credential.
api: university-of-basel:dsp-api
base_url: https://api.dasch.swiss
auth: none
generated: '2026-08-27'
method: generated
source: >-
  Grounded in operationIds verified present in openapi/university-of-basel-api-v2-api-openapi.yml,
  and in https://docs.dasch.swiss/latest/DSP-API/03-endpoints/api-v2/query-language/.
operations:
  - getV2SearchCountSearchterm
  - getV2SearchSearchterm
  - getV2SearchbylabelSearchterm
  - getV2SearchextendedCountP1
  - getV2SearchextendedP1
  - getV2Resources
  - getV2Resourcespreview
  - getV2ResourcesInfo
  - getV2GraphResourceiri
  - getV2SearchincominglinksResourceiri
  - getV2ResourcesHistoryResourceiri
  - getV2ValuesResourceiriValueuuid
  - getV2ResourcesIiifmanifestResourceiri
  - getV2TeiResourceiri
---

# Search humanities research data

Run [discover-projects-and-ontologies](university-of-basel-discover-projects-and-ontologies.md)
first. Gravsearch queries are written against a project's own classes and properties, so you need
the ontology in hand.

## 1. Count before you fetch

Every search endpoint has a count twin. Use it. There is no published rate limit, no
`RateLimit-*` header and no `Retry-After` — the courtesy is yours to supply, and a count call is
the cheapest way to avoid walking a result set you did not want.

- `getV2SearchCountSearchterm` — `GET /v2/search/count/{searchTerm}`
- `getV2SearchextendedCountP1` — `GET /v2/searchextended/count/{query}`

## 2. Pick the right search

- `getV2SearchSearchterm` — `GET /v2/search/{searchTerm}`. Full text across resources.
- `getV2SearchbylabelSearchterm` — `GET /v2/searchbylabel/{searchTerm}`. Label-only; much narrower
  and much faster when you already know roughly what a thing is called.
- `getV2SearchextendedP1` — `GET /v2/searchextended/{query}`. **Gravsearch**, the SPARQL-derived
  graph query language. This is the only way to express a real structural question ("letters written
  from Basel between 1520 and 1540 that mention a named person"). Write it against the classes and
  properties you read from the ontology.

Narrowing parameters that appear across these: `limitToProject`, `limitToResourceClass`,
`limitToStandoffClass`, `offset`, `page`, `page-size`, `order`.

## 3. Handle the 503 correctly

`getV2SearchSearchterm` and `getV2SearchCountSearchterm` are the only two operations in the whole
contract that declare a `503`, and it carries a `SearchTimeoutException`. **This is a per-request
time budget, not a rate limit.** Retrying the identical query will time out identically. Narrow the
term, add `limitToProject` or `limitToResourceClass`, or page with `offset`.

## 4. Pull what you found

- `getV2Resourcespreview` — `GET /v2/resourcespreview`. Lightweight; use for result lists.
- `getV2Resources` — `GET /v2/resources`. Full resources.
- `getV2ResourcesInfo` — `GET /v2/resources/info`.
- `getV2GraphResourceiri` — `GET /v2/graph/{resourceIri}`. The link graph around a resource.
- `getV2SearchincominglinksResourceiri` — `GET /v2/searchIncomingLinks/{resourceIri}`. What points
  *at* this resource, which the resource itself does not tell you.

## 5. Follow the scholarly formats

- `getV2ResourcesIiifmanifestResourceiri` — `GET /v2/resources/iiifmanifest/{resourceIri}`. A IIIF
  Presentation manifest; hand it straight to any IIIF viewer. Images are served by Sipi and support
  IIIF Image API 3.0.
- `getV2TeiResourceiri` — `GET /v2/tei/{resourceIri}`. Standoff-marked text rendered as TEI XML.
- `getV2ResourcesHistoryResourceiri` — `GET /v2/resources/history/{resourceIri}` and
  `getV2ValuesResourceiriValueuuid` — `GET /v2/values/{resourceIri}/{valueUuid}`. Values are
  versioned, never overwritten; history is a first-class read.

## 6. Cite with an ARK, not a URL

Responses carry `knora-api:arkUrl` and `knora-api:versionArkUrl` under NAAN `72163`. The version
ARK resolves to a specific state of the object. Use it in anything you write for a human.

## Deleted resources look like success

A resource that has been soft-deleted still resolves by IRI or ARK, but returns a
`knora-base:DeletedResource` — same IRI, `knora-api:isDeleted: true`, plus `deleteDate` and
sometimes `deleteComment`. Check `isDeleted` before treating a 200 as live data. Deleted resources
never appear in search results.
