# 🛰️ Human Mobility Analysis – Census Tract Level

This repository contains a high-performance geospatial pipeline to process and analyze consumer mobility data in Brazil at the **census tract (setor censitário)** level. It integrates mobility, spatial data, and sociodemographic indicators for scientific and market intelligence applications.

> ✅ Built for machines with 64 cores, 990 GB RAM, and 4 GPUs — every step maximizes computational resources.

---

## 🚦 Overview of Blocks

| Block | Description |
|-------|-------------|
| **Block 1** | Efficiently aggregates raw mobility data split across 35 files into a tract-level summary. |
| **Block 2** | Performs spatial join of mobility data with official census tract geometries using GeoPackage. |
| **Block 3** | Generates high-resolution choropleth maps for visits, unique visitors, and dwell time. |
| **Block 4** | Calculates **Moran’s I** for spatial autocorrelation and visualizes **LISA clusters**. |
| **Block 5** | Explores sociodemographic patterns by gender, age range, class, and region. |

---

## 📁 File Structure

### 📥 Input Files

- `/Mobility/Mobility Data (Splited)/mobility_part_*.csv.gz`: Raw mobility files (split format)
- `/e-WOM/BR_setores_CD2022.gpkg`: Official 2022 shapefile of Brazilian census tracts
- `/Mobility/Sisi/mobility_by_sector.csv.gz`: Clean, aggregated file generated in Block 1

### 📤 Output Files

- `/Mobility/Sisi/mobility_by_sector_joined.gpkg`: Mobility + geometry (joined GeoDataFrame)
- `/Mobility/Sisi/maps/`: Folder with PNGs of choropleth maps
- `/Mobility/Sisi/lisa_maps/`: Cluster maps from LISA analysis
- Notebooks, logs, and temporary files as needed

---

## ⚙️ Technologies & Libraries

- `pandas`, `numpy`
- `geopandas` (with `pyogrio` to avoid Fiona)
- `matplotlib`, `seaborn`
- `libpysal`, `esda`, `splot` for spatial diagnostics
- `tqdm`, `joblib` for parallel processing with progress bars

---

## 📊 Key Variables (Post-Aggregation)

| Column | Description |
|--------|-------------|
| `store_id` | Census tract ID (matches `CD_SETOR`) |
| `visits` | Total number of device-based visits |
| `unique` | Unique visitors |
| `dwell_time_mins` | Average dwell time (minutes) |
| `demographics_gender` | Gender (F, M) |
| `demographics_age_range` | Age range (e.g., 25_29) |
| `demographics_class` | Social class (A–E) |
| `state` | Brazilian federal unit (e.g., SP, RJ) |

---

## 🧪 Statistical Diagnostics

#📈 Descriptive Summary
Our dataset encompasses 436,868 census tracts across Brazil, each enriched with detailed mobility and sociodemographic attributes. This extensive coverage allows for a granular examination of urban dynamics, with São Paulo (SP) emerging as the most represented state (n = 102,062), consistent with its demographic and economic prominence.

In terms of gender, the sample reveals a slight skew toward female-dominated tracts, with 52.2% of visits attributed to women. Age distribution is centered on young adults, particularly those in the 25–29 age group, followed by 30–34 and 20–24, reflecting mobility patterns typical of the economically active and digitally connected population. Regarding social class, high-income areas (Class A) are the most prevalent, yet lower-income tracts remain well represented, ensuring sufficient heterogeneity for downstream stratified analyses.

To examine the spatial structure of mobility behaviors, we conducted global spatial autocorrelation diagnostics using Moran’s I for three key variables: total visits, unique visitors, and average dwell time. All metrics exhibit statistically significant positive spatial autocorrelation (p < 0.001), with Moran’s I values of 0.503 for total visits, 0.557 for unique visitors, and 0.271 for dwell time. These results indicate strong spatial clustering of mobility patterns—especially for volume-based measures—underscoring the importance of applying spatial econometric techniques in subsequent analyses.

Overall, the sample exhibits robust variation across geographic, demographic, and behavioral dimensions, while also showing significant spatial dependencies. These characteristics provide a solid empirical foundation for testing our hypotheses concerning mobility, digital sentiment, and sales performance in urban environments.

Moran’s I for spatial autocorrelation:

| Metric           | Moran’s I | p-value | z-score |
|------------------|-----------|---------|---------|
| `visits`         | 0.503     | 0.001   | 476.94  |
| `unique`         | 0.557     | 0.001   | 532.34  |
| `dwell_time_mins`| 0.271     | 0.001   | 264.35  |

---

## 🧠 Use Case

This notebook supports the research project:

**“Pathways to Consumption: Physical Mobility, Digital Voice, and the Geography of Market Access”**  
Albuquerque, Brei & Jain (2025)

It is designed to:
- validate spatial autocorrelation in mobility flows
- produce geovisualizations for publication
- describe demographic composition of the national sample

---

## 📌 How to Run

1. Ensure the machine has Python ≥ 3.8 and the listed libraries.
2. Replace paths if running outside FASRC.
3. Start from Block 1 and proceed sequentially.
4. Visual outputs are saved automatically as PNG.

---

## 📸 Sample Outputs

Choropleth maps:
- `choropleth_visits.png`
- `choropleth_unique.png`
- `choropleth_dwell_time_mins.png`

LISA clusters:
- `lisa_visits.png`

Descriptive plots:
- gender, class, state, and age distributions

---

## ✍️ Authors

- Jessica Miranda - Federal University of Rio Grande do Sul (UFRGS), Brazil
- Sisi Wang - UCS/Harvard CGA
- Rafael Albuquerque - UFRGS/Harvard CGA

---

## 🔐 Ethics & Disclaimer

- Data is anonymized and aggregated.
- No individual or personal data is present.
- For academic use only.
