---
title: Змінні та присвоєння
teaching: 10
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Створення програм, які присвоюють скалярні значення змінним і виконують обчислення з цими значеннями.
- Відстеження у програмах значень змінних, які використовують скалярне присвоєння.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Як я можу зберігати дані в програмах?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Використовуйте змінні для зберігання значень.

- **Змінні** - це імена значень.

- Імена змінних

  - can **only** contain letters, digits, and underscore `_` (typically used to separate words in long variable names)
  - не можуть починатися з цифри
  - are **case sensitive** (age, Age and AGE are three different variables)

- The name should also be meaningful so you or another programmer know what it is

- Імена змінних, які починаються з підкреслення, наприклад  __alistairs_real_age, мають особливе значення, тому ми не будемо цього робити, доки не зрозуміємо прийняті в мові Python домовленості.

- In Python the `=` symbol assigns the value on the right to the name on the left.

- The variable is created when a value is assigned to it.

- Here, Python assigns an age to a variable `age`
  and a name in quotes to a variable `first_name`.

  ```python
  age = 42
  first_name = 'Ahmed'
  ```

## Використовуйте `print` для виведення значень.

- Python має вбудовану функцію `print`, яка друкує щось як текст.
- Щоб викликати функцію (тобто, щоб виконати її), треба вказати її ім'я.
- Щоб передати функції значення (тобто дані для друку), їх треба помістити у дужки.
- To add a string to the printout, wrap the string in single or double quotes.
- Значення, які передаються до функції, називаються **аргументами**

```python
print(first_name, 'is', age, 'years old')
```

```output
Ahmed is 42 years old
```

- `print` automatically puts a single space between items to separate them.
- Також `print` переходить на новий рядок після друку.

## Змінні мають бути створені перед їх використанням.

- Якщо змінна ще не існує, або якщо ім'я було неправильно написано, Python повідомляє про помилку. (На відміну від деяких інших мов, які можуть "вгадати" якесь значення за замовчуванням.)

```python
print(last_name)
```

```error
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-1-c1fbb4e96102> in <module>()
----> 1 print(last_name)

NameError: name 'last_name' is not defined
```

