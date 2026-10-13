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
- `japan/` — data for Japan

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

Compiled data: CC BY-SA 4.0. Each source keeps its own terms as listed above.
