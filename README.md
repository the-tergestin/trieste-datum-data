# Trieste Datum — Open Data & AI Endpoints

**Website:** https://triestedatum.org  
**For AIs & programs:** https://triestedatum.org/world/ · https://triestedatum.org/llms.txt  
**Languages:** [English](https://triestedatum.org/) · [Italiano](https://triestedatum.org/it/) · [Slovenščina](https://triestedatum.org/sl/) · [Deutsch](https://triestedatum.org/de/) · [Hrvatski](https://triestedatum.org/hr/)  
**Guides:** https://triestedatum.org/guides/ · **Arrange (public channels):** https://triestedatum.org/actions/ · **Bora & shade:** https://triestedatum.org/bora/  
**Method & limits:** https://triestedatum.org/method  
**Italian national open-data showcase:** https://www.dati.gov.it/node/529

Trieste Datum is a copy of Trieste, Italy, being built for AIs: to read, to find their way through, and to act through. It fuses Regione Autonoma Friuli Venezia Giulia's 0.5 m LiDAR ground and surface models and regional topographic outlines (DBTfvg) with OpenStreetMap streets, stairs, and pedestrian crossings; dated official sources on public transport, parking, flat vs. steep areas, Bora climatology, and public channels for 102 things to arrange (245 channels); plus 15-minute live weather, sea-level, and alert readings.

## Four Evidence Labels

Every published fact carries an explicit label in the data (and where helpful on the page):

- **`measured`** — computed by Trieste Datum from Regione FVG's 0.5 m terrain and surface models and the OpenStreetMap street network (distances, heights, climb, slopes, horizon angles, solar shade, station counts).
- **`sourced`** — taken from a named source with the date it was read (streets, stairs, counted steps, names, transport, parking, opening facts, public channels, station records).
- **`reasoned`** — worked out from measured and sourced facts, and never passed off as either (walking times, steps estimated from stair height, public lift allowances, upwind building/wall verdicts in a Bora).
- **`verified`** — confirmed by an independent second check, such as a dated open photograph matching an independent OpenStreetMap ground survey, two independent official sources agreeing on the same fact, or ISPRA's harbour instrument tracking the regional waterfront station's wind speed (speed only, not gusts).

We copy no volatile timetables or prices and link to the operator's page with the day we read it.

## Primary Machine-Readable Doors

All endpoints are open, require no API key, and serve `Access-Control-Allow-Origin: *`.

- **Whole-city graph (`/world.json`, format 1.0, ODbL 1.0):** `https://triestedatum.org/world.json`  
  39 places and 445 connections (43 full walks with pages, 400 headline walks between other pairs of places, the Park San Giusto public lift, and the Opicina tram), with field-by-field `basis_by_field`, linked `action_ids`, Bora/shade summaries, and a self-contained `reading_guide`.
- **Public channels directory (`/actions/index.json`, ODbL 1.0 · page at `/actions/` in 5 languages):** `https://triestedatum.org/actions/index.json`  
  102 things a visitor may need to arrange (245 public channels across 7 domains: transit, ferries/cruise terminal, taxis, parking/ZTL/disability permits, cultural sites, tourism InfoPoints, civic/health), with explicit `automation_barriers`, `inputs_required`, and per-URL source read dates.
- **Bora wind & shade (`/bora/index.json`, ODbL 1.0 · page at `/bora/` in 5 languages):** `https://triestedatum.org/bora/index.json`  
  One observed 12-month cycle (May 2025 – April 2026) of ENE (`40°–90°`) Bora gusts at the waterfront and on the Karst from Regione FVG Civil Protection, plus 0.5 m 3D surface shares of what stands upwind close by (buildings and free-standing walls only; never trees or slopes) and solar shade (21 June 13:00 & 17:00, 21 December 12:00) across all 43 walks and their places. Never use it to say a place is calm, to rank windiness, or whether a Bora warning is in force.
- **Live readings (`/live.json`, CC BY 4.0):** `https://triestedatum.org/live.json`  
  Read every 15 minutes from Regione FVG Civil Protection (Molo Fratelli Bandiera waterfront + Borgo Grotta Gigante & Sgonico Karst weather; Molo Sartorio sea level), ISPRA Rete Mareografica Nazionale (Molo della Lega Navale harbour weather), and the National Civil Protection hydrological/storm bulletin for *Bacino di Levante / Carso*. Stale readings are withheld as `"stale"` or `"not known"` after 30–45 minutes; `bora_warning` explicitly stays `"not known"` and links to the Region's alerts page (`https://www.protezionecivile.fvg.it/it/allerte`).
- **Model & developer docs:** `https://triestedatum.org/world/` (HTML + `DataCatalog` JSON-LD) and `https://triestedatum.org/llms.txt` (`text/plain`).

## Guide, Walk & Place JSON Twins (ODbL 1.0)

- **All guides overview (5 languages):** `https://triestedatum.org/guides/`
- **All walks index:** `https://triestedatum.org/walks/index.json`
- **Getting around (city buses, Opicina tram, ferries, airport, cruise berths):** `https://triestedatum.org/getting-around/index.json`
- **Parking (car parks with measured walks to Piazza Unità, blue bays, ZTL, EU disability card, campers):** `https://triestedatum.org/parking/index.json`
- **Where to stay (flat vs. steep Trieste areas, measured climbs & 300 m street-height spreads):** `https://triestedatum.org/where-to-stay/index.json`
- **Bora and shade (station counts, upwind building shares, summer/winter shade):** `https://triestedatum.org/bora/index.json`
- **Individual walks:** Every HTML page at `/walks/<slug>` has a twin at `/walks/<slug>.json` (linked via `<link rel="alternate" type="application/json">`), with slope-segmented pieces, walker times, flight-by-flight stairs, verified photo counts and handrails where seen, pedestrian crossings, Bora/shade shares, coordinates, and provenance.
- **Place comparison hubs:** https://triestedatum.org/places/ — each hub has a twin at `/places/<slug>.json`:
  - Miramare Castle: https://triestedatum.org/places/miramare-castle (`.json`: https://triestedatum.org/places/miramare-castle.json)
  - San Giusto hill: https://triestedatum.org/places/san-giusto (`.json`: https://triestedatum.org/places/san-giusto.json)
  - Stazione Marittima cruise terminal: https://triestedatum.org/places/stazione-marittima (`.json`: https://triestedatum.org/places/stazione-marittima.json)

### Quick Examples (`curl`)

```bash
# Inspect the whole-city graph metadata and counts
curl -s https://triestedatum.org/world.json | jq '{format_version, counts, last_updated}'

# Check Bora climatology summary and 43-walk upwind shares
curl -s https://triestedatum.org/bora/index.json | jq '{last_updated, waterfront_days: .stations.waterfront.days, all_walks}'

# Check live waterfront wind and Molo Sartorio sea level
curl -s https://triestedatum.org/live.json | jq '{generated_at, sea_level: .sea_level.reading, waterfront: .weather.stations[0]}'

# List things to arrange by domain
curl -s https://triestedatum.org/actions/index.json | jq '{count, by_domain}'
```

## Licences & Attribution

- **Static data files (`/world.json`, `/actions/index.json`, `/bora/index.json`, guides, walks, places):** [Open Database License (ODbL) 1.0](https://opendatacommons.org/licenses/odbl/1-0/)
- **Live readings (`/live.json`):** [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)
- **Page text & graphics:** [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)
- **Credit:** `Trieste Datum, triestedatum.org`

### Upstream Sources (keep these credits when reusing)
- **Heights & 3D surface model:** Regione Autonoma Friuli Venezia Giulia, [Modelli altimetrici rilievo LIDAR RAFVG 2017–2020 (IRDAT 11826)](https://irdat.regione.fvg.it/consultatore-dati-ambientali-territoriali/detail/irdat/dataset/11826), 0.5 m DTM & DSM (flown March 2017; [IODL 2.0](https://www.dati.gov.it/content/italian-open-data-license-v20) — confirmed in writing by IRDAT on 25 Nov 2026 — and [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)).
- **Open paved ground, building & free-standing wall outlines:** Regione Autonoma Friuli Venezia Giulia, DBTfvg ([CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)).
- **Streets, stairs, crossings, and names:** [© OpenStreetMap contributors](https://www.openstreetmap.org/copyright) ([ODbL 1.0](https://opendatacommons.org/licenses/odbl/1-0/)).
- **Weather stations, sea level & hydrological alerts (`/live.json` & `/bora/index.json`):** Protezione Civile della Regione Autonoma Friuli Venezia Giulia ([CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)), ISPRA Rete Mareografica Nazionale ([CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)), and Dipartimento della Protezione Civile ([CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)).

*Trieste Datum is an independent project. It is not affiliated with, approved by, or endorsed by Regione Autonoma Friuli Venezia Giulia, the Municipality of Trieste, ISPRA, Dipartimento della Protezione Civile, or OpenStreetMap.*
