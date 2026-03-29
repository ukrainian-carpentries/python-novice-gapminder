---
title: Датафрейми Pandas
teaching: 15
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Вибір окремих значень з датафрейму Pandas.
- Виділення цілих рядків або цілих стовпців з датафрейму.
- Вибір підмножини рядків і стовпців з датафрейму за одну операцію.
- Вибір підмножини з датафрейму за єдиним булевим критерієм.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Як я можу виконати статистичний аналіз табличних даних?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Датафрейми та серії у Pandas

Датафрейм ([DataFrame][pandas-dataframe]) містить декілька серій ([Series][pandas-series]); Датафрейм — це спосіб представлення таблиці в Pandas, а серія — це структура даних, яку Pandas використовує для представлення окремого стовпця.

Pandas побудована на основі бібліотеки [Numpy][numpy], що означає, що більшість методів для масивів Numpy також застосовується до датафреймів та серій у Pandas.

Що робить Pandas таким привабливим? Це потужний інтерфейс для доступу до окремих записів таблиці, належної обробки відсутніх значень та підтримки операцій з датафреймами, подібних до тих, що застосовуються в реляційних базах даних.

## Вибір значень

Існує два способи доступу до значення в позиції `[i,j]` у датафреймі, залежно від того, як інтерпретується `i`.
Пам’ятайте, що датафрейм використовує _індекс_ для ідентифікації рядків таблиці; отже, кожен рядок має _позицію_ в таблиці, а також _заголовок рядка_ (_мітку_), яка однозначно визначає цей рядок у датафреймі.

## Використовуйте `DataFrame.iloc[..., ...]` для вибору значень за їх позицією

- Можна вказати позицію значення за допомогою числового індексу аналогічно 2D-версії вибору символів у рядках.

```python
import pandas as pd
data = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
print(data.iloc[0, 0])
```

```output
1601.056136
```

## Використовуйте `DataFrame.loc[..., ...]` для доступу до значень за їхніми мітками.

- Можна вказати розташування, використовуючи заголовок рядку та/або стовпця.

```python
print(data.loc["Albania", "gdpPercap_1952"])
```

```output
1601.056136
```

## Використовуйте лише `:` замість мітки для позначення всіх стовпців або всіх рядків.

- Це відповідає звичайному синтаксису зрізів у Python.

```python
print(data.loc["Albania", :])
```

```output
gdpPercap_1952    1601.056136
gdpPercap_1957    1942.284244
gdpPercap_1962    2312.888958
gdpPercap_1967    2760.196931
gdpPercap_1972    3313.422188
gdpPercap_1977    3533.003910
gdpPercap_1982    3630.880722
gdpPercap_1987    3738.932735
gdpPercap_1992    2497.437901
gdpPercap_1997    3193.054604
gdpPercap_2002    4604.211737
gdpPercap_2007    5937.029526
Name: Albania, dtype: float64
```

- Той самий результат можна отримати, використовуючи `data.loc["Albania"]` (без вказання другого індексу).

```python
print(data.loc[:, "gdpPercap_1952"])
```

```output
country
Albania                    1601.056136
Austria                    6137.076492
Belgium                    8343.105127
⋮ ⋮ ⋮
Switzerland               14734.232750
Turkey                     1969.100980
United Kingdom             9979.508487
Name: gdpPercap_1952, dtype: float64
```

- Той самий результат можна отримати, якщо надрукувати `data["gdpPercap_1952"]`
- Більш того, той самий результат можна отримати, застосовуючи нотацію `data.gdpPercap_1952` (але не рекомендується, оскільки її легко сплутати з позначенням `.` для використання методів)

## Вибирайте кілька стовпців або рядків за допомогою `DataFrame.loc` та визначеного зрізу.

```python
print(data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'])
```

