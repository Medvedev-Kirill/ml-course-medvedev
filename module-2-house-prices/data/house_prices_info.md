# 📊 House Prices Dataset — описание

**Источник:** https://www.kaggle.com/c/house-prices-advanced-regression-techniques

## Файлы
- `train.csv` - 1460 строк, 81 столбец (включая SalePrice)
- `test.csv` - 1459 строк, 80 столбцов (без SalePrice)

## Целевая переменная
- **SalePrice** - цена продажи в долларах
- Среднее: $180 921
- Медиана: $163 000
- Асимметрия (skew): 1.88 - правое смещение → нужно log1p
- Эксцесс: 6.51

## Ключевые признаки
| Признак | Тип | Описание |
|---------|-----|----------|
| OverallQual | int (1-10) | Общее качество |
| GrLivArea | float | Жилая площадь |
| TotalBsmtSF | float | Площадь подвала |
| YearBuilt | int | Год постройки |
| GarageCars | int | Вместимость гаража |
| Neighborhood | str | Район |

## Пропуски
- 19 столбцов с пропусками
- PoolQC, MiscFeature, Alley - >90% пропусков (смысловые → "None")
- LotFrontage - ~17% (MAR → медиана по Neighborhood)