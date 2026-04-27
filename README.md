# 🌍 Global Weather Trend Forecasting

**PM Accelerator Technical Assessment — Data Scientist Track**
Submitted by: Ramya Sri | MSc Artificial Intelligence, Northumbria University London

---

## 📌 PM Accelerator Mission

By making industry-leading tools and education available to individuals from all backgrounds, PM Accelerator levels the playing field for future Product Management leaders. The mission is to empower the next generation of Product Managers by providing hands-on training, mentorship, and exposure to real-world AI products through a global community of professionals from top-tier companies.

---

## 🎯 Project Overview

This project analyses the **Global Weather Repository** dataset (137,998 daily readings across 257 cities and 211 countries) to forecast weather trends and surface insights about climate and air quality. It covers both the **basic and advanced** assessment tracks:

- ✅ Data cleaning, preprocessing, EDA, and visualisation
- ✅ Time-series forecasting with ARIMA + Prophet + ensemble
- ✅ Anomaly detection on air quality
- ✅ Weather × air quality correlation analysis
- ✅ Feature importance via Random Forest
- ✅ Geographic patterns across cities and countries

---

## 📊 Key Findings

### Dataset
- **137,998** weather readings, **May 2024 → April 2026** (almost 2 years of daily data)
- **257 cities** across **211 countries**
- **Zero missing values** in the raw data
- **4 physically impossible readings** removed during EDA (e.g. a 79°C temperature, a 2,963 km/h wind reading — likely API glitches)

### Forecasting (London, 14-day horizon)
| Model | MAE (°C) | RMSE (°C) |
|---|---|---|
| **ARIMA(5,1,2)** ✅ best | **2.42** | **3.04** |
| Prophet | 3.95 | 4.41 |
| Ensemble (avg) | 2.76 | 3.24 |

ARIMA outperformed Prophet on this 14-day horizon. The ensemble didn't beat the best individual model here — a useful lesson that ensembling helps most when individual models have genuinely different error patterns.

### Air Quality Insights
- **Strongest weather → air quality correlation:** humidity ↔ ozone (r = −0.40). Drier air is consistently linked to higher ozone.
- **Top PM2.5 predictor:** latitude (50% feature importance via Random Forest), reflecting that pollution patterns are geographically structured.
- **Pollution hotspots identified via Z-score anomaly detection (|z| > 3):** Jakarta, Beijing, Riyadh, New Delhi, Santiago — all known real-world pollution centres, validating the analysis.
- **Anomaly rate:** 1.54% of all PM2.5 readings flagged as extreme.

### Climate & Geography
- Coldest city on average: **Chi-Chi-Erh** (−12.5°C)
- Hottest city on average: **Riyadh** (45.0°C)
- Wettest month globally: **July**
- Driest month globally: **February**

---

## 🛠️ Methodology

### 1. Data Cleaning
- Converted `last_updated` to datetime, derived month/year features
- Dropped 7 redundant imperial-unit columns (kept metric only)
- Ran IQR outlier detection but **kept extreme temperatures** (real-world readings, not errors)
- Caught and removed 4 physically impossible readings during EDA

### 2. Exploratory Data Analysis
- Global temperature distribution
- Top 10 hottest / coldest cities
- Correlation heatmap of 9 weather features
- Daily global temperature trend with 30-day rolling mean
- Monthly precipitation seasonality

### 3. Forecasting Models
- **Train/test split:** last 14 days held out
- **ARIMA(5,1,2)** — classical statistical baseline
- **Prophet** — Meta's library, weekly + yearly seasonality enabled
- **Ensemble** — simple average of both forecasts
- **Metrics:** MAE and RMSE

### 4. Advanced Analyses
- **Anomaly detection:** Z-score method on PM2.5 (|z| > 3)
- **Correlation analysis:** weather features × all air quality pollutants
- **Feature importance:** Random Forest regressor predicting PM2.5
- **Geographic analysis:** top countries and cities by mean PM2.5

---

## 📁 Repository Structure

```
.
├── README.md                          ← you are here
├── requirements.txt                   ← Python dependencies
├── notebooks/
│   └── weather_forecasting.ipynb      ← main analysis notebook
├── outputs/
│   ├── figures/                       ← all generated plots
│   ├── model_comparison.csv
│   ├── top_polluted_cities.csv
│   └── project_summary.json
└── demo/
    └── demo_link.md                   ← link to demo video
```

---

## ▶️ How to Run

### Option 1 — Google Colab (recommended)
1. Open `notebooks/weather_forecasting.ipynb` in [Google Colab](https://colab.research.google.com)
2. Upload the dataset `GlobalWeatherRepository.csv` to `/content/`
3. Run all cells (Runtime → Run all)
4. All plots and outputs will be generated in the `outputs/` folder

### Option 2 — Local
```bash
git clone https://github.com/<your-username>/global-weather-forecasting.git
cd global-weather-forecasting
pip install -r requirements.txt
jupyter notebook notebooks/weather_forecasting.ipynb
```

The dataset is available from Kaggle: [Global Weather Repository](https://www.kaggle.com/datasets/nelgiriyewithana/global-weather-repository).

---

## 📦 Requirements

See `requirements.txt`. Main libraries:
- `pandas`, `numpy` — data manipulation
- `matplotlib`, `seaborn` — visualisation
- `scikit-learn` — Random Forest for feature importance
- `statsmodels` — ARIMA forecasting
- `prophet` — Meta's forecasting library

---

## 🎬 Demo Video

A short 1–2 minute demo walk-through of the code and results is available here:
**[Demo video link]** *(to be added — see `demo/demo_link.md`)*

---

## 🧠 Reflections & Next Steps

A few things I'd want to explore with more time:

1. **Multi-city forecasting** — extend the pipeline to forecast all 257 cities and surface those with the largest predicted anomalies.
2. **Weighted ensembles** — the simple-average ensemble underperformed ARIMA here because Prophet had higher error. A weighted ensemble (inverse-error weighting) would likely beat both.
3. **External features** — incorporating El Niño / La Niña indices or large-scale climate signals could improve longer-horizon forecasts.
4. **Real-time dashboard** — wrap the forecasting pipeline in a Streamlit or FastAPI service for live querying.

---

## 👤 About Me

I'm Ramya Sri, an MSc Artificial Intelligence student at Northumbria University London (graduating 2026). My dissertation, **OnTimeLondon AI**, is a five-agent transport prediction system orchestrated in n8n, combining LSTM delay prediction, Dijkstra route optimisation, reinforcement learning, and an LLM-powered communication agent.

- 🌐 Portfolio: [ramya-portfolio.vercel.app](https://ramya-portfolio.vercel.app)
- 🛠️ Stack: Python, SQL, n8n, Supabase, scikit-learn, TensorFlow, LLMs

---

*Submitted as part of the Product Manager Accelerator (PMA) Data Scientist Internship technical assessment.*