```output
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy           8243.582340    10022.401310    12269.273780
Montenegro      4649.593785     5907.850937     7778.414017
Netherlands    12790.849560    15363.251360    18794.745670
Norway         13450.401510    16361.876470    18965.055510
Poland          5338.752143     6557.152776     8006.506993
```

У наведеному вище коді ми бачимо, що **зріз із використанням `loc` включає дані на обох вказаних кінцях**, на відміну від **зрізу із застосуванням `iloc`**, де зріз не включає кінцевий індекс.

## Результат зрізу можна використовувати в подальших операціях.

- Зазвичай зрізи формуються не тільки для друку.
- Усі статистичні оператори, які працюють зі цілими фреймами даних, так само працюють зі зрізами.
- Наприклад, обчислення максимальних значень у зрізі.

```python
print(data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'].max())
```

```output
gdpPercap_1962    13450.40151
gdpPercap_1967    16361.87647
gdpPercap_1972    18965.05551
dtype: float64
```

```python
print(data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'].min())
```

```output
gdpPercap_1962    4649.593785
gdpPercap_1967    5907.850937
gdpPercap_1972    7778.414017
dtype: float64
```

## Використовуйте операції порівняння для вибору даних на основі певного значення.

- Порівняння здійснюється поелементно.
- Повертає датафрейм подібної форми, що містить значення `True` та `False`.

```python
# Використовуємо частину даних, щоб результат був читабельним
subset = data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972']
print('Subset of data:\n', subset)

# Які значення перевищують 10000 ?
print('\nWhere are values large?\n', subset > 10000)
```

```output
Subset of data:
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy           8243.582340    10022.401310    12269.273780
Montenegro      4649.593785     5907.850937     7778.414017
Netherlands    12790.849560    15363.251360    18794.745670
Norway         13450.401510    16361.876470    18965.055510
Poland          5338.752143     6557.152776     8006.506993

Where are values large?
            gdpPercap_1962 gdpPercap_1967 gdpPercap_1972
country
Italy                False           True           True
Montenegro           False          False          False
Netherlands           True           True           True
Norway                True           True           True
Poland               False          False          False
```

## Вибір значень або NaN за допомогою булевої маски.

- Датафрейм, що містить лише булеві значення, іноді називають маскою через спосіб його використання.

```python
mask = subset > 10000
print(subset[mask])
```

```output
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy                   NaN     10022.40131     12269.27378
Montenegro              NaN             NaN             NaN
Netherlands     12790.84956     15363.25136     18794.74567
Norway          13450.40151     16361.87647     18965.05551
Poland                  NaN             NaN             NaN
```

- Результат містить оригінальні значення, коли умова виконується, та NaN (Not a Number - не число) у решті випадків.
- Це зручно, оскільки операції на кшталт max, min, average автоматично ігнорують значення NaN.

```python
print(subset[subset > 10000].describe())
```

```output
       gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
count        2.000000        3.000000        3.000000
mean     13120.625535    13915.843047    16676.358320
std        466.373656     3408.589070     3817.597015
min      12790.849560    10022.401310    12269.273780
25%      12955.737547    12692.826335    15532.009725
50%      13120.625535    15363.251360    18794.745670
75%      13285.513523    15862.563915    18879.900590
max      13450.401510    16361.876470    18965.055510
```

## Group By: групує, застосовує та комбінує

::::::::::::::::::::::::::::::::::::: instructor
Learners often struggle here, many may not work with financial data and concepts so they
find the example concepts difficult to get their head around. Однак основна проблема полягає в рядку, який обчислює `wealth_score`; цей крок потребує ретельного обговорення:

- Він використовує неявне перетворення між булевим і дійсним значенням, яке ще не розглядалося в курсі.
- Параметр axis=1 також потребує чіткого пояснення.
  :::::::::::::::::::::::::::::::::::::::::::::::::

Методи векторизації та операції групування Pandas — це функції, які надають користувачам велику гнучкість для аналізу своїх даних.

