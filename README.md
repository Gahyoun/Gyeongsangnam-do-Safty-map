# Gyeongsangnam-do Safety Map

Agent-based patrol simulation and safety heatmaps for all 18 municipalities
in Gyeongsangnam-do, Korea. This repository implements the workflow used in
the “융·복합 ICT 활용 공모전 2025” by the **데이터에 물리다 (Data in Physics)** team.

---

## Repository structure

- `Gyeongsangnam-do_18시군_EDGE10m_ens100_p0.010.html`
- `Gyeongsangnam-do_18시군_EDGE10m_ens100_p0.010.png`
- `Gyeongsangnam-do_18시군_EDGE10m_ens100_p0.010.pdf`  
  - Final, province-wide safety map (HTML / PNG / PDF).
- `Gyeongsangnam-do_18시군_EDGE10m_ens100_p0.010_summary_by_muni.csv`  
  - Per-city statistics of simulated patrol coverage.

Subregion exports:

- `Subregion html/` – per-city interactive HTML maps.
- `Subregion pdf/` – per-city high-resolution PDF maps.
- `Subregion png/` – per-city PNG snapshots.

Input data (not uploaded here, paths referenced in the notebook):

- `Data/경상남도 인구 및 면적.xlsx`
- `Data/경상남도 인구데이터.xlsx`
- `Data/경상남도 학교 목록_final.xlsx`
- `Data/경상남도 cctv 통합.xlsx`
- `Data/센서스 공간정보 지역 코드.xlsx`
- `Data/cctv data/…`

Main analysis notebook:

- `Gyeongsangnam_do_Safty_map.ipynb`  
  End-to-end pipeline: data loading, OSM road network processing,
  junction-graph construction, agent-based patrol simulation,
  and export of figures and HTML maps.

---

## Method overview (step-by-step)

1. **Data preparation**
   - Import census population, area statistics, school locations, and CCTV
     camera positions for all 18 municipalities in Gyeongsangnam-do.
   - Download and preprocess OpenStreetMap road networks.

2. **Route design (Step 2 in the proposal)**
   - Build base road graphs and extract feasible patrol loops for each
     police station.
   - Visualization of this step is available as a video:
     - ▶️ [Step-2 visualization video](https://youtu.be/I4iZ71uqNk0?si=87RsMyeVkgJIlquv)

3. **Agent-based patrol simulation (Step 3)**
   - Convert road graphs into junction graphs and 10 m edge segments.
   - Simulate 3-hour patrols with stochastic side-detours (probability of
     entering and returning).
   - Aggregate visit counts per edge and discretize them into 5 safety
     levels using quantiles.

4. **Province-wide aggregation**
   - Independently simulate each municipality and then merge all 18
     results into a single Gyeongsangnam-do safety layer.
   - Export:
     - High-resolution PNG/PDF maps with satellite basemaps.
     - Interactive Folium HTML map for web viewing.
     - CSV summaries by municipality.

---

## Technologies

- Python, NumPy, pandas
- NetworkX for graph construction and routing
- Folium & Leaflet.js for interactive web maps
- Matplotlib & contextily for static figures and basemaps
- Shapely & pyproj for geometry and CRS transforms

---

## Acknowledgment

This work was created for  
**“경상국립대학교 2025학년도 융·복합 ICT 활용 공모전”**  
by the **Data in Physics** team.

---
## GNU-NetworkSciencelab Copyright Notice (Parody)

Copyright (C) 2025  GNU-NetworkSciencelab  
(Data in Physics Team, Gyeongsang National University)

This program is intended to be shared in a GNU-style free-software spirit.  
You are welcome to run, study, and modify the source code, and to
redistribute modified versions, provided that proper credit is kept to
the original authors and that derivative works preserve the same open
and collaborative character.

This project is distributed in the hope that it will be useful for
research and education, but **without any warranty**; there is no
guarantee of correctness, fitness for a particular purpose, or safety
for operational deployment. Use at your own risk.

**Note**
All members are affiliated with GNU (Gyeongsang National University, Jinju, Korea)'s Physics department.
