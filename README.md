# India Flood Risk Platform

## Project Overview

The India Flood Risk Platform is an end-to-end catastrophe risk modelling project designed to simulate how insurers and reinsurers assess flood risk using historical disaster records, climate reanalysis data, geospatial analysis, and statistical modelling.

The project integrates multiple data sources to build a reproducible flood risk pipeline for India. It combines data engineering, geospatial analytics, actuarial concepts, time series analysis, and interactive business intelligence dashboards.

Rather than focusing on a single predictive model, the project aims to recreate the analytical workflow followed by catastrophe modelling teams within the insurance industry.

---

# Project Objectives

The project aims to:

- Build a reproducible catastrophe risk modelling pipeline.
- Integrate multiple heterogeneous datasets into a unified analytical framework.
- Transform climate reanalysis data into state-level hazard information.
- Develop actuarial-style frequency and severity models.
- Explore extreme value theory for catastrophic flood losses.
- Perform Monte Carlo simulations for portfolio risk estimation.
- Visualize insights using Power BI dashboards.

---

# Project Architecture

```
Raw Data

↓

Bronze Layer

↓

Silver Layer

↓

Gold Layer

↓

Risk Models

↓

Power BI Dashboard
```

---

# Technologies

### Programming

- Python
- SQL

### Data Engineering

- Pandas
- NumPy
- PyArrow

### Geospatial Analysis

- GeoPandas
- Shapely
- GADM

### Climate Data

- ERA5 Reanalysis
- Copernicus Climate Data Store

### Statistical Modelling

- Time Series Analysis
- Generalized Linear Models
- Extreme Value Theory
- Monte Carlo Simulation

### Visualization

- Power BI
- Matplotlib

---

# Data Sources

- EM-DAT Disaster Database
- ERA5 Reanalysis (Copernicus)
- GADM Administrative Boundaries
- IMD (planned)
- Census / Exposure datasets (planned)

---

# Repository Structure

```
docs/
Technical documentation

data/
Raw, Bronze, Silver and Gold datasets

notebooks/
Jupyter notebooks

src/
Reusable Python modules

dashboard/
Power BI dashboard

reports/
Engineering reports

references/
Research papers and supporting material
```

---

# Current Progress

| Component | Status |
|----------|:------:|
| Documentation | ✅ |
| Data Architecture | ✅ |
| EM-DAT Profiling | ✅ |
| ERA5 Onboarding | ✅ |
| GitHub Repository | ✅ |
| Bronze Layer | ⏳ |
| Silver Layer | ⏳ |
| Gold Layer | ⏳ |
| Risk Models | ⏳ |
| Dashboard | ⏳ |

---

# Project Roadmap

Version 0.1

- Repository setup
- Documentation
- Data acquisition

Version 0.2

- Bronze Layer
- Silver Layer
- Spatial joins

Version 0.3

- Hazard feature engineering

Version 0.4

- Frequency modelling

Version 0.5

- Severity modelling

Version 0.6

- Extreme Value Theory

Version 0.7

- Monte Carlo Simulation

Version 1.0

- Power BI dashboard
- Final documentation
- Portfolio release

---

# Author

**Suhana Gupta**

B.Sc. (Hons.) Statistics  
Lady Shri Ram College for Women, University of Delhi

---

This repository is maintained as an academic and portfolio project focused on catastrophe risk modelling, insurance analytics, and climate risk assessment.