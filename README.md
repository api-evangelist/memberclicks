# MemberClicks (memberclicks)

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

MemberClicks is association and membership management software owned by **Personify** and marketed as "MemberClicks by Personify". Its flagship **MC Professional** platform (formerly branded **Oasis**) is an all-in-one association management system (AMS) for professional associations, chambers of commerce, and trade groups - covering member profiles and databases, dues and invoicing, event registration, email and communications, community groups, and websites.

MemberClicks exposes a **documented public/partner developer API**: the **MC Professional API**, a JSON REST interface protected by the **OAuth 2.0** authorization framework. It is hosted per organization at `https://{orgId}.memberclicks.net`, and the developer help center explicitly notes the API is "intended for use by developers with technical expertise" and that MemberClicks support "is unable to assist with custom integrations."

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/memberclicks/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/memberclicks/refs/heads/main/apis.yml)

## Access Model

- **Real, documented, but gated.** This is not an open self-serve API. Access requires per-organization OAuth 2.0 client credentials (a client ID and secret) provisioned inside an MC Professional account under API Management. There is no public sandbox or open key issuance.
- **Per-tenant host.** Every organization has its own host, `https://{orgId}.memberclicks.net`, where `{orgId}` is the organization's MC Professional ID. There is no single global API hostname.
- **OAuth 2.0.** Clients obtain an access token by POSTing to `/oauth/v1/token` with the client ID and secret Base64-encoded in an HTTP Basic `Authorization` header. The requested scope is `read`, `write`, or `read write`. Every resource request then sends `Authorization: Bearer <token>` and `Accept: application/json`.
- **Developer documentation gate.** The detailed API reference lives in the MemberClicks help center (`help.memberclicks.com`), which is protected by Cloudflare/bot challenges and is not machine-fetchable without a browser session. The endpoints in this catalog were captured from the public help-center overview and search excerpts.

## Documented Resources

The MC Professional API is a JSON REST interface. Confirmed resources and endpoints include:

- **Profiles** - `GET /api/v1/profile` (list, paged), `GET /api/v1/profile/{profileId}` (retrieve), `POST /api/v1/profile` (create), and profile update.
- **Profile Search** - `POST /api/v1/profile/search` (create a search over the membership database).
- **Attributes** - list attributes and `GET /api/v1/attribute/{attributeId}/selection` (selection-set options for a custom attribute).
- **Member Types** - `GET /api/v1/member-type`.
- **Member Statuses** - `GET /api/v1/member-status`.
- **Continuing Education** - `GET /api/v1/continuing-education/credit` (filter by `profileId`, `pageNumber`, `pageSize`; max page size 100) and `GET /api/v1/continuing-education/credit/{creditId}`.
- **Countries** - reference lookup of countries.
- **Groups** - group membership, surfaced via a `groupsUrl` reference on a profile's group built-in attribute.
- **Events** - an Events API resource is documented in the developer help center.

Group and Event endpoint paths are **modeled** in this catalog: the resources are documented, but the exact request paths are behind the gated developer documentation and were not reproduced verbatim. See `review.yml` for the honest breakdown of what is confirmed versus modeled.

There is also an older **Oasis** generation of the API still referenced in the help center; the current documentation is branded MC Professional.

## Tags

- Membership Management
- Association Management
- AMS
- Nonprofit
- Events
- CRM
- Personify

## Timestamps

- **Created:** 2026-07-05
- **Modified:** 2026-07-05

## APIs

### MemberClicks Profiles API

Retrieve, create, and update member/contact profiles - the core people records in MC Professional.

- **Human URL:** [API Resources: Retrieve Profiles](https://help.memberclicks.com/hc/en-us/articles/15442882233485-API-Resources-Retrieve-Profiles)
- **Base URL:** `https://{orgId}.memberclicks.net/api/v1`

### MemberClicks Profile Search API

Create a profile search by POSTing criteria to `/api/v1/profile/search`, then page through matching profiles.

- **Human URL:** [API Resources: Profile Search](https://help.memberclicks.com/hc/en-us/articles/15442958956813-API-Resources-Profile-Search)
- **Base URL:** `https://{orgId}.memberclicks.net/api/v1`

### MemberClicks Attributes API

Describe the profile schema - list attributes and retrieve selection-set options via `/api/v1/attribute/{attributeId}/selection`.

- **Human URL:** [API Resources: Attributes](https://help.memberclicks.com/hc/en-us/articles/15442877631373-API-Resources-Attributes)
- **Base URL:** `https://{orgId}.memberclicks.net/api/v1`

### MemberClicks Member Types and Statuses API

Reference-data lookups: `GET /api/v1/member-type` and `GET /api/v1/member-status`.

- **Human URL:** [API Resources: Member Types](https://help.memberclicks.com/hc/en-us/articles/15442888509581-API-Resources-Member-Types)
- **Base URL:** `https://{orgId}.memberclicks.net/api/v1`

### MemberClicks Groups API

Read the groups a profile belongs to (surfaced via `groupsUrl`). Exact paths modeled.

- **Human URL:** [API section](https://help.memberclicks.com/hc/en-us/sections/14749781143437-API)
- **Base URL:** `https://{orgId}.memberclicks.net/api/v1`

### MemberClicks Events API

Read event and registration data. Documented resource; exact paths modeled.

- **Human URL:** [API Resources: Events](https://help.memberclicks.com/hc/en-us/articles/15442887570573-API-Resources-Events)
- **Base URL:** `https://{orgId}.memberclicks.net/api/v1`

### MemberClicks Continuing Education API

List and retrieve continuing education credits earned by members.

- **Human URL:** [API Resources: Continuing Education](https://help.memberclicks.com/hc/en-us/articles/15442888723341-API-Resources-Continuing-Education)
- **Base URL:** `https://{orgId}.memberclicks.net/api/v1`

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/memberclicks)
- [Website](https://memberclicks.com)
- [Documentation](https://help.memberclicks.com/hc/en-us/sections/14749781143437-API)
- [Sign Up / API Management](https://help.memberclicks.com/hc/en-us/articles/18581108667021-API-Management)
- [Plans](plans/memberclicks-plans-pricing.yml)
- [Rate Limits](rate-limits/memberclicks-rate-limits.yml)
- [Fin Ops](finops/memberclicks-finops.yml)

## Pricing

MemberClicks does not publish per-call API pricing; the API is included with an MC Professional (or MC Trade) subscription. Platform subscriptions are quoted by the size and needs of the organization and are billed annually, with reported entry pricing around **$3,500/year** and implementation from roughly $500 to $5,000+. Get a quote from [MemberClicks pricing](https://memberclicks.com/membership-software-pricing/).

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
