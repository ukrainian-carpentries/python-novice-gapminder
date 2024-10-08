---
title: Вбудовані функції та довідка
teaching: 15
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Пояснення призначення функцій.
- Коректний виклик вбудованих функцій Python.
- Правильне використання вкладених вбудованих функцій.
- Використання довідки для відображення документації про вбудовані функції.
- Правильний опис ситуацій, в яких виникають помилки SyntaxError і NameError.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Як я можу використовувати вбудовані функції?
- Як я можу дізнатися, для чого вони призначені?
- Які помилки можуть виникнути в програмах?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Використовуйте коментарі при створенні документації програм.

```python
# This sentence isn't executed by Python.
adjustment = 0.5   # Neither is this - anything after '#' is ignored.
```

## A function may take zero or more arguments.

- We have seen some functions already --- now let's take a closer look.
- An _argument_ is a value passed into a function.
- `len` потребує тільки один аргумент.
- `int`, `str`, and `float` create a new value from an existing one.
- `print` takes zero or more.
- `print` без аргументів повертає порожній рядок.
  - Потрібно завжди використовувати дужки, навіть якщо вони порожні, щоб Python знав, що викликається функція.

```python
print('before')
print()
print('after')
```

```output
before

after
```

## Кожна функція щось повертає.

- Кожен виклик функції дає певний результат.
- Якщо функція не має корисного результату для повернення, то вона зазвичай повертає спеціальне значення `None`. `None` - це об’єкт Python, який застосовується у будь-якому випадку, коли немає значення.

```python
result = print('example')
print('result of print is', result)
```

```output
example
result of print is None
```

## Поширені вбудовані функції `max`, `min` та `round`.

- Використовуйте `max`, щоб знайти найбільше з одного або декількох значень.
- Використовуйте `min`, щоб знайти найменше значення.
- Both work on character strings as well as numbers.
  - "Larger" and "smaller" use (0-9, A-Z, a-z) to compare letters.

```python
print(max(1, 2, 3))
print(min('a', 'A', '0'))
```

```output
3
0
```

## Functions may only work for certain (combinations of) arguments.

- `max` та `min` мають приймати принаймні один аргумент.
  - "Найбільше значення з порожньої множини" - запит, який не має сенсу.
- Крім того, аргументи функцій мають бути порівнюваними.

```python
print(max(1, 'a'))
```

```error
TypeError                                 Traceback (most recent call last)
<ipython-input-52-3f049acf3762> in <module>
----> 1 print(max(1, 'a'))

TypeError: '>' not supported between instances of 'str' and 'int'
```

## Функції можуть мати значення за замовчуванням для певних аргументів.

- `round` округлює дійсне число.
- За замовчуванням округлення відбувається до нуля знаків після точки.

```python
round(3.712)
```

```output
4
```

- We can specify the number of decimal places we want.

```python
round(3.712, 1)
```

```output
3.7
```

## Функції, приєднані до об'єктів, називаються методами

- Функції можуть набувати іншої форми, яка буде типовою для епізодів, пов'язаних з бібліотекою pandas.
- Методи мають такі дужки як функції, але з'являються в описі оператора після імені змінної.
- Деякі методи використовуються для внутрішніх операцій Python і відзначаються подвійними підкресленнями.

```python
my_string = 'Hello world!'  # створення об'єкта - рядка 

print(len(my_string))       # функція len приймає рядок як аргумент і повертає довжину рядка

print(my_string.swapcase()) # виклик методу swapcase для об’єкта my_string

print(my_string.__len__())  # виклик внутрішнього методу __len__ для об’єкта my_string, який використовується функцією len(my_string)

```

```output
12
hELLO WORLD!
12
```

- Ви навіть можете побачити, як вони зв’язані.  Вони працюють зліва направо.

```python
print(my_string.isupper())          # Функція перевіряє, чи всі літери заглавні
print(my_string.upper())            # Функція перетворює всі літери на заглавні
print(my_string.upper().isupper())  # Тепер всі літери заглавні
```

```output
False
HELLO WORLD
True
```

## Використовуйте вбудовану функцію `help`, щоб отримати довідку щодо функції.

- Кожна вбудована функція має онлайн-документацію.

```python
help(round)
```

```output
Файл допомоги щодо вбудованої функції round зі стандартної бібліотеки Python:

round(number, ndigits=None)
    Round a number to a given precision in decimal digits.
    
    The return value is an integer if ndigits is omitted or None.  Otherwise
    the return value has the same type as the number.  ndigits may be negative.
```

## Два шляхи отримання допомоги у Jupyter Notebook.

- Option 1: Place the cursor near where the function is invoked in a cell
  (i.e., the function name or its parameters),
  - Утримуйте <kbd>Shift</kbd>та натисніть <kbd>Tab</kbd>.
  - Зробіть це кілька разів для розширення інформації, що повертається.
- Варіант 2: Введіть ім'я функції в комірці зі знаком питання після нього. Потім запустіть комірку.

## Python повідомляє про синтаксичну помилку, коли він не може зрозуміти вихідний код програми.

- Він навіть не намагатиметься запустити програму, якщо її неможливо коректно прочитати.

```python
# Рядок не взято в лапки.
name = 'Feng
```

