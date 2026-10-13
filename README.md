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

## globe/ — the physical-geography globe

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
