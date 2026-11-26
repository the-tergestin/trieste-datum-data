# Trieste Datum — Open Data & JSON Guide

**Website:** https://triestedatum.org  
**Languages:** [English](https://triestedatum.org/) · [Italiano](https://triestedatum.org/it/) · [Slovenščina](https://triestedatum.org/sl/) · [Deutsch](https://triestedatum.org/de/) · [Hrvatski](https://triestedatum.org/hr/)  
**Method & limits:** https://triestedatum.org/method  
**Italian national open-data showcase:** https://www.dati.gov.it/node/529

Trieste Datum is an independent physical reference layer for moving through Trieste, Italy. It fuses Regione Autonoma Friuli Venezia Giulia's 0.5 m LiDAR bare-ground terrain model and regional topographic shapes (DBTfvg) with OpenStreetMap streets, stairs, and pedestrian crossings — plus dated, sourced local facts on public transport, parking, and flat vs. steep areas.

Every published figure is labelled either `measured` (computed from the terrain and street network) or `sourced` (taken from a named source with the date it was read). We publish no guesses and copy no volatile timetables or prices: the two allowances we cannot yet measure — both on the way through a public lift (the time for the lift and the indoor passage) — are marked `"not measured"` where they appear.

## Public Machine-Readable Endpoints

All JSON endpoints are static, open, require no API key, and serve `Access-Control-Allow-Origin: *`.

### Core Guide & Catalog Twins
- **All walks index:** `https://triestedatum.org/walks/index.json`
- **Getting around (city buses, Opicina tram, ferries, airport, cruise berths):** `https://triestedatum.org/getting-around/index.json`
- **Parking (car parks with measured walks to Piazza Unità, blue bays, ZTL, EU disability card, campers):** `https://triestedatum.org/parking/index.json`
- **Where to stay (flat vs. steep Trieste areas, measured climbs & 300 m street-height spreads):** `https://triestedatum.org/where-to-stay/index.json`

### Individual Walk & Place Twins
- **Individual walks:** Every HTML page at `/walks/<slug>` has a companion JSON file at `/walks/<slug>.json` (linked via `<link rel="alternate" type="application/json">`), containing full slope-segmented pieces, walker times, stair counts, pedestrian crossings, coordinates, and provenance.
- **Place comparison hubs:** https://triestedatum.org/places/ — each hub also has a companion `.json` file at `/places/<slug>.json`, for example:
  - Miramare Castle: https://triestedatum.org/places/miramare-castle (`.json`: https://triestedatum.org/places/miramare-castle.json)
  - San Giusto hill: https://triestedatum.org/places/san-giusto (`.json`: https://triestedatum.org/places/san-giusto.json)
  - Stazione Marittima cruise terminal: https://triestedatum.org/places/stazione-marittima (`.json`: https://triestedatum.org/places/stazione-marittima.json)

### Quick Examples (`curl`)

```bash
# List measured walks with distance, climb, steps and step-free availability
curl -s https://triestedatum.org/walks/index.json | jq '.walks[] | {title, distance_m, climb_m, steps_total, step_free}'

# Inspect measured flat vs. steep areas of Trieste
curl -s https://triestedatum.org/where-to-stay/index.json | jq '.'
```

## Licences & Attribution

- **Data files (`.json`):** [Open Database License (ODbL) 1.0](https://opendatacommons.org/licenses/odbl/1-0/)
- **Page text & graphics:** [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)
- **Credit:** `Trieste Datum, triestedatum.org`

### Upstream Sources (keep these credits when reusing)
- **Heights:** Regione Autonoma Friuli Venezia Giulia, [Modelli altimetrici rilievo LIDAR RAFVG 2017–2020 (IRDAT 11826)](https://irdat.regione.fvg.it/consultatore-dati-ambientali-territoriali/detail/irdat/dataset/11826), 0.5 m DTM (flown March 2017; [IODL 2.0](https://www.dati.gov.it/content/italian-open-data-license-v20) — confirmed in writing by IRDAT on 25 Nov 2026 — and [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)).
- **Open paved ground shapes:** Regione Autonoma Friuli Venezia Giulia, DBTfvg ([CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)).
- **Streets, stairs, crossings, and names:** [© OpenStreetMap contributors](https://www.openstreetmap.org/copyright) ([ODbL 1.0](https://opendatacommons.org/licenses/odbl/1-0/)).

*Trieste Datum is an independent project. It is not affiliated with, approved by, or endorsed by Regione Autonoma Friuli Venezia Giulia, the Municipality of Trieste, or OpenStreetMap.*
