# MemberClicks (memberclicks)

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
