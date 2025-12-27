# Data Directory

This directory contains the datasets used in the solar energy forecasting project.

## Files

### Required Data Files (not included in repository)

Due to size constraints, the following data files are **not included** in this repository. Please download or generate them as described below:

#### 1. `May_h.csv`
- **Description**: Hourly solar power generation data for May 2025
- **Location**: Huzhou, China (30.869°N, 120.093°E)
- **Columns**: 
  - `序号` (Index)
  - `时间` (Timestamp)
  - `功率1` (Power Output 1)
  - `功率2` (Power Output 2, optional)
- **How to obtain**: Generate using Open-Meteo API or use your own historical data

#### 2. `June_h.csv`
- **Description**: Hourly solar power generation data for June 2025
- **Format**: Same as May_h.csv
- **Purpose**: Test/validation dataset for forecasting

#### 3. `solar_AL.txt.gz`
- **Description**: Alabama solar power stations dataset (2006)
- **Source**: 137 solar power stations
- **Resolution**: 10-minute intervals
- **Size**: ~52,560 rows (one year of data)
- **Download**: [NREL Solar Dataset](https://www.nrel.gov/grid/solar-power-data.html) or similar sources

## Data Generation

### Using Open-Meteo API

To generate weather-based solar data similar to this project:

```python
import requests
import pandas as pd

base = "https://archive-api.open-meteo.com/v1/archive"
params = {
    "latitude": 30.869,   # Huzhou latitude
    "longitude": 120.093,  # Huzhou longitude
    "start_date": "2025-05-01",
    "end_date": "2025-06-30",
    "hourly": ",".join([
        "temperature_2m",
        "relativehumidity_2m",
        "shortwave_radiation",
        "direct_radiation",
        "diffuse_radiation",
        "precipitation",
        "windspeed_10m"
    ]),
    "timezone": "Asia/Shanghai",
    "models": "best_match"
}

response = requests.get(base, params=params)
data = response.json()

# Process into pandas DataFrame
# See EnergyForecasting.ipynb for complete implementation
```

## Data Format

### Expected CSV Format

```csv
序号,时间,功率1
1,2025-05-01 00:00:00,12.5
2,2025-05-01 01:00:00,8.3
3,2025-05-01 02:00:00,5.1
...
```

### Alternative Formats

If your data has different column names, update the notebook accordingly:

```python
# Adjust column mapping in the notebook
ds_col = your_data.columns[1]  # Timestamp column
y_col  = your_data.columns[2]  # Power output column
```

## Privacy & Security

⚠️ **Important**: 
- Do **NOT** commit sensitive or proprietary data to the repository
- The `.gitignore` file is configured to exclude `.csv` and `.gz` files
- Only share anonymized or publicly available datasets

## Usage

Place your data files in this directory and run the notebooks. The notebooks will automatically load data from this location.

## Sample Data

For demonstration purposes, you can create sample data:

```python
import pandas as pd
import numpy as np

# Generate sample hourly data
dates = pd.date_range('2025-05-01', '2025-05-31 23:00:00', freq='h')
power = np.random.uniform(0, 100, len(dates)) * np.sin(np.arange(len(dates)) * 2 * np.pi / 24)

sample_data = pd.DataFrame({
    '序号': range(1, len(dates) + 1),
    '时间': dates,
    '功率1': power
})

sample_data.to_csv('May_h.csv', index=False)
```

## Data Sources

- **Weather Data**: [Open-Meteo Archive API](https://open-meteo.com/)
- **Solar Data**: [NREL Solar Resource Data](https://www.nrel.gov/grid/solar-resource/)
- **Alternative Sources**: 
  - [NASA POWER Project](https://power.larc.nasa.gov/)
  - [Renewable Ninja](https://www.renewables.ninja/)

## Contributing

If you'd like to add datasets:
1. Ensure data is properly anonymized
2. Add data source and description to this README
3. Update the `.gitignore` if necessary
4. Document the data format clearly

---

For questions about data acquisition or format, please open an issue in the repository.
