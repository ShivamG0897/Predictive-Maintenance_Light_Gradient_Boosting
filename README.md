---

## 📊 Dataset Landscape & Features

This system integrates data from five core architectural tables to create a comprehensive picture of equipment health:

1. **Telemetry (`PdM_telemetry.csv`):** Hourly logs capturing voltage, rotation speeds, internal pressure fluctuations, and vibration patterns.
2. **Error Logs (`PdM_errors.csv`):** Non-fatal anomalies thrown by machines while remaining operational.
3. **Maintenance History (`PdM_maint.csv`):** Historical logs tracking exactly when components (`comp1`, `comp2`, `comp3`, `comp4`) were swapped out.
4. **Machine Profiles (`PdM_machines.csv`):** Structural attributes mapping unique machine IDs to hardware model types and operational age.
5. **Failures (`PdM_failures.csv`):** Explicit ground-truth logs capturing the exact date, time, and component that triggered a system breakdown.

---

## 🛠️ Step-by-Step Execution Guide

Follow these steps to set up your environment, prepare the dataset, and execute the training pipeline locally:

### 1. Environment Setup & Dependency Installation

Clone this repository into your local workspace, initialize an isolated virtual environment, and install all required framework packages:

```bash
# Clone the repository
git clone [https://github.com/ShivamG0897/Predictive-Maintenance_Light_Gradient_Boosting.git](https://github.com/ShivamG0897/Predictive-Maintenance_Light_Gradient_Boosting.git)
cd Predictive-Maintenance_Light_Gradient_Boosting

# Initialize python environment
python3 -m venv venv
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

```

### 2. Data Preparation Block

Ensure that your data folder contains the five raw CSV source files (`PdM_telemetry.csv`, `PdM_errors.csv`, `PdM_maint.csv`, `PdM_machines.csv`, `PdM_failures.csv`).

### 3. Executing the Production Pipeline

Once you've organized the folder structure, you can run the modular code sequentially or run the unified training file to generate features and train the model end-to-end:

```bash
# Triggers ingestion, constructs rolling feature windows, and builds maintenance lag tables
python src/feature_engineering.py

# Trains the LightGBM classifier and logs performance metrics
python src/model_training.py

```

---

## ⚙️ Core Engineering Design Choices

### Advanced Feature Re-sampling & Lag Matrices

Instead of running predictions directly on raw hourly telemetry data, this pipeline creates robust windows to capture deterioration over time:

* **Short-Term Context:** Processes rolling 3-hour mean and standard deviation windows to capture rapid spikes in sensor noise.
* **Long-Term Degradation Profiles:** Builds 24-hour rolling mean and standard deviation variations to trace gradual component wear.
* **Maintenance Recency Vectors:** Processes historical logs to continuously compute a rolling metric tracking the exact *number of days elapsed since a specific component was last replaced*.

### Handling Imbalanced Anomaly Data

Actual machinery breakdowns are sparse events, resulting in heavily skewed datasets. This pipeline addresses class imbalance through programmatic configurations within LightGBM using the `scale_pos_weight` argument. This ensures the model prioritizes identifying critical, high-risk operational anomalies without getting overwhelmed by normal running records.

```

---

### What to do next:
1. Create the `data/`, `notebooks/`, and `src/` folders locally.
2. Move your data CSVs into `data/` and your chosen prototype notebook into `notebooks/`.
3. Commit this fresh, clean `README.md` to your main branch. 

Once your directory layout is updated, we can start breaking down the notebook sections into the individual python files inside the `src/` folder!

```
