---
title: Обробка багатьох файлів у циклі
teaching: 5
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Навчитися читати та писати вирази модулю glob, які визначають набори файлів.
- Використовувати модуль glob для створення списків файлів
- Створювати цикли `for` для виконання операцій зі списком файлів.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Як обробляти багато наборів даних за допомогою однієї команди?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Використовуйте цикл `for` для послідовної обробки файлів, імена яких містяться у списку.

- Ім'я файлу - це рядок символів.
- Списки, своєю чергою, можуть містити рядки символів.

```python
import pandas as pd
for filename in ['data/gapminder_gdp_africa.csv', 'data/gapminder_gdp_asia.csv']:
    data = pd.read_csv(filename, index_col='country')
    print(filename, data.min())
```

```output
data/gapminder_gdp_africa.csv gdpPercap_1952    298.846212
gdpPercap_1957    335.997115
gdpPercap_1962    355.203227
gdpPercap_1967    412.977514
⋮ ⋮ ⋮
gdpPercap_1997    312.188423
gdpPercap_2002    241.165877
gdpPercap_2007    277.551859
dtype: float64
data/gapminder_gdp_asia.csv gdpPercap_1952    331
gdpPercap_1957    350
gdpPercap_1962    388
gdpPercap_1967    349
⋮ ⋮ ⋮
gdpPercap_1997    415
gdpPercap_2002    611
gdpPercap_2007    944
dtype: float64
```

## Використовуйте [`glob.glob`](https://docs.python.org/3/library/glob.html#glob.glob), щоб знайти набори файлів, імена яких відповідають шаблону.

- В Unix термін "globbing" означає "відповідність набору файлів шаблону".
- Найпоширеніші шаблони:
  - `*` означає "відповідати нулю або більшій кількості символів"
  - `?` означає "відповідати в точності одному символу"
