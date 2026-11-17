# Звіт до лабораторної роботи № 10 — варіант 17

## Мета й дані
Трансферне навчання EfficientNetB0 на Food-101; Python 3.9.6, TensorFlow 2.16.2, Keras 3.10.0. Класи: cheese_plate, garlic_bread, pizza (індекси 16, 46, 76). На кожен клас: 600 train, 150 validation, 250 test. Застосовано незмінний manifest Lab9 (seed 42); точних SHA-256-дублікатів та пошкоджених JPEG не знайдено. Різні кадри одного об'єкта за ID надійно не ідентифікуються.

## Метод
RGB 224×224, пікселі [0, 255], оскільки EfficientNetB0 містить препроцесинг. Аугментація лише train: горизонтальне віддзеркалення та невеликий поворот. Feature extraction: заморожена база, GAP, Dropout 0.2, softmax-голова, Adam 1e-3. Fine-tuning: block7* і top_* без BatchNormalization, Adam 1e-5. Зупинка та checkpoints за validation loss.

## Порівняння validation
| Етап | Розморожені блоки | LR | Навчувані параметри | Епохи | Validation loss | Validation accuracy |
| --- | --- | ---: | ---: | ---: | ---: | ---: |
| feature_extraction | лише голова | 1e-03 | 3843 | 10 | 0.1744 | 0.9333 |
| fine_tuning | block7*, top_* (без BatchNorm) | 1e-05 | 1125427 | 10 | 0.1629 | 0.9333 |

Обрано **fine_tuning** за меншою validation loss (за рівності — перший етап). Часткове донавчання зменшило validation loss. Найнижча validation loss на епосі 10 першого етапу та 10 другого. Train loss загалом зменшувалася, validation accuracy після початкового зростання трималася близько 0.933. Стійкого зростання validation loss не спостерігається; ліміт епох міг зупинити подальше поліпшення. Графіки: `training_curves.png`.

## Незалежний test
Accuracy: **0.9627**; macro-F1: **0.9626**. У Lab9 на тому самому поділі: accuracy 0.7507, macro-F1 0.7493. Матриця помилок: `confusion_matrix.png`; приклади: `errors.png`.

Покласовий звіт:
```
              precision    recall  f1-score   support

cheese_plate      0.976     0.964     0.970       250
garlic_bread      0.955     0.944     0.950       250
       pizza      0.957     0.980     0.968       250

    accuracy                          0.963       750
   macro avg      0.963     0.963     0.963       750
weighted avg      0.963     0.963     0.963       750

```

Найбільша плутанина: **garlic_bread → pizza**, 9 фото. Можливі причини: схожі інгредієнти, фон, ракурс та шумні мітки train. Висока softmax-імовірність не гарантує правильності.

## Висновок
За одним seed оцінка має варіативність. Test не використовувався для вибору моделі чи параметрів. Наступна перевірка: спробувати розморозити також block6* за того самого LR та validation-протоколу; її слід виконати з того самого найкращого checkpoint першого етапу і порівняти за validation до нового незалежного test.

Джерело: https://data.vision.ee.ethz.ch/cvl/datasets_extra/food-101/ . Права на фото належать авторам; їх не поширюємо в репозиторії. Код: https://github.com/StanisLaw194/data-mining .
