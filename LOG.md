# UrbanFlow : Development Log
Here I will be documenting daily experiments and learning on the project

# Day 1 Development Log
**Date:** 25 November 2026

### 1. Work Completed
- Set up the GitHub repository, project folders, Python virtual environment and Jupyter notebook.
- Installed required libraries: Pandas, NumPy, Matplotlib, Scikit-learn, NetworkX, OSMnx, Jupyter and PyTables.
- Downloaded and loaded the METR-LA dataset using Pandas.
- Explored traffic patterns through time-series visualisations.
- Created a chronological 70:10:20 train/validation/test split.

### 2. Dataset Findings
- Shape: **34,272 timestamps × 207 sensors**.
- Duration: 1 March – 27 June 2012.
- Sampling interval: 5 minutes.
- NaN values: 0.
- Zero readings: 575,302 (approximately 8.11%).
- Network-wide average speed was lowest around 5 PM (46.53 mph) and highest around 8 PM (59.83 mph).
- Observed differences between sampled weekday and weekend traffic patterns.

### 3. Challenges & Solutions
- **PyTables dependency:** Installed `tables` to enable HDF5 loading through Pandas.
- **Pandas–PyTables loading error:** Downgraded Pandas from 3.1.1 to 2.2.3, which resolved the loading issue.
- **Broken frequency metadata:** Reconstructed the DatetimeIndex using `pd.DatetimeIndex(data.index.values)` and verified the actual 5-minute interval.

### 4. Important Learnings
- Time-series data, sensors, timesteps and frequency metadata.
- Pandas operations: `iloc`, `loc`, `groupby()` and aggregation.
- Daily traffic patterns and potential seasonality.
- Importance of investigating zero readings before treating them as missing data.
- Chronological splitting to prevent data leakage.

### 5. Train/Validation/Test Split

| Split | Observations | Period |
|---|---:|---|
| Training (70%) | 23,990 | Mar 1 – May 23 |
| Validation (10%) | 3,427 | May 23 – Jun 4 |
| Testing (20%) | 6,855 | Jun 4 – Jun 27 |

**Outcome:** Successfully completed environment setup and initial METR-LA exploration. Ready to move towards spatial analysis and traffic forecasting.
# Day 2 — Forecasting Baselines, Road Network & SUMO

## 1. Forecasting Baselines

Implemented and evaluated two baseline forecasting methods on METR-LA.

### Historical Average
- Calculated average speed for each sensor based on day of week and time of day.
- Used historical averages to predict future traffic speeds.

### Persistence Baseline
- Used the current observed speed to predict future speeds.
- Evaluated at 15, 30 and 60-minute horizons.

### Results

| Model | MAE (mph) | RMSE (mph) |
|---|---:|---:|
| Historical Average | 7.1025 | 9.8237 |
| Persistence — 15 min | 3.4583 | 6.3070 |
| Persistence — 30 min | 4.1454 | 7.9166 |
| Persistence — 60 min | 5.3077 | 10.2236 |

### Observations
- Persistence performed best at the 15-minute horizon.
- Prediction errors increased as the forecasting horizon increased.
- Historical Average had a better RMSE than Persistence at the 60-minute horizon.
- These baselines will serve as reference points for future ML models.

## 2. Road Network Extraction using OSMnx

- Installed OSMnx and NetworkX.
- Downloaded a 500-metre road network around Koramangala, Bengaluru.
- Extracted a graph containing 245 nodes and 580 edges.
- Visualised the road network.
- Inspected road attributes such as length and highway type.

### Road Statistics
- Average road segment length: 63.57 metres
- Longest road segment: 245.43 metres
- Shortest road segment: 4.82 metres

Learned that OSMnx represents road networks using NetworkX graph structures.

## 3. SUMO Installation and First Simulation

- Installed SUMO 1.28.0 on Windows.
- Configured the SUMO `bin` directory in the User PATH environment variable.
- Verified access to `sumo` and `sumo-gui`.
- Learned the basics of SUMO XML configuration files.

### Created a simple simulation
- `network.nod.xml` — defined two junctions.
- `network.edg.xml` — defined one directed road.
- `network.net.xml` — generated the network using `netconvert`.
- `routes.rou.xml` — defined a car type, route and vehicle.
- `simulation.sumocfg` — configured the simulation.

### Simulation Results
Successfully ran a 100-second simulation.

- Vehicles inserted: 1
- Vehicles running at the end: 0
- Vehicles waiting at the end: 0
- Simulation completed successfully.

## 4. Key Learnings

- Understood MAE and RMSE evaluation for forecasting.
- Learned how OSMnx and NetworkX represent road networks.
- Understood XML structure and its role in SUMO.
- Learned how to generate a SUMO network using `netconvert`.
- Successfully executed a basic traffic simulation.

## 5. Pending / Next Steps

- Improve the visualisation of the SUMO simulation and verify vehicle movement.
- Explore more realistic road networks and traffic demand.
- Continue developing forecasting models.
- Begin connecting traffic forecasting with incident-response logic.

## Day 2 Status

Completed forecasting baselines, initial road network extraction, and SUMO installation with a successful first simulation.