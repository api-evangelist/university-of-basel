---
name: harvest-edoc-open-access
description: >-
  Harvest the University of Basel's open-access institutional repository (edoc) — either through
  OAI-PMH 2.0 for bulk metadata in eleven formats including an OpenAIRE-CRIS stream, or through the
  DSpace 7 HAL+JSON REST API for browsing and item detail. Both are anonymous.
api: university-of-basel:edoc-oai, university-of-basel:edoc-rest
base_url: https://edoc.unibas.ch
auth: none for reads
generated: '2026-08-27'
method: generated
source: >-
  Grounded in live anonymous probes of https://edoc.unibas.ch/server/oai/request and
  https://edoc.unibas.ch/server/api on 2026-08-27 (both HTTP 200). edoc publishes no OpenAPI, so
  this skill is grounded in the OAI-PMH 2.0 and DSpace 7 protocols the server demonstrably speaks,
  not in operationIds.
operations:
  - 'OAI-PMH verb: Identify'
  - 'OAI-PMH verb: ListMetadataFormats'
  - 'OAI-PMH verb: ListSets'
  - 'OAI-PMH verb: ListIdentifiers'
  - 'OAI-PMH verb: ListRecords'
  - 'OAI-PMH verb: GetRecord'
  - 'DSpace REST: GET /server/api (HAL root)'
---

# Harvest edoc, the University of Basel open-access repository

edoc runs **DSpace 7.6.2 / DSpace-CRIS cris-2023.02.06**. It publishes no OpenAPI. Two anonymous
machine interfaces exist and they are good at different things.

## Which interface

- **OAI-PMH** (`https://edoc.unibas.ch/server/oai/request`) for bulk metadata. This is the right
  choice for any complete or incremental harvest.
- **DSpace REST** (`https://edoc.unibas.ch/server/api`) for browsing, search, and pulling a single
  item with its bitstreams. Answers `application/hal+json`; every collection is reachable by
  following `_links` from the root.

## OAI-PMH

### 1. Identify

```
GET /server/oai/request?verb=Identify
```

Confirmed live. Returns `protocolVersion 2.0`, `repositoryName` "edoc: Open Access Repository
University of Basel", `adminEmail` `openaccess@unibas.ch`, `granularity`
`YYYY-MM-DDThh:mm:ssZ`, `deletedRecord` `transient`, and `earliestDatestamp` `2025-04-18T15:42:50Z`.

`deletedRecord: transient` matters: edoc does not guarantee that deletions stay visible in the
harvest stream, so a purely incremental harvester can drift. Re-baseline periodically.

### 2. Choose a metadata format

`GET /server/oai/request?verb=ListMetadataFormats` returns eleven prefixes:

`oai_dc`, `qdc`, `dim`, `mods`, `mets`, `marc`, `rdf`, `ore`, `didl`, `etdms`, `uketd_dc`

Take `oai_dc` for interoperability, `mods` or `marc` for library ingest, `etdms` for theses.

### 3. Harvest

```
GET /server/oai/request?verb=ListIdentifiers&metadataPrefix=oai_dc
GET /server/oai/request?verb=ListRecords&metadataPrefix=oai_dc
GET /server/oai/request?verb=ListRecords&metadataPrefix=oai_dc&from=2026-01-01T00:00:00Z
GET /server/oai/request?verb=GetRecord&metadataPrefix=oai_dc&identifier=oai:edoc.unibas.ch:20.500.14716/199665
```

Page with `resumptionToken`, serially. **No rate limit is published and no `Retry-After` header is
returned**, so pace yourself: one request at a time, and mail `openaccess@unibas.ch` before a full
harvest.

### 4. The OpenAIRE-CRIS stream

`Identify` advertises a second base URL under the OpenAIRE CERIF profile 1.1:

```
https://edoc.unibas.ch/server/oai/openairecris
```

Use it if you are aggregating for OpenAIRE or any CRIS-compatible system.

## Identifiers

Record identifiers are Handle-based: `oai:edoc.unibas.ch:20.500.14716/199665`, under Handle naming
authority `20.500.14716`. Resolve a Handle at `https://hdl.handle.net/20.500.14716/199665`. Persist
the Handle, not the edoc URL.

## DSpace REST

```
GET /server/api                       # HAL root; every endpoint is in _links
GET /server/api/core/items
GET /server/api/discover/search/objects?query=...
GET /server/api/core/bitstreams/{uuid}/content
```

Pagination is Spring Data `?page=&size=` with `_links.next`. Anonymous for public items.
`GET /server/api/authn/status` returns `{"authenticated": false, ...}` and the response advertises
`WWW-Authenticate: password realm="DSpace REST API"` — password login only on the public REST
surface, no Shibboleth method exposed there.

`GET /server/v3/api-docs`, `/server/api/openapi.json` and `/server/swagger.json` all return 404
(probed 2026-08-27). Do not go looking for a spec; use the upstream DSpace 7 REST contract.