Наприклад, скажімо, ми хочемо мати більш чітке уявлення про те, як європейські країни розподілені відповідно до свого ВВП.

1. Ми можемо поглянути на ситуацію, поділивши країни на дві групи за роки спостережень: ті, у яких ВВП _вище_ середнього по Європі, і країни з _нижчим_ ВВП.
2. Далі ми оцінюємо показник заможності на основі історичних значень (з 1962 по 2007 рік), підраховуючи, скільки разів кожна країна входила до груп із вищим або нижчим ВВП

```python
mask_higher = data > data.mean()
wealth_score = mask_higher.aggregate('sum', axis=1) / len(data.columns)
print(wealth_score)
```

```output
country
Albania                   0.000000
Austria                   1.000000
Belgium                   1.000000
Bosnia and Herzegovina    0.000000
Bulgaria                  0.000000
Croatia                   0.000000
Czech Republic            0.500000
Denmark                   1.000000
Finland                   1.000000
France                    1.000000
Germany                   1.000000
Greece                    0.333333
Hungary                   0.000000
Iceland                   1.000000
Ireland                   0.333333
Italy                     0.500000
Montenegro                0.000000
Netherlands               1.000000
Norway                    1.000000
Poland                    0.000000
Portugal                  0.000000
Romania                   0.000000
Serbia                    0.000000
Slovak Republic           0.000000
Slovenia                  0.333333
Spain                     0.333333
Sweden                    1.000000
Switzerland               1.000000
Turkey                    0.000000
United Kingdom            1.000000
dtype: float64
```

Нарешті, для кожної групи в таблиці `wealth_score` ми підсумовуємо їх (фінансовий) внесок за роки дослідження, використовуючи ланцюжок методів:

```python
print(data.groupby(wealth_score).sum())
```

```output
          gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  gdpPercap_1967  \
0.000000    36916.854200    46110.918793    56850.065437    71324.848786   
0.333333    16790.046878    20942.456800    25744.935321    33567.667670   
0.500000    11807.544405    14505.000150    18380.449470    21421.846200   
1.000000   104317.277560   127332.008735   149989.154201   178000.350040   

          gdpPercap_1972  gdpPercap_1977  gdpPercap_1982  gdpPercap_1987  \
0.000000    88569.346898   104459.358438   113553.768507   119649.599409   
0.333333    45277.839976    53860.456750    59679.634020    64436.912960   
0.500000    25377.727380    29056.145370    31914.712050    35517.678220   
1.000000   215162.343140   241143.412730   263388.781960   296825.131210   

          gdpPercap_1992  gdpPercap_1997  gdpPercap_2002  gdpPercap_2007  
0.000000    92380.047256   103772.937598   118590.929863   149577.357928  
0.333333    67918.093220    80876.051580   102086.795210   122803.729520  
0.500000    36310.666080    40723.538700    45564.308390    51403.028210  
1.000000   315238.235970   346930.926170   385109.939210   427850.333420
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Вибір індивідуальних значень

Припустімо, що Pandas було імпортовано та дані Gapminder про ВВП для Європи завантажено.

```python
import pandas as pd

data_europe = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
```

Напишіть вираз для визначення ВВП Сербії на душу населення у 2007 році.

:::::::::::::::  solution

## Відповідь

Вибір можна зробити за допомогою мітки "Сербія" для рядка, та мітки "gdpPercap\_2007" для стовпця:

```python
print(data_europe.loc['Serbia', 'gdpPercap_2007'])
```

Результат є таким

```output
9786.534714
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Межі зрізу

1. Чи дають два наведені нижче твердження однаковий результат?
2. На основі цього, яке правило визначає, що включено (чи ні) до числових та іменованих зрізів у Pandas?

```python
print(data_europe.iloc[0:2, 0:2])
print(data_europe.loc['Albania':'Belgium', 'gdpPercap_1952':'gdpPercap_1962'])
```

:::::::::::::::  solution

## Відповідь

