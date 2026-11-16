# Porto City Break — interactive map

A single-file, offline-friendly map of **4 walking routes through Porto, exactly as printed in the guide** — Route 1 (17 stops), Route 2 (6), Route 3 (6), Route 4 (3) — over 133 geocoded destinations with photos, opening hours and websites. One route on screen at a time, colour-coded by how badly you shouldn't skip it.

**Live demo:** `https://hamzafelix.github.io/Porto-Map-3Days/`.

![mobile preview](preview-mobile.png)

## What's in it

- **133 pinned destinations** across seven colour-coded areas (Historic Centre / Ribeira, Baixa, West Porto / Boavista, River and Sea, East Porto, Vila Nova de Gaia, Day trips), each numbered per area.
- **83 with photographs** (176 images) — hotlinked Wikimedia thumbs, every one validated against the destination's real coordinates so you don't get a photo of the wrong building in the wrong city.
- **28 opening hours + 34 official websites**, matched from OpenStreetMap tags. Clérigos really does say `Mo-Su 09:00-19:00` and links `torredosclerigos.pt`.
- **Photo viewer** — tap any photo for fullscreen: swipe or arrow keys to flip, double-tap to zoom, drag to pan.
- **Halal food (21)** — 5 explicitly tagged `diet:halal=yes`, the other 16 are kebab/Arab/Pakistani places marked *halal-friendly, not certified*. Deliberately not blurred together.
- **Supermarkets (220)** from OSM, off by default.
- **Four routes, one at a time** — Route 1 (Capela das Almas → Rua de Cedofeita, 17 stops), Route 2 (São Bento → the port lodges, 6), Route 3 (Sé → Santo Ildefonso, 6), Route 4 (Boavista → Serralves, 3). Selecting a route draws only that route, filters the list to its stops **in walking order**, renumbers the pins 1–n and prints the start/finish line. Nothing else is on the map: area chips, halal and supermarket layers are stripped while a route is open. Tap the active route again to get the full city back.
- **Importance from the guide** — every stop is tagged *not to be missed* (blue), *important* (mustard) or *secondary* (magenta). The pin colour, the list badge and a legend under the chips all follow that scale, and each popup says which tier it's in.
- **"Near me"** — hits your GPS, drops a blue dot, re-sorts the whole list by walking distance.
- **Search + area filters**, and a Google Maps directions link on every pin.
- **Vector basemap with tilt and rotate** — MapLibre GL over OpenFreeMap's OpenMapTiles style (no API key, no token): two-finger rotate, two-finger drag to pitch, built-in 3D buildings, plus a **3D** button that flips between flat and 58°. Replaces the old raster Esri/OSM tiles.
- **Mobile-first layout** — full-screen map, floating search card, bottom Map/List tabs, 44px tap targets, safe-area padding, marker clustering so the pins don't turn into spaghetti.
- **KML export** (`porto-destinations.kml`) — 403 placemarks in 17 folders for Google My Maps: the four routes as paths, three importance folders, plus every area, halal and supermarket layer.

## Running it

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Or just open `index.html` — it works from `file://` too. One difference: over `file://` the OpenStreetMap layer stays hidden, because OSM's tile servers reject requests without a `Referer` and serve a "tile usage policy" image instead. Served over http(s) the layer appears automatically.

## What's not here

- **Star ratings.** No free source exists — Google Places, Foursquare and Yelp all need an API key, and I wasn't going to invent numbers.
- **3 destinations are unpinned** (Vodafone Building, Sta. Catarina Chapel Viewpoint, Infante Bridge). The geocoder put them 3km off or collided them with a similarly named place, so they're listed but not mapped rather than pinned at a lie.
- **28 destinations have no photo** — modern office blocks, minor gardens, stretches of old wall. No free image exists.

## Data sources and licences

See [ATTRIBUTION.md](ATTRIBUTION.md). Short version: destinations from the official Visit Porto guide, photos from Wikimedia (CC BY-SA / public domain, credited per popup), map attributes from OpenStreetMap (ODbL), tiles © Esri.

Code is MIT — see [LICENSE](LICENSE). It does not cover the photographs, map tiles or OSM data.

## Files

| File | What |
|---|---|
| `index.html` | the whole app — HTML, CSS, JS and embedded JSON, no build step |
| `porto-destinations.kml` | Google My Maps import |
| `ATTRIBUTION.md` | photo and data credits |
| `preview-mobile.png` | three-phone screenshot |
| `preview-desktop.png` | desktop screenshot |

## Route credits

Route order, start/finish and the blue/mustard/magenta importance scale come from the printed Porto city guide (the "Suggested Routes" pages, p.17-18). Coordinates for the sixteen stops that weren't in the Visit Porto list — Rua de Santa Catarina, Fonte dos Leões, Rua de Miguel Bombarda, Praça de Carlos Alberto, Rua de Cedofeita, Rua das Flores, Praça de Mouzinho de Albuquerque, Praça da República, Igreja da Lapa, Cemitério do Prado do Repouso, plus the Gaia cellars, WOW, cable car, Serra do Pilar, Foz do Douro and Matosinhos — come from OpenStreetMap via Nominatim, bounded to Porto and checked against the map.
