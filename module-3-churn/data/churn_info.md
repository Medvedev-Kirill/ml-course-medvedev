# 📊 Telco Customer Churn Dataset — описание

**Источник:** https://www.kaggle.com/datasets/blastchar/telco-customer-churn

## Файлы

- `telco_churn.csv` — 7043 строки, 21 столбец

## Целевая переменная

- **Churn** — ушёл ли клиент (Yes / No)
- No (остался): **5174 (73.5%)**
- Yes (ушёл): **1869 (26.5%)**
- Дисбаланс классов: **73.5 / 26.5** — умеренный

## Структура признаков

| Категория | Количество | Примеры |
|-----------|------------|---------|
| Демографические | 4 | gender, SeniorCitizen, Partner, Dependents |
| Услуги | 9 | PhoneService, MultipleLines, InternetService, OnlineSecurity, OnlineBackup, DeviceProtection, TechSupport, StreamingTV, StreamingMovies |
| Аккаунт | 6 | Contract, PaperlessBilling, PaymentMethod, MonthlyCharges, TotalCharges, tenure |

## Ключевые столбцы

| Столбец | Тип | Описание | Пропуски |
|---------|-----|----------|----------|
| customerID | object | Уникальный ID | 0% |
| gender | object | Пол (Male / Female) | 0% |
| SeniorCitizen | int (0/1) | Пенсионер | 0% |
| tenure | int | Месяцев с компанией (0-72) | 0% |
| MonthlyCharges | float | Ежемесячная плата | 0% |
| TotalCharges | object | Общая сумма | **~0.2%** (11 пропусков) |
| Contract | object | Тип контракта (Month-to-month / One year / Two year) | 0% |
| Churn | object | **Целевая** (Yes / No) | 0% |

## Пропуски

- **TotalCharges** - 11 пропусков (0.2%)
- Причина: значения пустые строки в исходном CSV
- Решение: `pd.to_numeric(errors='coerce')` + заполнение медианой

## Обработка

1. **TotalCharges** → `float` через `pd.to_numeric(errors='coerce')`
2. **Пропуски TotalCharges** → медиана
3. **Churn** → бинарная (Yes=1, No=0)
4. **customerID** → удалён
5. **15 категориальных** → LabelEncoder
6. **Разделение** → `train_test_split(test_size=0.2, stratify=y)`

## Feature Engineering

- **TenureYears** = tenure / 12
- **AvgMonthlyCharge** = TotalCharges / (tenure + 1)
- **IsNewClient** = (tenure <= 6).astype(int)
- **HasMultipleServices** = счётчик подключённых услуг

## Ключевые инсайты

- **Contract** - сильнейший предиктор (Month-to-month: 42.7% ушли)
- **tenure** - первые 6 месяцев самые рискованные (53.3% ушли)
- **Fiber optic** - выше отток (41.9%)
- **OnlineSecurity / TechSupport** - снижают отток