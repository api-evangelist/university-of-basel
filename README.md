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

The University of Basel (Universität Basel), founded in 1460, is the oldest university in Switzerland. This repository catalogs the institution's public, machine-readable footprint as an [APIs.json](https://apisjson.org) provider profile for the API Evangelist network. Basel operates no developer portal and no public product API. What it does operate is scholarly infrastructure, federated identity, and the back ends of its own administrative systems — and telling those apart from the vendor and national-infrastructure services running under its name is the whole job here.

- APIs.json: https://raw.githubusercontent.com/api-evangelist/university-of-basel/refs/heads/main/apis.yml
- Run it with Naftiko: https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=university-of-basel-api-evangelist&utm_content=repo

## Type

- Type: university (Public Research University)
- Position: Consumer
- Access: 3rd-Party

## Tags

University, Higher Education, Education, Switzerland, Basel, Research Data, Research Information, Institutional Repository, Open Access, OAI-PMH, Identity Federation, Library, Research Computing

## Surfaces, and who operates them

Every entry carries an `x-operator` in `apis.yml`. At a university that matters more than the artifact count: an institution is a federation of buyers, and most of what appears under its name is somebody else's engineering.

**Institution-operated**

- **UNIverse Research Information System API** — the REST back end of `universe.unibas.ch`, serving an OpenAPI 3.1.0 contract (1,671 paths, 1,170 schemas) and a Swagger UI anonymously, with a bearer token enforced on data paths (401). Base: `https://universe-intern.unibas.ch/api`. The only contract the university itself serves. It is deliberately **not** mirrored into this repository — see `x-harvest-decision` on the entry.
- **edoc DSpace REST API** — the open-access institutional repository, DSpace-CRIS 7.6.2. Base: `https://edoc.unibas.ch/server/api`
- **edoc OAI-PMH** — OAI-PMH 2.0, eleven metadata formats plus an OpenAIRE-CRIS context. Base: `https://edoc.unibas.ch/server/oai/request`
- **SWITCHaai / eduGAIN Identity Provider** — SAML 2.0, entityID `https://aai-logon.unibas.ch/idp/shibboleth`, scope `unibas.ch`, Sirtfi certified, with 32 Basel service providers alongside it in the federation aggregate.
- **sciCORE OpenID Connect Issuer** — Keycloak realm at the university's scientific computing centre. Base: `https://iam.scicore.unibas.ch/realms/switch-eduid`
- **ADAM (ILIAS) LTI launch endpoint** — `https://adam.unibas.ch/lti.php`

**Tenant — Basel's data, somebody else's contract**

- **swisscovery (SLSP / Ex Libris Alma) SRU** — Basel holds the 41SLSP_UBS institution zone; SLSP AG runs the platform. Base: `https://swisscovery.slsp.ch/view/sru/41SLSP_UBS`

**Removed 2026-08-30 — not Basel's**

The DaSCH Service Platform API (`api.dasch.swiss`) was catalogued here as Basel's from 2026-06-03 until 2026-08-30. It is not. DaSCH is a legally independent association — its legal notice names DaSCH at Kornhausgasse 7, 4051 Basel, and its about page states it acts "independently of any single Higher Education Institution" — which the University of Basel hosts and part-funds. The contract names DaSCH as `info.contact` and `api.dasch.swiss` as its only server. Six OpenAPI contracts, eight `apis[]` entries and 45 derived artifacts were removed. The hosting relationship is a real institutional fact and is recorded in the profile description and in `x-coverage`; the engineering credit is not Basel's to take.

## Standards actually spoken

Verified against live documents, not prose: OAI-PMH 2.0, ORCID, DataCite (provider ILEN), Crossref (member 27920), SAML 2.0, Shibboleth/SWITCHaai/eduGAIN, LTI, OpenID Connect Discovery, OpenAPI 3.1, HAL. See [conformance/university-of-basel-conformance.yml](conformance/university-of-basel-conformance.yml). Probed and absent: SCIM, OneRoster, Ed-Fi, Caliper, QTI.

## Plans

See [plans/university-of-basel-plans-pricing.yml](plans/university-of-basel-plans-pricing.yml).

## Rate Limits

See [rate-limits/university-of-basel-rate-limits.yml](rate-limits/university-of-basel-rate-limits.yml).

## FinOps

See [finops/university-of-basel-finops.yml](finops/university-of-basel-finops.yml).

## Timestamps

- Created: 2026-06-03
- Modified: 2026-08-30

## Common Properties

- Website: https://www.unibas.ch/en
- GitHub Organization: https://github.com/ITS-Unibas
- Source Code: https://github.com/RISE-UNIBAS
- Research Repository: https://edoc.unibas.ch/
- Identity Federation: https://metadata.aai.switch.ch/metadata.switchaai.xml
- Research Computing: https://scicore.unibas.ch/
- Course Catalog: https://vorlesungsverzeichnis.unibas.ch/en/course-directory
- AI Policy: https://www.unibas.ch/en/Studies/Learning-and-Teaching/AI-in-learning-and-teaching.html
- LinkedIn: https://www.linkedin.com/school/university-of-basel/

## Notes

Every URL in this profile was fetched and its status recorded on 2026-08-30; nothing was credited from link presence alone. Two soft-200 traps were caught and are recorded as absences rather than documents: `universe.unibas.ch` and `forschdb2.unibas.ch` return the same 384 KB Angular shell at HTTP 200 on every probed API path, and `universe-intern.unibas.ch` returns HTTP 200 with that shell on every `/.well-known/` path including `security.txt`. Confirmed absent by DNS: `api.unibas.ch`, `data.unibas.ch`, `developer.unibas.ch`, `opendata.unibas.ch`, `research.unibas.ch`. The University of Basel runs a public vulnerability disclosure program on Intigriti but publishes no `/.well-known/security.txt` anywhere.

## Maintainers

- Kin Lane — kin@apievangelist.com
