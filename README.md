# Varsha AI

## Regime-Aware AI Post-Processing of Monsoon Rainfall Forecasts

> A practical AI/ML system that improves rainfall forecasts by identifying the prevailing weather regime before applying bias correction.

**Smart India Hackathon 2026**  
**Problem Statement ID:** 26080  
**Organization:** Ministry of Earth Sciences (MoES)  
**Department:** National Centre for Medium Range Weather Forecasting (NCMRWF)  
**Category:** Software  
**Theme:** Smart Automation

---

## 1. Overview

Rainfall forecast errors over India are not the same in every weather situation. A model may perform reasonably well during an active monsoon phase but show larger errors during a break monsoon period, coastal rainfall, orographic rainfall, or a monsoon low or depression.

Most traditional correction methods apply one common correction strategy to all situations. This can limit their performance, especially for heavy and very heavy rainfall events.

**Varsha AI** addresses this challenge through a regime-aware post-processing approach. It first identifies the prevailing weather regime and then applies a correction method designed for that specific situation.

The system is designed to work as an intelligent layer over existing Numerical Weather Prediction (NWP) systems. It improves the forecast without replacing the underlying NWP model.

---

## 2. Problem Statement

Rainfall forecasts over India often face the following challenges:

- Forecast errors change with the weather regime.
- Heavy rainfall events are difficult to predict accurately.
- Raw NWP output may contain systematic regional and seasonal biases.
- A single bias-correction model may not work well across all regions.
- District-level decision-makers need simple, local, and actionable information.
- Forecast users need confidence levels and probabilities, not only a single rainfall value.

These challenges affect disaster preparedness, agriculture, water management, flood planning, and emergency response.

---

## 3. Proposed Solution

Varsha AI uses a two-stage approach:

```text
NWP Forecast + Observations + Terrain Data
                    |
                    v
          Weather Regime Classifier
                    |
                    v
       Regime-Specific Bias Correction
                    |
                    v
 Corrected Rainfall + Heavy Rain Probability
                    |
                    v
        District Dashboard and Alerts
```

### Stage 1: Weather Regime Classification

The system identifies the most likely prevailing regime, such as:

- Active monsoon
- Break monsoon
- Monsoon low or depression
- Coastal rainfall
- Orographic rainfall
- Western disturbance or other special regimes

### Stage 2: Regime-Specific Post-Processing

After classification, the rainfall forecast is sent through the most appropriate correction model. Different regimes may use different correction parameters or model pathways.

The output includes:

- Bias-corrected rainfall forecast
- Rainfall probability
- Heavy and very heavy rainfall probability
- Confidence score
- Weather regime label
- District-level forecast table
- Interactive rainfall map
- Raw NWP versus corrected forecast comparison

---

## 4. Key Features

### Forecast Intelligence

- Regime-aware rainfall correction
- District-level and grid-level rainfall forecasts
- Heavy rainfall probability estimation
- Confidence-aware forecast products
- Comparison between raw and corrected NWP output

### Operational Dashboard

- Overview of the current weather regime
- Live forecast page
- District rainfall outlook
- Spatial rainfall intensity map
- Verification and skill metrics
- Profile and workspace preferences

### Verification and Transparency

The system is designed to report:

- RMSE — Root Mean Square Error
- ETS — Equitable Threat Score
- CSI — Critical Success Index
- POD — Probability of Detection
- FAR — False Alarm Ratio
- FSS — Fractions Skill Score

Performance can be analysed by:

- Weather regime
- Forecast lead time
- Region
- Rainfall intensity threshold
- Season
- District or grid cell

---

## 5. System Architecture

```text
+-----------------------------+
| NWP Forecasts               |
| Rainfall, wind, humidity,   |
| pressure, temperature, etc. |
+--------------+--------------+
               |
               v
+-----------------------------+
| Observation and Context Data|
| Rain gauges, satellite,     |
| radar, terrain, land-sea    |
| mask, historical rainfall   |
+--------------+--------------+
               |
               v
+-----------------------------+
| Data Quality Control         |
| Alignment, missing values,  |
| outlier checks, resampling  |
+--------------+--------------+
               |
               v
+-----------------------------+
| Feature Engineering          |
| Atmospheric, geographic,    |
| temporal and regime features|
+--------------+--------------+
               |
               v
+-----------------------------+
| Weather Regime Classifier    |
| Active, break, coastal,     |
| orographic, depression, etc.|
+--------------+--------------+
               |
               v
+-----------------------------+
| Regime-Specific Correction   |
| Quantile mapping, boosting, |
| U-Net or probabilistic ML   |
+--------------+--------------+
               |
               v
+-----------------------------+
| Forecast Products            |
| Corrected rainfall, risk,   |
| probability and confidence  |
+--------------+--------------+
               |
               v
+-----------------------------+
| Dashboard, Reports and APIs  |
+-----------------------------+
```

