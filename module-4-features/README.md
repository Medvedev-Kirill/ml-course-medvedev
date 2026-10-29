# 🛒 Module 4 — Online Shoppers: Инженерия признаков

**Автор:** Медведев Кирилл Андриянович, АСОиУб-23-2  
**Дата:** 2026-10-14

## 📊 Результаты

| Модель | Accuracy | Precision | Recall | F1 | ROC-AUC | Время |
|--------|----------|-----------|--------|-----|---------|-------|
| Random Forest | 0.8743 | 0.5717 | 0.7513 | 0.6493 | 0.9262 | 0.314 сек |
| XGBoost | **0.8804** | **0.5928** | 0.7277 | 0.6533 | 0.9219 | 0.230 сек |
| LightGBM | 0.8727 | 0.5651 | 0.7723 | 0.6527 | 0.9265 | **0.140 сек** |
| CatBoost | 0.8690 | 0.5526 | 0.8115 | 0.6575 | 0.9268 | 0.630 сек |
| **CatBoost (Optuna)** | — | — | — | — | **0.9298** | — |

**Лучшая модель:** CatBoost (Optuna) — ROC-AUC = **0.9298**

**Optuna:** 30 trials, 143 сек, прирост +0.30% (от baseline 0.9268)

## 🚀 Быстрый старт

```python
import joblib
import requests
from io import BytesIO

BASE_URL = "https://raw.githubusercontent.com/Medvedev-Kirill/ml-course-medvedev/main/module-4-features"
model = joblib.load(BytesIO(requests.get(f"{BASE_URL}/models/best_model.pkl").content))
features = requests.get(f"{BASE_URL}/models/feature_cols.json").json()

## 📁 Структура модуля

module-4-features/
├── README.md                          
├── notebook.ipynb                     
├── requirements.txt                   
│
├── data/
│   ├── online_shoppers_intention.csv  
│   └── dataset_info.md                
│
├── models/
│   ├── best_model.pkl                 
│   ├── rf_model.pkl                  
│   ├── xgb_model.pkl                 
│   ├── lgbm_model.pkl                 
│   ├── cat_model.pkl                  
│   ├── feature_cols.json              
│   └── metrics.json                   
│
└── examples/
    ├── eda_plots.png                  
    ├── roc_curves.png                 
    ├── feature_importance.png         
    ├── shap_summary.png               
    └── shap_waterfall.png             