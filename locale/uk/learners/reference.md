---
title: 'Довідник'
---

## Довідник

## [Запуск та завершення роботи](episodes/01-run-quit.md)

- Файли Python мають розширення `.py`.
- Можуть бути створені у текстовому редакторі або у [Jupyter Notebook][jupyter].
  - Блокноти Jupyter мають розширення `.ipynb`
  - Блокноти Jupyter можуть бути відкриті в [Anaconda](https://docs.continuum.io/anaconda/install) або з командного рядка за допомогою команди `jupyter notebook`
    - В комірках markdown для документування коду можна використовувати як Markdown так і HTML.

## [Змінні та присвоєння](episodes/02-variables.md)

- Значення змінних зберігаються за допомогою `=`.
  - Рядки символів визначаються в лапках `'...'`.
  - Цілі числа та числа з плаваючою комою визначаються без лапок.
- Імена змінних можуть складатися з літер, цифр та символів підкреслення "_".
  - Імена змінних не можуть починатися з цифри.
  - Слід уникати імен змінних, які починаються з підкреслення.
- Використовуйте `print(...)` для виведення значень у вигляді тексту.
- Can use indexing on strings.
  - Індексація починається з 0.
  - Позиція вказується у квадратних дужках `[position]` після імені змінної.
  - Take a slice using `[start:stop]`. Це створює копію частини оригінального рядка символів.
    - `start` є індексом першого елемента.
    - `stop` є індексом елемента після останнього потрібного елемента.
- Використовуйте `len(...)` для визначення довжини змінної або рядка.

## [Типи даних та їх перетворення](episodes/03-types-conversion.md)

- Кожне значення має тип. Він визначає, що можна робити з цим значенням.
  - `int` представляє ціле число.
  - `float` представляє число з плаваючою комою.
  - `str` представляє рядок символів.
- Щоб визначити тип змінної, скористайтеся вбудованою функцією `type(...)`, вказавши назву змінної в дужках.
- Модифікація рядків символів:
  - Використовуйте `+` для об'єднання (конкатенації) рядків.
  - Використовуйте `*`, щоб повторити рядок задану кількість разів.
  - Числа та рядки не можна додавати один до іншого.
    - Перетворити рядок на ціле число: `int(...)`.
    - Перетворити ціле число на рядок : `str(...)`.

## [Вбудовані функції та Довідка](episodes/04-built-in.md)

- Щоб додати коментар, поставте `#` перед тим, що ви не хочете виконувати.
- Вбудовані функції, які часто використовуються:
  - `min()` визначає найменше значення.
  - `max()` визначає найбільше значення.
  - `round()` округлює число з плаваючою комою.
  - `help()` відображає документацію для функції в дужках.
    - Серед інших способів отримання допомоги — одночасне натискання `shift` і `tab` у блокнотах Jupyter.

## [Бібліотеки](episodes/06-libraries.md)

- Імпорт бібліотеки:
  - Використовуйте `import ...` для завантаження бібліотеки.
  - Звертайтеся до цієї бібліотеки у форматі `module_name.thing_name`.
    - `.` indicates 'part of'.
- Щоб імпортувати певний елемент із бібліотеки, використовуйте команду `from ...  import ...`
- Щоб імпортувати бібліотеку та створити її псевдонім, використовуйте команду `import ...  as ...`
- Імпорт математичної бібліотеки: `import math`
  - Приклад звернення до елемента за допомогою імені модуля: `math.cos(math.pi)`.
- Імпорт графічної бібліотеки та позначення її за допомогою псевдоніма: `import matplotlib as mpl`

## [Імпорт табличних даних у датафрейми](episodes/07-reading-tabular.md)

- Використовуйте бібліотеку pandas для статистичного аналізу табличних даних. Завантажуйте її за допомогою `import pandas as pd`.
  - Щоб прочитати дані у файлі csv, використовуйте команду: `pd.read_csv()`, вказавши шлях до файлу в дужках.
    - Щоб використовувати значення стовпця як заголовки рядків: використовуйте `pd.read_csv('path', index_col='column name')`, де `path` та `column name` слід замінити відповідними значеннями.
- Щоб дізнатися більше про датафрейм, використовуйте `DataFrame.info`, замінивши `DataFrame` назвою відповідної змінної.
- Використовуйте команду `DataFrame.columns` для перегляду назв стовпців.
- Use `DataFrame.T` to transpose a DataFrame.
- Використовуйте `DataFrame.describe`, щоб отримати підсумкову статистику для ваших даних.

## [Датафрейми Pandas](episodes/08-data-frames.md)

- Вибирайте дані за допомогою `[i,j]`
  - Вибір за індексом: `DataFrame.iloc[..., ...]`
    - Це включає весь діапазон, крім останнього індексу.
  - Для вибору за міткою елемента використовуйте: `DataFrame.loc[..., ...]`
    - Можна вибрати кілька рядків або стовпців, вказавши їх діапазон.
    - Включає і початкове, і кінцеве значення.
  - Використовуйте `:`, щоб обрати всі рядки або стовпці.
- Також можна вибирати дані на основі булевих значень `True` та `False`. Це булева маска.
  - Наприклад, `mask = subset > 10000`
  - Ми можемо потім використовувати вище визначену маску для вибору значень.
- Формат операції select-apply-combine (вибрати-застосувати-комбінувати) є таким: `data.apply(lambda x: x > x.mean())`, де `mean()` може бути будь-якою операцією, яку користувач хоче застосувати до `x`.

## [Побудова графіків](episodes/09-plotting.md)

- The most widely used plotting library is `matplotlib`.
  - Зазвичай імпортується за допомогою `import matplotlib.pyplot as plt`.
  - Для побудови графіків використовується команда `plt.plot(time, position)`.
  - Для створення легенди використовується команда `plt.legend(['label1', 'label2'], loc='upper left')`
    - Can also define labels within the plot statements by using `plt.plot(time, position, label='label')`. To make the legend show up, use `plt.legend()`
  - Для позначення осей x і y використовуються команди `plt.xlabel('label')` та `plt.ylabel('label')`.
- Графіки можна будувати безпосередньо з датафреймів Pandas, застосовуючи команду `DataFrame.plot()`. Будь-які операції, які можна використовувати для датафреймів, можна застосовувати під час побудови графіків.
  - To plot a bar plot `data.plot(kind='bar')`

```python
import matplotlib.puplot as plot
plt.plot(time, position, label='label')
plt.xlabel('x axis label')
plt.ylabel('y axis label')
plt.legend()
```

## [Списки](episodes/11-lists.md)

- Defined within `[...]` and separated by `,`.
  - An empty list can be created by using `[]`.
- Can use `len(...)` to determine how many values are in a list.
- Can index just as done in previous lessons.
  - Indexing can be used to reassign values `list_name[0] = newvalue`.
- To add an item to a list use `list_name.append()`, with the item to append in the parenthesis.
- To combine two lists use `list_name_1.extend(list_name_2)`.
- To remove an item from a list use `del list_name[index]`.

## [Цикли for](episodes/12-for-loops.md)

- Start a for loop with `for number in [1, 2, 3]:`, with the following lines indented.
  - `[1, 2, 3]` is considered the collection.
  - `number` is the loop variable.
  - The action following the collection is the body.
- To iterate over a sequence of numbers use `range(start, end)`

```python
for number in range(0,5):
    print(number)
```

## [Умовні оператори](episodes/13-conditionals.md)

- Defined similarly to a loop, using `if variable conditional value:`.
  - For example, `if variable > 5:`.
- Use `elif:` for additional tests.
- Use `else:` for when if statement is not true.
- Can combine more than one conditional by using `and` or `or`.
- Often used in combination with for loops.
- Conditions that can be used:
  - `==` equal to.
  - `>=` greater than or equal to.
  - `<=` less than or equal to.
  - `>` greater than.
  - `<` less than.

```python
for m in [3, 6, 7, 2, 8]:
    if m > 5:
        print(m, 'is large')
    elif m == 5:
        print(m, 'is 5')
    else:
        print(m, 'is small')
```

## [Перегляд наборів даних в циклі](episodes/14-looping-data-sets.md)

- Use a for loop: `for filename in [file1, file2]:`
- To find a set of files using a pattern use `glob.glob`
  - Must import first using `import glob`.
  - `*` indicates "match zero or more characters"
  - `?` indicates "match exactly one character"
    - For example: `glob.glob(*.txt)` will find all files that end with `.txt` in the current directory.
- Combine these by writing a loop using: `for filename in glob.glob(*.txt):`

```python
for filename in glob.glob(*.txt):
  data = pd.read_csv(filename)
```

## [Написання функцій](episodes/16-writing-functions.md)

- Define a function using `def function_name(parameters):`. Replace `parameters` with the variables to use when the function is executed.
- Run by using `function_name(parameters)`.
- To return a result to the caller use `return ...` in the function.

```python
def add_numbers(a, b):
    result = a + b
    return result

add_numbers(1, 4)
```

## [Область видимості змінної](episodes/17-scope.md)

- A local variable is defined in a function and can only be seen and used within that function.
- A global variable is defined outside of a function and can be seen or used anywhere after definition.

## [Стиль програмування](episodes/18-style.md)

- Document your code.
- Use clear and meaningful variable names.
- Follow [the PEP8 style guide](https://www.python.org/dev/peps/pep-0008) when setting up your code.
- Use assertions to check for internal errors.
- Use docstrings to provide help.

## Glossary

Arguments
:     Values passed to functions.

Array
:     A container holding elements of the same type.

Boolean
:     An object composed of `True` and `False`.

DataFrame
:     The way Pandas represents a table; a collection of series.

Element
:     An item in a list or an array. For a string, these are the individual characters.

Function
:     A block of code that can be called and re-used elsewhere.

Global variable
:     A variable defined outside of a function that can be used anywhere.

Index
:     The position of a given element.

Jupyter Notebook
:     Interactive coding environment allowing a combination of code and markdown.

Library
:     A collection of files containing functions used by other programs.

Local Variable
:     A variable defined inside of a function that can only be used inside of that function.

Mask
:     A boolean object used for selecting data from another object.

Method
:     An action tied to a particular object. Called by using `object.method`.

Modules
:     The files within a library containing functions used by other programs.

Parameters
:     Variables used when executing a function.

Series
:     A Pandas data structure to represent a column.

Substring
:     A part of a string.

Variables
:     Names for values.




