# Urban Flood Risk & Green Space Analysis
### Phoenix Metro Area · QGIS 3.34 · AI Training Dataset

An interactive geospatial analysis project identifying flood vulnerability zones across the Phoenix metropolitan area, designed to generate labeled training data for AI-based flood risk prediction models.

https://github.com/FatimaMehvash408/geospatial-portfolio/blob/main/index.html

---

## Project Overview

This project combines satellite imagery, LiDAR elevation data, and census demographics to produce a multi-layer risk assessment of urban flood exposure. The resulting labeled polygon dataset is structured for use as supervised training data in machine learning pipelines.

**Study Area:** Phoenix Metro, AZ (Maricopa County)  
**CRS:** WGS 84 (EPSG:4326)  
**Tools:** QGIS 3.34, GRASS GIS, Sentinel-2, USGS 1m LiDAR  

---

## Methodology

1. **DEM Acquisition** — USGS 1m LiDAR data processed for slope and flow accumulation using GRASS `r.watershed`
2. **NDVI Calculation** — Sentinel-2 Band 4/8 ratio computed via QGIS Raster Calculator
3. **Imperviousness Layer** — Derived from NLCD 2021 urban land cover classification
4. **Weighted Risk Overlay** — Three-factor scoring model:
   - Slope: 40%
   - NDVI: 35%
   - Imperviousness: 25%
5. **Vectorization** — Risk raster converted to labeled polygons using QGIS Polygonize
6. **Attribute Labeling** — Each polygon annotated with risk class, NDVI value, slope, population (Census 2020)
7. **Validation** — F1 score of 0.84 against FEMA National Flood Hazard Layer

---

## Layers

| Layer | Type | Description |
|---|---|---|
| Flood Risk Zones | Polygon | High / Medium / Low risk classification |
| Green Spaces | Polygon | Parks and riparian buffers with NDVI values |
| Drainage Network | Polyline | Flow corridors derived from DEM |
| Monitoring Stations | Point | Hydrology sensor locations with flow readings |

---

## AI Training Data Output

The labeled polygon GeoJSON export (`training_labels.geojson`) contains **1,247 features** with the following schema:

```json
{
  "id": "FL-001",
  "risk_class": "High",
  "ndvi": 0.06,
  "slope_deg": 6.3,
  "impervious_pct": 0.81,
  "pop_affected": 12400,
  "label": 2
}
```

Risk classes map to integer labels: `Low = 0`, `Medium = 1`, `High = 2`

---

## Skills Demonstrated

- Raster analysis (DEM, NDVI, slope, zonal statistics)
- Vector processing (spatial joins, buffer analysis, polygonization)
- Multi-criteria weighted overlay analysis
- Geospatial data labeling for ML training pipelines
- Web map export with Leaflet.js
- Validation against authoritative datasets (FEMA)

---

## Data Sources

- [USGS 3DEP LiDAR](https://www.usgs.gov/3d-elevation-program)
- [Sentinel-2 Imagery — Copernicus Open Access Hub](https://scihub.copernicus.eu/)
- [NLCD 2021 — Multi-Resolution Land Characteristics](https://www.mrlc.gov/)
- [US Census Bureau 2020](https://www.census.gov/)
- [FEMA National Flood Hazard Layer](https://msc.fema.gov/)

---

*Created by Fatima Mehvash · MS Computer Science (AI), SUNY Binghamton*  
