---
title: Looping Over Data Sets
teaching: 5
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Be able to read and write globbing expressions that match sets of files.
- Use glob to create lists of files.
- Write for loops to perform operations on files given their names in a list.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I process many data sets with a single command?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Use a `for` loop to process files given a list of their names.

- Ім'я файлу - це рядок символів.
- And lists can contain character strings.

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
- Python's standard library contains the [`glob`](https://docs.python.org/3/library/glob.html) module to provide pattern matching functionality
- The [`glob`](https://docs.python.org/3/library/glob.html) module contains a function also called `glob` to match file patterns
- E.g., `glob.glob('*.txt')` matches all files in the current directory
  whose names end with `.txt`.
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

## Use `glob` and `for` to process batches of files.

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

- This includes all data, as well as per-region data.
- Use a more specific pattern in the exercises to exclude the whole data set.
- But note that the minimum of the entire data set is also the minimum of one of the data sets,
  which is a nice check on correctness.

:::::::::::::::::::::::::::::::::::::::  challenge

## Determining Matches

Який із цих файлів _не_ відповідає виразу `glob.glob('data/*as*.csv')`?

1. `data/gapminder_gdp_africa.csv`
2. `data/gapminder_gdp_americas.csv`
3. `data/gapminder_gdp_asia.csv`

:::::::::::::::  solution

## Відповідь

1 is not matched by the glob.

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

Note that the [`DataFrame.shape()` method][shape-method]
returns a tuple with the number of rows and columns of the data frame.

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
What other special strings does the [`float` function][float-function] recognize?

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Порівняння даних

Напишіть програму, яка читає регіональні набори даних і будує графік середнього ВВП на душу населення для кожного регіону в часі в одній діаграмі. Pandas видасть помилку, якщо зустріне при цьому нечислові стовпці, тому ви маєте або відфільтрувати ці стовпці, або вказати Pandas ігнорувати їх.

:::::::::::::::  solution

## Відповідь

This solution builds a useful legend by using the [string `split` method][split-method] to
extract the `region` from the path 'data/gapminder\\_gdp\\_a\\_specific\\_region.csv'.

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

## Dealing with File Paths

The [`pathlib` module][pathlib-module] provides useful abstractions for file and path manipulation like
returning the name of a file without the file extension. This is very useful when looping over files and
directories. In the example below, we create a `Path` object and inspect its attributes.

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

**Hint:** Check all available attributes and methods on the `Path` object with the `dir()`
function.

::::::::::::::::::::::::::::::::::::::::::::::::::

[shape-method]: https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.shape.html
[float-function]: https://docs.python.org/3/library/functions.html#float
[split-method]: https://docs.python.org/3/library/stdtypes.html#str.split
[pathlib-module]: https://docs.python.org/3/library/pathlib.html

:::::::::::::::::::::::::::::::::::::::: keypoints

- Use a `for` loop to process files given a list of their names.
- Використовуйте `glob.glob` для пошуку наборів файлів, імена яких відповідають шаблону.
- Використовуйте `glob` і `for` для обробки груп файлів.

::::::::::::::::::::::::::::::::::::::::::::::::::


