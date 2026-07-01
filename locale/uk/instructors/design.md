---
title: Дизайн уроку
---

:::::::::::::::::::::::::::::::::::::::::  callout

## Де потрібна допомога

**Ми додаємо вправи [нижче](#stage-3-learning-plan) для того, щоб план уроку був більш детальним.
Будемо вдячні за пропозиції (як у вигляді нових готових вправ, так і у вигляді коментарів щодо конкретних вправ, їх порядку та часу виконання).**

::::::::::::::::::::::::::::::::::::::::::::::::::

## Процес розробки

> Поради Майкла Поллана, якби він викладав програмування на R або Python:
>
> 1. Пишіть код.
> 2. Не надто багато.
> 3. Переважно для побудови графіків.
>
> — [Michael Koontz](https://twitter.com/_mikoontz/status/758021742078025728)
> {: .quotation}

Урок розроблено за скороченою версією методу "Розуміння за дизайном".
Основні етапи:

1. Припущення щодо аудиторії, часу тощо.
   (Поточні нотатки також містять певні висновки та рішення в цьому розділі — їх слід переробити.)

2. Бажані результати: загальні цілі, підсумкові оцінювання кожні півдня викладання, що слухачі мають знати та вміти.

3. Навчальний план: кожен епізод містить заголовок з узагальненням матеріалу, що буде розглянуто, оцінку часу на викладання та виконання вправ, а також перелік вправ у вигляді маркованого списку.

## Етап 1: Припущення

- Аудиторія
  - Аспіранти з різних наукових напрямків — від космології до археології
  - Які у минулому обробляли дані в електронних таблицях, а також за допомогою інтерактивних інструментів, таких як SAS
  - Але _не просунулися_ далі CPD (copy-paste-despair / скопіював-вставив-впав в розпач)
- Обмеження
  - Один повний день 09:00-16:30
    - 06:15 час для занять
    - 0:45 обід
    - 0:30 загалом на дві перерви на каву
  - Слухачі використовують власні інсталяції програмного забезпечення на своїх комп'ютерах
    - Можуть використовувати віртуальні машини або хмарні ресурси на розсуд інструктора
    - Але локально інстальоване програмне забезпечення на власному комп'ютері має залишатися варіантом
  - Немає залежності від інших модулів Carpentry
    - Зокрема, не вимагається знання роботи з командним рядком та системи контролю версій
  - Використовується Jupyter Notebook
    - Надійний інструмент, який використовують багато інструкторів
    - Насправді альтернативи просто немає
    - І це означає, що навіть ті, хто вже трохи працював із Python, скоріше за все, дізнаються для себе щось нове
- Мотиваційний приклад
  - Створення двовимірних графіків, придатних для включення до наукових публікацій
  - Цікавий майже всім
  - Робить урок придатним для використання в обох програмах Carpentries (тобто Software Carpentry, Data Carpentry)
    - І це означає, що навіть ті, хто вже трохи працював із Python, скоріше за все, дізнаються для себе щось нове
- Дані
  - Використовувати дані gapminder протягом усього уроку
  - Але розділити на кілька файлів за континентами
    - Щоб зробити виведення результатів з прикладів охайнішим (наприклад, використовувати Australia/New Zealand, що містять лише два рядки)
    - Та показати приклади роботи з кількома наборами даних одночасно
- Зробити фокус на Pandas замість NumPy
  - Зробити урок придатним до використання для Data Carpentry та Software Carpentry
  - Абсолютні початківці, ймовірно, захочуть побачити приклад аналізу даних
  - Водночас слухачі з деяким попереднім досвідом:
    - сприймуть аналіз даних як реальне завдання,
    - та, швидше за все, ще не працювали з Pandas, тому урок буде все одно для них корисним
- Завдання здебільшого _не_ будуть вимагати "написати цей код з нуля"
  - Бажано мати багато коротких вправ, які можна надійно закінчити за відведений час
  - Тому використовуємо питання з множинним вибором, заповнення пропусків, проблеми Парсонса, "змініть цей код" тощо.

## Етап 2: Бажані результати

### Питання

Як мені...

- ...читати табличні дані?
- ...побудувати графік одного набору значень?
- ...створити графік часового ряду?
- ...створити окремий графік для кожного набору даних?
- ...отримати з набору даних додаткові дані для побудови графіку?
- ...писати зрозумілі програми, якими можна скористатися пізніше?

### Навички

Я зможу...

- ...писати короткі скрипти з використанням циклів та умовних операторів.
- ...писати функції з фіксованою кількістю параметрів, які повертають єдиний результат.
- ...імпортувати бібліотеки з використанням псевдонімів та звертатися до їхнього вмісту.
- ...читати та форматувати дані за допомогою Pandas.

### Визначення

Я дізнаюся...

- ...що програма - це частина лабораторного обладнання, яке виконує аналіз
  - Програму потрібно перевіряти/налагоджувати перед/під час використання
  - Програма робить аналіз відтворюваним, придатним для перегляду та поширення
- ...що програми пишуться для людей, а не для комп'ютерів
  - Інформативні імена змінних
  - Модульність коду для зручності його читання та повторного використання
  - Без дублювання коду
  - Пояснюйте, для чого написана програма і як нею користуватися
- ... що програми, якими вони користуються, принципово не відрізняються від тих, які вони пишуть
- ... як призначити значення змінним
- ... що таке цілі числа, числа з плаваючою комою, рядки, масиви NumPy та датафрейми Pandas
- ...як відстежувати виконання циклу `for`
- ...як відстежувати виконання команд `if`/`else`
- ... як створювати списки та отримувати їхні елементи
- ... як створити та індексувати масиви NumPy
- ... як створювати датафрейми Pandas та звертатися до їхніх елементів за індексом
- ... як створити графік, який показує зміни з часом
- ... різниця між визначенням і викликом функції
- ... де знайти документацію до стандартних бібліотек
- ... як дізнатися, що ще пропонує Python для наукових обчислень

## Етап 3: Навчальний план

### Підсумкове оцінювання

- Середина курсу: створення графіка часових рядів для кожного файлу в каталозі.
- Завершення: отримання даних з датафрейма Pandas
  і зображення декількох часових рядів на одному графіку для їх порівняння.

### [Інтерактивний запуск і вихід з програми](../episodes/01-run-quit.md) (9:00)

- Навчання: 15 хв (з урахуванням проблем із налаштуванням)
  - Запустіть Jupyter Notebook, створіть новий документ та вийдіть із Jupyter Notebook.
  - Створіть в блокноті комірки типу Markdown.
  - Створіть та запустіть комірки Python у блокноті.
- Завдання: 0 хв (враховується в навчальний час - без окремої вправи)
  - Створіть список у Markdown
  - What is displayed when several expressions are put in a single cell?
  - Change an existing cell from code to Markdown
  - Візуалізація рівнянь у LaTeX

### [Змінні та присвоєння](../episodes/02-variables.md) (9:15)

- Навчання: 10 хв.
  - Напишіть програми, які присвоюють скалярні значення змінним і виконують обчислення з цими значеннями.
  - Правильно відстежуйте значення змінних у програмах, які використовують скалярне присвоєння.
- Завдання: 10 хв.
  - Відстеження виконання коду, що міняє місцями два значення за допомогою проміжної змінної.
  - Передбачення кінцевих значень змінних після виконання декількох присвоєнь.
  - Що станеться, якщо спробувати звернутися до числа за індексом (а не до списку чи рядку)?
  - Яке ім'я для змінної є кращим: `m`, `min` або `minutes`?
  - Що повертають наступні вирази?

### [Типи даних та їх перетворення](../episodes/03-types-conversion.md) (09:35)

- Навчання: 10 хв.
  - Поясніть, чим цілі числа відрізняються від чисел із плаваючою комою.
  - Поясніть ключові відмінності між числами та символьними рядками.
  - Використовуйте вбудовані функції для перетворень між цілими числами, числами з плаваючою комою та символьними рядками.
- Завдання: 10 хв.
  - Який тип має значення 3.4?
  - Який тип має значення 3.25 + 4?
  - Який тип значення ви б використали для представлення:
    - Кількості днів, які пройшли з початку року.
    - Часу, що минув з початку року.
    - тощо.
  - Як можна використовувати `//` (цілочисельне ділення) та `%` (залишок від ділення)?
  - Що поверне функція `int("3.4")`?
  - Для даних значень типу float, int та string, які з виразів повернуть певний результат?
  - Що, на вашу думку, виведе вираз `1+2j + 3`?

### [Вбудовані функції та Довідка](../episodes/04-built-in.md) (09:55)

- Навчання: 15 хв.
  - Пояснення призначення функцій.
  - Правильний виклик вбудованих функцій Python.
  - Правильні вкладені виклики вбудованих функцій.
  - Використання довідки для зображення документації про вбудовані функції.
  - Правильний опис ситуацій, в яких виникають помилки SyntaxError та NameError.
- Завдання: 10 хв.
  - Пояснення порядку операцій у певному складному виразі.
  - Що поверне кожна вкладена комбінація функцій `min` та `max`?
  - Чому `max` та `min` не повертають `None`, якщо їм не передано аргументів?
  - Враховуючи те, що ми вже вивчили, який індексний вираз поверне останній символ у рядку?

### [Перерва на каву](../episodes/05-coffee.md): 15 min (10:20)

### [Бібліотеки](../episodes/06-libraries.md) (10:35)

- Навчання: 10 хв.
  - Поясніть, що таке бібліотека та для чого програмісти їх створюють і використовують.
  - Пишіть програми, які імпортують і використовують стандартні бібліотеки Python.
  - Знаходьте та читайте документацію про стандартні бібліотеки в інтерактивному режимі (в інтерпретаторі) та онлайн.
- Завдання: 10 хв.
  - Яку функцію зі стандартної математичної бібліотеки можна використати для обчислення квадратного кореня?
  - Яка бібліотека підходить для вибору випадкового значення з набору даних?
  - Якщо `help(math)` видає помилку, що ви забули зробити?
  - Заповніть пропуски в коді нижче, щоб імпорт та програма в цілому запрацювали.

### [Читання табличних данних](../episodes/07-reading-tabular.md) (10:55)

- Навчання: 10 хв.
  - Імпортуйте бібліотеку Pandas.
  - Використайте Pandas, щоб завантажити простий набір даних CSV.
  - Отримайте базову інформацію про датафрейм Pandas.
- Завдання: 10 хв.
  - Зчитайте дані про Північну та Південну Америки та відобразіть їхню підсумкову статистику.
  - Що роблять `.head` та `.tail`?
  - Який (які) рядок (рядки) слід передати в `read_csv`, щоб зчитати файли з інших каталогів?
  - Як можна записати дані у форматі CSV?

### [Датафрейми](../episodes/08-data-frames.md) (11:15)

- Навчання: 15 хв.
  - Виберіть окремі значення з DataFrame Pandas.
  - Select entire rows or entire columns from a dataframe.
  - Виберіть підмножину рядків і стовпців із датафрейму за одну операцію.
  - Виберіть підмножину з датафрейму за єдиним булевим критерієм.
- Завдання: 15 хв.
  - Напишіть вираз для визначення ВВП Сербії на душу населення у 2007 році.
  - What rule governs what is (or isn't) included in numerical and named slices in Pandas?
  - Що робить кожен рядок у наступній короткій програмі?
  - Що роблять `idxmin` та `idxmax`?
  - Напишіть вирази для отримання значення ВВП на душу населення для всіх країн у 1982 році,
    та для усіх країн _після_ 1985 тощо.
  - Given the way its borders have changed since 1900,
    what would you do if asked to create a table of GDP per capita for Poland
    for the Twentieth Century?

### [Побудова графіків](../episodes/09-plotting.md) (11:45)

- Навчання: 15 хв.
  - Create a time series plot showing a single data set.
  - Create a scatter plot showing relationship between two data sets.
- Вправи: 15 хв.
  - Fill in the blanks to plot the minimum GDP per capita over time for European countries.
  - Modify the example to create a scatter plot of GDP per capita in Asian countries.
  - Explain what each argument to `plot` does in the following example.

### [Перерва](../episodes/10-lunch.md) (12:15): 45 min

### [Списки](../episodes/11-lists.md) (13:00)

- Teaching: 10 min
  - Explain why programs need collections of values.
  - Write programs that create flat lists, index them, slice them, and modify them through assignment and method calls.
- Challenges: 10 min
  - Fill in the blanks so that the program produces the output shown.
  - How large are the following slices?
  - What do negative index expressions print?
  - What does a "stride" in a slice do?
  - How do slices treat out-of-range bounds?
  - What are the differences between sorting these two ways?
  - What is the difference between `new = old` and `new = old[:]`?

### [Цикли](../episodes/12-for-loops.md) (13:20)

- Teaching: 10 min
  - Explain what for loops are normally used for.
  - Trace the execution of a simple (unnested) loop and correctly state the values of variables in each iteration.
  - Write for loops that use the Accumulator pattern to aggregate values.
- Challenges: 15 min
  - Is an indentation error a syntax error or a runtime error?
  - Trace which lines of this program are executed in what order.
  - Fill in the blanks in this program so that it reverses a string.
  - Fill in the blanks in this series of examples to get practice accumulating values.
  - Reorder and indent these lines to calculate the cumulative sum of the list values.

### [Looping Over Data Sets](13-looping-data-sets) (13:45)

- Teaching: 5 min
  - Be able to read and write globbing expressions that match sets of files.
  - Use glob to create lists of files.
  - Write for loops to perform operations on files given their names in a list.
- Challenges: 10 min
  - Which filenames are _not_ matched by this glob expression?
  - Modify this program so that it prints the number of records in the shortest file.
  - Write a program that reads and plots all of the regional data sets.

### [Writing Functions](14-writing-functions) (14:00)

- Teaching: 10 min
  - Explain and identify the difference between function definition and function call.
  - Write a function that takes a small, fixed number of arguments and produces a single result.
- Challenges: 15 min
  - This code defines and calls a function - what does it print when run?
  - Explain why this short program prints things in the order it does.
  - Fill in the blanks to create a function that finds the minimum value in a data file.
  - Fill in the blanks to create a function that finds the first negative value in a list.
    What does your function do if the list is empty?
  - Why is it sometimes useful to pass arguments by naming the corresponding parameters?
  - Fill in the blanks and turn this short piece of code into a function.

### [Variable Scope](15-scope) (14:25)

- Teaching: 10 min
  - Identify local and global variables.
  - Identify parameters as local variables.
  - Read a traceback and determine the file, function, and line number on which the error occurred.
- Challenges: 10 min
  - Trace the changes to the values in this program,
    being careful to distinguish local from global values.

### [Coffee](16-coffee) (14:45): 15 min

### [Conditionals](17-conditionals) (15:00)

- Teaching: 10 min
  - Correctly write programs that use if and else statements and simple Boolean expressions (without logical operators).
  - Trace the execution of unnested conditionals and conditionals inside loops.
- Challenges: 15 min
  - Trace the execution of this conditional statement.
  - Fill in the blanks so that this function replaces negative values with zeroes.
  - Modify this program so that it only processes files with fewer than 50 records.
  - Modify this program so that it always finds the largest and smallest values in a list
    no matter what the list's values are.

### [Стиль програмування](../episodes/18-style.md) (15:25)

- Teaching: 15 min
  - How can I make my programs more readable?
  - How do most programmers format their code?
  - How can programs check their own operation?
- Challenges: 15 min
  - Which lines in this code will be available as online help?
  - Turn the comments in this program into docstrings.
  - Rewrite this short program to be more readable.

### [Підведення підсумків](../episodes/19-wrap.md) (15:55)

- Teaching: 20 min
  - Name and locate scientific Python community sites for software, workshops, and help.
- Challenges: 0 min
  - None.

### [Feedback](../episodes/20-feedback.md) (16:15)

- Teaching: 0 min
- Challenges: 15 min
  - Collect feedback

### Finish (16:30)


