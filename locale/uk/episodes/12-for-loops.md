---
title: Цикли for
teaching: 10
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Поясніть, для чого зазвичай використовуються цикли for.
- Проаналізуйте виконання простого (невкладеного) циклу та правильно вкажіть значення змінних у кожній ітерації.
- Напишіть цикли for, які використовують шаблон накопичувача для агрегування значень.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Як змусити програму робити багато речей?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Цикл for виконує команди один раз для кожного значення в колекції.

- Doing calculations on the values in a list one by one
  is as painful as working with `pressure_001`, `pressure_002`, etc.
- A _for loop_ tells Python to execute some statements once for each value in a list,
  a character string,
  or some other collection.
- "для кожного елемента в цій групі виконайте ці операції"

```python
for number in [2, 3, 5]: 
     print(number)
```

- Цей цикл `for` є еквівалентним наступному:

```python
print(2) 
print(3) 
print(5)
```

- І результат циклу `for` є таким:

```output
2
3
5
```

## Цикл `for` складається з колекції, змінної циклу та тіла циклу.

```python
for number in [2, 3, 5]: 
    print(number)
```

- Колекція `[2, 3, 5]` є те, що опрацьовується в циклі.
- Тіло циклу, `print(number)`, визначає, що робити для кожного значення в колекції.
- Змінна циклу, `number`, змінюється для кожної ітерації циклу.
  - "Поточне значення".

## Перший рядок циклу `for` має закінчуватися двокрапкою, а тіло циклу має бути з відступом.

- Двокрапка в кінці першого рядка вказує на початок блоку операторів.
- Python використовує відступ, а не `{}` або `begin`/`end`, щоб показати _вкладеність_.
  - Будь-який послідовний відступ є допустимим, але майже усі використовують чотири пробіли.

```python
for number in [2, 3, 5]:
print(number)
```

```error
IndentationError: expected an indented block
```

- Відступи у Python завжди важливі.

```python
firstName = "Jon"
  lastName = "Smith"
```

```error
  File "<ipython-input-7-f65f2962bf9c>", line 2
    lastName = "Smith"
    ^
IndentationError: unexpected indent
```

- Ця помилка може бути виправлена шляхом видалення зайвих пробілів
  на початку другого рядку.

## Змінні циклу можна називати як завгодно.

- Як і всі інші змінні, змінні циклу:
  - Створюються за потреби
  - Не несуть смислового навантаження: їх імена можуть бути будь-якими.

```python
for kitten in [2, 3, 5]: 
    print(kitten)
```

## Тіло циклу може містити багато операторів.

- Але жоден цикл не повинен мати довжину більше кількох рядків.
- Людям важко запам’ятати великі фрагменти коду.

```python
primes = [2, 3, 5]
for p in primes: 
    squared = p ** 2 
    cubed = p ** 3 
    print(p, squared, cubed)
```

```output
2 4 8 
3 9 27 
5 25 125
```

## Використовуйте `range` для перебору послідовності чисел.