---

## 6. Suggested Technology Stack

### Machine Learning

- Python
- NumPy
- Pandas
- Xarray
- Scikit-learn
- XGBoost or LightGBM
- PyTorch or TensorFlow
- MLflow for experiment tracking

### Data and Geospatial Processing

- NetCDF and GRIB data support
- Rasterio
- GeoPandas
- Cartopy
- PostGIS or spatial database support

### Backend and APIs

- FastAPI
- PostgreSQL
- Object storage for forecast files
- Scheduled jobs for NWP cycle processing
- Docker for reproducible deployment

### Frontend

- React or a static web interface
- D3.js or Plotly for visualizations
- Responsive district and grid-level maps
- Role-based operational dashboard in later phases

---

## 7. Model Development Workflow

### Step 1: Collect and Align Data

Collect historical NWP forecasts and match them with rain gauge, satellite, radar, and gridded observations. Align data by time, location, forecast lead time, and spatial resolution.

### Step 2: Perform Quality Control

- Remove or flag invalid observations.
- Handle missing values.
- Detect extreme outliers.
- Check forecast-observation time alignment.
- Maintain clear data lineage.

### Step 3: Create Regime Labels

Regime labels can be created using a combination of:

- Expert meteorological rules
- Atmospheric pressure and circulation patterns
- Rainfall distribution
- Wind and moisture transport
- Clustering techniques
- Historical event catalogues

### Step 4: Train the Regime Classifier

Start with interpretable baseline models such as Random Forest, XGBoost, or LightGBM. Evaluate classification accuracy, precision, recall, F1 score, and confusion matrices.

### Step 5: Train Correction Models

Train separate correction pathways for each regime. Initial models may include:

- Quantile mapping
- Quantile regression
- Random Forest regression
- Gradient boosting
- Probabilistic regression

Advanced versions may use:

- CNNs
- U-Net architectures
- ConvLSTM
- Temporal Transformers
- Spatially conditioned deep-learning models

### Step 6: Generate Probabilistic Forecasts

Estimate the probability that rainfall will exceed operational thresholds. Calibrate the probabilities using historical observations and reliability analysis.

### Step 7: Verify and Monitor

Compare the corrected forecast with raw NWP output and observation data. Track performance separately by regime, region, threshold, and lead time.

---

## 8. Evaluation Framework

The system should be evaluated using time-based validation rather than random splitting, so that future weather events are not accidentally included in training data.

### Continuous Forecast Metrics

- RMSE
- MAE
- Mean bias
- Correlation
- Quantile error

### Categorical Event Metrics

- ETS
- CSI
- POD
- FAR
- Frequency bias

### Spatial Metrics

- FSS
- Neighbourhood-based rainfall verification
- Spatial pattern correlation

### Probabilistic Metrics

- Brier score
- Brier skill score
- Reliability diagrams
- ROC-AUC
- Calibration error

### Recommended Evaluation Groups

- 6-hour, 12-hour, 24-hour and longer lead times
- Active, break, coastal, orographic and depression regimes
- Light, moderate, heavy and very heavy rainfall thresholds
- Coastal, central, northeast, Himalayan and arid regions
- Monsoon and non-monsoon periods where relevant

---

## 9. Dashboard Pages

The prototype dashboard is organised into separate pages:

### Overview

A high-level operational view containing:

- Current weather regime
- Precipitation accuracy
- Heavy rainfall probability
- Spatial rainfall outlook
- District-level forecast table
- Recent operational activity

### Live Forecast

Provides:

- 24-hour, 48-hour and 72-hour forecast views
- District rainfall outlook
- Rainfall intensity map
- Regime confidence
- Operational notes

### Verification

Provides:

- Overall skill score
- RMSE, ETS, CSI, POD, FAR and FSS
- Regime-level comparison
- Raw NWP versus post-processed performance

