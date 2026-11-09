# Лабораторна робота 8 — варіант 5

Для номера у списку 17: `(17 - 1) % 12 + 1 = 5`. Прогнозується ціна житла за одиницю площі в районі Сіньдянь, Новий Тайбей, за шістьма ознаками угоди. Повний аналіз та фактичні результати містяться в [Lab8.ipynb](Lab8.ipynb).

## Дані та атрибуція

- Джерело: I-Cheng Yeh, [Real Estate Valuation](https://archive.ics.uci.edu/dataset/477/real+estate+valuation+data+set), UCI Machine Learning Repository, 2018, [DOI 10.24432/C5J30W](https://doi.org/10.24432/C5J30W).
- Ліцензія: [Creative Commons Attribution 4.0](https://creativecommons.org/licenses/by/4.0/).
- Оригінальний файл: `data/Real estate valuation data set.xlsx`, аркуш `工作表1`; завантажено 2026-11-09. 414 рядків, 6 ознак, ідентифікатор `No` та ціль `Y house price of unit area` (10 000 нових тайванських доларів за пінг; 1 пінг ≈ 3,3 м²).
- Для повторного отримання завантажте XLSX зі [сторінки UCI](https://archive.ics.uci.edu/dataset/477/real+estate+valuation+data+set) або [прямого посилання](https://archive.ics.uci.edu/ml/machine-learning-databases/00477/Real%20estate%20valuation%20data%20set.xlsx) і покладіть його під наведеною назвою в `data/` без редагування.

## Запуск

У VS Code виберіть для ноутбука інтерпретатор `Lab5/.venv/bin/python` з уже наявного в репозиторії середовища: там встановлено TensorFlow 2.16.2. Потрібні пакети перелічено в `requirements.txt`. Запустіть усі клітинки `Lab8.ipynb` послідовно. Залежності препроцесора оцінюються тільки на train; дата поділяє дані хронологічно без розриву однакових дат.

Результати створюються в `model_comparison.csv`, `test_predictions.csv`, `metadata.json`, `figures/` і `artifacts/`. `lab8_model.keras` і `preprocessor.joblib` становлять комплект нейромережевого прогнозу; `best_classical.joblib` зберігається, якщо класична модель найкраща за validation. Завантажуйте файли Joblib лише з довіреного джерела.