- Стандартна бібліотека Python містить модуль [`glob`](https://docs.python.org/3/library/glob.html) для роботи з наборами файлів, які задані за допомогою шаблонів
- Модуль [`glob`](https://docs.python.org/3/library/glob.html) містить функцію, яка також називається `glob`, для відбору файлів за шаблоном.
- Наприклад, `glob.glob('*.txt')` знайде всі файли в поточному каталозі,
  імена яких закінчуються на `.txt`.
- Результатом є (можливо, порожній) список рядків символів.

```python
import glob
print('all csv files in data directory:', glob.glob('data/*.csv'))
```

```output
all csv files in data directory: ['data/gapminder_all.csv', 'data/gapminder_gdp_africa.csv', \
'data/gapminder_gdp_americas.csv', 'data/gapminder_gdp_asia.csv', 'data/gapminder_gdp_europe.csv', \
'data/gapminder_gdp_oceania.csv']
```

```python
print('all PDB files:', glob.glob(' .pdb'))
```

```output
all PDB files: []
```

## Використовуйте `glob` та `for` для обробки груп файлів.

- Систематичне та послідовне іменування файлів — запорука ефективного пошуку за шаблонами.

```python
for filename in glob.glob('data/gapminder_*.csv'):
    data = pd.read_csv(filename)
    print(filename, data['gdpPercap_1952'].min())
```

```output
data/gapminder_all.csv 298.8462121
data/gapminder_gdp_africa.csv 298.8462121
data/gapminder_gdp_americas.csv 1397.717137
data/gapminder_gdp_asia.csv 331.0
data/gapminder_gdp_europe.csv 973.5331948
data/gapminder_gdp_oceania.csv 10039.59564
```

- Перелік має файл `data/gapminder_all.csv` з усіма даними, а також файли з даними по окремих регіонах.
- У вправах нижче використовуйте більш точний шаблон. Це дозволить виключити загальний набір даних `data/gapminder_all.csv` і відібрати лише файли для окремих регіонів.
- Слід зазначити, що мінімум у файлі `data/gapminder_all.csv` збігається з мінімумом одного з менших файлів. Це є гарною перевіркою результату.

:::::::::::::::::::::::::::::::::::::::  challenge

## Розуміння шаблонів

Який із цих файлів _не_ відповідає виразу `glob.glob('data/*as*.csv')`?

1. `data/gapminder_gdp_africa.csv`
2. `data/gapminder_gdp_americas.csv`
3. `data/gapminder_gdp_asia.csv`

:::::::::::::::  solution

## Відповідь

Заданому шаблону не відповідає перший з файлів.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Мінімальний розмір файлу

Змініть цю програму, щоб вона визначала та виводила мінімальну кількість
записів серед усіх файлів.

```python
import glob
import pandas as pd
fewest = ____
for filename in glob.glob('data/*.csv'):
    dataframe = pd.____(filename)
    fewest = min(____, dataframe.shape[0])
print('smallest file has', fewest, 'records')
```

Зверніть увагу, що метод [`DataFrame.shape()`][shape-method]
повертає кортеж (tuple), елементами якого є кількість рядків та кількість стовпців у датафреймі.

:::::::::::::::  solution

## Відповідь

```python
import glob
import pandas as pd
fewest = float('Inf')
for filename in glob.glob('data/*.csv'):
    dataframe = pd.read_csv(filename)
    fewest = min(fewest, dataframe.shape[0])
print('smallest file has', fewest, 'records')
```

Можна було б ініціалізувати змінну `fewest` числом, що перевищує всі числа у наборі даних, однак це може спричинити помилки при повторному використанні коду з більшими числами.
Python дозволяє використати додатну нескінченність, яка буде працювати незалежно від значень ваших чисел.
Які інші спеціальні рядки розпізнає [функція `float`][float-function]?

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Порівняння даних

Напишіть програму, яка читає регіональні набори даних і будує графік середнього ВВП на душу населення для кожного регіону в часі в одній діаграмі. Pandas видасть помилку, якщо зустріне при цьому нечислові стовпці, тому ви маєте або відфільтрувати ці стовпці, або вказати Pandas ігнорувати їх.

:::::::::::::::  solution

## Відповідь

Це рішення створює корисну легенду за допомогою [методу `split` для рядків][split-method] для вилучення `region` зі шляху 'data/gapminder\\_gdp\\_a\\_specific\\_region.csv'.

```python
import glob
import pandas as pd
import matplotlib.pyplot as plt
fig, ax = plt.subplots(1,1)
for filename in glob.glob('data/gapminder_gdp*.csv'):
    dataframe = pd.read_csv(filename)
    # Вилучаємо <region> з назви файлу, який має бути у форматі 'data/gapminder_gdp_<region>.csv'.
    # Розділимо рядок за допомогою методу split та роздільника `_`,
    # отримаємо останній рядок зі списку, який повертає split (`<region>.csv`),
    # а потім видалимо із цього рядка розширення `.csv`.
    # ПРИМІТКА: модуль pathlib, описаний у наступному блоці, також пропонує
    # зручні абстракції для роботи зі шляхами файлової системи і може вирішити це завдання:
    # from pathlib import Path
    # region = Path(filename).stem.split('_')[-1]
    region = filename.split('_')[-1][:-4]
    # Вилучаємо роки зі стовпців датафрейму
    headings = dataframe.columns[1:]
    years = headings.str.split('_').str.get(1)
    # Pandas видає помилку, коли зустрічає нечислові стовпці в обчисленнях з датафреймом,
    # але ми можемо вказати Pandas ігнорувати їх за допомогою параметра `numeric_only`
    dataframe.mean(numeric_only=True).plot(ax=ax, label=region)
    # ПРИМІТКА: інший спосіб — застосувати метод filter для вибору лише стовпців, що містять gdp у назві
    # dataframe.filter(like="gdp").mean().plot(ax=ax, label=region)
# Встановлюємо заголовок та підписи
ax.set_title('ВВП на душу населення для регіонів у часі')
ax.set_xticks(range(len(years)))
ax.set_xticklabels(years)
ax.set_xlabel('Рік')
plt.tight_layout()
plt.legend()
plt.show()
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Робота зі шляхами до файлів та каталогів

Модуль [`pathlib`][pathlib-module] надає зручні інструменти для роботи з файлами та шляхами, наприклад отримання назви файлу без його розширення. Застосування цього модуля є особливо доцільним під час перегляду файлів і каталогів у циклах. Цей модуль дозволяє створювати обʼєкти, які відповідають файлам та шляхам, на відміну від звичайних рядків з іменами файлів та каталогів, які ми бачили вище. У прикладі нижче ми створюємо об'єкт типу `Path` і аналізуємо його атрибути.

```python
from pathlib import Path

p = Path("data/gapminder_gdp_africa.csv")
print(p.parent)
print(p.stem)
print(p.suffix)
```

```output
data
gapminder_gdp_africa
.csv
```

**Підказка:** Перегляньте всі доступні атрибути та методи для об'єкта типу `Path` за допомогою функції `dir()`.

::::::::::::::::::::::::::::::::::::::::::::::::::

[shape-method]: https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.shape.html
[float-function]: https://docs.python.org/3/library/functions.html#float
[split-method]: https://docs.python.org/3/library/stdtypes.html#str.split
[pathlib-module]: https://docs.python.org/3/library/pathlib.html

:::::::::::::::::::::::::::::::::::::::: keypoints

- Використовуйте цикл `for` для обробки файлів, імена яких містяться у списку.
- Використовуйте `glob.glob` для пошуку наборів файлів, імена яких відповідають шаблону.
- Використовуйте `glob` і `for` для обробки груп файлів.

::::::::::::::::::::::::::::::::::::::::::::::::::


