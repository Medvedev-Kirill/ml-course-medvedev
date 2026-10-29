# 📉 Module 3 - Customer Churn: Ансамблевые методы

**Автор:** Медведев Кирилл Андриянович, АСОиУб-23-2  
**Дата:** 2026-10-14

## 📊 Результаты

| Модель | Accuracy | Precision | Recall | F1 | ROC-AUC | Время |
|--------|----------|-----------|--------|-----|---------|-------|
| Random Forest | 0.7729 | 0.5551 | 0.7273 | 0.6296 | 0.8400 | 0.256 сек |
| XGBoost | 0.7594 | 0.5355 | 0.7059 | 0.6090 | 0.8285 | 0.286 сек |
| LightGBM | 0.7601 | 0.5344 | 0.7487 | 0.6236 | 0.8379 | 1.627 сек |
| CatBoost | 0.7559 | 0.5279 | 0.7594 | 0.6228 | 0.8381 | 0.669 сек |
| **LightGBM (Optuna)** | - | - | - | - | **0.8455** | - |

**Лучшая модель:** LightGBM (Optuna) - ROC-AUC = 0.8455

**Optuna:** 30 trials, 13 сек, прирост +0.76%

## 🚀 Быстрый старт

```python
import joblib
import requests
from io import BytesIO

BASE_URL = "https://raw.githubusercontent.com/Medvedev-Kirill/ml-course-medvedev/main/module-3-churn"
model = joblib.load(BytesIO(requests.get(f"{BASE_URL}/models/best_model.pkl").content))