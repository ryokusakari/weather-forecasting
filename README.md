# Weather Forecasting

An end-to-end weather forecasting project developed as a first-stage, UK-only time-series pipeline. The current implementation uses the London observations available in the source dataset to predict next-day temperature and compare a persistence baseline, XGBoost, and an LSTM neural network.

This is a proof of concept for the next phase: a global spatiotemporal forecasting model that can learn from both weather history and geographical relationships between locations.

## Project Status

The UK pipeline is under active development. It currently includes data preparation, exploratory analysis, XGBoost forecasting, and an LSTM implementation with time-series cross-validation. Final model evaluation and the global spatiotemporal extension are planned next.

## Pipeline

1. Download the Global Weather Repository data with KaggleHub.
2. Filter the data to UK observations (currently London), clean redundant fields, and create time and wind features.
3. Resample observations to a daily time series and impute missing dates using forward fill.
4. Explore seasonal patterns, correlations, PCA structure, and unusual weather events.
5. Forecast next-day temperature using:
   - a persistence baseline (the latest observed temperature),
   - XGBoost with lagged weather features and expanding-window validation, and
   - an LSTM with sliding input windows and expanding-window validation.
6. Evaluate models on a final 20% chronological hold-out test period using explained variance, R², MSE, RMSE, and MAE.

## Methods and Tools

- **Data processing:** pandas, NumPy, KaggleHub
- **Exploratory analysis:** matplotlib, seaborn, SciPy, PCA, Hotelling's T² outlier detection
- **Machine learning:** scikit-learn, XGBoost, `TimeSeriesSplit`
- **Deep learning:** PyTorch and Lightning

## Repository Structure

```text
weather-forecasting/
|-- Data-main/                 # Downloaded Global Weather Repository data
|-- feature_engineering.ipynb  # Feature-engineering experiments
|-- UKforecasting.ipynb        # Main UK forecasting pipeline
|-- requirements.txt           # Python dependencies
`-- README.md
```

## Local Setup

### 1. Clone the repository

```bash
git clone https://github.com/ryokusakari/weather-forecasting.git
cd weather-forecasting
```

### 2. Create and activate a virtual environment

```bash
python3 -m venv .venv
source .venv/bin/activate
```

On Windows PowerShell, activate it with:

```powershell
.\.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

```bash
python -m pip install -r requirements.txt
```

### 4. Run the notebooks

Open `UKforecasting.ipynb` in VS Code or Jupyter, select the project virtual environment as the kernel, then run the cells from top to bottom. The notebook downloads the latest dataset into `Data-main/` through KaggleHub.

## Current Limitations

- The UK stage currently models London, because it is the available UK location in this dataset.
- The data contains approximately one observation per day, recorded at variable times of day.
- The recorded period covers only about one annual weather cycle, so longer-term generalisation is not yet established.
- The LSTM is still being stabilised and evaluated; its results should not yet be treated as final.

## Next Steps

- Complete the final comparison of baseline, XGBoost, and LSTM test performance.
- Improve the reproducibility and packaging of the notebook workflow.
- Expand from the London proof of concept to a **global spatiotemporal model** that represents location as well as time, allowing information to be shared across weather stations.

## Data Source

The pipeline downloads the [Global Weather Repository](https://www.kaggle.com/datasets/nelgiriyewithana/global-weather-repository) through KaggleHub.

## Author

Ryo Kusakari
[GitHub](https://github.com/ryokusakari)
