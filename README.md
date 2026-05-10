# US Accidents — Weather Impact Analysis

## Project Overview

This project investigates whether weather conditions can be used to predict 
road accident severity and the extent of road affected across the United States. 
Using a dataset of over 2.8 million accident records, the analysis moves through 
data cleaning, exploratory visualization, geospatial mapping, and both supervised 
and unsupervised machine learning to test the relationship between weather variables 
and accident outcomes.

---

## Research Questions

- Do weather conditions such as precipitation, humidity, and visibility 
  meaningfully influence accident severity?
- Which US states have the highest accident rates relative to population?
- Can weather variables predict the distance of road affected by an accident 
  (linear regression)?
- Do accidents naturally cluster into distinct weather condition groups 
  (K-means clustering)?

---

## Dataset

Source: [US Accidents (Dec 2021) — Kaggle](https://www.kaggle.com/datasets/sobhanmoosavi/us-accidents)

- ~2.8 million accident records across 49 US states (Feb 2016 – Dec 2021)
- 47 attributes including accident severity, location, weather conditions, 
  and time of day
- Supplementary US state population data used for accident rate normalization

---

## Project Structure

US-Accidents-Python/
└── 03 Scripts/
├── 6.1 Cleaning & Summary.ipynb
├── 6.2 Exploring relationships.ipynb
├── 6.3 Geospatial analysis.ipynb
├── 6.4 Supervised machine learning.ipynb
└── 6.5 Unsupervised machine learning.ipynb

---

## Analysis Pipeline

**6.1 — Data Cleaning & Summary**
- Null value handling — rows dropped on `Wind_Chill` as a proxy for 
  weather-related completeness
- Mixed-type column detection and resolution across 12 categorical columns
- Date/year extraction from `Weather_Timestamp`
- `Severity` and `Number` recast as string types to prevent erroneous 
  numerical operations
- Clean dataset exported as `.pkl` for downstream notebooks

**6.2 — Exploring Relationships**
- Correlation heatmap across 7 weather variables: temperature, humidity, 
  pressure, wind speed, precipitation, visibility, and distance
- Key findings:
  - Moderate negative correlation between humidity and visibility
  - Weak negative relationship between precipitation and visibility
  - Weak positive correlation between temperature and visibility
- Scatterplots and pair plots used to investigate variable relationships
- Humidity categorized into Low / Average / High bands for categorical analysis

**6.3 — Geospatial Analysis**
- US state population data merged to calculate per-capita accident rates
- Three interactive choropleth maps built with Folium:
  - Accident count by state
  - Average humidity by state
  - Average precipitation by state
- California, Florida, and Texas identified as the highest accident volume states
- Extreme values removed (precipitation > 2in, visibility > 8mi) before mapping

**6.4 — Supervised Machine Learning (Linear Regression)**
- Three regression models built using scikit-learn:
  - Precipitation → Visibility
  - Precipitation → Humidity
  - Precipitation → Distance of road affected
- 70/30 train-test split applied across all models
- Model performance evaluated using MSE and R² score
- Analysis repeated on a cleaned subset with extreme values removed 
  to assess impact on model accuracy

**6.5 — Unsupervised Machine Learning (K-Means Clustering)**
- Elbow technique used to determine optimal cluster count
- Initial K-means model with 5 clusters on raw weather subset
- Second model run on StandardScaler-normalized data with extreme 
  values removed, converging on 3 optimal clusters
- Clusters profiled using mean/median aggregations across all 
  weather variables
- Precipitation vs. distance scatter plot used to visualize cluster separation

---

## Tools & Libraries

- **Python 3** — pandas, NumPy, Matplotlib, Seaborn
- **scikit-learn** — LinearRegression, KMeans, StandardScaler, train_test_split
- **Folium** — interactive choropleth mapping
- **Jupyter Notebook** — analysis environment

---

## Key Findings

- Humidity shows the strongest negative correlation with visibility 
  among all weather variables tested
- Precipitation alone is a weak predictor of both visibility and road 
  distance affected — other compounding factors likely play a larger role
- K-means clustering on normalized data reveals 3 distinct weather 
  condition profiles present during accidents
- California, Florida, and Texas account for the highest absolute 
  accident volumes nationally