Ні, вони не дають однакові результати! Результатом першого виразу є:

```output
        gdpPercap_1952  gdpPercap_1957
country                                
Albania     1601.056136     1942.284244
Austria     6137.076492     8842.598030
```

Другий вираз дає:

```output
        gdpPercap_1952  gdpPercap_1957  gdpPercap_1962
country                                                
Albania     1601.056136     1942.284244     2312.888958
Austria     6137.076492     8842.598030    10750.721110
Belgium     8343.105127     9714.960623    10991.206760
```

Вочевидь, другий вираз повертає додатковий стовпець і додатковий рядок у порівнянні з першим.  
Який висновок ми можемо зробити? Ми бачимо, що числовий зріз 0:2 _не включає_ кінцевий індекс (тобто, індекс 2), тоді як іменований зріз 'gdpPercap\_1952':'gdpPercap\_1962' _включає_ кінцевий елемент.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Реконструювання даних

Опишіть, що робить кожен рядок наведеної короткої програми та які значення зберігаються в змінних `first`, `second` тощо?

```python
first = pd.read_csv('data/gapminder_all.csv', index_col='country')
second = first[first['continent'] == 'Americas']
third = second.drop('Puerto Rico')
fourth = third.drop('continent', axis = 1)
fourth.to_csv('result.csv')
```

:::::::::::::::  solution

## Відповідь

Перегляньмо цей фрагмент коду рядок за рядком.

```python
first = pd.read_csv('data/gapminder_all.csv', index_col='country')
```

В цьому рядку дані про ВВП з усіх країн завантажуються у датафрейм `first`. Параметр `index_col='country'` вказує, який стовпець використовується як заголовки рядків у датафреймі.

```python
second = first[first['continent'] == 'Americas']
```

Цей рядок фільтрує дані: вибираються лише ті рядки з `first`, у яких стовпець 'continent' містить значення 'Americas'. Зверніть увагу, як логічний вираз у дужках, `first['continent'] == 'Americas'`, використовується для вибору лише тих рядків, де вираз є істинним.
Спробуйте надрукувати цей вираз! Чи можете ви також надрукувати його окремі елементи True/False?
(підказка: спочатку призначте вираз певній змінній)

```python
third = second.drop('Puerto Rico')
```

Як підказує синтаксис, цей код видаляє рядок з міткою 'Puerto Rico' з датафрейму `second`. У результаті датафрейм `third` містить на один рядок менше, ніж вихідний датафрейм `second`.

```python
fourth = third.drop('continent', axis = 1)
```

Знову ми застосовуємо функцію `drop`, але в цьому випадку ми видаляємо не рядок, а цілий стовпець.
Для цього нам також потрібно вказати параметр `axis` (ми хочемо видалити другий стовпець, який має індекс 1).

```python
fourth.to_csv('result.csv')
```

Останнім кроком є ​​збереження даних, над якими ми працювали, у файл csv. Pandas спрощує це завдання за допомогою функції `to_csv()`. Єдиним обов’язковим аргументом для функції є ім’я файлу. Зверніть увагу, що файл буде записано в каталозі, з якого ви розпочали сесію Jupyter або Python.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Вибір індексів

Поясніть простими словами, що роблять `idxmin` і `idxmax` у короткій програмі нижче.
У яких випадках ви б використовували ці методи?

```python
data = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
print(data.idxmin())
print(data.idxmax())
```

:::::::::::::::  solution

## Відповідь

Для кожного стовпця в `data`, `idxmin` поверне значення індексу, що відповідає мінімуму кожного стовпця; `idxmax` зробить те саме для максимального значення кожного стовпця.

Ви можете використовувати ці функції щоразу, коли потрібно отримати індекс рядка з мінімальним або максимальним значенням, а не саме значення.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Потренуйтеся з вибором

Припустімо, що Pandas було імпортовано та дані Gapminder про ВВП для Європи завантажено.
Напишіть вираз, щоб вибрати кожне з наступного:

