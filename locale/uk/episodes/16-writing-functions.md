---
title: Створення функцій
teaching: 10
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Знайдіть і поясніть різницю між визначенням функції та викликом функції.
- Створити функцію, яка приймає невелику фіксовану кількість вхідних аргументів і повертає єдиний результат.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Як створювати власні функції?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Щоб програми було легше зрозуміти, розбивайте їх на функції.

- Людина може одночасно зберігати лише декілька речей у своїй робочій пам’яті.
- Розуміння складніших/більших ідей досягається шляхом осмислення та поєднання їхніх складових.
  - Компоненти в машині.
  - Леми при доведенні теорем.
- Функції служать тій же меті в програмах.
  - _Encapsulate_ complexity so that we can treat it as a single "thing".
- Також сприяють _повторному використанню_ кода.
  - Пишемо один раз, використовуємо багаторазово.

## Функція визначається за допомогою `def` та задається її назвою, параметрами та блоком коду.

- Визначення нової функції починається з `def`.
- Далі йде назва функції.
  - Назви функцій мають відповідати тим самим правилам, що й імена змінних.
- Потім _параметри_ в дужках.
  - Порожні дужки, якщо функція не приймає жодних вхідних даних.
  - Ми обговоримо це детально нижче.
- Потім двокрапка.
- Потім блок коду з відступом.

```python
def print_greeting():
    print('Hello!')
    print('The weather is nice today.')
    print('Right?')
```

## Визначення функції не виконує її.

- Визначення функції не виконує її.
  - Аналогічно до присвоєння значення змінній.
- Щоб виконати код функції, її необхідно викликати.

```python
print_greeting()
```

```output
Hello!
```

## Arguments in a function call are matched to its defined parameters.

- Функції найбільш корисні, коли вони можуть працювати з різними даними.
- Укажіть _параметри_ під час визначення функції.
  - Вони стають змінними під час виконання функції.
  - Are assigned the arguments in the call (i.e., the values passed to the function).
  - Якщо ви не називаєте аргументи під час їх використання у виклику, аргументи будуть зіставлені з параметрами в тому порядку, у якому параметри визначені у функції.

```python
def print_date(year, month, day):
    joined = str(year) + '/' + str(month) + '/' + str(day)
    print(joined)

print_date(1871, 3, 19)
```

```output
1871/3/19
```

Or, we can name the arguments when we call the function, which allows us to
specify them in any order and adds clarity to the call site; otherwise as
one is reading the code they might forget if the second argument is the month
or the day for example.

```python
print_date(month=3, day=19, year=1871)
```

```output
1871/3/19
```

