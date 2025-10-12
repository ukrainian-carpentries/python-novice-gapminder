---
title: Списки
teaching: 10
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Поясніть, навіщо програмам потрібні набори значень.
- Напишіть програми, які створюють списки, індексують їх, а також розрізають і змінюють їх через присвоювання значень та виклик методів.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Як зберігати декілька значень?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Список є структурою даних, яка містить в собі багато значень.

- Doing calculations with a hundred variables called `pressure_001`, `pressure_002`, etc.,
  would be at least as slow as doing them by hand.
- Використовуйте список для зберігання багатьох значень разом.
  - Список позначається квадратними дужками `[...]`.
  - Значення розділяються комами `,`.
- Використовуйте `len`, щоб дізнатися, скільки значень у списку.

```python
pressures = [0.273, 0.275, 0.277, 0.275, 0.276]
print('pressures:', pressures)
print('length:', len(pressures))
```

```output
pressures: [0.273, 0.275, 0.277, 0.275, 0.276]
length: 5
```

## Щоб отримати елемент списку, використовуйте його індекс.

- Just like strings.

```python
print('zeroth item of pressures:', pressures[0])
print('fourth item of pressures:', pressures[4])
```

```output
zeroth item of pressures: 0.273
fourth item of pressures: 0.276
```

## Значення елементів списків можна замінити шляхом присвоєння.

- Використовуйте індексний вираз ліворуч від знаку присвоєння, щоб замінити значення.

```python
pressures[0] = 0.265
print('pressures is now:', pressures)
```

```output
Нові значення pressures: [0.265, 0.275, 0.277, 0.275, 0.276]
```

## Додавання елементів до списку подовжує його.

- Щоб додати елементи в кінець списку, використовуйте `list_name.append`.

```python
primes = [2, 3, 5]
print('primes is initially:', primes)
primes.append(7)
print('primes has become:', primes)
```

```output
primes is initially: [2, 3, 5]
primes has become: [2, 3, 5, 7]
```

- `append` is a _method_ of lists.
  - Методи подібні функціям, але вони прив’язані до певних об’єктів.
- Для виклику методів використовується синтаксис `object_name.method_name` .
  - Deliberately resembles the way we refer to things in a library.
- По ходу роботи ми познайомимося з іншими методами, визначеними для списків.
  - Use `help(list)` for a preview.
- `extend` - це метод, схожий на `append`, але він дозволяє об’єднувати два списки.  Наприклад:

```python
teen_primes = [11, 13, 17, 19]
middle_aged_primes = [37, 41, 43, 47]
print('primes is currently:', primes)
primes.extend(teen_primes)
print('primes has now become:', primes)
primes.append(middle_aged_primes)
print('primes has finally become:', primes)
```

```output
primes is currently: [2, 3, 5, 7]
primes has now become: [2, 3, 5, 7, 11, 13, 17, 19]
primes has finally become: [2, 3, 5, 7, 11, 13, 17, 19, [37, 41, 43, 47]]
```

Note that while `extend` maintains the "flat" structure of the list, appending a list to a list means
the last element in `primes` will itself be a list, not an integer. Lists can contain values of any
type; therefore, lists of lists are possible.

## Use `del` to remove items from a list entirely.

- We use `del list_name[index]` to remove an element from a list (in the example, 9 is not a prime number) and thus shorten it.
- `del` - це оператор мови програмування, а не функція і не метод.

```python
primes = [2, 3, 5, 7, 9]
print('primes before removing last item:', primes)
del primes[4]
print('primes after removing last item:', primes)
```

```output
primes before removing last item: [2, 3, 5, 7, 9]
primes after removing last item: [2, 3, 5, 7]
```

## Порожній список не містить жодних значень.

- Use `[]` on its own to represent a list that doesn't contain any values.
  - Порожній список - це "нуль списків."
- Корисно у якості початкової точки для введення значень
  (як ми побачимо в [наступному епізоді](12-for-loops.md)).

## Списки можуть містити значення різних типів.

- Один список може містити числа, рядки та будь-що інше.

```python
goals = [1, 'Створити списки.', 2, 'Вилучити елементи із списків.', 3, 'Змінити списки.']
```

## Рядки символів можна індексувати як списки.

- Отримати окремі символи з рядка символів можна за допомогою індексів у квадратних дужках.

```python
element = 'carbon'
print('zeroth character:', element[0])
print('third character:', element[3])
```

```output
zeroth character: c
third character: b
```

## Рядки символів незмінні.

- Неможливо змінити символи в рядку після його створення.
  - _Immutable_: can't be changed after creation.
  - In contrast, lists are _mutable_: they can be modified in place.
- Python considers the string to be a single value with parts,
  not a collection of values.

```python
element[0] = 'C'
```

```error
TypeError: 'str' object does not support item assignment
```

- Lists and character strings are both _collections_.

## Indexing beyond the end of the collection is an error.

- Python reports an `IndexError` if we attempt to access a value that doesn't exist.
  - This is a kind of [runtime error](04-built-in.md).
  - Cannot be detected as the code is parsed
    because the index might be calculated based on data.

```python
print('99th element of element is:', element[99])
```

```output
IndexError: string index out of range
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Fill in the Blanks

Fill in the blanks so that the program below produces the output shown.

```python
values = ____
values.____(1)
values.____(3)
values.____(5)
print('first time:', values)
values = values[____]
print('second time:', values)
```

```output
first time: [1, 3, 5]
second time: [3, 5]
```

:::::::::::::::  solution

## Рішення

```python
values = []
values.append(1)
values.append(3)
values.append(5)
print('first time:', values)
values = values[1:]
print('second time:', values)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Наскільки є великим зріз?

