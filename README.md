# GeoShield — Standalone Geospatial Risk Explorer

## The problem

Infrastructure teams often need an initial answer to:

> "Is this location potentially exposed to geospatial flood/infrastructure risk?"

Elevation, hydrology, buildings and imagery normally come from different systems. GeoShield demonstrates a fast, explainable screening workflow that brings those indicators into one operational view.

## This version is genuinely standalone

This build intentionally has **zero external JavaScript, CSS, map-tile or API dependencies**.

You can:

1. Extract the ZIP.
2. Double-click `index.html`.
3. Run the application immediately.

It does **not** require Python, Node.js, npm, a local web server, Leaflet, OpenStreetMap or internet access.

This eliminates the previous:

- `file://` CORS error
- `Unsafe attempt to load URL file:///...`
- OpenStreetMap access-block error
- external CDN dependency

## What is demonstrated

- Geospatial coordinate input
- Area-of-interest visualization
- Risk screening algorithm
- Building-density indicator
- Hydrology proximity indicator
- Terrain visualization
- Coordinate grid
- Layer controls
- Responsive professional UI
- Exportable JSON screening report
- Production architecture guidance

## Important engineering distinction

The map visualization in this standalone build is a local geospatial visualization, not live OSM imagery.

For a production implementation, the recommended architecture is:

Browser
→ ASP.NET Core Geo API
→ PostGIS / spatial indexes
→ vector tiles
→ DEM / hydrology / imagery object storage
→ Redis/CDN

Common expensive operations should be precomputed or returned as aggregates. The browser should not query public Overpass directly.

## Production data path

1. Ingest authoritative GIS datasets.
2. Validate and normalize CRS.
3. Store vector data in PostGIS.
4. Store raster/DEM in object storage.
5. Build spatial indexes and H3/S2 aggregates.
6. Expose bounded APIs through ASP.NET Core.
7. Serve visualization through vector tiles.
8. Cache frequently requested cells.
9. Run detailed hydraulic analysis asynchronously.

## Disclaimer

The included screening calculation is a demonstration algorithm. It must not be used as a substitute for calibrated flood models, engineering surveys, regulatory analysis or insurance decisions.