1. ВВП на душу населення для всіх країн у 1982 році.
2. ВВП на душу населення для Данії за всі роки.
3. ВВП на душу населення для всіх країн за роки _після_ 1985 року.
4. ВВП на душу населення у 2007 році для кожної країни, виражене як кратне до ВВП на душу населення цієї ж країни у 1952 році.

:::::::::::::::  solution

## Відповідь

1:

```python
data['gdpPercap_1982']
```

2:

```python
data.loc['Denmark',:]
```

3:

```python
data.loc[:,'gdpPercap_1985':]
```

Пакет pandas досить розумний, щоб розпізнати число в кінці заголовку стовпця й не видати помилки, навіть якщо стовпця з назвою `gdpPercap_1985` не існує. Це зручно, якщо нові стовпці додаються до файлу CSV пізніше.

4:

```python
data['gdpPercap_2007']/data['gdpPercap_1952']
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Багато способів доступу

Отримати значення або зріз з датафрейму можна щонайменше двома способами: за назвою або за індексом.
Однак існує багато інших варіантів. Наприклад, можна отримати окремий стовпець або рядок як `DataFrame`
або `Series` об'єкт.

Запропонуйте різні способи виконання наступних операцій з датафреймами:

1. Доступ до одного стовпця
2. Доступ до одного рядку
3. Доступ до окремого елемента датафрейму
4. Доступ до декількох стовпців
5. Доступ до декількох рядків
6. Доступ до підмножини, заданої визначеними рядками та стовпцями
7. Доступ до підмножини, заданої діапазонами рядків та стовпців

:::::::::::::::  solution

## Відповідь

1\. Доступ до одного стовпця:

```python
# by name
data["col_name"]   # as a Series
data[["col_name"]] # as a DataFrame

# by name using .loc
data.T.loc["col_name"]  # as a Series
data.T.loc[["col_name"]].T  # as a DataFrame

# Dot notation (Series)
data.col_name

# by index (iloc)
data.iloc[:, col_index]   # as a Series
data.iloc[:, [col_index]] # as a DataFrame

# using a mask
data.T[data.T.index == "col_name"].T
```

2\. Доступ до одного рядку:

```python
# by name using .loc
data.loc["row_name"] # as a Series
data.loc[["row_name"]] # as a DataFrame

# by name
data.T["row_name"] # as a Series
data.T[["row_name"]].T # as a DataFrame

# by index
data.iloc[row_index]   # as a Series
data.iloc[[row_index]]   # as a DataFrame

# using mask
data[data.index == "row_name"]
```

3\. Доступ до окремого елемента датафрейму:

```python
# by column/row names
data["column_name"]["row_name"]         # as a Series

data[["col_name"]].loc["row_name"]  # as a Series
data[["col_name"]].loc[["row_name"]]  # as a DataFrame

data.loc["row_name"]["col_name"]  # as a value
data.loc[["row_name"]]["col_name"]  # as a Series
data.loc[["row_name"]][["col_name"]]  # as a DataFrame

data.loc["row_name", "col_name"]  # as a value
data.loc[["row_name"], "col_name"]  # as a Series. Preserves index. Column name is moved to `.name`.
data.loc["row_name", ["col_name"]]  # as a Series. Index is moved to `.name.` Sets index to column name.
data.loc[["row_name"], ["col_name"]]  # as a DataFrame (preserves original index and column name)

# by column/row names: Dot notation
data.col_name.row_name

# by column/row indices
data.iloc[row_index, col_index] # as a value
data.iloc[[row_index], col_index] # as a Series. Preserves index. Column name is moved to `.name`
data.iloc[row_index, [col_index]] # as a Series. Index is moved to `.name.` Sets index to column name.
data.iloc[[row_index], [col_index]] # as a DataFrame (preserves original index and column name)

# column name + row index
data["col_name"][row_index]
data.col_name[row_index]
data["col_name"].iloc[row_index]

