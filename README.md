
# 🛰️ Kelowna Urban Street Network & OD Indicator Toolkit

This repository provides a complete geospatial analysis pipeline to calculate **OpenStreetMap-based street network indicators**, generate **Origin-Destination (OD) pairs**, and visualize transport access in **Kelowna, Canada** using Python, GeoPandas, and OSMnx.

---

## 📌 Key Features

- 🔍 **Street Network Indicators** from OSM:
  - Intersection Density
  - Circuity
  - Node Density & Edge Density
  - Betweenness and Closeness Centrality
  - 1-, 2-, and 4-way Intersections
  - Total Street Length and Segment Count

- 🚦 **OD Pair Generation** using:
  - Contiguity (Queen/Rook method)
  - Fixed Buffer distance (4km–5km)
  - Car and Transit modes

- 🧠 **Integrated Machine Learning Workflow** for:
  - Regression Modeling
  - Spatial Lag and GWR Analysis
  - Public Transport vs Private Car Analysis (PT/Car Distance & Time Ratios)

- 🌐 **Interactive Visualizations**:
  - Folium-based maps
  - Static plots (matplotlib, seaborn)
  - Choropleth overlays on shapefiles

---


---

## 🔧 Installation

1. Clone the repository:
```bash
git clone https://github.com/<your-username>/kelowna-urban-indicators.git
cd kelowna-urban-indicators
````

2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. (Optional) If using Jupyter/Colab notebooks:

```bash
jupyter notebook
```

---

## 🚀 Usage Guide

### ▶️ Run the Main Script

```bash
python scripts/kewlona_indicator.py
```

This will:

* Read the 1km Kelowna grid shapefile
* Download street networks from OSM for each polygon
* Calculate network-based indicators
* Save result as shapefiles and network plots

---

## 📈 Sample Indicators Extracted

| Indicator                    | Description                                       |
| ---------------------------- | ------------------------------------------------- |
| `intersection_density`       | Number of intersections per km²                   |
| `circuity`                   | Ratio of network length to straight-line distance |
| `street_segment_count`       | Total number of road segments                     |
| `street_length_total`        | Cumulative length of streets                      |
| `streets_per_node_avg`       | Average number of connections per node            |
| `edge_density`               | Edge length per km²                               |
| `node_density`               | Node count per km²                                |
| `avg_closeness_centrality`   | Mean closeness centrality                         |
| `avg_betweenness_centrality` | Mean betweenness centrality                       |

---

## 🌍 OD Matrix Generation

You can generate OD matrices using:

```python
generate_od_pairs(grid_shapefile='data/shapefiles/kelowna_all__grids_indicators.shp',
                  buffer_distance_km=4,
                  output_csv='data/csv/kelowna_od_pairs_car_transit.csv')
```

### Sample Output Format

| origin\_id | destination\_id | OriginLat | OriginLon | DestLat | DestLon  | travel\_mode |
| ---------- | --------------- | --------- | --------- | ------- | -------- | ------------ |
| 101        | 205             | 49.886    | -119.453  | 49.901  | -119.489 | car          |
| 101        | 208             | 49.886    | -119.453  | 49.909  | -119.498 | transit      |

---

## 🗺️ Visualization

Generate **interactive OD maps**:

```python
visualize_od_pairs(od_pairs_df, display_count=100)
```

Or export shapefiles for QGIS/ArcGIS:

```python
origins_gdf.to_file('results/od_origins.shp')
destinations_gdf.to_file('results/od_destinations.shp')
```

---

## 📊 Regression & Spatial Modeling

* 🔎 Linear Regression using `sklearn`
* 🌐 Spatial Lag Model using `pysal`
* 🗺️ GWR for local variation mapping
* 📈 Moran’s I for spatial autocorrelation

```python
from spreg import GM_Lag
model = GM_Lag(y.values, X_scaled, w=w)
```

---

## 🧪 Sample Result: PT vs Car Time Ratio

| Origin | Destination | PT\_time | Car\_time | PT/car\_time |
| ------ | ----------- | -------- | --------- | ------------ |
| A      | B           | 21.4     | 14.3      | 1.49         |

---

## 🧠 Future Additions

* ✅ OD cost surface estimation
* ✅ Isochrone maps with `networkx` & `folium`
* 🔜 Accessibility score calculations
* 🔜 API wrapper for Google/Transit APIs

---

## 👤 Author

* **Niloy Biswas**
  📧 [niloyurp48@gmail.com](mailto:niloyurp48@gmail.com)
  🌐 [ResearchGate](https://www.researchgate.net/profile/Niloy-Biswas)