If `start` and `stop` are both non-negative integers,
how long is the list `values[start:stop]`?

:::::::::::::::  solution

## Рішення

The list `values[start:stop]` has up to `stop - start` elements.  For example,
`values[1:4]` has the 3 elements `values[1]`, `values[2]`, and `values[3]`.
Why 'up to'? As we saw in [episode 2](02-variables.md),
if `stop` is greater than the total length of the list `values`,
we will still get a list back but it will be shorter than expected.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Від рядків до списків і назад.

Given this:

```python
print('string to list:', list('tin'))
print('list to string:', ''.join(['g', 'o', 'l', 'd']))
```

```output
string to list: ['t', 'i', 'n']
list to string: gold
```

1. What does `list('some string')` do?
2. What does `'-'.join(['x', 'y', 'z'])` generate?

:::::::::::::::  solution

## Рішення

1. [`list('some string')`](https://docs.python.org/3/library/stdtypes.html#list) converts a string into a list containing all of its characters.

2. [`join`](https://docs.python.org/3/library/stdtypes.html#str.join) returns a string that is the _concatenation_
   of each string element in the list and adds the separator between each element in the list. This results in
   `x-y-z`. The separator between the elements is the string that provides this method.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Working With the End

Що друкує наступна програма?

```python
element = 'helium'
print(element[-1])
```

1. How does Python interpret a negative index?
2. If a list or string has N elements,
   what is the most negative index that can safely be used with it,
   and what location does that index represent?
3. If `values` is a list, what does `del values[-1]` do?
4. How can you display all elements but the last one without changing `values`?
   (Hint: you will need to combine slicing and negative indexing.)

:::::::::::::::  solution

## Рішення

The program prints `m`.

1. Python interprets a negative index as starting from the end (as opposed to
   starting from the beginning).  The last element is `-1`.

2. The last index that can safely be used with a list of N elements is element
   `-N`, which represents the first element.

3. `del values[-1]` removes the last element from the list.

4. `values[:-1]`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Перехід по списку

Що друкує наступна програма?

```python
element = 'fluorine'
print(element[::2])
print(element[::-1])
```

1. If we write a slice as `low:high:stride`, what does `stride` do?
2. What expression would select all of the even-numbered items from a collection?

:::::::::::::::  solution

## Рішення

The program prints

```python
furn
eniroulf
```

1. `stride` is the step size of the slice.

2. Зріз `1::2` вибирає всі елементи з парними номерами з колекції: він починається з елементу `1` (який є другим елементом, оскільки індексація починається з `0`), продовжується до кінця (оскільки `end` не задано) і використовує розмір кроку `2` (таким чином обираючи кожний другий елемент).

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Границі зрізу

Що друкує наступна програма?

```python
element = 'lithium'
print(element[0:20])
print(element[-1:3])
```

:::::::::::::::  solution

## Рішення

```output
lithium

```

The first statement prints the whole string, since the slice goes beyond the total length of the string.
The second statement returns an empty string, because the slice goes "out of bounds" of the string.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Sort and Sorted

Що друкують ці дві програми?
Простими словами поясніть різницю між `sorted(letters)` and `letters.sort()`.

```python
# Program A
letters = list('gold')
result = sorted(letters)
print('letters is', letters, 'and result is', result)
```

```python
# Program B
letters = list('gold')
result = letters.sort()
print('letters is', letters, 'and result is', result)
```

:::::::::::::::  solution

## Рішення

Program A prints

```output
letters is ['g', 'o', 'l', 'd'] and result is ['d', 'g', 'l', 'o']
```

Program B prints

```output
letters is ['d', 'g', 'l', 'o'] and result is None
```

`sorted(letters)` returns a sorted copy of the list `letters` (the original
list `letters` remains unchanged), while `letters.sort()` sorts the list
`letters` in-place and does not return anything.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Копіювання (чи ні)

Що друкують ці дві програми?
Простими словами поясніть різницю між `new = old` and `new = old[:]`.

```python
# Program A
old = list('gold')
new = old      # simple assignment
new[0] = 'D'
print('new is', new, 'and old is', old)
```

```python
# Program B
old = list('gold')
new = old[:]   # assigning a slice
new[0] = 'D'
print('new is', new, 'and old is', old)
```

:::::::::::::::  solution

## Solution

Program A prints

```output
new is ['D', 'o', 'l', 'd'] and old is ['D', 'o', 'l', 'd']
```

Program B prints

```output
new is ['D', 'o', 'l', 'd'] and old is ['g', 'o', 'l', 'd']
```

`new = old` makes `new` a reference to the list `old`; `new` and `old` point
towards the same object.

`new = old[:]` however creates a new list object `new` containing all elements
from the list `old`; `new` and `old` are different objects.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- A list stores many values in a single structure.
- Щоб отримати елемент списку, використовуйте його індекс.
- Значення елементів списків можна замінити шляхом присвоєння.
- Додавання елементів до списку подовжує його.
- Щоб повністю видалити елементи зі списку, використовуйте `del`.
- Порожній список не містить жодних значень.
- Списки можуть містити значення різних типів.
- Рядки символів можна індексувати як списки.
- Рядки символів незмінні.
- Індексація після кінця колекції є помилкою.

::::::::::::::::::::::::::::::::::::::::::::::::::


