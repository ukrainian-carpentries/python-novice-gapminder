---
title: Область видимості змінної
teaching: 10
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Визначення локальних і глобальних змінних.
- Ідентифікація параметрів як локальних змінних.
- Read a traceback and determine the file, function, and line number on which the error occurred, the type of error, and the error message.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Як насправді виклики функцій працюють?
- Як можна визначити, де виникають помилки?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Область змінної - це частина програми, яка може "бачити" цю зміну.

- There are only so many sensible names for variables.
- People using functions shouldn't have to worry about
  what variable names the author of the function used.
- People writing functions shouldn't have to worry about
  what variable names the function's caller uses.
- Частина програми, в якій змінна є видимою, називається її _областю_.

```python
pressure = 103.9

def adjust(t):
    temperature = t * 1.43 / pressure
    return temperature
```

- `pressure` – це _глобальна змінна_.
  - Визначається поза будь-якою конкретною функцією.
  - Є видимою у будь-якому місці програми.
- `t` and `temperature` are _local variables_ in `adjust`.
  - Визначені всередині функції.
  - Не є видимими у головній програмі.
  - Нагадування: параметр функції – це змінна, якій автоматично присвоюється значення під час виклику функції.

```python
print('adjusted:', adjust(0.9))
print('temperature after call:', temperature)
```

```output
adjusted: 0.01238691049085659
```

```error
Traceback (most recent call last):
  File "/Users/swcarpentry/foo.py", line 8, in <module>
    print('temperature after call:', temperature)
NameError: name 'temperature' is not defined
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Використання локальних і глобальних змінних

Відстежте значення всіх змінних у цій програмі під час її виконання.
(Use '---' as the value of variables before and after they exist.)

```python
limit = 100

def clip(value):
    return min(max(0.0, value), limit)

value = -22.5
print(clip(value))
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Читання повідомлень про помилки

Read the traceback below, and identify the following:

1. How many levels does the traceback have?
2. Як називається файл, у якому сталася помилка?
3. Як називається функція, у якій сталася помилка?
4. В якому рядку цієї функції виникла помилка?
5. Який тип помилки?
6. Яке повідомлення про помилку?

```error
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-2-e4c4cbafeeb5> in <module>()
      1 import errors_02
----> 2 errors_02.print_friday_message()

/Users/ghopper/thesis/code/errors_02.py in print_friday_message()
     13
     14 def print_friday_message():
---> 15     print_message("Friday")

/Users/ghopper/thesis/code/errors_02.py in print_message(day)
      9         "sunday": "Aw, the weekend is almost over."
     10     }
---> 11     print(messages[day])
     12
     13

KeyError: 'Friday'
```

:::::::::::::::  solution

## Рішення

1. Три рівні.

2. `errors_02.py`

3. `print_message`

4. Рядок 11

5. `KeyError`. Ці помилки виникають при спробі звернутися до ключа, який не існує (зазвичай в структурі
   даних на кшталт словника). We can find more information about the `KeyError` and other built-in exceptions
   in the [Python docs](https://docs.python.org/3/library/exceptions.html#KeyError).

6. `KeyError: 'Friday'`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Область змінної - це частина програми, яка може "бачити" цю зміну.

::::::::::::::::::::::::::::::::::::::::::::::::::


