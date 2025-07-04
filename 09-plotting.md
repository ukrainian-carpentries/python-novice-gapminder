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

## [`matplotlib`](https://matplotlib.org/) is the most widely used scientific plotting library in Python.

- Commonly use a sub-library called [`matplotlib.pyplot`](https://matplotlib.org/stable/tutorials/introductory/pyplot.html).
- The Jupyter Notebook will render plots inline by default.

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

![](fig/9_simple_position_time_plot.svg){alt='A line chart showing time (hr) relative to position (km), using the values provided in the code block above. By default, the plotted line is blue against a white background, and the axes have been scaled automatically to fit the range of the input data.'}

:::::::::::::::::::::::::::::::::::::::::  callout

## Display All Open Figures

In our Jupyter Notebook example, running the cell should generate the figure directly below the code.
The figure is also included in the Notebook document for future viewing.
However, other Python environments like an interactive Python session started from a terminal
or a Python script executed via the command line require an additional command to display the figure.

Instruct `matplotlib` to show a figure:

```python
plt.show()
```

This command can also be used within a Notebook - for instance, to display multiple figures
if several are created by a single cell.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Побудова графіків безпосередньо з [Pandas dataframes](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html).

- Для побудови графіків можна також використовувати [фрейми даних Pandas](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html).
- Before plotting, we convert the column headings from a `string` to `integer` data type, since they represent numerical values,
  using [str.replace()](https://pandas.pydata.org/docs/reference/api/pandas.Series.str.replace.html) to remove the `gpdPercap_`
  prefix and then [astype(int)](https://pandas.pydata.org/docs/reference/api/pandas.Series.astype.html)
  to convert the series of string values (`['1952', '1957', ..., '2007']`) to a series of integers: `[1925, 1957, ..., 2007]`.

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

![](fig/9_gdp_australia.svg){alt='GDP plot for Australia'}

## Виділіть та трансформуйте дані, а потім побудуйте графік.

- By default, [`DataFrame.plot`](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.plot.html#pandas.DataFrame.plot) plots with the rows as the X axis.
- Ми можемо транспонувати дані, щоб побудувати кілька графіків разом.

```python
data.T.plot()
plt.ylabel('GDP per capita')
```

![](fig/9_gdp_australia_nz.svg){alt='GDP plot for Australia and New Zealand'}

## Доступні багато стилів графіків.

- For example, do a bar plot using a fancier style.

```python
plt.style.use('ggplot')
data.T.plot(kind='bar')
plt.ylabel('GDP per capita')
```

![](fig/9_gdp_bar.svg){alt='GDP barplot for Australia'}

## Data can also be plotted by calling the `matplotlib` `plot` function directly.

- Формат команди є таким: `plt.plot(x, y)`
- The color and format of markers can also be specified as an additional optional argument e.g., `b-` is a blue line, `g--` is a green dashed line.

## Get Australia data from dataframe

```python
years = data.columns
gdp_australia = data.loc['Australia']

plt.plot(years, gdp_australia, 'g--')
```

![](fig/9_gdp_australia_formatted.svg){alt='GDP formatted plot for Australia'}

## Can plot many sets of data together.

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

За замовчуванням matplotlib спробує розмістити легенду у відповідному місці. If you
would rather specify a position this can be done with the `loc=` argument, e.g to place
the legend in the upper left corner of the plot, specify `loc='upper left'`

::::::::::::::::::::::::::::::::::::::::::::::::::

![](fig/9_gdp_australia_nz_formatted.svg){alt='GDP formatted plot for Australia and New Zealand'}

- Побудуйте точкову діаграму співвідношення ВВП Австралії та Нової Зеландії
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

Fill in the blanks below to plot the minimum GDP per capita over time
for all the countries in Europe.
Modify it again to plot the maximum GDP per capita over time for Europe.

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

![](fig/9_correlations_solution1.svg){alt='Correlations Solution 1'}

No particular correlations can be seen between the minimum and maximum GDP values
year on year. Здається, статки азійських країн не зростають і не падають разом.

:::::::::::::::::::::::::

You might note that the variability in the maximum is much higher than
that of the minimum.  Take a look at the maximum and the max indexes:

```python
data_asia = pd.read_csv('data/gapminder_gdp_asia.csv', index_col='country')
data_asia.max().plot()
print(data_asia.idxmax())
print(data_asia.idxmin())
```

:::::::::::::::  solution

## Рішення

![](fig/9_correlations_solution2.png){alt='Correlations Solution 2'}

Seems the variability in this value is due to a sharp drop after 1972.
Some geopolitics at play perhaps? Given the dominance of oil producing countries,
maybe the Brent crude index would make an interesting comparison?
У той час як М’янма постійно має найнижчий ВВП, країна з найвищим ВВП змінюється більш помітно.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## More Correlations

This short program creates a plot showing
the correlation between GDP and life expectancy for 2007,
normalizing marker size by population:

```python
data_all = pd.read_csv('data/gapminder_all.csv', index_col='country')
data_all.plot(kind='scatter', x='gdpPercap_2007', y='lifeExp_2007',
              s=data_all['pop_2007']/1e6)
```

Using online help and other resources,
explain what each argument to `plot` does.

:::::::::::::::  solution

## Рішення

![](fig/9_more_correlations_solution.svg){alt='More Correlations Solution'}

Гарне місце для пошуку документації до функції графіків -
help(data\_all.plot).

kind - As seen already this determines the kind of plot to be drawn.

x and y - A column name or index that determines what data will be
placed on the x and y axes of the plot

s - Details for this can be found in the documentation of plt.scatter.
A single number or one value for each data point. Визначає розмір маркера.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Збереження вашого графіка в файл

If you are satisfied with the plot you see you may want to save it to a file,
perhaps to include it in a publication. У модулі matplotlib.pyplot є функція, яка виконує це:
[savefig](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.savefig.html).
Виклик цієї функції

```python
plt.savefig('my_figure.png')
```

збереже поточний графік у файл `my_figure.png`. Формат файлу буде автоматично визначено з розширення імені файлу (інші формати: pdf, ps, eps і svg).

Note that functions in `plt` refer to a global figure variable
and after a figure has been displayed to the screen (e.g. with `plt.show`)
matplotlib will make this  variable refer to a new empty figure.
Therefore, make sure you call `plt.savefig` before the plot is displayed to
the screen, otherwise you may find a file with an empty plot.

When using dataframes, data is often generated and plotted to screen in one line.
In addition to using `plt.savefig`, we can save a reference to the current figure
in a local variable (with `plt.gcf`) and call the `savefig` class method from
that variable to save the figure to file.

```python
data.plot(kind='bar')
fig = plt.gcf() # get current figure
fig.savefig('my_figure.png')
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Зробіть ваш графік доступним

Whenever you are generating plots to go into a paper or a presentation, there are a few things you can do to make sure that everyone can understand your plots.

- Завжди перевіряйте, що ваш текст достатньо великий для читання. Use the `fontsize` parameter in `xlabel`, `ylabel`, `title`, and `legend`, and [`tick_params` with `labelsize`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.tick_params.html) to increase the text size of the numbers on your axes.
- Similarly, you should make your graph elements easy to see. Use `s` to increase the size of your scatterplot markers and `linewidth` to increase the sizes of your plot lines.
- Using color (and nothing else) to distinguish between different plot elements will make your plots unreadable to anyone who is colorblind, or who happens to have a black-and-white office printer. For lines, the `linestyle` parameter lets you use different types of lines. Для діаграм розсіювання `marker` дозволяє змінювати форму ваших точок. If you're unsure about your colors, you can use [Coblis](https://www.color-blindness.com/coblis-color-blindness-simulator/) or [Color Oracle](https://colororacle.org/) to simulate what your plots would look like to those with colorblindness.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- [`matplotlib`](https://matplotlib.org/) — це найпоширеніша наукова бібліотека для побудови графіків у Python.
- Побудова графіків можлива безпосередньо з використанням фреймів даних Pandas.
- Побудова графіків включає виділення та трансформацію даних.
- Many styles of plot are available: see the [Python Graph Gallery](https://python-graph-gallery.com/matplotlib/) for more options.
- Can plot many sets of data together.

::::::::::::::::::::::::::::::::::::::::::::::::::


