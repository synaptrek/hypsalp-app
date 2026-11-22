# HypsAlp

**Altimeter & mountain tools for iPhone.**

HypsAlp (capital H, capital A, pronounced "ipsalp" - from *hýpsos*, Greek for "height", and Alp) is a barometric altimeter for the mountains with a set of offline tools around it. Its core separates the two causes of a pressure change, a change of altitude and a change of weather, and estimates both at once. The tools (compass, slope, height difference, daylight and way back, sun and shade, moon, lightning distance, oxygen, boiling point, snow profile notebook, emergency card) reuse the same sensors and the same terrain data. Everything runs on-device and works offline: the app itself makes no network calls. Terrain data for Europe comes in regional packs that iOS downloads from Apple's servers.

<a href="https://apps.apple.com/it/app/hypsalp/id6823210152?itscg=30200&itsct=apps_box_badge&mttnsubad=6823210152" style="display: inline-block;">
    <img src="https://toolbox.marketingtools.apple.com/api/v2/badges/download-on-the-app-store/black/en-us?releaseDate=1794268800" alt="Download on the App Store" style="height: 50px; vertical-align: middle; object-fit: contain;" />
</a>


## What's in this repository

| Item | Content |
|---|---|
| `index.html` | Support, Privacy Policy and Terms of Use, published with GitHub Pages at **[synaptrek.github.io/hypsalp-app](https://synaptrek.github.io/hypsalp-app/)**. This is the Privacy Policy URL used on the App Store and in the app. |
| `points_dataset_ODbL/points.json.gz` | The dataset of summits, saddles, passes, huts and bivouacs contained in the app's terrain packs, released under the **ODbL 1.0**. |
| `README.md` | This file. |

The app's source code is **not** included: HypsAlp is proprietary software.

## Privacy in short

HypsAlp does not collect any data. There is no account, no advertising, no analytics, no tracking, no third-party SDK and no server. The app uses only Apple frameworks and makes no network calls of its own. Terrain packs are downloaded by iOS from Apple's servers, in the same way as the app itself: the Alps pack automatically when the app is installed or updated, every other region only when you choose to download it. Nothing about you, your location or your measurements is sent with these downloads, and the developer receives no personal data. Everything you record or save stays on your iPhone, and data leaves the device only when you explicitly export or share it. The App Store privacy label is **"Data Not Collected"**.

The full policy, including your rights under the GDPR, is on the [web page](https://synaptrek.github.io/hypsalp-app/#privacy) and in the app.

## Points dataset (ODbL)

`points_dataset_ODbL/points.json.gz` contains the summits, saddles, passes, mountain huts and bivouacs, with their elevations, that HypsAlp uses to show nearby summits and huts and to calibrate the altimeter. It is a **Derivative Database** of OpenStreetMap data and is published here under the **Open Database License 1.0**, as that license requires, in the same version that is distributed in the app's terrain packs. It may also be useful on its own.

| | |
|---|---|
| Source data | © OpenStreetMap contributors, ODbL 1.0 - Geofabrik extract of Europe, data as of 2026-11-21 |
| This dataset | ODbL 1.0, see `License and attribution` below |
| Built on | 2026-11-22 |
| File | `points.json.gz`, about 7 MB, UTF-8 JSON (gzip-compressed: `gunzip -k points.json.gz`) |
| Coverage | The European Union, the United Kingdom, Norway, Switzerland, Liechtenstein, Iceland, Andorra, Monaco, San Marino, Vatican City, the Western Balkans (Albania, Bosnia and Herzegovina, Kosovo, Montenegro, North Macedonia, Serbia) and the whole of Cyprus; excluding the Azores, Madeira, the Canary Islands, Svalbard and overseas territories. Points span 34.65°–71.18° N, 24.36° W–34.25° E. |

### Contents

| | Count |
|---|---|
| Points, total | 422,292 |
| — `peak` | 372,998 |
| — `saddle` | 40,495 |
| — `pass` | 3,504 |
| — `hut` | 2,442 |
| — `bivouac` | 2,853 |
| With a name | 304,527 |
| Elevation from OpenStreetMap (`src: "osm"`) | 417,366 |
| Elevation from the terrain model (`src: "dem"`) | 4,926 |

### Format

```json
{
  "attribution": "© OpenStreetMap contributors (ODbL)",
  "osmDate": "2026-11-21",
  "points": [
    { "lat": 45.832706, "lon": 6.865171, "ele": 4807, "kind": "peak", "src": "osm", "name": "Mont Blanc / Monte Bianco" }
  ]
}
```

| Field | Meaning |
|---|---|
| `lat`, `lon` | WGS 84 decimal degrees |
| `ele` | Elevation in whole meters |
| `kind` | `peak`, `saddle`, `pass`, `hut` or `bivouac` |
| `src` | Where the elevation comes from: `osm` or `dem` (see below) |
| `name` | The name, when the point has one, absent otherwise |
| `tree` | Only for `src: "dem"`: share of tree cover (0–100 %) around the point, from ESA WorldCover; under trees the terrain model reads the canopy, so the estimate is less reliable |

### Where the elevations come from

- **`src: "osm"`**: the elevation is OpenStreetMap's own `ele` tag. These tags are contributed data and **can be wrong**. When the dataset is built, each one is compared with the Copernicus DEM GLO-30 at the same spot, and points more than 80 m below or 120 m above the terrain model are left out. HypsAlp treats the remaining values as surveyed, but never blindly.
- **`src: "dem"`**: huts, bivouacs and passes that have no `ele` tag in OpenStreetMap. Their elevation was read from the **Copernicus DEM GLO-30** when the dataset was built and is an estimate. These values are **not** OpenStreetMap data and are covered by the Copernicus WorldDEM-30 license, not by the ODbL; the same applies to the `tree` values, which come from ESA WorldCover (CC BY 4.0). HypsAlp shows these points as approximate and never uses them to calibrate the altimeter, because the terrain model would only be confirming itself.

### How it was extracted

From the Geofabrik OpenStreetMap extract of Europe, keeping the nodes tagged:

| OpenStreetMap tag | `kind` |
|---|---|
| `natural=peak` | `peak` |
| `natural=saddle` | `saddle` |
| `mountain_pass=yes` | `pass` |
| `tourism=alpine_hut` | `hut` |
| `tourism=wilderness_hut` | `bivouac` |

Elevations come from the `ele` tag where present (meters or feet, converted to whole meters), checked against the Copernicus DEM as described above. For huts, bivouacs and passes without one, from the Copernicus DEM, marked `src: "dem"`. Points that fall where the terrain model has no data (open sea) are left out. Each point appears once, even where the app's regional packs overlap.

### License and attribution

The database is made available under the **[Open Database License 1.0 (ODbL)](https://opendatacommons.org/licenses/odbl/1-0/)**; any rights in its individual contents are licensed under the **[Database Contents License 1.0](https://opendatacommons.org/licenses/dbcl/1-0/)**. (The ODbL allows a distributor to supply either a copy of the license or its URI; this repository supplies the URIs.)

- **Attribution to keep with the data, and with anything produced from it:** `© OpenStreetMap contributors`, as described at [openstreetmap.org/copyright](https://www.openstreetmap.org/copyright).
- **Elevations marked `src: "dem"`** are derived from the Copernicus DEM GLO-30, used under the Copernicus WorldDEM-30 license.
- **`tree` values** are derived from ESA WorldCover 10 m 2021 v200, CC BY 4.0: © ESA WorldCover project 2021 / Contains modified Copernicus Sentinel data (2021) processed by ESA WorldCover consortium.

In short, the ODbL asks that you **attribute** (keep "© OpenStreetMap contributors" visible wherever you use the data), **share alike** (if you publicly use an adapted version of this database, offer it under the ODbL as well) and **keep it open** (if you redistribute it in a technically restricted form, also provide a version without those restrictions). That summary is not a substitute for the license.

The data is provided as is, without warranty of any kind. Elevations in OpenStreetMap are contributed by volunteers and can be wrong; elevations from the terrain model are estimates. **Do not rely on this data alone for navigation or for safety in the mountains.**

If you find a wrong elevation or a missing summit, the best place to fix it is OpenStreetMap itself: the fix then reaches everyone, and this dataset the next time it is rebuilt.

## Terrain data and other data

HypsAlp's terrain data is organised in regional packs built around mountain ranges: each range lies entirely within one pack, and the few tiles where two ranges meet are included in both. The Alps pack is downloaded automatically when the app is installed or updated; every other region is downloaded only when you choose it, under **Settings ▸ Terrain Data**, and can be removed at any time. Outside the regions you have downloaded, the app still works as a barometric altimeter and says so.

Each pack contains:

- **Copernicus DEM GLO-30** elevation model (Copernicus WorldDEM-30 license; relief images carry the attribution the license requires).
- **Tree cover** derived from **ESA WorldCover 10 m 2021 v200** (CC BY 4.0): © ESA WorldCover project 2021 / Contains modified Copernicus Sentinel data (2021) processed by ESA WorldCover consortium. Changed from the original: the "Tree cover" class was resampled to the terrain grid as a percentage of each cell. HypsAlp uses it to recognise where the terrain model reads the top of the forest rather than the ground.
- The points of the dataset above.

The map of the regions in the app uses coastlines from **Natural Earth** (public domain). The app also bundles NOAA's **World Magnetic Model WMM2025** (public domain, valid until 2030.0). Snow grain shapes and classes in the snow profile notebook follow the international snow classification (Fierz et al., 2009); the symbols are drawn by HypsAlp and are not the IACS symbol font. Snow profiles export to CAAML, a format of the Canadian Avalanche Association. HypsAlp is not affiliated with IACS, UNESCO or the CAA. Full attributions are in the app, under **Settings ▸ Data & Licenses**.

## Support

Found a problem, or have an idea? Write to **hypsalp [at] tuta [dot] io**, or use **Settings ▸ Send Feedback** inside the app, which opens a pre-filled email in your Mail app that you review and send yourself.

Please don't include other people's personal information in your message.

## Safety

HypsAlp is an instrument and a notebook, never a verdict. It is **not** a certified navigation or safety device and does not replace a map, a compass, training, or judgment in the field. The storm warning is a hint from the barometer, not a forecast. The snow profile records your own observations and does not assess snowpack stability or avalanche danger. In an emergency, use your phone's official emergency features and call the rescue services.

## Trademarks

HypsAlp is compatible with RuuviTag sensors. RuuviTag is a product of Ruuvi Innovations Ltd (Oy), and Ruuvi® is a registered trademark of Ruuvi Innovations Ltd (Oy). BTHome is an open standard maintained at [bthome.io](https://bthome.io). The Bluetooth® word mark is a registered trademark owned by Bluetooth SIG, Inc. Apple, iPhone and Apple Watch are trademarks of Apple Inc.; Garmin is a trademark of Garmin Ltd. HypsAlp is an independent app and is not affiliated with, endorsed or sponsored by any of these parties.

## License

- `points_dataset_ODbL/points.json.gz`: **ODbL 1.0**, as described above.
- Everything else in this repository: © 2026 the developer of HypsAlp. All rights reserved. The texts of the web page are provided for information and may not be reused without permission.
