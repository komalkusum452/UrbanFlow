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