- Via [Twitter](https://twitter.com/minisciencegirl/status/693486088963272705):
  `()` contains the ingredients for the function
  while the body contains the recipe.

## Functions may return a result to their caller using `return`.

- Use `return ...` to give a value back to the caller.
- Може виникнути будь-де у функції.
- But functions are easier to understand if `return` occurs:
  - На початку функції для обробки особливих випадків.
  - At the very end, with a final result.

```python
def average(values):
    if len(values) == 0:
        return None
    return sum(values) / len(values)
```

```python
a = average([1, 3, 4])
print('average of actual values:', a)
```

```output
average of actual values: 2.6666666666666665
```

```python
print('average of empty list:', average([]))
```

```output
average of empty list: None
```

- Пам'ятайте: [кожна функція щось повертає](04-built-in.md).
- Функція, яка не містить `return` явно, автоматично повертає `None`.

```python
result = print_date(1871, 3, 19)
print('result of call is:', result)
```

```output
1871/3/19
result of call is: None
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Виявлення синтаксичних помилок

1. Прочитайте наведений нижче код і спробуйте знайти помилки без його запуску.
2. Запустіть код і прочитайте повідомлення про помилку.
   Це `SyntaxError` чи `IndentationError`?
3. Виправте помилку.
4. Повторюйте кроки 2 та 3 доки не виправите всі помилки.

```python
def another_function
  print("Syntax errors are annoying.")
   print("But at least python tells us about them!")
  print("So they are usually not too hard to fix.")
```

:::::::::::::::  solution

## Відповідь

```python
def another_function():
  print("Syntax errors are annoying.")
  print("But at least Python tells us about them!")
  print("So they are usually not too hard to fix.")
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Визначення та використання

Що друкує наступна програма?

```python
def report(pressure):
    print('pressure is', pressure)

print('calling', report, 22.5)
```

:::::::::::::::  solution

## Відповідь

```output
calling <function report at 0x7fd128ff1bf8> 22.5
```

Виклик функції завжди потребує круглі дужки, інакше повертається адреса об'єкта функції в пам'яті. Отже, якщо ми хочемо викликати функцію з назвою `report` і надати їй значення 22,5 для обробки, виклик функції матиме такий вигляд:

```python
print("calling")
report(22.5)
```

```output
calling
pressure is 22.5
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Порядок виконання операцій

1. Що не так у цьому прикладі?

```python
result = print_time(11, 37, 59)

def print_time(hour, minute, second):
   time_string = str(hour) + ':' + str(minute) + ':' + str(second)
   print(time_string)
```

2. Після виправлення проблеми вище поясніть, чому виконання цього прикладу:

```python
result = print_time(11, 37, 59)
print('result of call is:', result)
```

дає такий результат:

```output
11:37:59
result of call is: None
```

3. Чому результатом виклику є `None`?

:::::::::::::::  solution

## Відповідь

1. Проблема цього прикладу полягає в тому, що функція `print_time()` визначається _після_ виклику функції. Python не може розпізнати ім'я `print_time` оскільки воно ще не визначено і генерує помилку `NameError`, тобто `NameError: name 'print_time' is not defined`

2. Перший рядок виводу `11:37:59` з'являється завдяки першому рядку коду `result = print_time(11, 37, 59)`.
   Він викликає функцію `print_time` і присвоює повернуте нею значення змінній `result`. Другий рядок є результатом наступного виклику функції `print`, який виводить вміст
   змінної `result`.

3. `print_time()` явно не повертає значення за допомогою `return`, тому автоматично повертає `None`.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Encapsulation

Заповніть порожні поля, щоб створити функцію, яка приймає одне ім’я файлу як аргумент і завантажує дані з цього файлу. Функція має повертати мінімальне значення з цих даних.

```python
import pandas as pd

def min_in_data(____):
    data = ____
    return ____
```

:::::::::::::::  solution

## Відповідь

```python
import pandas as pd

def min_in_data(filename):
    data = pd.read_csv(filename)
    return data.min()
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Пошук першого від'ємного значення

Заповніть порожні поля, щоб створити функцію, яка приймає список чисел як аргумент і повертає перше від’ємне значення в списку.
Що робить ваша функція, якщо список порожній? Що відбувається, якщо список не містить жодного від'ємного числа?

```python
def first_negative(values):
    for v in ____:
        if ____:
            return ____
```

:::::::::::::::  solution

## Відповідь

```python
def first_negative(values):
    for v in values:
        if v < 0:
            return v
```

Якщо до функції передати порожній список або список з лише додатними значеннями, вона повертає `None`:

```python
my_list = []
print(first_negative(my_list))
```

```output
None
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Виклик з іменованими аргументами

Раніше ми розглядали цю функцію:

```python
def print_date(year, month, day):
    joined = str(year) + '/' + str(month) + '/' + str(day)
    print(joined)
```

Ми бачили, що можна викликати функцію за допомогою \*іменованих аргументів \*, наприклад:

```python
print_date(day=1, month=2, year=2003)
```

1. Що друкує `print_date(day=1, month=2, year=2003)`?
2. Коли ви раніше бачили подібний виклик функції?
3. За яких умов і з якою метою доцільно використовувати іменовані аргументи при виклику функцій?

:::::::::::::::  solution

## Відповідь

1. `2003/2/1`

2. Ми бачили приклади використання іменованих аргументів під час роботи з бібліотекою pandas. Наприклад, під час читання набору даних за допомогою `data = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')`, останній аргумент `index_col` є іменованим аргументом.

3. Використання іменованих аргументів покращує читабельність коду — з виклику функції можна побачити, які імена мають аргументи всередині функції. Це також зменшує ймовірність передачі аргументів у неправильному порядку, оскільки при використанні іменованих аргументів порядок не має значення.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Винесення блоку If/Print в окрему функцію

Наведений нижче код призначений для друку етикеток для курячих яєць.  Цифрові ваги повідомляють комп’ютер про масу курячого яйця (у грамах), після чого комп'ютер друкує етикетку.

```python
import random
for i in range(10):

    # імітація маси курячого яйця
    # маса має випадкове значення у диапазоні 70 +/- 20 грамів
    mass = 70 + 20.0 * (2.0 * random.random() - 1.0)

    print(mass)

    # друк етикетки машиною для сортування яєць
    if mass >= 85:
        print("jumbo")
    elif mass >= 70:
        print("large")
    elif mass < 70 and mass >= 55:
        print("medium")
    else:
        print("small")
```

Блок `if`, який класифікує яйця, може бути корисним в інших ситуаціях. Щоб уникнути його повторення доцільно виділити його в окрему функцію `get_egg_label()`.
Переписавши програму з використанням зазначеної функції, отримаємо такий результат:

```python
# revised version
import random
for i in range(10):

    # імітація маси курячого яйця
    # маса має випадкове значення у диапазоні 70 +/- 20 грамів
    mass = 70 + 20.0 * (2.0 * random.random() - 1.0)

    print(mass, get_egg_label(mass))

```

1. Create a function definition for `get_egg_label()` that will work with the revised program above.  Зверніть увагу на значення, яке повертає функція `get_egg_label()`. Зразок виводу програми вище буде `71.23 large`.
2. Брудне яйце може мати масу понад 90 грамів, а зіпсоване чи розбите яйце, ймовірно, матиме масу менше ніж 50 грамів.  Змініть функцію `print_egg_label()` для врахування цих умов. Можливий вивід програми: `25 too light, probably spoiled`.

:::::::::::::::  solution

## Відповідь

```python
def get_egg_label(mass):
    # друк етикетки машиною для сортування яєць
    egg_label = "Unlabelled"
    if mass >= 90:
        egg_label = "warning: egg might be dirty"
    elif mass >= 85:
        egg_label = "jumbo"
    elif mass >= 70:
        egg_label = "large"
    elif mass < 70 and mass >= 55:
        egg_label = "medium"
    elif mass < 50:
        egg_label = "too light, probably spoiled"
    else:
        egg_label = "small"
    return egg_label
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Функція для аналізу даних

Припустимо, що був виконаний наступний код:

```python
import pandas as pd

data_asia = pd.read_csv('data/gapminder_gdp_asia.csv', index_col=0)
japan = data_asia.loc['Japan']
```

1. Complete the statements below to obtain the average GDP for Japan
   across the years reported for the 1980s.

```python
year = 1983
gdp_decade = 'gdpPercap_' + str(year // ____)
avg = (japan.loc[gdp_decade + ___] + japan.loc[gdp_decade + ___]) / 2
```

2. Перетворіть наведений вище код в окрему функцію.

```python
def avg_gdp_in_decade(country, continent, year):
    data_countries = pd.read_csv('data/gapminder_gdp_'+___+'.csv',delimiter=',',index_col=0)
    ____
    ____
    ____
    return avg
```

3. Як узагальнити функцію, якщо роки у стовпцях заздалегідь невідомі?
   Наприклад, якщо набір даних також містить роки, що закінчуються на 1 та 9 для кожного десятиліття?
   (Підказка: використовуйте стовпці, щоб відфільтрувати їх за десятиліттям.)

:::::::::::::::  solution

## Відповідь

1. Середній ВВП Японії по відзвітованих роках з 1980-тих обчислюється за допомогою:

```python
year = 1983
gdp_decade = 'gdpPercap_' + str(year // 10)
avg = (japan.loc[gdp_decade + '2'] + japan.loc[gdp_decade + '7']) / 2
```

2. Цей код як функція:

```python
def avg_gdp_in_decade(country, continent, year):
    data_countries = pd.read_csv('data/gapminder_gdp_' + continent + '.csv', index_col=0)
    c = data_countries.loc[country]
    gdp_decade = 'gdpPercap_' + str(year // 10)
    avg = (c.loc[gdp_decade + '2'] + c.loc[gdp_decade + '7'])/2
    return avg
```

3. Щоб отримати середнє значення за відповідні роки, нам потрібно застосувати цикл:

```python
def avg_gdp_in_decade(country, continent, year):
    data_countries = pd.read_csv('data/gapminder_gdp_' + continent + '.csv', index_col=0)
    c = data_countries.loc[country]
    gdp_decade = 'gdpPercap_' + str(year // 10)
    total = 0.0
    num_years = 0
    for yr_header in c.index: # індекс c містить звітні роки
        if yr_header.startswith(gdp_decade):
            total = total + c.loc[yr_header]
            num_years = num_years + 1
    return total/num_years
```

Ця функція тепер може викликатися наступним чином:

```python
avg_gdp_in_decade('Japan','asia',1983)
```

```output
20880.023800000003
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Моделювання динамічної системи

У математиці [динамічна система](https://en.wikipedia.org/wiki/Dynamical_system) - це система, у якій функція описує залежність розташування точки в геометричному просторі від часу. Канонічний приклад динамічної системи - це [логістичне відображення](https://en.wikipedia.org/wiki/Logistic_map), тобто модель зростання, яка обчислює нову щільність популяції (від 0 до 1) на основі її поточного значення. В цій моделі час приймає дискретні значення 0, 1, 2, ... (тобто змінюється кроками, а не плавно)

1. Define a function called `logistic_map` that takes two inputs: `x`, representing the current
   population (at time `t`), and a parameter `r = 1`. Ця функція має повертати значення,
   що представляє стан системи (популяції) у момент часу `t + 1`, використовуючи наступну функцію:

`f(t+1) = r * f(t) * [1 - f(t)]`

2. Using a `for` or `while` loop, iterate the `logistic_map` function defined in part 1, starting
   from an initial population of 0.5, for a period of time `t_final = 10`. Зберігайте проміжні результати в списку, щоб після завершення циклу ви накопичили послідовність значень, що представляють стан системи в моменти часу `t = [0,1,...,t_final]` (11 значень в цілому).
   Виведіть цей список, щоб побачити, як змінюється популяція з часом.

3. Encapsulate the logic of your loop into a function called `iterate` that takes the initial
   population as its first input, the parameter `t_final` as its second input and the parameter
   `r` as its third input. The function should return the list of values representing the state of
   the logistic map at times `t = [0,1,...,t_final]`. Run this function for periods `t_final = 100`
   and `1000` and print some of the values. Чи рухається популяція до стабільного стану?

:::::::::::::::  solution

## Відповідь

1.

```python
def logistic_map(x, r):
    return r * x * (1 - x)
```

2.

```python
initial_population = 0.5
t_final = 10
r = 1.0
population = [initial_population]

for t in range(t_final):
    population.append( logistic_map(population[t], r) )
```

3.

```python
def iterate(initial_population, t_final, r):
    population = [initial_population]
    for t in range(t_final):
        population.append( logistic_map(population[t], r) )
    return population

for period in (10, 100, 1000):
    population = iterate(0.5, period, 1)
    print(population[-1])
```

```output
0.06945089389714401
0.009395779870614648
0.0009913908614406382
```

Здається, популяція наближається до нуля.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Використання функцій з умовними операторами в Pandas

Функції часто містять перевірку умов.  Нижче наведено короткий приклад, що визначає належність аргументу до певного квартиля на основі попередньо заданих граничних значень квартилів.

```python
def calculate_life_quartile(exp):
    if exp < 58.41:
        # Це спостереження знаходиться в першому квартилі
        return 1
    elif exp >= 58.41 and exp < 67.05:
        # Це спостереження знаходиться у другому квартилі
       return 2
    elif exp >= 67.05 and exp < 71.70:
        # Це спостереження знаходиться у третьому квартилі
       return 3
    elif exp >= 71.70:
        # Це спостереження знаходиться в четвертому квартилі
       return 4
    else:
        # Це спостереження містить невірні дані
       return None

calculate_life_quartile(62.5)
```

```output
2
```

Зазвичай така функція використовується всередині циклу `for`. Але Pandas має інший, більш ефективний спосіб робити те саме - _застосування_ функції до датафрейму або його частини.  Розглянемо приклад, використовуючи наведене вище визначення функції.

```python
data = pd.read_csv('data/gapminder_all.csv')
data['life_qrtl'] = data['lifeExp_1952'].apply(calculate_life_quartile)
```

У другому рядку коду багато цікавого, тож розберімо його по частинах.
On the right side of the `=` we start with `data['lifeExp']`, which is the
column in the dataframe called `data` labeled `lifExp`.  Ми використовуємо `apply()`, щоб застосувати функцію `calculate_life_quartile` до усіх значень цього стовпця.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Розбивайте програми на функції, щоб їх було легше зрозуміти.
- Функції визначаються за допомогою `def` з назвою, параметрами та блоком коду.
- Визначення функції не запускає її.
- Аргументи виклику функції зіставляються з її визначеними параметрами.
- Функції можуть повертати результат свого виклику за допомогою `return`.

::::::::::::::::::::::::::::::::::::::::::::::::::


