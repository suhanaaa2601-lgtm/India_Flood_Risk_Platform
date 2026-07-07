# Data Inventory

## Project

**India Flood Risk Platform**

Version: 0.1

Last Updated: July 2026

---

# Purpose

This document serves as the master inventory of every dataset used in the India Flood Risk Platform.

It documents:

- Dataset source
- Purpose
- File location
- Update frequency
- Variables
- Data quality observations
- Pipeline stage (Raw → Bronze → Silver → Gold)

This inventory ensures that every dataset used in the project is reproducible and fully documented.

---

# Dataset Catalogue

| Dataset ID | Dataset | Source | Format | Purpose | Status |
|------------|---------|--------|--------|---------|--------|
| DS001 | EM-DAT India Flood Events | EM-DAT | Excel (.xlsx) | Historical flood events | ✅ Downloaded |
| DS002 | ERA5 Daily Rainfall | Copernicus Climate Data Store | NetCDF (.nc) | Hazard data | ⏳ Downloading |
| DS003 | India State Boundaries | GADM | Shapefile | Spatial joins | ⏳ Pending |
| DS004 | IMD Rainfall (Optional) | IMD | CSV / NetCDF | Validation dataset | ⏳ Future |
| DS005 | Population Data | Census of India / WorldPop | CSV | Exposure modelling | ⏳ Future |
| DS006 | GDP / Economic Indicators | MOSPI / World Bank | CSV | Exposure modelling | ⏳ Future |

---

# Dataset Details

---

## DS001 — EM-DAT India Flood Events

### Description

The EM-DAT dataset provides a historical record of significant flood disasters in India.

Each record represents one disaster event.

### Source

EM-DAT (Centre for Research on the Epidemiology of Disasters)

### File Location

data/raw/emdat/

### File Name

EMDAT_India_Floods_2000_2025.xlsx

### Time Coverage

2000–2025

### Spatial Coverage

India

### Analytical Role

Event Layer

### Key Variables

- Disaster ID
- Start Date
- End Date
- Flood Type
- State / Location
- Latitude
- Longitude
- Total Affected
- Total Deaths
- Total Damage
- Insured Damage

### Planned Pipeline

Raw

↓

Event Master Table

↓

Feature Engineering

↓

Gold Dataset

---

## DS002 — ERA5 Daily Rainfall

### Description

ERA5 provides reanalysis-based daily rainfall estimates across India using a regular latitude–longitude grid.

Each observation represents rainfall at one grid cell for one day.

### Source

Copernicus Climate Data Store

### File Location

data/raw/era5/

### File Name

ERA5_India_TotalPrecipitation_2023.nc

### Variable

Total Precipitation

### Units

Metres (converted to millimetres in Bronze Layer)

### Temporal Resolution

Daily

### Spatial Resolution

0.25°

### Coverage

India

### Analytical Role

Hazard Layer

### Planned Pipeline

NetCDF

↓

Bronze Layer

↓

Spatial Join

↓

State Rainfall Dataset

↓

Hazard Features

---

## DS003 — India State Boundaries

### Description

Administrative boundaries for Indian states used to spatially assign rainfall grids to states.

### Source

GADM

### Format

ESRI Shapefile

### File Location

data/raw/boundaries/

### Analytical Role

Spatial Layer

### Planned Pipeline

Shapefile

↓

GeoDataFrame

↓

Spatial Join

↓

Grid-to-State Lookup

---

# Data Pipeline Overview

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

Dashboard

---

# Current Download Status

| Dataset | Status |
|----------|--------|
| EM-DAT | ✅ |
| ERA5 | ⏳ |
| GADM | ⏳ |
| IMD | ⏳ |
| Exposure Data | ⏳ |

---

# Notes

This inventory will be updated whenever a new dataset is introduced into the project.

No dataset should be used without being documented in this inventory first.