# column index + row name
data.iloc[:, [col_index]].loc["row_name"]  # as a Series
data.iloc[:, [col_index]].loc[["row_name"]]  # as a DataFrame

# using masks
data[data.index == "row_name"].T[data.T.index == "col_name"].T
```

4\. Доступ до декількох стовпців:

```python
# by name
data[["col1", "col2", "col3"]]
data.loc[:, ["col1", "col2", "col3"]]

# by index
data.iloc[:, [col1_index, col2_index, col3_index]]
```

5\. Доступ до декількох рядків

```python
# by name
data.loc[["row1", "row2", "row3"]]

# by index
data.iloc[[row1_index, row2_index, row3_index]]
```

6\. Доступ до підмножини, заданої визначеними рядками та стовпцями

```python
# by names
data.loc[["row1", "row2", "row3"], ["col1", "col2", "col3"]]

# by indices
data.iloc[[row1_index, row2_index, row3_index], [col1_index, col2_index, col3_index]]

# column names + row indices
data[["col1", "col2", "col3"]].iloc[[row1_index, row2_index, row3_index]]

# column indices + row names
data.iloc[:, [col1_index, col2_index, col3_index]].loc[["row1", "row2", "row3"]]
```

7\. Доступ до підмножини, заданої діапазонами рядків та стовпців

```python
# by name
data.loc["row1":"row2", "col1":"col2"]

# by index
data.iloc[row1_index:row2_index, col1_index:col2_index]

# column names + row indices
data.loc[:, "col1_name":"col2_name"].iloc[row1_index:row2_index]

# column indices + row names
data.iloc[:, col1_index:col2_index].loc["row1":"row2"]
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Пошук доступних методів використовуючи функцію `dir()`

У Python є функція `dir()`, яка дозволяє переглянути всі доступні методи (функції), які вбудовані в об’єкт даних.  В епізоді 4 ми використали деякі методи для рядка. Але за допомогою `dir()` можна побачити ще більше доступних методів:

```python
my_string = 'Hello world!'   # creation of a string object 
dir(my_string)
```

Ця команда повертає:

```python
['__add__',
...
'__subclasshook__',
'capitalize',
'casefold',
'center',
...
'upper',
'zfill']
```

Ви можете використати `help()` або <kbd>Shift</kbd>\+<kbd>Tab</kbd>, щоб дізнатися більше про призначення цих методів.

Припустимо, що Pandas вже імпортовано, а дані Gapminder про ВВП Європи завантажено в змінну `data`.  Тоді скористайтеся `dir()`, щоб знайти функцію, яка друкує середній ВВП на душу населення для всіх європейських країн за кожен доступний рік.

:::::::::::::::  solution

## Відповідь

Серед багатьох варіантів `dir()` пропонує функцію `median()`.  Таким чином,

```python
data.median()
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Інтерпретація даних

Кордони Польщі стабільні з 1945 року, але до цього кілька разів змінювалися.
Як би ви врахували це при створенні таблиці ВВП на душу населення для Польщі за все ХХ століття?

::::::::::::::::::::::::::::::::::::::::::::::::::

[pandas-dataframe]: https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html
[pandas-series]: https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html
[numpy]: https://www.numpy.org/

:::::::::::::::::::::::::::::::::::::::: keypoints

- Використовуйте `DataFrame.iloc[..., ...]` для вибору значень за їх позицією
- Використовуйте лише `:` замість міток для позначення всіх стовпців або всіх рядків.
- Вибирайте кілька стовпців або рядків за допомогою `DataFrame.loc` та зрізу, заданого іменами стовпців або рядків.
- Результат застосування операції зрізу може бути використаний у подальших операціях.
- Використовуйте порівняння для вибору даних на основі їх значень.
- Вибирайте значення або NaN за допомогою булевої маски.

::::::::::::::::::::::::::::::::::::::::::::::::::