- Останній рядок у повідомленні про помилку є найбільш інформативним.
- We will look at error messages in detail [later](17-scope.md#reading-error-messages).

:::::::::::::::::::::::::::::::::::::::::  callout

## Змінні зберігаються між комірками

Майте на увазі, що в блокноті Jupyter важливий порядок виконання комірок, а не порядок їх появи. Python will remember _all_ the code that was run previously, including any variables you have
defined, irrespective of the order in the notebook. Тому, якщо ви визначите змінні нижче в блокноті, а потім (повторно) запустите комірки вище, то ті комірки, що визначені нижче, все одно будуть присутні. Як приклад, створіть дві комірки наступного вмісту у такому порядку:

```python
print(myval)
```

```python
myval = 1
```

If you execute this in order, the first cell will give an error. However, if you run the first cell _after_ the second
cell it will print out `1`. To prevent confusion, it can be helpful to use the `Kernel` -> `Restart & Run All` option which
clears the interpreter and runs everything from a clean slate going top to bottom.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Змінні можна використовувати для обчислень.

- Ми можемо використовувати змінні в обчисленнях так само, як би вони були значеннями.
  - Пам’ятайте, ми присвоїли значення `42` змінній `age` кількома рядками вище.

```python
age = age + 3 
print('Age in three years:', age)
```

```output
Age in three years: 45
```

## Використовуйте індекс, щоб отримати один символ із рядка.

- The characters (individual letters, numbers, and so on) in a string are
  ordered. Наприклад, рядок `'AB'` не те саме, що `'BA'`. Завдяки такому упорядкуванню ми можемо розглядати рядок як список символів.
- Each position in the string (first, second, etc.) is given a number. This
  number is called an **index** or sometimes a subscript.
- Індекси нумеруються від 0.
- Використовуйте індекс позиції у квадратних дужках, щоб отримати символ з тієї позиції у рядку.

![Рядок кода Python, print(atom\\_name\[0\]), демонструє, що використання нульового індексу виведе лише початкову літеру, у цьому випадку 'h' for helium.](fig/2_indexing.svg)

```python
atom_name = 'helium'
print(atom_name[0])
```

```output
h
```

## Використовуйте зріз, щоб отримати підрядок.

- A part of a string is called a **substring**. A substring can be as short as a
  single character.
- Список складається з елементів. У випадку, коли рядок розглядається як список, його елементами є окремі символи.
- Зріз - це частина рядка (в загальному випадку, будь-який вираз).
- We take a slice with the notation `[start:stop]`, where `start` is the integer
  index of the first element we want and `stop` is the integer index of
  the element _just after_ the last element we want.
- Проміжок між `stop` and `start` - це довжина зрізу.
- Визначення зрізу не змінює вміст вихідного рядка. Натомість, визначений зріз повертає копію початкового рядка.

```python
atom_name = 'sodium'
print(atom_name[0:3])
```

```output
sod
```

## Використовуйте вбудовану функцію `len`, щоб знайти довжину рядка.

```python
print(len('helium'))
```

```output
6
```

- Nested functions are evaluated from the inside out,
  like in mathematics.

## Python is case-sensitive.

- Python вважає, що букви верхнього та нижнього регістру відрізняються, отже `Name` і `name` - різні змінні.
- Існують домовленості про використання великих літер на початку імен змінних, тому ми будемо використовувати малі літери.

## Використовуйте змістовні назви змінних.

- Python doesn't care what you call variables as long as they obey the rules
  (alphanumeric characters and the underscore).

```python
flabadab = 42
ewr_422_yY = 'Ahmed'
print(ewr_422_yY, 'is', flabadab, 'years old')
```

- Використовуйте змістовні назви змінних, щоб допомогти іншим зрозуміти, що робить програма.
- The most important "other person" is your future self.

:::::::::::::::::::::::::::::::::::::::  challenge

## Заміна значень

Fill the table showing the values of the variables in this program
_after_ each statement is executed.

```python
# Оператор  # Значення x   # Значення y   # Значення swap #
x = 1.0     #              #              #               #
y = 3.0     #              #              #               #
swap = x    #              #              #               #
x = y       #              #              #               #
y = swap    #              #              #               # 
```

:::::::::::::::  solution

## Рішення

```output
# Оператор # Значення x   # Значення y   # Значення swap #
x = 1.0    # 1.0          # не визначено # не визначено  #
y = 3.0    # 1.0          # 3.0          # не визначено  #
swap = x   # 1.0          # 3.0          # 1.0           #
x = y      # 3.0          # 3.0          # 1.0           #
y = swap   # 3.0          # 1.0          # 1.0           #
```

Ці три рядки обмінюються значеннями в `x` і `y` використовуючи змінну `swap`
для тимчасового зберігання. Це досить поширена ідіома програмування.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Прогнозування значень

Яким є остаточне значення змінної `position` у програмі нижче?
(Try to predict the value without running the program,
then check your prediction.)

```python
initial = 'left'
position = initial
initial = 'right'
```

:::::::::::::::  solution

## Рішення

```python
print(position)
```

```output
left
```

The `initial` variable is assigned the value `'left'`.
У другому рядку змінна `position` також отримує
значення `'left'`. У третьому рядку змінній `initial` надається значення `'right'`, але змінна `position` зберігає своє значення `'left'`.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Challenge

Якщо ви присвоїли `a = 123`,
що станеться, якщо ви спробуєте отримати другу цифру `a` через `a[1]`?

:::::::::::::::  solution

## Рішення

Numbers are not strings or sequences and Python will raise an error if you try to perform an index operation on a
number. У [наступному уроці про типи даних і перетворення типів](03-types-conversion.md)
ми дізнаємось більше про типи і як конвертувати один тип в інший. Якщо вам потрібна N-та цифра числа, ви можете перетворити число на рядок за допомогою вбудованої функції `str`, а потім виконати операцію індексування цього рядка.

```python
a = 123
print(a[1])
```

```error
TypeError: 'int' object is not subscriptable
```

```python
a = str(123)
print(a[1])
```

```output
2
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Вибір імені

Яке ім'я для змінної є кращим: `m`, `min` або `minutes`?
Чому?
Hint: think about which code you would rather inherit
from someone who is leaving the lab:

1. `ts = m 60 + s`
2. `tot_sec = min 60 + sec`
3. `total_seconds = minutes * 60 + seconds`

:::::::::::::::  solution

## Рішення

`minutes` is better because `min` might mean something like "minimum"
(and actually is an existing built-in function in Python that we will cover later).

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Практика застосування зрізів

Що друкує наступна програма?

```python
atom_name = 'carbon'
print('atom_name[1:3] is:', atom_name[1:3])
```

:::::::::::::::  solution

## Рішення

```output
atom_name[1:3] is: ar
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Різноманітні види зрізів

Є наступний рядок:

```python
species_name = "Acacia buxifolia"
```

What would these expressions return?

1. `species_name[2:8]`
2. `species_name[11:]` (без значення після двокрапки)
3. `species_name[:4]` (без значення до двокрапки)
4. `species_name[:]` (тільки двокрапка)
5. `species_name[11:-3]`
6. `species_name[-5:-3]`
7. What happens when you choose a `stop` value which is out of range? (тобто спробуйте виконати `species_name[0:20]` або `species_name[:103]`)

:::::::::::::::  solution

## Рішення

1. `species_name[2:8]` повертає підрядок `'acia b'`

2. `species_name[11:]` повертає підрядок `'folia'`, з позиції 11 до кінця рядку

3. `species_name[:4]` повертає підрядок `Acac'`, з початку рядку до позиції 4, не включаючи цю позицію

4. `species_name[:]` повертає весь рядок 'Acacia buxifolia'\`

5. `species_name[11:-3]` повертає підрядок `'fo'`, з 11 позиції до третьої позиції з кінця рядку, не включаючи її

6. `species_name[-5:-3]` також повертає підрядок `'fo'`, з п'ятої позиції з кінця до третьої позиції з кінця, не включаючи її

7. Якщо частина фрагмента виходить за межі діапазону, операція не повертає помилку. `species_name[0:20]` дає той самий результат, що і `species_name[0:]`, та `species_name[:103]` дає такий самий результат, як `species_name[:]`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Використовуйте змінні для зберігання значень.
- Використовуйте `print` для виводу значень.
- Variables persist between cells.
- Змінні мають бути створені перед їх використанням.
- Змінні можна використовувати для обчислень.
- Використовуйте індекс, щоб отримати один символ із рядка.
- Використовуйте зріз, щоб отримати підрядок.
- Використовуйте вбудовану функцію `len`, щоб знайти довжину рядка.
- У Python важливо, який регістр використовується.
- Використовуйте змістовні назви змінних.

::::::::::::::::::::::::::::::::::::::::::::::::::