### Profile

Provides:

- User identity and role
- Region and workspace details
- Heavy rainfall alerts
- Regime shift notifications
- Verification digest preferences
- Default forecast horizon and map layer

---

## 10. Feasibility and Implementation Roadmap

### Phase 1: Baseline Prototype

- Collect and align historical data.
- Build the quality-control pipeline.
- Create initial regime labels.
- Train a baseline classifier.
- Implement quantile mapping and gradient boosting correction.
- Build the district-level dashboard.

### Phase 2: Advanced AI Model

- Add terrain and land-sea features.
- Introduce spatial-temporal deep learning.
- Improve extreme rainfall probability calibration.
- Add regime-specific model comparison.
- Implement automated verification reports.

### Phase 3: Operational Pilot

- Connect to the operational NWP cycle.
- Automate post-processing after each model run.
- Generate district and grid-level products.
- Add alert routing and user roles.
- Monitor model drift and retraining requirements.

---

## 11. Risks and Mitigation

| Risk | Mitigation |
|---|---|
| Limited extreme rainfall samples | Use long historical datasets, reforecasts, event-based sampling and regime-wise validation. |
| Uncertainty in regime labels | Combine expert-defined rules with atmospheric indicators and clustering. |
| Regional performance differences | Use spatial features, regional calibration and district-level verification. |
| Model overfitting | Use time-based validation, holdout years and strict leakage controls. |
| Forecast drift | Monitor live performance and retrain periodically. |
| Low user trust | Display regime, confidence, raw forecast and verification evidence together. |
| Missing observations | Use quality flags, multiple observation sources and uncertainty estimates. |

---

## 12. Expected Impact

Varsha AI can support:

- Earlier warnings for heavy rainfall and flood risk
- Better district-level disaster preparedness
- Improved agricultural planning and crop protection
- More informed reservoir and water resource operations
- Better urban drainage and landslide preparedness
- More transparent and measurable NWP forecast improvement
- A reusable AI post-processing framework for additional weather hazards

The system is designed to improve the usefulness of forecasts, not only their numerical accuracy. A forecast becomes valuable when it helps an administrator, forecaster, farmer, or emergency team make a timely decision.

---

## 13. Research References

1. World Meteorological Organization / WGNE. *Suggested Methods for the Verification of Precipitation Forecasts.*  
   https://wgne.net/publications/suggested-methods-for-precipitation-verification/

2. National Centre for Medium Range Weather Forecasting. *Weather Products and Forecast Dashboard.*  
   https://nwp.ncmrwf.gov.in/forecast-dashboard

3. *Deep learning with spatio-temporal conditioning improves subseasonal precipitation forecasts.* Nature Portfolio, 2026.  
   https://www.nature.com/articles/s41612-026-01430-8

4. Liu, S. et al. *Statistical postprocessing of subseasonal cumulative precipitation forecasts using a spatial heterogeneity-aware U-Net.* Journal of Hydrology, 2025.  
   https://doi.org/10.1016/j.jhydrol.2025.134854

5. Guan, H. et al. *GEFSv12 reforecast dataset for supporting subseasonal and hydrometeorological applications.* Monthly Weather Review, 2022.  
   https://doi.org/10.1175/MWR-D-21-0245.1

6. Roberts, N. M. and Lean, H. W. *Scale-Selective Verification of Rainfall Forecasts.* Monthly Weather Review, 2008.

7. Ronneberger, O., Fischer, P. and Brox, T. *U-Net: Convolutional Networks for Biomedical Image Segmentation.* 2015.  
   https://arxiv.org/abs/1505.04597

---

## 14. Project Status

The current project includes a polished multi-page dashboard prototype with:

- Overview page
- Live Forecast page
- Verification page
- Profile page
- Responsive layout
- Regime-aware rainfall concepts
- District-level forecast presentation
- Verification metric presentation

The machine learning pipeline, live data connectors, and operational NWP integration are planned for the next implementation phase.

---

## 15. License

This project is proposed as an educational and research prototype for Smart India Hackathon 2026. Licensing and data-use terms should be finalised before operational or public deployment.

---

## 16. Contact

**Project:** Varsha AI  
**Problem Statement:** 26080  
**Organization:** Ministry of Earth Sciences / NCMRWF  
**Team:** [Add registered team name]  
**Email:** [Add team email]
