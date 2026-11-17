# Лабораторна робота № 10 — трансферне навчання

Варіант 17. Класи Food-101: `cheese_plate`, `garlic_bread`, `pizza` (індекси 16, 46, 76). Основний файл — [Lab10.ipynb](Lab10.ipynb).

Використовується той самий поділ, що в лабораторній № 9: `Lab9/data/food101_lab9/{train,val,test}` та `Lab9/manifest.json`. На кожен клас припадає 600 train, 150 validation і 250 test фото. Якщо даних локально немає, спочатку виконайте кроки підготовки в `Lab9/Lab9.ipynb`.

Оберіть Jupyter-ядро `Lab5/.venv/bin/python` (Python 3.9, TensorFlow 2.16.2, Keras 3.10.0) і виконайте ноутбук згори донизу. За потреби встановіть залежності з `Lab10/requirements.txt`. Перший запуск EfficientNetB0 завантажує ImageNet-ваги й потребує доступу до інтернету. На CPU навчання може тривати довго. Усі графіки, checkpoints, метрики й звіт ноутбук записує до `Lab10/results/`.

Модель обирається **лише за мінімальною validation loss** між feature extraction і fine-tuning; незалежний test використовується після вибору. Код перевіряє цілісність і склад вибірок, виявляє точні дублікати за SHA-256, а також зберігає manifest поділу.

## Результат виконання

| Етап | Епохи | Validation loss | Validation accuracy |
| --- | ---: | ---: | ---: |
| Feature extraction | 10 | 0,1744 | 0,9333 |
| Fine-tuning | 10 | **0,1629** | 0,9333 |

Обрано fine-tuning. На незалежному test із 750 фото: accuracy **0,9627**, macro-F1 **0,9626**. Повний [звіт](results/report.md), [графіки навчання](results/training_curves.png), [матриця помилок](results/confusion_matrix.png) і [приклади помилок](results/errors.png) збережені в `results/`. Код і опис розміщуються в [репозиторії](https://github.com/StanisLaw194/data-mining).

Джерело даних: [Food-101, ETH Zürich](https://data.vision.ee.ethz.ch/cvl/datasets_extra/food-101/). Зображення походять із Foodspotting. [Картка набору ETH](https://huggingface.co/datasets/ethz/food101/blob/main/README.md) застерігає, що використання поза науковими цілями потрібно узгоджувати з власниками фото. Зображення не додаються до репозиторію.
