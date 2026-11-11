# EV Charging

The common EV-charging vocabulary -- the charging locations drivers find, the chargers and connectors at them, the charging sessions drivers start, the tariffs that price them and the charge detail records that bill them -- distilled from the APIs that already exist, the OCPI standard included. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged EV Charging, Electric Vehicles, E-Mobility, eMobility, Charging Infrastructure, OCPP, OCPI in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| charger | 4 | 4 | id 100%, name 75% | chargers 2, connectors 1, evses 1, charge-points 1 |
| charging_session | 3 | 3 | id 100% | sessions 1, charging_sessions 1, charging-sessions 1 |

Cohort: 41 providers with harvested OpenAPI, 4 crosswalks. Of the providers exposing a charger: 25% create, 75% list, 100% fetch, 50% update, 25% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- EV charging publishes the least of any context in the commons: 41 tagged providers, 4 with a charger or session the census can read. Chargers agree on id and name; sessions on an id.
- OCPI -- the roaming standard that defines locations, EVSEs, sessions, tariffs and charge detail records -- does not appear in this cohort as harvested OpenAPI: no provider here publishes an OCPI contract the census can read. The standard exists; its OpenAPI is not in the catalog.
- Measured against OCPI 2.2.1, the standard defines all of a charging session's core and every core property of a charger except a display name -- and it defines locations, tariffs and charge detail records that no provider in the cohort publishes as OpenAPI. OCPI is the spine this context lacked; its crosswalk is in standards/.

## Measured against the standard

The census reads what providers publish. Where the domain has a standard, the standard's own
definition is read as one more voice: how much of the measured core it defines, and what it
defines that no provider in the cohort publishes. Crosswalks are in [standards/](standards).

| Standard | Concept | Core defined by the standard | Fields only the standard has |
| --- | --- | ---: | ---: |
| [ocpi-2.2.1](https://github.com/ocpi/ocpi/tree/release-2.2.1-bugfixes) | `charger` | 50% | 15 |
| [ocpi-2.2.1](https://github.com/ocpi/ocpi/tree/release-2.2.1-bugfixes) | `charging_session` | 100% | 10 |
| [ocpi-2.2.1](https://github.com/ocpi/ocpi/tree/release-2.2.1-bugfixes) | `charging_location` *(not published by the market)* | -- | 26 |
| [ocpi-2.2.1](https://github.com/ocpi/ocpi/tree/release-2.2.1-bugfixes) | `tariff` *(not published by the market)* | -- | 14 |
| [ocpi-2.2.1](https://github.com/ocpi/ocpi/tree/release-2.2.1-bugfixes) | `charge_detail_record` *(not published by the market)* | -- | 30 |

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- Only chargers and charging sessions are published; locations, tariffs and charge detail records were measured and dropped, and are recorded for the next re-measure.
- Chargers cover EVSEs, charge points and charge boxes; sessions are `/charging-sessions`.
- An OCPI pass -- reading the standard's own module definitions as the reference, as the models context does for the OpenAI interface -- would give this context its spine. Noted as the next step rather than done by hand.
- Duplicates merged: Leap into Leapfrog Power.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
