# Southeast Asian Daily Weather Patterns (2000–2024)

### Big Data Analytics — Final Project (UWE, ITITWE20026)

This project applies a PySpark pipeline, regression/time-series analysis, and three anomaly-detection methods to the NOAA GHCN-Daily dataset for 10 Southeast Asian countries across 2000–2024. It addresses four research questions on regional warming, extreme-rainfall trends, anomalous climate events, and seasonal-pattern shifts.

## Repository layout

```
Project/
├── notebooks/                    # 5 Jupyter notebooks (execute in order)
│   ├── 01_process_data.ipynb     # Raw GHCN CSV ingestion → filtered Parquet
│   ├── 02_eda.ipynb              # Exploratory data analysis (10 figures)
│   ├── 03_anomaly_detection.ipynb  # Z-score, IQR, Isolation Forest
│   ├── 04_regression.ipynb       # OLS warming trends + seasonal decomposition
│   └── 05_visualisation.ipynb    # Final portfolio (radar, dashboard, index)
├── data/
│   ├── raw/                      # NOAA GHCN daily CSVs, one per year 2000–2024
│   └── processed/                # Cleaned Parquet (produced by nb 01)
├── output/                       # All figures (.png) and anomaly_catalogue.csv
├── src/                          # (reserved for reusable modules — none used)
├── requirements.txt              # Python dependencies
└── README.md                     # This file
```

## Environment and requirements

- Read the IMPORTANT.txt in /data/raw and download the raw csv files from 2000-2024 at https://www.ncei.noaa.gov/pub/data/ghcn/daily/by_year/
- Python 3.10+
- Apache Spark 4.1 (PySpark)
- 8 GB+ RAM (Spark driver memory is set to 8 GB in each notebook)

Install Python dependencies:

```bash
pip install -r requirements.txt
```

## How to run

The notebooks are written to run sequentially and use relative paths (`../data/...`, `../output/...`). Launch Jupyter from the project root:

```bash
cd notebooks
jupyter notebook
```

Then execute the notebooks in order: 01 → 02 → 03 → 04 → 05.

Notebook 01 produces the processed Parquet that the remaining four notebooks read. If `data/processed/sea_weather_2000_2024.parquet` is already present, notebooks 02–05 can be run independently.

## Outputs

All figures and data artifacts produced by the notebooks are written to `output/`. The final cell of `05_visualisation.ipynb` prints a complete index mapping each figure to the section of the report and research question it supports.

## Dataset

NOAA Global Historical Climatology Network — Daily (GHCN-Daily).
Access: https://www.ncei.noaa.gov/products/land-based-station/global-historical-climatology-network-daily
Variables used: `TMAX`, `TMIN`, `PRCP`. Derived: `TEMP_RANGE = TMAX − TMIN`.
Countries (10): Vietnam, Thailand, Indonesia, Philippines, Malaysia, Laos, Myanmar, Singapore, Cambodia, Brunei.
