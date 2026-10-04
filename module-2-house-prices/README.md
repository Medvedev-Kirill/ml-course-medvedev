# Module 2 - House Prices: предобработка и регрессия

**Автор:** Медведев Кирилл Андриянович, АСОиУб-23-2  
**Дата:** 2026-10-04

## Результаты

| Модель | RMSE (log) | MAE (log) | R² | RMSE ($) |
|--------|-----------|-----------|-----|---------|
| Linear Regression | 0.1237 | 0.0887 | 0.8969 | $22,409 |
| Ridge | 0.1239 | — | 0.8965 | $22,379 |
| **Lasso** | **0.1214** | **0.0849** | **0.9005** | **$21,758** |
| ElasticNet | 0.1215 | 0.0849 | 0.9004 | $21,723 |

**Лучшая модель:** Lasso (R² = 0.9005, RMSE = $21,758)

**Время обучения:** < 0.1 сек на модель

## 🚀 Быстрый старт

```python
import joblib
import requests
from io import BytesIO

BASE_URL = "https://raw.githubusercontent.com/Medvedev-Kirill/ml-course-medvedev/main/module-2-house-prices"
model = joblib.load(BytesIO(requests.get(f"{BASE_URL}/models/lasso_model.pkl").content))
scaler = joblib.load(BytesIO(requests.get(f"{BASE_URL}/models/scaler.pkl").content))