- Вбудована функція [`range`](https://docs.python.org/3/library/stdtypes.html#range) створює послідовність чисел.
  - _Не_ список: номери виробляються на вимогу,
    щоб зробити цикл у великих діапазонах більш ефективним.
- `range(N)` є набором чисел 0..N-1
  - Точні індекси списку або рядка символів довжиною N

```python
print('a range is not a list: range(0, 3)')
for number in range(0, 3):
    print(number)
```

```output
a range is not a list: range(0, 3)
0
1
2
```

## The Accumulator pattern turns many values into one.

- A common pattern in programs is to:
  1. Initialize an _accumulator_ variable to zero, the empty string, or the empty list.
  2. Update the variable with values from a collection.

```python
# Sum the first 10 integers.
total = 0
for number in range(10):
   total = total + (number + 1)
print(total)
```

```output
55
```

- Read `total = total + (number + 1)` as:
  - Add 1 to the current value of the loop variable `number`.
  - Add that to the current value of the accumulator variable `total`.
  - Assign that to `total`, replacing the current value.
- We have to add `number + 1` because `range` produces 0..9, not 1..10.

:::::::::::::::::::::::::::::::::::::::  challenge

## Classifying Errors

Is an indentation error a syntax error or a runtime error?

:::::::::::::::  solution

## Solution

An IndentationError is a syntax error. Programs with syntax errors cannot be started.
A program with a runtime error will start but an error will be thrown under certain conditions.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Tracing Execution

Create a table showing the numbers of the lines that are executed when this program runs,
and the values of the variables after each line is executed.

```python
total = 0
for char in "tin":
    total = total + 1
```

:::::::::::::::  solution

## Solution

| Line no | Variables            |
| ------- | -------------------- |
| 1       | total = 0            |
| 2       | total = 0 char = 't' |
| 3       | total = 1 char = 't' |
| 2       | total = 1 char = 'i' |
| 3       | total = 2 char = 'i' |
| 2       | total = 2 char = 'n' |
| 3       | total = 3 char = 'n' |

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Reversing a String

Fill in the blanks in the program below so that it prints "nit"
(the reverse of the original character string "tin").

```python
original = "tin"
result = ____
for char in original:
    result = ____
print(result)
```

:::::::::::::::  solution

## Solution

```python
original = "tin"
result = ""
for char in original:
    result = char + result
print(result)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Practice Accumulating

Fill in the blanks in each of the programs below
to produce the indicated result.

```python
# Total length of the strings in the list: ["red", "green", "blue"] => 12
total = 0
for word in ["red", "green", "blue"]:
    ____ = ____ + len(word)
print(total)
```

:::::::::::::::  solution

## Solution

```python
total = 0
for word in ["red", "green", "blue"]:
    total = total + len(word)
print(total)
```

:::::::::::::::::::::::::

```python
# List of word lengths: ["red", "green", "blue"] => [3, 5, 4]
lengths = ____
for word in ["red", "green", "blue"]:
    lengths.____(____)
print(lengths)
```

:::::::::::::::  solution

## Solution

```python
lengths = []
for word in ["red", "green", "blue"]:
    lengths.append(len(word))
print(lengths)
```

:::::::::::::::::::::::::

```python
# Concatenate all words: ["red", "green", "blue"] => "redgreenblue"
words = ["red", "green", "blue"]
result = ____
for ____ in ____:
    ____
print(result)
```

:::::::::::::::  solution

## Solution

```python
words = ["red", "green", "blue"]
result = ""
for word in words:
    result = result + word
print(result)
```

:::::::::::::::::::::::::

**Create an acronym:** Starting from the list `["red", "green", "blue"]`, create the acronym `"RGB"` using
a for loop.

**Hint:** You may need to use a string method to properly format the acronym.

:::::::::::::::  solution

## Solution

```python
acronym = ""
for word in ["red", "green", "blue"]:
    acronym = acronym + word[0].upper()
print(acronym)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Cumulative Sum

Reorder and properly indent the lines of code below
so that they print a list with the cumulative sum of data.
The result should be `[1, 3, 5, 10]`.

```python
cumulative.append(total)
for number in data:
cumulative = []
total = total + number
total = 0
print(cumulative)
data = [1,2,2,5]
```

:::::::::::::::  solution

## Solution

```python
total = 0
data = [1,2,2,5]
cumulative = []
for number in data:
    total = total + number
    cumulative.append(total)
print(cumulative)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Identifying Variable Name Errors

1. Read the code below and try to identify what the errors are
   _without_ running it.
2. Run the code and read the error message.
   What type of `NameError` do you think this is?
   Is it a string with no quotes, a misspelled variable, or a
   variable that should have been defined but was not?
3. Fix the error.
4. Repeat steps 2 and 3, until you have fixed all the errors.

```python
for number in range(10):
    # use a if the number is a multiple of 3, otherwise use b
    if (Number % 3) == 0:
        message = message + a
    else:
        message = message + "b"
print(message)
```

:::::::::::::::  solution

## Solution

- Python variable names are case sensitive: `number` and `Number` refer to different variables.
- The variable `message` needs to be initialized as an empty string.
- We want to add the string `"a"` to `message`, not the undefined variable `a`.

```python
message = ""
for number in range(10):
    # use a if the number is a multiple of 3, otherwise use b
    if (number % 3) == 0:
        message = message + "a"
    else:
        message = message + "b"
print(message)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Identifying Item Errors

1. Read the code below and try to identify what the errors are
   _without_ running it.
2. Run the code, and read the error message. What type of error is it?
3. Fix the error.

```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
print('My favorite season is ', seasons[4])
```

:::::::::::::::  solution

## Solution

This list has 4 elements and the index to access the last element in the list is `3`.

```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
print('My favorite season is ', seasons[3])
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- A _for loop_ executes commands once for each value in a collection.
- A `for` loop is made up of a collection, a loop variable, and a body.
- The first line of the `for` loop must end with a colon, and the body must be indented.
- Indentation is always meaningful in Python.
- Loop variables can be called anything (but it is strongly advised to have a meaningful name to the looping variable).
- The body of a loop can contain many statements.
- Use `range` to iterate over a sequence of numbers.
- The Accumulator pattern turns many values into one.

::::::::::::::::::::::::::::::::::::::::::::::::::


