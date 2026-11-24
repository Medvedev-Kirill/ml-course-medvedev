# 📈 Module 5 - Electricity Load: Временные ряды и прогнозирование

**Автор:** Медведев Кирилл Андриянович, АСОиУб-23-2  
**Дата:** 2026-12-01

## 📊 Результаты

| Модель | RMSE | MAE | MAPE (%) | sMAPE (%) | MASE | Время обучения |
|--------|------|-----|----------|-----------|------|----------------|
| Naive (Baseline) | 20458.3 | 16996.2 | 50.4 | 63.9 | 4.356 | 0.001 сек |
| **Seasonal Naive** | **5534.5** | **3368.1** | **10.8** | **9.8** | **0.863** | 0.001 сек |
| ETS (Holt-Winters) | 12067.8 | 10708.8 | 40.5 | 54.0 | 2.745 | 3.69 сек |
| SARIMA | 9331.3 | 8531.7 | 37.4 | 52.2 | 2.187 | 34.33 сек |
| ARIMAX + Фурье | 9842.0 | 8822.1 | 43.2 | 63.7 | 2.261 | 74.91 сек |
| Gradient Boosting | 9385.4 | 7948.9 | 31.8 | 29.7 | 2.037 | 17.28 сек |

**Лучшая модель:** Seasonal Naive — MASE = **0.863** (превосходит обычный Naive в 5 раз)

## 🎯 Метрики качества (Rolling-Origin Backtest)

| Фолд | Период теста | MASE (Seasonal Naive) |
|------|--------------|-----------------------|
| 1 | 25.12.2014 – 01.01.2015 | 0.863 |
| 2 | 18.12.2014 – 25.12.2014 | 0.610 |
| 3 | 11.12.2014 – 18.12.2014 | 0.516 |
| 4 | 04.12.2014 – 11.12.2014 | 0.552 |

**Среднее MASE:** 0.635 ± 0.136 (подтверждает отсутствие утечки данных)

## 🚀 Быстрый старт

```python
import joblib
import requests
from io import BytesIO
import json
import pandas as pd

BASE_URL = "https://raw.githubusercontent.com/Medvedev-Kirill/ml-course-medvedev/main/module-5-timeseries"

# Загрузка модели Gradient Boosting и списка ее признаков
model = joblib.load(BytesIO(requests.get(f"{BASE_URL}/models/gb_model.pkl").content))
features = requests.get(f"{BASE_URL}/models/feature_cols.json").json()

# Загрузка параметров ARIMAX 
arimax_params = requests.get(f"{BASE_URL}/models/arimax_params.json").json()

print(f"Модель GB загружена. Ожидаемые признаки: {len(features)}")
print(f"Параметры SARIMAX: {arimax_params}")

module-5-timeseries/
├── README.md                          
├── notebook.ipynb                     
├── requirements.txt                   
│
├── data/
│   ├── electricity_hourly.csv
│   └── dataset_info.md
│
├── models/
│   ├── best_model.pkl
│   ├── gb_model.pkl
│   ├── ets_model.pkl
│   ├── sarima_model.pkl
│   ├── arimax_params.json
│   ├── train_history.npy
│   ├── feature_cols.json
│   ├── forecast_config.json
│   └── metrics.json
│
└── examples/
    ├── eda_plots.png
    ├── stl_decomposition.png
    ├── acf_pacf.png
    ├── forecast_with_ci.png
    ├── error_by_horizon.png
    └── backtest_folds.png