# University of Basel (university-of-basel)

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
