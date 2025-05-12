# 🚕 NY Taxi Fare Prediction (2022)

**Authors**: Alessandro Bosi, Federico Busetto  
**Project for**: Protiviti – Data Science Training Program  
**Year**: 2024

---

## 📌 Objective

This project analyzes a representative sample of **NYC Yellow Taxi Trips (2022)** to:
- Explore and visualize trip behavior across time and space.
- Build **predictive models** to estimate taxi fares using trip features (distance, duration, location, etc.).
- Perform **geospatial clustering** to identify high-density pickup/dropoff areas in New York.

---

## 📊 Dataset Overview

- **Source**: TLC Yellow Taxi Trip Records 2022  
- **Initial size**: ~36 million records  
- **Sample used**: ~100,000 rows (balanced sample across all months)

### Key Variables
- `pickup_datetime`, `dropoff_datetime`
- `passenger_count`, `trip_distance`
- `fare_amount`, `tip_amount`
- `pickup_location_id`, `dropoff_location_id`

---

## 🧹 Data Cleaning

- Converted monetary and distance values to floats.
- Filled `passenger_count` nulls with mode (1).
- Removed entries with:
  - Negative fares or tips
  - Dropoff time earlier than pickup time
  - Distance > 50 miles or `passenger_count` = 0 (for modeling phase)

---

## 📈 Exploratory Analysis & Insights

- Most rides are under **5 km**, with a secondary peak near **15 km** (likely to/from airports).
- Majority of fares are **under $20**, with outliers above $100.
- Average tips are **$0–5**, but some outliers exceed $50.
- Ride demand peaks around **6 PM**; lowest at **5 AM**.

---

## 🔍 Predictive Modeling

### Models Built:
- **Linear Regression**
- **Random Forest Regressor**

### Key Features Used:
- `trip_distance`, `time_duration`, `passenger_count`, `rush_hour` (dummy)

### Results:

| Model             | MSE     | R²     | Notes                                               |
|------------------|---------|--------|-----------------------------------------------------|
| Linear Regression| ~27.5   | 0.74   | Good baseline model with standardized variables     |
| Random Forest    | ~39.5   | 0.78   | Best overall model; `trip_distance` most important  |

- Removing `rush_hour` and `passenger_count` had negligible impact.
- **Distance** and **duration** were the only consistently useful predictors.

---

## 📍 Geospatial & Clustering Analysis

### Clustering (DBSCAN, centroid-based):
- Identified clusters of rides:
  - Cluster 0: Most rides, high variability
  - Cluster 1: Short, cheap urban trips
  - Cluster 2: Medium trips with low cost (possibly flat fare promotions)

### Geospatial Data:
- Used shapefiles to map:
  - Most frequent pickup zones
  - Mean fare and tip by zone

### Spatial Autocorrelation:
- Used **Moran’s I** and **Geary’s C** to test correlation across space:
  - Fare: moderate spatial autocorrelation
  - Tip: stronger spatial pattern

---

## 🧠 Conclusions

- **Trip distance** is the dominant predictor of taxi fare in NYC.
- `passenger_count` and `rush_hour` have limited impact on fare.
- Clustering reveals key zones with unique ride characteristics.
- The final models predict fare within ~$5–6 of actual value, which is reasonable in a dynamic urban context.

---

## 📬 Contacts

- **Alessandro Bosi** – alessandro.bosi31@gmail.com  
- **Federico Busetto** – federico.busetto2@gmail.com

---

## 🛠️ Tools & Technologies

- Python (Pandas, Matplotlib, Scikit-learn)
- GeoPandas & Geospatial Analysis
- DBSCAN, Random Forest, Linear Regression
- SQL + PostgreSQL (for spatial joins)
- Jupyter Notebook

---
