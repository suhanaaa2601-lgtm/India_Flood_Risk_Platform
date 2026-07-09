# Silver Hazard Layer Report


# Objective

The objective of the Silver Hazard Layer is to transform the standardized Bronze ERA5 rainfall dataset into a structured analytical dataset suitable for spatial analysis, database design, and downstream flood risk modelling.

Unlike the Bronze layer, which preserves the original rainfall observations, the Silver layer introduces relational data modelling by separating the spatial component (grid locations) from the temporal rainfall observations.

---

# Input Dataset

Source Dataset

ERA5 Daily Total Precipitation (2023)

Input File

```
data/bronze/bronze_rainfall_2023.parquet
```

Dimensions

* Records: 5,697,285
* Daily observations: 365
* Latitude points: 129
* Longitude points: 121

Variables

* Date
* Latitude
* Longitude
* Rainfall (m)
* Rainfall (mm)

---

# Engineering Steps

## 1. Bronze Dataset Loading

The Bronze Parquet dataset was imported into Pandas while preserving all rainfall observations generated during the Bronze preprocessing stage.

Validation included:

* Successful file loading
* Dataset dimensions
* Data type verification

---

## 2. Creation of Spatial Grid Master

A unique spatial grid was created by extracting distinct latitude and longitude combinations.

The following operations were performed:

* Selected latitude and longitude columns
* Removed duplicate coordinate pairs
* Sorted coordinates
* Reset the index

Result

```
Grid Cells = 15,609
```

This represents the complete ERA5 spatial grid covering the study region.

---

## 3. Grid Identifier Engineering

A unique integer identifier (Grid ID) was assigned to every ERA5 grid cell.

Structure

```
grid_id
latitude
longitude
```

This creates a permanent spatial reference that can be used throughout the project without repeatedly storing geographic coordinates.

---

## 4. Grid Validation

The generated Grid Master was validated using:

* Duplicate detection
* Grid count verification
* Grid ID uniqueness

Validation Results

* Total Grid Cells: 15,609
* Duplicate Coordinates: 0
* Grid IDs: Unique

---

## 5. Integration with Rainfall Dataset

The Grid Master was merged back with the Bronze rainfall observations using latitude and longitude as matching keys.

Merge Type

```
Left Join
```

Join Keys

```
Latitude
Longitude
```

Validation

* Missing Grid IDs: 0
* Original row count preserved

---

## 6. Dataset Normalization

To reduce redundancy, latitude and longitude were removed from the production rainfall dataset after Grid IDs had been assigned.

Final rainfall table contains only:

* Date
* Grid ID
* Rainfall (mm)

The spatial coordinates are stored separately in the Grid Master.

This normalization follows standard relational database design principles and minimizes repeated storage of geographic information.

---

# Outputs Generated

## 1. Grid Master

Output File

```
data/silver/silver_grid_master.parquet
```

Schema

| Column    | Description                 |
| --------- | --------------------------- |
| grid_id   | Unique ERA5 grid identifier |
| latitude  | Grid latitude               |
| longitude | Grid longitude              |

Rows

```
15,609
```

---

## 2. Rainfall Fact Table

Output File

```
data/silver/silver_rainfall_2023.parquet
```

Schema

| Column      | Description                   |
| ----------- | ----------------------------- |
| date        | Observation date              |
| grid_id     | Spatial identifier            |
| rainfall_mm | Daily rainfall in millimetres |

Rows

```
5,697,285
```

---

# Validation Summary

| Check                          | Result    |
| ------------------------------ | --------- |
| Bronze dataset loaded          | ✅ Passed  |
| Grid Master created            | ✅ Passed  |
| Unique grid cells              | 15,609    |
| Duplicate coordinates          | 0         |
| Missing Grid IDs after merge   | 0         |
| Rainfall observations retained | 5,697,285 |
| Final Silver datasets exported | ✅ Passed  |

---

# Final Data Architecture

```
                Bronze Layer
      bronze_rainfall_2023.parquet
                  │
                  ▼
        Extract Unique Coordinates
                  │
                  ▼
        silver_grid_master.parquet
      (grid_id, latitude, longitude)
                  │
                  ▼
       Merge Grid IDs with Rainfall
                  │
                  ▼
      silver_rainfall_2023.parquet
      (date, grid_id, rainfall_mm)
```


# Key Achievements

* Successfully transformed the Bronze rainfall dataset into a normalized analytical data model.
* Established a permanent spatial reference system using unique Grid IDs.
* Eliminated redundant storage of latitude and longitude in the rainfall observations.
* Produced two production-ready Silver datasets for downstream spatial joins and flood risk modelling.
* Implemented a relational structure consistent with industry-standard data engineering and geospatial analytics practices.

# Next Phase

The next stage of the project is the Silver Exposure Layer, where the EM-DAT flood event dataset will be cleaned, standardized, and engineered into an analytical event table. This layer will later be spatially linked with the ERA5 Grid Master to associate rainfall observations with historical flood events, forming the foundation of the flood risk modelling pipeline.

