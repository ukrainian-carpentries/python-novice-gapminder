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
- Option 2: Type the function name in a cell with a question mark after it. Then run the cell.

## Python reports a syntax error when it can't understand the source of a program.

- Won't even try to run the program if it can't be parsed.

```python
# Forgot to close the quote marks around the string.
name = 'Feng
```

```error
  File "<ipython-input-56-f42768451d55>", line 2
    name = 'Feng
                ^
SyntaxError: EOL while scanning string literal
```

```python
# An extra '=' in the assignment.
age = = 52
```

```error
  File "<ipython-input-57-ccc3df3cf902>", line 2
    age = = 52
          ^
SyntaxError: invalid syntax
```

- Look more closely at the error message:

```python
print("hello world"
```

```error
  File "<ipython-input-6-d1cc229bf815>", line 1
    print ("hello world"
                        ^
SyntaxError: unexpected EOF while parsing
```

- The message indicates a problem on first line of the input ("line 1").
  - In this case the "ipython-input" section of the file name tells us that
    we are working with input into IPython,
    the Python interpreter used by the Jupyter Notebook.
- The `-6-` part of the filename indicates that
  the error occurred in cell 6 of our Notebook.
- Next is the problematic line of code,
  indicating the problem with a `^` pointer.

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

- Fix syntax errors by reading the source and runtime errors by tracing execution.

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

## Solution

1. Order of operations:

2. `1.1 * radiance = 1.1`

3. `1.1 - 0.5 = 0.6`

4. `min(radiance, 0.6) = 0.6`

5. `2.0 + 0.6 = 2.6`

6. `max(2.1, 2.6) = 2.6`

7. At the end, `radiance = 2.6`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Spot the Difference

1. Predict what each of the `print` statements in the program below will print.
2. Does `max(len(rich), poor)` run or produce an error message?
   If it runs, does its result make any sense?

```python
easy_string = "abc"
print(max(easy_string))
rich = "gold"
poor = "tin"
print(max(rich, poor))
print(max(len(rich), len(poor)))
```

:::::::::::::::  solution

## Solution

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

## Why Not?

Why is it that `max` and `min` do not return `None` when they are called with no arguments?

:::::::::::::::  solution

## Solution

`max` and `min` return TypeErrors in this case because the correct number of parameters
was not supplied. If it just returned `None`, the error would be much harder to trace as it
would likely be stored into a variable and used later in the program, only to likely throw
a runtime error.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Last Character of a String

If Python starts counting from zero,
and `len` returns the number of characters in a string,
what index expression will get the last character in the string `name`?
(Note: we will see a simpler way to do this in a later episode.)

:::::::::::::::  solution

## Solution

`name[len(name) - 1]`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Explore the Python docs!

The [official Python documentation](https://docs.python.org/3/) is arguably the most complete
source of information about the language. It is available in different languages and contains a lot of useful
resources. The [Built-in Functions page](https://docs.python.org/3/library/functions.html) contains a catalogue of
all of these functions, including the ones that we've covered in this lesson. Some of these are more advanced and
unnecessary at the moment, but others are very simple and useful.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Use comments to add documentation to programs.
- A function may take zero or more arguments.
- Commonly-used built-in functions include `max`, `min`, and `round`.
- Functions may only work for certain (combinations of) arguments.
- Functions may have default values for some arguments.
- Use the built-in function `help` to get help for a function.
- The Jupyter Notebook has two ways to get help.
- Every function returns something.
- Python reports a syntax error when it can't understand the source of a program.
- Python reports a runtime error when something goes wrong while a program is executing.
- Fix syntax errors by reading the source code, and runtime errors by tracing the program's execution.

::::::::::::::::::::::::::::::::::::::::::::::::::
