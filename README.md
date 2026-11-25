# Trieste Datum — Open Data & JSON Guide

**Website:** https://triestedatum.org  
**Method & limits:** https://triestedatum.org/method  
**Walks catalog (JSON):** https://triestedatum.org/walks/index.json

Trieste Datum is an independent physical reference layer for walking in Trieste, Italy. It fuses Regione Autonoma Friuli Venezia Giulia's 0.5 m LiDAR bare-ground terrain model and regional topographic shapes (DBTfvg) with OpenStreetMap streets, stairs, and pedestrian crossings to publish measured distances, elevation profiles, sustained 20 m slopes, step counts, and stair-avoiding alternatives.

Every published figure is labelled either `measured` (computed from the terrain and street network) or `sourced` (taken from a named source with its date). We publish no guesses: the few things we have to assume, such as the 2 minutes allowed for a public lift, are marked as assumptions ("not measured") where they appear.

## Public Machine-Readable Endpoints

All JSON endpoints are static, open, require no API key, and serve `Access-Control-Allow-Origin: *`.

- **All walks index:** `https://triestedatum.org/walks/index.json`
- **Individual walk twins:** Every HTML page at `/walks/<slug>` has a companion JSON file at `/walks/<slug>.json` (linked via `<link rel="alternate" type="application/json">`), containing full slope-segmented pieces, walker times, stair counts, pedestrian crossings, coordinates, and provenance.
- **Place comparison hubs:**
  - Reaching Miramare Castle (4 approaches): https://triestedatum.org/places/miramare-castle (`.json`: https://triestedatum.org/places/miramare-castle.json)
  - Reaching San Giusto hill (4 hubs): https://triestedatum.org/places/san-giusto (`.json`: https://triestedatum.org/places/san-giusto.json)
  - On foot from Stazione Marittima cruise terminal (5 walks): https://triestedatum.org/places/stazione-marittima (`.json`: https://triestedatum.org/places/stazione-marittima.json)

### Quick Example (`curl`)

```bash
curl -s https://triestedatum.org/walks/index.json | jq '.walks[] | {title, distance_m, climb_m, steps_total, step_free}'
```

## Licences & Attribution

- **Data files (`.json`):** [Open Database License (ODbL) 1.0](https://opendatacommons.org/licenses/odbl/1-0/)
- **Page text & graphics:** [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)
- **Credit:** `Trieste Datum, triestedatum.org`

### Upstream Sources (keep these credits when reusing)
- **Heights:** Regione Autonoma Friuli Venezia Giulia, [Modelli altimetrici rilievo LIDAR RAFVG 2017–2020 (IRDAT 11826)](https://irdat.regione.fvg.it/consultatore-dati-ambientali-territoriali/detail/irdat/dataset/11826), 0.5 m DTM (flown March 2017; [IODL 2.0](https://www.dati.gov.it/content/italian-open-data-license-v20) and [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)).
- **Open paved ground shapes:** Regione Autonoma Friuli Venezia Giulia, DBTfvg ([CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)).
- **Streets, stairs, crossings, and names:** [© OpenStreetMap contributors](https://www.openstreetmap.org/copyright) ([ODbL 1.0](https://opendatacommons.org/licenses/odbl/1-0/)).

*Trieste Datum is an independent project. It is not affiliated with, approved by, or endorsed by Regione Autonoma Friuli Venezia Giulia, the Municipality of Trieste, or OpenStreetMap.*
