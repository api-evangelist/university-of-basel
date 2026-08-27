---
name: discover-projects-and-ontologies
description: >-
  Find a DaSCH research project and read the ontology that defines the shape of its data, before
  attempting any read or write against DSP-API. This is the mandatory first step for any DSP work:
  there is no global content schema, so a resource's valid shape is whatever the project's ontology
  declares.
api: university-of-basel:dsp-api
base_url: https://api.dasch.swiss
auth: none required for every operation in this skill
generated: '2026-08-27'
method: generated
source: >-
  Grounded in operationIds verified present in openapi/university-of-basel-admin-api-api-openapi.yml
  and openapi/university-of-basel-api-v2-api-openapi.yml, and in
  https://docs.dasch.swiss/latest/DSP-API/02-dsp-ontologies/knora-base/.
operations:
  - getHealth
  - getVersion
  - getAdminProjects
  - getAdminProjectsShortcodeProjectshortcode
  - getAdminProjectsKeywords
  - getV2OntologiesMetadata
  - getV2OntologiesAllentitiesOntologyiri
  - getV2OntologiesClassesClassiri
---

# Discover projects and ontologies

Every DSP project owns its own data model. There is no shared content schema, so you cannot
construct a valid query — let alone a valid write — until you have read the project's ontology.
Do these steps in order.

## 1. Confirm the service is up and note the version

- `getHealth` — `GET /health`. Returns
  `{"name":"AppState","severity":"non fatal","status":true,"message":"Application is healthy"}`.
- `getVersion` — `GET /version`. Returns the running `webapi`, `fuseki`, `scala` and `sipi`
  versions. Record `webapi`; the API surface changes weekly and v37.0.0 renamed a project field.

Neither needs a credential.

## 2. Find the project

- `getAdminProjects` — `GET /admin/projects`. Lists every project.
- `getAdminProjectsShortcodeProjectshortcode` — `GET /admin/projects/shortcode/{projectShortcode}`.
  The shortcode is a **4-digit hexadecimal string** (the contract's own example is `0001`). This is
  the handle to prefer; IRIs and shortnames also work but are longer-lived only by convention.
- `getAdminProjectsKeywords` — `GET /admin/projects/Keywords` if you are browsing by subject.

Keep `id` (the project IRI, e.g. `http://rdfh.ch/projects/0001`) and `ontologies` from the response.
`ontologies` is the list you need for step 3.

## 3. Read the ontologies

- `getV2OntologiesMetadata` — `GET /v2/ontologies/metadata` for the metadata of all ontologies, or
  scope it with `?limitToProject={projectIri}`.
- `getV2OntologiesAllentitiesOntologyiri` — `GET /v2/ontologies/allentities/{ontologyIri}`. **This
  is the one that matters.** It returns every resource class and property the project defines,
  with their cardinalities.
- `getV2OntologiesClassesClassiri` — `GET /v2/ontologies/classes/{classIri}` for a single class.

## 4. Choose your response shape before you parse

DSP-API v2 negotiates both serialisation and semantics. Set these deliberately:

- `Accept:` one of `application/ld+json` (default), `text/turtle`, `application/trig`,
  `application/n-quads`, `application/rdf+xml`.
- `x-knora-accept-schema:` complex or simple ontology schema.
- `x-knora-json-ld-rendering:` flat or hierarchical JSON-LD.
- `x-knora-accept-markup:` how standoff markup comes back.

The `schema` and `markup` query parameters are equivalents if you cannot set headers.

## Errors you will actually hit

- `404` with `{"message": "..."}` — wrong shortcode, or the project is soft-deleted.
- `400 GravsearchException` only appears once you reach the search skill; ontology reads fail with
  `BadRequestException` on a malformed IRI.
- No `Retry-After` and no rate-limit header exists. Pace yourself.

## Do not

- Do not assume a class or property name from another project. Ontologies are per-project.
- Do not cache an ontology across a `webapi` major version bump without re-reading it.