```error
  File "<ipython-input-56-f42768451d55>", line 2
    name = 'Feng
                ^
SyntaxError: EOL while scanning string literal
```

```python
# Додатковий знак '=' у присвоєнні. 
age = = 52
```

```error
  File "<ipython-input-57-ccc3df3cf902>", line 2
    age = = 52
          ^
SyntaxError: invalid syntax
```

- Подивіться уважніше на повідомлення про помилку:

```python
print("hello world"
```

```error
  File "<ipython-input-6-d1cc229bf815>", line 1
    print ("hello world"
                        ^
SyntaxError: unexpected EOF while parsing
```

- Повідомлення вказує на проблему в першому рядку введеної програми ("line 1").
  - In this case the "ipython-input" section of the file name tells us that
    we are working with input into IPython,
    the Python interpreter used by the Jupyter Notebook.
- Фрагмент `-6-` в назві файлу вказує на те, що помилка сталася в комірці 6.
- Далі йде проблемний рядок коду, на що вказує символ `^`.

## Python reports a runtime error when something goes wrong while a program is executing. {#runtime-error}

```python
age = 53
remaining = 100 - aege # mis-spelled 'age'
```

```error
NameError                                 Traceback (most recent call last)
<ipython-input-59-1214fb6c55fc> in <module>
      1 age = 53
----> 2 remaining = 100 - aege # mis-spelled 'age'

NameError: name 'aege' is not defined
```

- Аналіз вихідного кода дозволяє виправити синтаксичні помилки, а на етапі компілювання можна виправити помилки виконання.

:::::::::::::::::::::::::::::::::::::::  challenge

## What Happens When

1. Explain in simple terms the order of operations in the following program:
   when does the addition happen, when does the subtraction happen,
   when is each function called, etc.
2. What is the final value of `radiance`?

```python
radiance = 1.0
radiance = max(2.1, 2.0 + min(radiance, 1.1 * radiance - 0.5))
```

:::::::::::::::  solution

## Рішення

1. Порядок виконання операцій:

2. `1.1 * radiance = 1.1`

3. `1.1 - 0.5 = 0.6`

4. `min(radiance, 0.6) = 0.6`

5. `2.0 + 0.6 = 2.6`

6. `max(2.1, 2.6) = 2.6`

7. At the end, `radiance = 2.6`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Знайдіть відмінності

1. Подумайте, що виведе кожен з операторів `print` у наведеній нижче програмі.
2. Функція `max(len(rich), poor)` поверне відповідь або повідомлення про помилку?
   Якщо поверне відповідь, чи буде вона мати сенс?

```python
easy_string = "abc"
print(max(easy_string))
rich = "gold"
poor = "tin"
print(max(rich, poor))
print(max(len(rich), len(poor)))
```

:::::::::::::::  solution

## Рішення

```python
print(max(easy_string))
```

```output
c
```

```python
print(max(rich, poor))
```

```output
tin
```

```python
print(max(len(rich), len(poor)))
```

```output
4
```

`max(len(rich), poor)` throws a TypeError. This turns into `max(4, 'tin')` and
as we discussed earlier a string and integer cannot meaningfully be compared.

```error
TypeError                                 Traceback (most recent call last)
<ipython-input-65-bc82ad05177a> in <module>
----> 1 max(len(rich), poor)

TypeError: '>' not supported between instances of 'str' and 'int'
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Чому ні?

Чому саме `max` і `min` не повертають `None`, коли вони викликаються без аргументів?

:::::::::::::::  solution

## Рішення

`max` and `min` повертають TypeErrors у цьому випадку, тому що не було вказано правильну кількість параметрів. Якби компілятор просто повернув `None`, помилку було б набагато важче відстежити, тому що це значення було б збережено в змінній і використано пізніше в програмі.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Останній символ рядка

Якщо Python починає рахувати з нуля, та `len` повертає кількість символів у рядку, то який індекс отримає останній символ у рядку `name`?
(Примітка: ми побачимо простіший спосіб зробити це в подальшому епізоді)

:::::::::::::::  solution

## Рішення

`name[len(name) - 1]`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Вивчайте документацію Python!

The [official Python documentation](https://docs.python.org/3/) is arguably the most complete
source of information about the language. It is available in different languages and contains a lot of useful
resources. The [Built-in Functions page](https://docs.python.org/3/library/functions.html) contains a catalogue of
all of these functions, including the ones that we've covered in this lesson. Деякі з них більш досконалі та на цей час зайві, але інші - дуже прості та корисні.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Використовуйте коментарі при створенні документації програм.
- A function may take zero or more arguments.
- Поширені вбудовані функції `max`, `min` та `round`.
- Функції можуть працювати лише з певними аргументами (комбінаціями аргументів).
- Функції можуть мати значення за замовчуванням для певних аргументів.
- Використовуйте вбудовану функцію `help`, щоб отримати довідку щодо функції.
- The Jupyter Notebook has two ways to get help.
- Кожна функція щось повертає.
- Python повідомляє про синтаксичну помилку, коли він не може зрозуміти джерело програми.
- Python reports a runtime error when something goes wrong while a program is executing.
- Якщо перечитаєте джерело, можна виправити синтаксичні помилки, а якщо відстежите компілювання - помилки виконання.

::::::::::::::::::::::::::::::::::::::::::::::::::
