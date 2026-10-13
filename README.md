# ortho-data

Static data files for the [ortho-earth](https://www.ortho-earth.com/) demos, served by GitHub Pages:

```
https://kenjiyoshidahome2026-bit.github.io/ortho-data/<path>
```

Every file is plain static content with `access-control-allow-origin: *`, so any page can `fetch` it.
`.geopbf` files are [GeoPBF](https://github.com/kenjiyoshidahome2026-bit/geopbf) (`npm install geopbf`).

## Layout

Files are grouped by the extent of the data, not by the app that reads them:

- `globe/` — worldwide data
- `us/` — data for the United States
- `japan/` — data for Japan

Each folder has a `manifest.json` that lists its files with a short content hash (`{ files: { path: sha1[0:12] } }`).

Names that belong to a database sit next to it (`<DB>.i18n/<lang>.json`) and are published in the same push,
so a database and its names never drift apart.

## globe/ — worldwide data

`manifest.json` lists every file under `globe/` with a short content hash (`{ files: { path: sha1[0:12] } }`).
GitHub Pages has no directory listing, so readers use it to see what changed and which flags exist.

### Countries of the world

Read by [www.ortho-earth.com/world](https://www.ortho-earth.com/world/), the [quiz](https://www.ortho-earth.com/quiz/),
[Equal Earth](https://www.ortho-earth.com/equal/) and the country and city labels of the globe.

| File | Contents | Source |
|---|---|---|
| `NationDB.json` | 262 countries and territories: codes, capital, area, population, GDP, HDI and more | Wikidata (CC0), World Bank, IMF, UNDP |
| `CityDB.json` · `LanguageDB.json` · `CurrencyDB.json` · `Conflicts.json` | capitals and large cities, languages, currencies, disputed territories | Wikidata (CC0) |
| `<DB>.i18n/<lang>.json` | names for that database in 25 languages (English is in the database itself) | Wikidata (CC0) |
| `ne-cities/<lang>.json` | names of the smaller Natural Earth cities | Natural Earth (public domain) |
| `flags/<key>.svg` | flags, by country key | Wikimedia Commons (public domain or as stated per file) |
| `geoms/<key>.png` | locator maps, 512 px | drawn from Natural Earth |
| `sfx.zip` | sound effects of the viewer | OtoLogic (CC BY 4.0) |
| `search/base.json` · `search/<lang>.json` | place-name search index: 13,154 countries, states, cities and landforms | Natural Earth, Wikidata |

### Landforms of the world

Read by [www.ortho-earth.com/globe/physical](https://www.ortho-earth.com/globe/physical).

| File | Contents | Source |
|---|---|---|
| `TerrainDB.json` | ~1,000 landforms: category, representative point, physical quantities | Wikidata (CC0) |
| `TerrainDB.i18n/<lang>.json` | names of those landforms in 25 languages (English is in `TerrainDB.json`) | Wikidata (CC0) |
| `ne-physical.geopbf` | shapes of the landforms (polygons, lines, points, range axes) | Natural Earth (public domain) |
| `ne-physical-lines.geopbf` | equator, tropics, polar circles | Natural Earth (public domain) |
| `plates.geopbf` | plate boundaries and plates | PB2002 — Bird (2003), *An updated digital model of plate boundaries* |
| `climate-koppen.geopbf` | Köppen–Geiger climate classes, 1991–2020 | Beck et al. (2023), CC BY 4.0 |

Compiled data under `globe/`: CC BY-SA 4.0. Each source keeps its own terms as listed above.

## us/ — data for the United States

Read by [www.ortho-earth.com/globe/parks](https://www.ortho-earth.com/globe/parks).

| File | Contents | Source |
|---|---|---|
| `parks-us.json` | the 63 national parks: names in 26 languages, Wikipedia page titles, photo links with their credits, area, date established, visitors, states | Wikidata (CC0); Wikimedia Commons (each photo under its own license, credited in the file); figures from Wikipedia, *List of national parks of the United States* (NPS acreage report 2023, visitation 2025) |
| `parks-us.geopbf` | boundaries of the national parks and their preserves | National Park Service, Land Resources Division — NPS Boundary (public domain) |
| `nps-units.geopbf` | boundaries of the other NPS units (monuments, historic sites, seashores, recreation areas…), grouped by kind | National Park Service, Land Resources Division — NPS Boundary (public domain) |

## japan/ — data for Japan

### National parks

Read by [www.ortho-earth.com/japan/parks](https://www.ortho-earth.com/japan/parks).

| File | Contents | Source |
|---|---|---|
| `parks.json` | the 35 national parks: names in 26 languages, Wikipedia page titles, photo links with their credits, land area, date designated, prefectures | Wikidata (CC0); Wikimedia Commons (each photo under its own license, credited in the file); Ministry of the Environment, list of national parks (2024) |
| `parks.geopbf` | outline of each park (the zoning polygons dissolved per park) | Ministry of the Environment, Environmental Geoportal — national park areas (`nps_all`), processed |

### Landforms

Read by [www.ortho-earth.com/japan/terrain](https://www.ortho-earth.com/japan/terrain).

| File | Contents | Source |
|---|---|---|
| `terrain.json` | ~1,500 landforms: category, representative point, physical quantities, names in Japanese and English | Wikidata (CC0), Wikipedia (CC BY-SA 4.0); the selection follows the annotations of the GSI vector tiles (Geospatial Information Authority of Japan) |
| `terrain.i18n/<lang>.json` | names of those landforms in 24 more languages | Wikidata (CC0) |
| `terrain.geopbf` | shapes: lakes, rivers, axes of mountain ranges and trenches, ocean currents, tectonic lines | lakes — MLIT National Land Numerical Information, Lakes (W09), cut out by name and simplified; rivers — © OpenStreetMap contributors (ODbL), the main stem of each river's waterway relation, joined and simplified. The axes, currents and tectonic lines are drawn by hand |

国土数値情報（湖沼データ）（国土交通省）を加工して作成。 River lines © [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors, available under the Open Database License.

### Hot springs

Read by [www.ortho-earth.com/japan/onsen](https://www.ortho-earth.com/japan/onsen).

| File | Contents | Source |
|---|---|---|
| `onsen.json` | ~2,000 hot springs and the hot-spring areas they belong to: spring quality, prefecture, coordinates, member inns | Japanese Wikipedia (CC BY-SA 4.0); Wikidata (CC0); estimated coordinates © OpenStreetMap contributors (ODbL) and the GSI address search; member inns from the Japan Association of Secluded Hot Spring Inns (日本秘湯を守る会) |

### Railways

Lines and stations of the MLIT railway data (N02) matched to Wikipedia and Wikidata. Details, counts and the matching method in [`rail/README.md`](japan/rail/README.md) (Japanese).

| File | Contents | Source |
|---|---|---|
| `rail/lines.geopbf` | 597 lines (operator × line name), sections joined into one MultiLineString each: Wikidata id, Wikipedia titles (ja/en), length, number of stations, opened/closed | MLIT National Land Numerical Information, Railway (N02-25, FY2025); Wikidata (CC0); Wikipedia titles (CC BY-SA 4.0) |
| `rail/stations.geopbf` | 10,234 station records (station × line): station and group codes, operator, line, Wikidata id, Wikipedia titles | same |
| `rail/station-groups.geopbf` | 9,046 stations grouped by transfer (one article each) | same |
| `rail/stats.json` | counts of the matching (10,231 of 10,234 records matched, 596 of 596 lines) | — |

国土数値情報（鉄道データ）（国土交通省）を加工して作成。

### Landmarks in 3D

Read by [www.ortho-earth.com/japan/models](https://www.ortho-earth.com/japan/models).

| File | Contents | Source |
|---|---|---|
| `models.json` | catalogue of the landmark models: names, where to fly, credits (the GLB files themselves are served elsewhere) | MLIT Project PLATEAU 3D city models (CC BY 4.0) |

### Observation networks

Read by the catalogue of Japanese public GIS data (gishub-jp).

| File | Contents | Source |
|---|---|---|
| `jishin/seismic.geopbf` | seismic observation stations, the yearly lists from 2013 on overlaid (first and last year listed) | Headquarters for Earthquake Research Promotion (地震調査研究推進本部), observation facilities |
| `jishin/fault.geopbf` | upper edges of the source fault models used for ground-motion calculation (not surveyed fault traces) | Headquarters for Earthquake Research Promotion, National Seismic Hazard Maps for Japan 2009, appendix 2 |
| `jma/amedas.geopbf` | AMeDAS weather stations: kind, location, start of observation, instrument heights | Japan Meteorological Agency website (Public Data License 1.0), processed |

### Terms for us/ and japan/

The CC BY-SA 4.0 statement above covers `globe/` only. Files under `us/` and `japan/` are compiled or processed from
the sources listed, and each keeps the terms of its sources. Note in particular that the river lines in `japan/terrain.geopbf`
and the estimated coordinates in `japan/onsen.json` are derived from OpenStreetMap and are under the ODbL.
