---
title: Побудова графіків
teaching: 15
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Створення графіку часового ряду, який відповідає одному набору даних.
- Створення діаграми розсіювання, яка показує зв’язок між двома наборами даних.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Як побудувати графік за моїми даними?
- Як зберегти графік для публікації?

::::::::::::::::::::::::::::::::::::::::::::::::::

## [`matplotlib`](https://matplotlib.org/) є найпоширенішою науковою бібліотекою для візуалізації даних в Python.

- Зазвичай використовується його частина - бібліотека [`matplotlib.pyplot`](https://matplotlib.org/stable/tutorials/introductory/pyplot.html).
- За замовчуванням Jupyter Notebook відображає графіки безпосередньо в блокноті.

```python
import matplotlib.pyplot as plt
```

- Створення простих графіків є (відносно) нескладним.

```python
time = [0, 1, 2, 3]
position = [0, 100, 200, 300]

plt.plot(time, position)
plt.xlabel('Time (hr)')
plt.ylabel('Position (km)')
```

![](fig/9_simple_position_time_plot.svg){alt='Лінійний графік, що показує залежність позиції (км) від часу (год), використовуючи дані з наведеного вище коду. За замовчуванням графік має синю лінію на білому фоні, а вісі масштабуються автоматично відповідно до діапазону вхідних даних.'}

:::::::::::::::::::::::::::::::::::::::::  callout

## Display All Open Figures

У прикладі з Jupyter Notebook виконання комірки призводить до побудови графіку безпосередньо під кодом.
Графік також зберігається у блокноті для подальшого перегляду.
Проте, інші середовища Python, такі як інтерактивна сесія Python, що ініціюється з термінала, або Python скрипт, виконаний за допомогою командного рядка, потребують додаткової команди для зображення графіку.

Доручіть `matplotlib` зобразити графік:

```python
plt.show()
```

Цю команду також можна використати в блокноті - наприклад, для зображення декількох графіків одночасно, якщо відповідний командний код міститься в одній комірці.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Побудова графіків безпосередньо з [Pandas dataframes](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html).

- Для побудови графіків можна також використовувати [фрейми даних Pandas](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html).
- Перед побудовою графіку ми перетворюємо назви стовпців із типу `string` на `integer`, оскільки вони представляють числові значення. Для цього використовуємо метод [str.replace()](https://pandas.pydata.org/docs/reference/api/pandas.Series.str.replace. tml), щоб видалити префікс `gpdPercap_`, а потім [astype(int)](https://pandas.pydata.org/docs/reference/api/pandas.Series.astype. tml), щоб перетворити ряд значень рядка (`['1952', '1957', ...'2007']`) у ряд цілих чисел: `[1925, 1957, ..., 2007]`.

```python
import pandas as pd

data = pd.read_csv('data/gapminder_gdp_oceania.csv', index_col='country')

# Extract year from last 4 characters of each column name
# The current column names are structured as 'gdpPercap_(year)', 
# so we want to keep the (year) part only for clarity when plotting GDP vs. years
# To do this we use replace(), which removes from the string the characters stated in the argument
# This method works on strings, so we use replace() from Pandas Series.str vectorized string functions

years = data.columns.str.replace('gdpPercap_', '')

# Convert year values to integers, saving results back to dataframe

data.columns = years.astype(int)

data.loc['Australia'].plot()
```

![](fig/9_gdp_australia.svg){alt='Графік, що показує дані ВВП Австралії'}

## Виділіть та трансформуйте дані, а потім побудуйте графік.

- За замовчуванням, [`DataFrame.plot`](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.plot.html#pandas.DataFrame.plot) зображує рядки на осі X.
- Ми можемо транспонувати дані, щоб побудувати кілька графіків разом.

```python
data.T.plot()
plt.ylabel('GDP per capita')
```

![](fig/9_gdp_australia_nz.svg){alt='Графік ВВП для Австралії та Нової Зеландії'}

## Доступні багато стилів графіків.

- For example, do a bar plot using a fancier style.

```python
plt.style.use('ggplot')
data.T.plot(kind='bar')
plt.ylabel('GDP per capita')
```

![](fig/9_gdp_bar.svg){alt='Стовпчикова діаграма ВВП для Австралії'}

## Графік також можна побудувати, викликавши безпосередньо функцію `plot` бібліотеки `matplotlib`.

- Формат команди є таким: `plt.plot(x, y)`
- Колір та формат маркерів також можна вказати як додатковий необов'язковий аргумент, тобто, `b-` - це синя лінія, `g--` - це зелена пунктирна лінія.

## Get Australia data from dataframe

```python
years = data.columns
gdp_australia = data.loc['Australia']

plt.plot(years, gdp_australia, 'g--')
```

![](fig/9_gdp_australia_formatted.svg){alt='Форматований графік ВВП для Австралії'}

## Можна побудувати кілька графіків за різними наборами даних одночасно.

```python
# Select two countries' worth of data.
gdp_australia = data.loc['Australia']
gdp_nz = data.loc['New Zealand']

# Plot with differently-colored markers.
plt.plot(years, gdp_australia, 'b-', label='Australia')
plt.plot(years, gdp_nz, 'g-', label='New Zealand')

# Create legend.
plt.legend(loc='upper left')
plt.xlabel('Year')
plt.ylabel('GDP per capita ($)')
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Додавання легенди

Often when plotting multiple datasets on the same figure it is desirable to have
a legend describing the data.

Це можна зробити в `matplotlib` за два етапи:

- Вкажіть мітку для кожного набору даних у графіку:

```python
plt.plot(years, gdp_australia, label='Australia')
plt.plot(years, gdp_nz, label='New Zealand')
```

- Доручіть `matplotlib` створити легенду.

```python
plt.legend()
```

За замовчуванням matplotlib спробує розмістити легенду у відповідному місці. Якщо необхідно вказати конкретне розташування, можна застосувати аргументи функції `loc=`, наприклад, щоб розмістити легенду в лівому верхньому куті графіку, задайте `loc='upper left'`

::::::::::::::::::::::::::::::::::::::::::::::::::

![](fig/9_gdp_australia_nz_formatted.svg){alt='Форматований графік ВВП для Австралії та Нової Зеландії'}

- Plot a scatter plot correlating the GDP of Australia and New Zealand
- Use either `plt.scatter` or `DataFrame.plot.scatter`

```python
plt.scatter(gdp_australia, gdp_nz)
```

![](fig/9_gdp_correlation_plt.svg){alt='GDP correlation using plt.scatter'}

```python
data.T.plot.scatter(x = 'Australia', y = 'New Zealand')
```

![](fig/9_gdp_correlation_data.svg){alt='GDP correlation using data.T.plot.scatter'}

:::::::::::::::::::::::::::::::::::::::  challenge

## Мінімум та максимум

Заповніть порожні поля нижче, щоб побудувати графік мінімального ВВП на душу населення протягом часу для всіх країн Європи.
Потім побудуйте графік максимального ВВП на душу населення в Європі.

```python
data_europe = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
data_europe.____.plot(label='min')
data_europe.____
plt.legend(loc='best')
plt.xticks(rotation=90)
```

:::::::::::::::  solution

## Рішення

```python
data_europe = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
data_europe.min().plot(label='min')
data_europe.max().plot(label='max')
plt.legend(loc='best')
plt.xticks(rotation=90)
```

![](fig/9_minima_maxima_solution.png){alt='Minima Maxima Solution'}

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Співвідношення

Модифікуйте приклад у примітках, щоб створити діаграму розсіювання, що показує співвідношення між мінімальним і максимальним ВВП на душу населення серед країн Азії за кожен рік у наборі даних.
Який зв’язок ви бачите (якщо такий є)?

:::::::::::::::  solution

## Рішення

```python
data_asia = pd.read_csv('data/gapminder_gdp_asia.csv', index_col='country')
data_asia.describe().T.plot(kind='scatter', x='min', y='max')
```

![](fig/9_correlations_solution1.svg){alt='Співвідношення Рішення 1'}

No particular correlations can be seen between the minimum and maximum GDP values
year on year. Здається, статки азійських країн не зростають і не падають разом.

:::::::::::::::::::::::::

You might note that the variability in the maximum is much higher than
that of the minimum.  Зверніть увагу на максимальні значення та відповідні індекси:

```python
data_asia = pd.read_csv('data/gapminder_gdp_asia.csv', index_col='country')
data_asia.max().plot()
print(data_asia.idxmax())
print(data_asia.idxmin())
```

:::::::::::::::  solution

## Рішення

![](fig/9_correlations_solution2.png){alt='Співвідношення Рішення 2'}

Seems the variability in this value is due to a sharp drop after 1972.
Some geopolitics at play perhaps? Given the dominance of oil producing countries,
maybe the Brent crude index would make an interesting comparison?
У той час як М’янма постійно має найнижчий ВВП, країна з найвищим ВВП змінюється більш помітно.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Більше кореляцій

This short program creates a plot showing
the correlation between GDP and life expectancy for 2007,
normalizing marker size by population:

```python
data_all = pd.read_csv('data/gapminder_all.csv', index_col='country')
data_all.plot(kind='scatter', x='gdpPercap_2007', y='lifeExp_2007',
              s=data_all['pop_2007']/1e6)
```

Використовуючи онлайн-довідку та інші ресурси, поясніть роль кожного аргументу, який передається у функцію plot.

:::::::::::::::  solution

## Рішення

![](fig/9_more_correlations_solution.svg){alt='More Correlations Solution'}

Гарне місце для пошуку документації до функції графіків -
help(data\_all.plot).

kind - Як вже було показано, цей параметр визначає тип графіку, який буде створено.

x and y - A column name or index that determines what data will be
placed on the x and y axes of the plot

s - Інформацію про цей аргумент можна знайти в документації plt.scatter.
Це одне число або одне значення для кожної точки даних. Визначає розмір маркера.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Збереження вашого графіка в файл

Якщо вас влаштовує побудований графік, можливо, ви захочете зберегти його у файл — наприклад, для включення у публікацію. У модулі matplotlib.pyplot є функція, яка виконує це:
[savefig](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.savefig.html).
Виклик цієї функції

```python
plt.savefig('my_figure.png')
```

збереже поточний графік у файл `my_figure.png`. Формат файлу буде автоматично визначено з розширення імені файлу (інші формати: pdf, ps, eps і svg).

Зауважимо, що функції в `plt` посилаються на глобальну змінну графіка і після того, як графік виведено на екран (наприклад, за допомогою `plt.show`) matplotlib змусить цю змінну посилатися на новий порожній графік.
Тому переконайтеся, що ви викликаєте `plt.savefig` перед тим, як графік буде зображено на екрані, інакше ви можете створити файл із порожнім графіком.

При використанні фреймів даних дані часто генеруються та виводяться на екрані однією лінією.
На додаток до `plt.savefig`, ми можемо зберегти посилання на поточний графік у локальну змінну (використовуючи `plt.gcf`), а потім викликати `savefig` метод цієї змінної для збереження графіка у файл.

```python
data.plot(kind='bar')
fig = plt.gcf() # get current figure
fig.savefig('my_figure.png')
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Зробіть ваш графік доступним

Щоразу, коли ви створюєте графіки для статті чи презентації, варто врахувати кілька речей, щоб переконатися, що всі зрозуміють ваші графіки.

- Завжди перевіряйте, що ваш текст достатньо великий для читання. Використовуйте параметр `fontsize` в `xlabel`, `ylabel`, `title`, та `legend`, а також [`tick_params` з `labelsize`](https://matplotlib.org/2.1.1/api/_as_gen/matplotlib.pyplot.tick_params.html) щоб збільшити розмір чисел на ваших осях.
- Також слід подбати, щоб елементи графіка були добре помітними. Використовуйте `s`, щоб збільшити розмір маркерів діаграми розсіювання, і `linewidth`, щоб збільшити розміри ліній вашого графіка.
- Якщо розрізняти елементи графіка тільки за кольором, це може ускладнити його сприйняття для людей із дальтонізмом або тих, хто переглядає матеріали в чорно-білому вигляді (наприклад, після друку). Для ліній можна використовувати параметр `linestyle`, щоб задати різні стилі ліній. Для діаграм розсіювання `marker` дозволяє змінювати форму ваших точок. Якщо ви не впевнені у вибраній кольоровій палітрі, скористайтеся інструментами на кшталт [Coblis](https://www.color-blindness.com/coblis-color-blindness-simulator/) або [Color Oracle](https://colororacle.org/) щоб імітувати, як виглядатимуть ваші графіки для людей з дальтонізмом.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- [`matplotlib`](https://matplotlib.org/) — це найпоширеніша наукова бібліотека для побудови графіків у Python.
- Побудова графіків можлива безпосередньо з використанням фреймів даних Pandas.
- Побудова графіків включає виділення та трансформацію даних.
- Many styles of plot are available: see the [Python Graph Gallery](https://python-graph-gallery.com/matplotlib/) for more options.
- Can plot many sets of data together.

::::::::::::::::::::::::::::::::::::::::::::::::::


