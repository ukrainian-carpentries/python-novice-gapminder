---
title: Стиль програмування
teaching: 15
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Дотримуйтесь основних правил стилю кодування.
- Виконуйте рефакторинг односторінкових програм, щоб зробити їх більш читабельними та обґрунтувати зміни.
- Дотримуйтесь стандартів кодування, прийнятих у спільноті користувачів Python (PEP-8).

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Як я можу зробити свої програми більш читабельними?
- Як більшість програмістів форматують свій код?
- Яким чином програми можуть самостійно перевіряти, що вони працюють правильно?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Стиль кодування

Дотримання послідовного стилю кодування сприяє кращому розумінню коду іншими особами (зокрема нами самими в майбутньому). Код читається набагато частіше, ніж пишеться, і, як стверджує [Дзен Python](https://www.python.org/dev/peps/pep-0020), "читабельність має значення".
Стандартний стиль для Python було запропоновано в одному з перших документів PEP (Python Enhancement Proposal), [PEP8](https://www.python.org/dev/peps/pep-0008).

Варто відзначити такі моменти:

- документуйте ваш код, чітко зазначаючи припущення, внутрішні алгоритми, очікувані вхідні та вихідні дані тощо
- використовуйте зрозумілі, змістовні назви змінних
- для відступів використовуйте пробіли, а _не табуляцію_ (табуляція може призводити до проблем у різних текстових редакторах, операційних системах і системах контролю версій)

## Дотримуйтеся стандартного стилю Python у своєму коді.

- [PEP8](https://www.python. rg/dev/peps/pep-0008):
  рекомендації зі стилю Python, що описують такі аспекти, як назви змінних,
  відступи в коді, структуру операторів `import`
  тощо.
  Дотримання стандарту PEP8 сприяє кращому розумінню коду іншими розробниками Python, а також розумінню того, яким має бути формат їхнього внеску.
- Щоб перевірити свій код на відповідність PEP8, можна використовувати [застосунок pycodestyle](https://pypi.org/project/pycodestyle/, який повідомляє про порушення стилю. Такі інструменти, як [black code formatter](https://github.com/psf/black), можуть автоматично виправити форматування коду відповідно до PEP8 (для Jupyter notebook існує [nb\_black](https://github.com/dnanhkhoa/nb_black)).
- Деякі групи та організації застосовують інші стандарти стилю, відмінні від PEP8. Наприклад, [настанови Google зі стилю Python](https://google.github.io/styleguide/pyguide.html)  містять дещо інші рекомендації. Google створила застосунок під назвою [yapf](https://github.com/google/yapf/), який може допомогти вам форматувати код відповідно до стилю Google або PEP8.
- Щодо стилю кодування, ключовим фактором є _послідовність_. Оберіть стиль для свого проєкту (PEP8, стиль Google або інший) і подбайте про те, щоб ви та інші учасники команди дотримувалися його. Послідовність у проєкті зазвичай впливає сильніше, ніж вибір конкретного стилю. Послідовний стиль полегшує читання та розуміння коду іншими розробниками, а також вами самими в майбутньому.

## Застосовуйте твердження для виявлення внутрішніх помилок.

Твердження (assertions) — простий, але дієвий спосіб переконатися, що контекст виконання коду відповідає вашим очікуванням.

```python
def calc_bulk_density(mass, volume):
    '''Повертає щільність сухої речовини = маса / об'єм.'''
    assert volume > 0
    return mass / volume
```

Якщо твердження має значення `False`, інтерпретатор Python викличе виняток `AssertionError` під час виконання програми. Вихідний код виразу, що спричинив помилку, виводиться як частина повідомлення про помилку. Щоб ігнорувати твердження у вашому коді, запустіть інтерпретатор з опцією '-O' (оптимізація). Твердження повинні містити лише прості перевірки та ніколи не змінювати стан програми. Наприклад, твердження ніколи не повинне містити присвоєння.

## Використовуйте рядки документації (docstrings) для створення вбудованої довідки.

У випадку, коли першим елементом тіла функції є рядок символів, який не присвоєно жодній змінній, Python автоматично прив'язує його до функції у вигляді атрибута. Цей атрибут стає доступним за допомогою вбудованої функції  `help`. Цей рядок, що забезпечує документацію, також відомий як _docstring_.

```python
def average(values):
    "Повертає середнє значення або None, якщо значення не надано."

    if len(values) == 0:
        return None
    return sum(values) / len(values)

help(average)
```

```output
Help on function average in module __main__:

average(values)
    Повертає середнє значення або None, якщо значення не надано.
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Багаторядкові рядки

Often use _multiline strings_ for documentation.
These start and end with three quote characters (either single or double)
and end with three matching characters.

```python
"""Цей рядок охоплює
кілька рядків.

Порожні рядки дозволені."""
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Що буде показано?

Highlight the lines in the code below that will be available as online help.
Are there lines that should be made available, but won't be?
Чи призведе якийсь із рядків до синтаксичної помилки або помилки виконання?

```python
"Find maximum edit distance between multiple sequences."
# This finds the maximum distance between all sequences.

def overall_max(sequences):
    '''Determine overall maximum edit distance.'''

    highest = 0
    for left in sequences:
        for right in sequences:
            '''Avoid checking sequence against itself.'''
            if left != right:
                this = edit_distance(left, right)
                highest = max(highest, this)

    # Report.
    return highest
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Document This

Застосовуйте коментарі для опису та пояснення розділів коду або окремих рядків, що можуть бути неінтуїтивно зрозумілими для інших. Вони є особливо корисними для будь-кого, хто матиме потребу зрозуміти та відредагувати ваш код у майбутньому, зокрема для вас самих.

Застосовуйте рядки документації для опису допустимих вхідних даних та очікуваних вихідних даних методу чи класу, а також їхнього призначення, припущень і передбачуваної поведінки. Docstrings are displayed
when a user invokes the builtin `help` method on your method or class.

Turn the comment in the following function into a docstring
and check that `help` displays it properly.

```python
def middle(a, b, c):
    # Повертає середнє значення для трьох величин.
    # Передбачається, що значення можна порівняти.
    values = [a, b, c]
    values.sort()
    return values[1]
```

:::::::::::::::  solution

## Відповідь

```python
def middle(a, b, c):
    '''Повертає середнє значення для трьох величин.
    Передбачається, що значення можна порівняти.'''
    values = [a, b, c]
    values.sort()
    return values[1]
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Clean Up This Code

1. Read this short program and try to predict what it does.
2. Run it: how accurate was your prediction?
3. Refactor the program to make it more readable.
   Remember to run it after each change to ensure its behavior hasn't changed.
4. Compare your rewrite with your neighbor's.
   What did you do the same?
   What did you do differently, and why?

```python
n = 10
s = 'et cetera'
print(s)
i = 0
while i < n:
    # print('at', j)
    new = ''
    for j in range(len(s)):
        left = j-1
        right = (j+1)%len(s)
        if s[left]==s[right]: new = new + '-'
        else: new = new + '*'
    s=''.join(new)
    print(s)
    i += 1
```

:::::::::::::::  solution

## Відповідь

Here's one solution.

```python
def string_machine(input_string, iterations):
    """
    Takes input_string and generates a new string with -'s and *'s
    corresponding to characters that have identical adjacent characters
    or not, respectively.  Iterates through this procedure with the resultant
    strings for the supplied number of iterations.
    """
    print(input_string)
    input_string_length = len(input_string)
    old = input_string
    for i in range(iterations):
        new = ''
        # iterate through characters in previous string
        for j in range(input_string_length):
            left = j-1
            right = (j+1) % input_string_length  # ensure right index wraps around
            if old[left] == old[right]:
                new = new + '-'
            else:
                new = new + '*'
        print(new)
        # store new string as old
        old = new     

string_machine('et cetera', 10)
```

```output
et cetera
*****-***
----*-*--
---*---*-
--*-*-*-*
**-------
***-----*
--**---**
*****-***
----*-*--
---*---*-
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Follow standard Python style in your code.
- Use docstrings to provide builtin help.

::::::::::::::::::::::::::::::::::::::::::::::::::


