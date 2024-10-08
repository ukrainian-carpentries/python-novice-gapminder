---
title: Типи даних та їх перетворення
teaching: 10
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Визначення ключових відмінностей між цілими числами та числами з плаваючою точкою.
- З'ясувати ключові відмінності між числами та символьними рядками.
- Використання вбудованих функцій для перетворення цілих чисел, чисел з плаваючою точкою та рядків.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Які види даних зберігають програми?
- Як я можу перетворити один тип в інший?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Кожне значення має тип.

- Every value in a program has a specific type.
- Ціле число (`int`): зображує додатні або від’ємні цілі числа, наприклад 3 або -512.
- Число з плаваючою крапкою (`float`): зображує дійсні числа, наприклад 3.14159 або -2.5.
- Character string (usually called "string", `str`): text.
  - Укладені в одинарні або подвійні лапки (тип лапок має збігатися).
  - Під час відображення рядку лапки не друкуються.

## Вбудована функція `type` повертає тип значення.

- Використовуйте вбудовану функцію `type`, щоб з'ясувати, який тип має значення.
- Це також працює зі змінними.
  - But remember: the _value_ has the type --- the _variable_ is just a label.

```python
print(type(52))
```

```output
<class 'int'>
```

```python
fitness = 'average' print(type(fitness))
```

```output
<class 'str'>
```

## Types control what operations (or methods) can be performed on a given value.

- Тип значення визначає, що може робити з ним програма.

```python
print(5 - 3)
```

```output
2
```

```python
print('hello' - 'h')
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-2-67f5626a1e07> in <module>()
----> 1 print('hello' - 'h')

TypeError: unsupported operand type(s) for -: 'str' and 'str'
```

## You can use the "+" and "\*" operators on strings.

- "Adding" character strings concatenates them.

```python
full_name = 'Ahmed' + ' ' + 'Walsh'
print(full_name)
```

```output
Ahmed Walsh
```

- Якщо рядок помножити на ціле число _N_, то це створить новий рядок, який буде містити вихідний рядок, повторений _N_ разів.
  - Оскільки множення - це повторюване додавання.

```python
separator = '=' * 10
print(separator)
```

```output
==========
```

## Рядки мають довжину (але числа її не мають).

- Вбудована функція `len` повертає кількість символів у рядку.

```python
print(len(full_name))
```

```output
11
```

- Але числа не мають довжини (навіть нульової).

```python
print(len(52))
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-3-f769e8e8097d> in <module>()
----> 1 print(len(52))

TypeError: object of type 'int' has no len()
```

## Must convert numbers to strings or vice versa when operating on them. {#convert-numbers-and-strings}

- Додавання чисел та рядків неможливе.

```python
print(1 + '2')
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-4-fe4f54a023c6> in <module>()
----> 1 print(1 + '2')

TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

- Таке додавання не дозволено, тому що воно не визначене: чи має `1 + '2'` повертати `3` чи `'12'`?
- Перетворення типу виконується за допомогою функції, яка має те ж саме імʼя, що і потрібний тип.

```python
print(1 + int('2'))
print(str(1) + '2')
```

```output
3
12
```

## Can mix integers and floats freely in operations.

- Цілі та дійсні числа можна використовувати разом для арифметичних дій.
  - Python 3 автоматично перетворить цілі числа у дійсні, якщо це потрібно.

```python
print('half is', 1 / 2.0)
print('three squared is', 3.0 ** 2)
```

```output
half is 0.5
three squared is 9.0
```

## Variables only change value when something is assigned to them.

- Якщо в електронних таблицях ми зробимо одну комірку залежною від іншої та оновимо останню,
  перша оновиться автоматично.
- This does **not** happen in programming languages.

```python
variable_one = 1
variable_two = 5 * variable_one
variable_one = 2
print('first is', variable_one, 'and second is', variable_two)
```

```output
first is 2 and second is 5
```

- The computer reads the value of `variable_one` when doing the multiplication,
  creates a new value, and assigns it to `variable_two`.
- Після того, як значення `variable_two` встановлено, воно _не залежить від значення `variable_one`_, отже його значення не змінюється автоматично, коли `variable_one` змінюється.

:::::::::::::::::::::::::::::::::::::::  challenge

## Дроби

What type of value is 3.4?
Як це можна встановити?

:::::::::::::::  solution

## Рішення

It is a floating-point number (often abbreviated "float").
Це можна перевірити, використовуючи вбудовану функцію `type()`.

```python
print(type(3.4))
```

```output
<class 'float'>
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Автоматичне перетворення типів

Який тип має вираз 3.25 + 4?

:::::::::::::::  solution

## Рішення

Це - дійсне число: цілі числа автоматично перетворюються у дійсні, коли це необхідно.

```python
result = 3.25 + 4
print(result, 'is', type(result))
```

