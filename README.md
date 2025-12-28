# ☀️ Solar Energy Forecasting with TimeGPT

A time-series forecasting project that predicts solar power generation using Nixtla's TimeGPT model and real-world meteorological data from Huzhou, China.

## 📋 Project Overview

This project demonstrates the application of state-of-the-art foundation models (TimeGPT) for renewable energy forecasting. The system predicts hourly solar power generation by:

- Collecting historical weather data via Open-Meteo API
- Training TimeGPT on historical power generation patterns
- Fine-tuning the model for improved accuracy
- Forecasting future solar energy output

## 🎯 Key Features

- **Real-world Data Integration**: Uses Open-Meteo archive API for meteorological data (temperature, humidity, radiation, precipitation, wind speed)
- **Foundation Model Application**: Leverages TimeGPT, a pre-trained transformer model for time-series forecasting
- **Multi-scale Analysis**: Handles data at both 10-minute and hourly intervals
- **Model Fine-tuning**: Implements custom fine-tuning steps for domain adaptation
- **Comprehensive Visualization**: Compares actual vs. predicted power generation

## 📊 Datasets

### 1. Alabama Solar Data
- **Source**: 137 solar power stations in Alabama (2006)
- **Resolution**: 10-minute intervals
- **Features**: Raw power generation data
- **Application**: Initial model training and validation

### 2. Huzhou Weather Data
- **Location**: Huzhou, China (30.869°N, 120.093°E)
- **Period**: May - June 2025
- **Resolution**: Hourly
- **Features**:
  - Temperature (2m)
  - Relative Humidity
  - Shortwave & Direct Radiation
  - Diffuse Radiation
  - Precipitation
  - Wind Speed (10m)

## 🛠️ Technologies Used

- **Python 3.10**
- **TimeGPT** (Nixtla): Foundation model for time-series forecasting
- **Pandas**: Data manipulation and analysis
- **NumPy**: Numerical computing
- **Matplotlib**: Data visualization
- **Requests**: API data collection
- **Open-Meteo API**: Weather data provider

## 📁 Project Structure

```
solar-energy-forecasting/
├── README.md
├── requirements.txt
├── timegpt.ipynb              # Initial TimeGPT exploration (Alabama data)
├── EnergyForecasting.ipynb    # Main forecasting workflow (Huzhou data)
├── data/
│   ├── May_h.csv              # May 2025 power generation data
│   ├── June_h.csv             # June 2025 power generation data
│   └── solar_AL.txt.gz        # Alabama solar stations data
└── results/
    └── forecast_plots/        # Generated visualization outputs
```

## 🚀 Getting Started

### Prerequisites

```bash
python >= 3.10
```

### Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/solar-energy-forecasting.git
cd solar-energy-forecasting
```

2. Create a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Set up your Nixtla API key:
   - Sign up at [Nixtla](https://www.nixtla.io/)
   - Get your API key
   - Replace `NIXTLA_API_KEY` in the notebooks with your actual key

### Usage

#### Notebook 1: TimeGPT Exploration (`timegpt.ipynb`)
Demonstrates basic TimeGPT usage with Alabama solar data:
- Data preprocessing and aggregation
- Hourly resampling
- Train/test split (Jan-Oct vs. Nov)
- Model forecasting with fine-tuning

#### Notebook 2: Weather-Based Forecasting (`EnergyForecasting.ipynb`)
Complete forecasting pipeline for Huzhou:
1. Fetch weather data from Open-Meteo API
2. Prepare time-series data
3. Train TimeGPT on May data
4. Forecast June power generation
5. Visualize and evaluate results

**Example:**
```python
from nixtlats import NixtlaClient

client = NixtlaClient(api_key="your_api_key")

forecast = client.forecast(
    df=may_data,
    h=len(june_data),
    freq="H",
    time_col="ds",
    target_col="y",
    finetune_steps=50
)
```

## 📈 Results

The model successfully forecasts solar power generation with:
- Training period: May 2025 (full month)
- Forecast period: June 2025 (full month)
- Fine-tuning steps: 50
- Visualization showing actual vs. predicted values

*Example output from `EnergyForecasting.ipynb`:*
- Clear correlation between predicted and actual values
- Model captures daily generation patterns
- Accounts for weather variations

## 🔍 Methodology

1. **Data Collection**: Historical weather data retrieved from Open-Meteo archive
2. **Feature Engineering**: Multiple meteorological variables as predictors
3. **Model Training**: TimeGPT pre-trained model fine-tuned on May data
4. **Forecasting**: Hour-by-hour predictions for June
5. **Validation**: Visual comparison of actual vs. predicted generation

## 🎓 Skills Demonstrated

- **Data Analysis**: Time-series data processing and feature engineering
- **API Integration**: Programmatic data collection from weather services
- **Machine Learning**: Application of foundation models for forecasting
- **Python Programming**: Clean, documented code with best practices
- **Domain Knowledge**: Understanding of solar energy and meteorological factors

## 📝 Future Improvements

- [ ] Add evaluation metrics (MAE, RMSE, MAPE)
- [ ] Implement cross-validation
- [ ] Include more meteorological features
- [ ] Compare with traditional forecasting methods (ARIMA, LSTM)
- [ ] Create interactive dashboard for results
- [ ] Extend to multi-location forecasting
- [ ] Add uncertainty quantification

## 📚 References

- [Nixtla TimeGPT Documentation](https://docs.nixtla.io/)
- [Open-Meteo API](https://open-meteo.com/)
- [TimeGPT Paper](https://arxiv.org/abs/2310.03589)

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👤 Author

- LinkedIn: https://www.linkedin.com/in/yi-xie-172471327/
- Email: starinaxie@163.com

## 🙏 Acknowledgments

- Nixtla for providing TimeGPT API
- Open-Meteo for weather data access
- NREL for Alabama solar dataset

---

⭐ Star this repository if you find it helpful!
