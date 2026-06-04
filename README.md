# University of Basel (university-of-basel)

The University of Basel (Universität Basel), founded in 1460, is the oldest university in Switzerland and is ranked #85 in the QS World University Rankings 2025. This repository catalogs the institution's public, machine-readable developer/API footprint as an [APIs.json](https://apisjson.org) provider profile for the API Evangelist network. Basel does not operate a single central developer portal; instead its public APIs are concentrated in scholarly and research-data infrastructure — the edoc institutional repository, the DaSCH Service Platform API, and the SLSP swisscovery library discovery platform.

- APIs.json: https://raw.githubusercontent.com/api-evangelist/university-of-basel/refs/heads/main/apis.yml
- Run it with Naftiko: https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=university-of-basel-api-evangelist&utm_content=repo

## Type

- Type: Index
- Position: Consumer
- Access: 3rd-Party

## Tags

Education, Higher Education, University, Switzerland, Research Data, Open Access, Institutional Repository, Library, Digital Humanities

## APIs

- **edoc DSpace REST API** — Public DSpace REST API for the University of Basel open-access repository (DSpace-CRIS 7.6.2). Base: `https://edoc.unibas.ch/server/api`. Docs: https://ub.unibas.ch/en/services/dh-digital-services/edoc/
- **edoc OAI-PMH** — OAI-PMH 2.0 metadata harvesting interface for edoc, including an OpenAIRE-CRIS stream. Base: `https://edoc.unibas.ch/server/oai/request`. Docs: https://ub.unibas.ch/en/services/dh-digital-services/edoc/
- **DaSCH DSP-API** — Open-source RDF-based humanities research data API (formerly Knora) developed at the University of Basel by DaSCH. Base: `https://api.dasch.swiss`. Docs: https://docs.dasch.swiss/latest/DSP-API/ — Code: https://github.com/dasch-swiss/dsp-api
- **swisscovery (SLSP Alma) SRU** — Standards-based SRU search/retrieve interface to the SLSP swisscovery/Alma catalogue for the Basel institution zone (41SLSP_UBS). Base: `https://swisscovery.slsp.ch/view/sru/41SLSP_UBS`. Docs: https://ub.unibas.ch/en/search-find/library-catalogues/swisscovery-registration-and-help/

## Plans

See [plans/university-of-basel-plans-pricing.yml](plans/university-of-basel-plans-pricing.yml).

## Rate Limits

See [rate-limits/university-of-basel-rate-limits.yml](rate-limits/university-of-basel-rate-limits.yml).

## FinOps

See [finops/university-of-basel-finops.yml](finops/university-of-basel-finops.yml).

## Timestamps

- Created: 2026-06-03
- Modified: 2026-06-03

## Common Properties

- Website: https://www.unibas.ch/en
- Developer Portal: https://docs.dasch.swiss/latest/DSP-API/
- GitHub: https://github.com/ITS-Unibas
- Source Code: https://github.com/dasch-swiss
- LinkedIn: https://www.linkedin.com/school/university-of-basel/

## Notes

All APIs and properties listed were confirmed against live URLs during research; no endpoints were fabricated. The edoc REST API and OAI-PMH interface both returned HTTP 200, with the OAI Identify verb reporting "edoc: Open Access Repository University of Basel". The DSP-API documentation and `dasch-swiss/dsp-api` repository resolve (HTTP 200), and the live `api.dasch.swiss/v2/ontologies` path returns HTTP 405 on GET (a verb/method is required), which confirms the endpoint exists. The SLSP swisscovery SRU endpoint for the Basel zone resolves (HTTP 200). The UNIverse research portal resolves but exposes no separately documented public API. The LinkedIn school page returns the standard HTTP 999 anti-bot status; the page exists.

## Maintainers

- Kin Lane — kin@apievangelist.com