```output
7.25 is <class 'float'>
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Вибір типу

What type of value (integer, floating point number, or character string)
would you use to represent each of the following?  Спробуйте знайти більш ніж одну гарну відповідь для кожної проблеми.  For example, in  # 1, when would counting days with a floating point variable make more sense than using an integer?

1. Кількість днів, які пройшли з початку року.
2. Час, що пройшов від початку року до сьогоднішнього дня.
3. Серійний номер лабораторного обладнання.
4. Вік лабораторного зразка
5. Поточне населення міста.
6. Average population of a city over time.

:::::::::::::::  solution

## Рішення

Відповіді на запитання:

1. Ціле, оскільки число днів належить діапазону від 1 до 365.

2. Дійсне число, оскільки потрібно використовувати частини дня.

3. Символьний рядок, якщо серійний номер містить літери та цифри, або ціле число, якщо серійний номер складається лише з цифр.

4. Це залежить від багатьох факторів! Як вимірюється вік зразка? whole days since collection (integer)?  Дата і час (рядок)?

5. Виберіть дійсне число, щоб представити приблизну кількість населення за допомогою округлення (наприклад, до мільйонів), або ціле число, щоб представити точну кількість населення.

6. Floating point number, since an average is likely to have a fractional part.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Типи операцій ділення

In Python 3, the `//` operator performs integer (whole-number) floor division, the `/` operator performs floating-point
division, and the `%` (or _modulo_) operator calculates and returns the remainder from integer division:

```python
print('5 // 3:', 5 // 3)
print('5 / 3:', 5 / 3)
print('5 % 3:', 5 % 3)
```

```output
5 // 3: 1
5 / 3: 1.6666666666666667
5 % 3: 2
```

If `num_subjects` is the number of subjects taking part in a study,
and `num_per_survey` is the number that can take part in a single survey,
write an expression that calculates the number of surveys needed
to reach everyone once.

:::::::::::::::  solution

## Рішення

We want the minimum number of surveys that reaches everyone once, which is
the rounded up value of `num_subjects/ num_per_survey`. Це
еквівалентно виконанню дійсного ділення за допомогою оператору `//` і додаванню 1 до результату. Before
the division we need to subtract 1 from the number of subjects to deal with
the case where `num_subjects` is evenly divisible by `num_per_survey`.

```python
num_subjects = 600
num_per_survey = 42
num_surveys = (num_subjects - 1) // num_per_survey + 1

print(num_subjects, 'subjects,', num_per_survey, 'per survey:', num_surveys)
```

```output
600 subjects, 42 per survey: 15
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Перетворення рядків у числа

Якщо потрібно, функція `float()` перетворить рядок у дійсне число, а функція `int()` перетворить дійсне число в ціле:

```python
print("string to float:", float("3.4"))
print("float to int:", int(3.4))
```

```output
string to float: 3.4
float to int: 3
```

Якщо перетворення не має сенсу, то генерується повідомлення про помилку.

```python
print("string to float:", float("Hello world!"))
```

```error
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-5-df3b790bf0a2> in <module>
----> 1 print("string to float:", float("Hello world!"))

ValueError: could not convert string to float: 'Hello world!'
```

Given this information, what do you expect the following program to do?

Що вона робить насправді?

Як це пояснити?

```python
print("fractional string to int:", int("3.4"))
```

:::::::::::::::  solution

## Рішення

Що ви очікуєте від цієї програми? Чому б не очікувати, що у Python 3 команда `int` перетворить рядок "3.4" на 3.4 та виконає додаткове перетворення у ціле число 3. After all, Python 3 performs a lot of other
magic - isn't that part of its charm?

```python
int("3.4")
```

```output
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-2-ec6729dfccdc> in <module>
----> 1 int("3.4")
ValueError: invalid literal for int() with base 10: '3.4'
```

Однак Python 3 видає помилку. Чому? Можливо, щоб бути послідовним. If you ask Python to perform two consecutive
typecasts, you must convert it explicitly in code.

```python
int(float("3.4"))
```

```output
3
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Арифметичні дії з різними типами

Яка з наступних команд поверне дійсне число `2.0`?
Примітка: це питання може мати декілька коректних відповідей.

```python
first = 1.0
second = "1"
third = "1.1"
```

1. `first + float(second)`
2. `float(second) + float(third)`
3. `first + int(third)`
4. `first + int(float(third))`
5. `int(first) + int(float(third))`
6. `2.0 * second`

:::::::::::::::  solution

## Рішення

Правильні відповіді: 1 та 4

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Комплексні числа

Python provides complex numbers,
which are written as `1.0+2.0j`.
If `val` is a complex number,
its real and imaginary parts can be accessed using _dot notation_
as `val.real` and `val.imag`.

```python
a_complex_number = 6 + 2j
print(a_complex_number.real)
print(a_complex_number.imag)
```

```output
6.0
2.0
```

1. Чому, на вашу думку, Python використовує `j` замість `i` для уявної частини?
2. What do you expect `1 + 2j + 3` to produce?
3. Що ви очікуєте від `4j`?  А що від `4 j` або `4 + j`?

:::::::::::::::  solution

## Рішення

1. Стандартні математичні позначення зазвичай використовують `i` для позначення комплексного числа. However, from media reports it
   was an early convention established from electrical engineering that now presents a technically expensive area to
   change. [Stack Overflow містить додаткові пояснення та обговорення.](http://stackoverflow.com/questions/24812444/why-are-complex-numbers-in-python-denoted-with-j-instead-of-i)

2. `(4+2j)`

3. `4j` або `Syntax Error: invalid syntax`. В останньому випадку `j` вважається змінною і значення виразу залежить від того, чи є `j` визначеним.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Кожне значення має тип.
- Вбудована функція `type` повертає тип значення.
- Types control what operations can be done on values.
- Рядки можна додавати і помножувати.
- Рядки мають довжину (але числа її не мають).
- Необхідно перетворювати числа в рядки або навпаки під час виконання певних операцій.
- Цілі та дійсні числа можна використовувати разом.
- Змінні можуть набути своє значення тільки через присвоювання.

::::::::::::::::::::::::::::::::::::::::::::::::::
