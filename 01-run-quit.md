---
title: Запуск та завершення роботи
teaching: 15
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives

- Запуск серверу JupyterLab.
- Створення нового скрипту Python.
- Створення блокноту Jupyter.
- Завершення роботи сервера JupyterLab.
- Розуміння різниці між скриптом Python і блокнотом Jupyter.
- Створення в блокноті комірок типу Markdown.
- Створення та виконання в блокноті комірок Python.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Як запустити програми Python?

::::::::::::::::::::::::::::::::::::::::::::::::::

Для роботи з Python, протягом цього семінару ми будемо використовувати \[блокноти Jupyter]\[jupyter] у середовищі [JupyterLab][jupyterlab]. Блокноти Jupyter широко застосовуються з метою аналізу та візуалізації даних, а також є зручним інструментальним засобом для запуску коду на Python в інтерактивному режимі, де ми можемо легко переглядати результати його виконання, та ділитися нашим кодом з іншими.

Існують й інші способи редагування, організації та виконання коду. Розробники програмного забезпечення часто використовують інтегроване середовище розробки (IDE), подібне до [PyCharm](https://www.jetbrains. om/pycharm/) або [Visual Studio Code](https://code.visualstudio.com/) або текстові редактори такі як Vim або Emacs, щоб створити та відредагувати свої програми Python. Після редагування та збереження ваших програм Python ви можете виконувати ці програми в самому IDE або безпосередньо в командному рядку. На відміну від цього, блокноти Jupyter дозволяють відразу переглянути результати нашого Python коду.

JupyterLab має декілька інших зручних функцій:

- Ви можете легко вводити, редагувати, копіювати та вставляти блоки коду.
- Автодоповнення за допомогою клавіші Tab дозволяє легко отримувати доступ до назв об'єктів, які ви використовуєте.
- Дозволяє легко доповнювати свій код посиланнями, текстом різного розміру, маркерами тощо, щоб зробити його доступнішим для вас і ваших колег.
- Дозволяє розміщувати графічні елементи безпосередньо поруч із кодом, який їх створює,
  щоб продемонструвати повну історію аналізу даних.

Кожен блокнот містить одну або кілька комірок, що містять код, текст або зображення.

## Початок роботи з JupyterLab

JupyterLab є сервером застосунків із вебінтерфейсом користувача від [Project Jupyter][jupyter], що
дозволяє працювати з документами та іншими застосунками, такими як блокноти Jupyter, текстові редактори, термінали, і навіть спеціальні компоненти, гнучким, інтегрованим і розширюваним способом. JupyterLab потребує досить сучасний браузер (в ідеалі – поточна версія Chrome, Safari або Firefox); Internet Explorer версії 9 і нижче _не_ підтримується.

JupyterLab є частиною інсталяційного пакета Anaconda Python. Якщо ви не встановили дистрибутив Anaconda Python, дивіться інструкції щодо процесу інсталяції [тут](../learners/setup.md).

На цьому уроці ми запустимо JupyterLab локально на наших власних пристроях, тому для цього підключення до Інтернету буде потрібно лише на початку для завантаження та встановлення середовищ розробки Anaconda та JupyterLab

- Запустіть сервер JupyterLab на вашому комп'ютері
- Використовуйте веббраузер для відкриття спеціальної локальної URL-адреси для з'єднання з сервером JupyterLab
- The JupyterLab server does the work and the web browser renders the result
- Type code into the browser and see the results after your JupyterLab server has finished executing your code

:::::::::::::::::::::::::::::::::::::::::  callout

## JupyterLab? А чому не Jupyter Notebook?

JupyterLab є [подальшим кроком в еволюції Jupyter Notebook](https://jupyterlab.readthedocs.io/en/stable/getting_started/overview.html#overview).
Якщо ви використовували Jupyter Notebook раніше, то ви добре зрозумієте діапазон можливостей JupyterLab.

Досвідчені користувачі блокнотів Jupyter, зацікавлені у більш детальному обговоренні схожостей і відмінностей між інтерфейсами JupyterLab і Jupyter Notebook, можуть знайти більше інформації у [документації з інтерфейсу користувача JupyterLab][jupyterlab-ui].

::::::::::::::::::::::::::::::::::::::::::::::::::

## Початок роботи з JupyterLab

Ви можете запустити сервер JupyterLab через командний рядок або через застосунок, що має назву 'Anaconda Navigator'. JupyterLab є частиною інсталяційного пакета Anaconda Python.

### macOS - командний рядок

Для запуску сервера JupyterLab вам потрібно отримати доступ до командного рядка через Terminal.
Існує два способи відкрити термінал на Mac.

1. In your Applications folder, open Utilities and double-click on Terminal
2. Натисніть <kbd>Command</kbd> + <kbd>spacebar</kbd> для запуску Spotlight. Введіть `Terminal`, а потім двічі клацніть на результаті пошуку або натисніть <kbd>Enter</kbd>

Після запуску Terminal введіть команду для запуску сервера JupyterLab.

```bash
$ jupyter lab
```

### Користувачі Windows - Командний рядок

Для запуску сервера JupyterLab вам потрібен застосунок Anaconda Prompt.

Press <kbd>Windows Logo Key</kbd> and search for `Anaconda Prompt`, click the result or press enter.

Після запуску Anaconda Prompt введіть команду:

```bash
$ jupyter lab
```

### Anaconda Navigator

Для запуску серверу JupyterLab з Anaconda Navigator ви маєте спочатку [запустити Anaconda Navigator (натисніть для докладних інструкцій з macOS, Windows та Linux)](https://docs.anaconda.com/free/navigator/getting-started/#navigator-starting-navigator). Ви можете виконати пошук Anaconda Navigator через Spotlight на macOS (<kbd>Command</kbd> + <kbd>spacebar</kbd>), скористатися функцією пошуку Windows (<kbd>ключ Windows Logo</kbd>) або відкривши термінал та виконавши команду `anaconda-navigator` у командному рядку.

Після того, як ви запустили Anaconda Navigator, натисніть кнопку `Launch` під JupyterLab. Можливо, вам знадобиться продивитись список донизу, аби знайти її.

Нижче наведено скриншот сторінки Anaconda Navigator, схожої на ту, яка має відкриватися для macOS або Windows.

<p align='center'>
  <img alt="Anaconda Navigator landing page" src="fig/0_anaconda_navigator_landing_page.png" width="750"/>
</p>

Нижче наведено скриншот екрана стартової сторінки JupyterLab, схожої на ту, яка має відкритися у вашому веббраузері за замовчуванням після запуску сервера JupyterLab в операційній системі macOS або Windows.

<p align='center'>
  <img alt="JupyterLab landing page" src="fig/0_jupyterlab_landing_page.png" width="750"/>
</p>

## Інтерфейс JupyterLab

JupyterLab має багато функцій, які можна знайти в традиційних інтегрованих середовищах розробки (IDE), але його особливістю є забезпечення гнучких "будівельних блоків" для інтерактивних дослідницьких обчислень.

[Інтерфейс JupyterLab][jupyterlab-ui] складається з панелі меню, лівої бічної панелі (що згортається за потреби), і основної робочої області, яка містить вкладки з документами та різними застосунками JupyterLab.

### Панель меню

Панель меню у верхній частині вікна JupyterLab містить меню верхнього рівня, яке зображує різні дії доступні в JupyterLab разом із їхніми комбінаціями клавіш (де це можливо). Наступні пункти меню наявні за замовчуванням.

- **File:** Дії, пов’язані з файлами та каталогами, такі як _New_, _Open_, _Close_, _Save_ тощо. Меню _File_ також містить дію _Shut Down_, яка застосовується для завершення роботи сервера JupyterLab.
- **Edit:** Дії, пов’язані з редагуванням документів та іншими видами діяльності, такими як _Undo_, _Cut_, _Copy_, _Paste_ тощо.
- **View:** Дії, які змінюють зовнішній вигляд інтерфейсу JupyterLab.
- **Run:** Дії для запуску коду в різних застосунках, таких як Jupyter Notebook та командний рядок (розглянуто нижче).
- \*\* Kernel:\*\* Дії щодо управління ядрами. Ядра у Jupyter будуть детально описані нижче.
- **Tabs:** Список відкритих документів та застосунків у робочій області.
- **Settings:** За допомогою цього меню можна налаштувати загальні параметри JupyterLab. Окрім того, у ньому також є опція _Advanced Settings Editor_, яка забезпечує більш детальний контроль параметрів і опцій для конфігурації JupyterLab.
- **Help:** Список посилань на довідку JupyterLab та інші ресурси.

:::::::::::::::::::::::::::::::::::::::::  callout

## Ядра

The JupyterLab [docs](https://jupyterlab.readthedocs.io/en/stable/user/documents_kernels.html)
define kernels as "separate processes started by the server that runs your code in different programming languages and environments."
When we open a Jupyter Notebook, that starts a kernel - a process - that is going to run the code.
In this lesson, we'll be using the Jupyter ipython kernel which lets us run Python 3 code interactively.

Using other Jupyter [kernels for other programming languages](https://github.com/jupyter/jupyter/wiki/Jupyter-kernels) would let us
write and execute code in other programming languages in the same JupyterLab interface, like R, Java, Julia, Ruby, JavaScript, Fortran,
etc.

::::::::::::::::::::::::::::::::::::::::::::::::::

A screenshot of the default Menu Bar is provided below.

<p align='center'>   <img alt="JupyterLab Menu Bar" src="fig/0_jupyterlab_menu_bar.png" width="750"/>
</p>

### Ліва бічна панель

The left sidebar contains a number of commonly used tabs, such as a file browser (showing the
contents of the directory where the JupyterLab server was launched), a list of running kernels
and terminals, the command palette, and a list of open tabs in the main work area. A screenshot of
the default Left Side Bar is provided below.

<p align='center'>   <img alt="JupyterLab Left Side Bar" src="fig/0_jupyterlab_left_side_bar.png" width="250"/>
</p>

Ліву бічну панель можна згорнути або розгорнути вибравши пункт “Show Left Sidebar” у меню View, або натиснувши на активну вкладку бічної панелі.

### Основна робоча область

Основна робоча область в JupyterLab дозволяє упорядковувати документи (блокноти, текстові файли та ін.)
and other activities (terminals, code consoles, etc.) into panels of tabs that can be resized or
subdivided. A screenshot of the default Main Work Area is provided below.

Якщо Ви не бачите вкладку Launcher на панелі запуску, натисніть синій плюс під "File" та "Edit" у панелі меню, і ця вкладка з'явиться.

<p align='center'>   <img alt="JupyterLab Main Work Area" src="fig/0_jupyterlab_main_work_area.png" width="750"/>
</p>

Drag a tab to the center of a tab panel to move the tab to the panel. Subdivide a tab panel by
dragging a tab to the left, right, top, or bottom of the panel. The work area has a single current
activity. Вкладка для поточної дії позначена кольоровою верхньою рамкою (за замовчуванням - синьою).

## Створення скрипту Python

- Щоб почати писати нову програму на Python, натисніть піктограму текстового файлу під заголовком _Other_ на вкладці Launcher (Запуск) головної робочої області.
  - Можна також створити новий текстовий файл, якщо обрати _New -> Text File_ у меню _File_ на панелі меню.
- Щоб перетворити цей звичайний текстовий файл на програму Python, виберіть дію _Save File As_ у меню _File_ на панелі меню та надайте новому текстовому файлу назву, яка закінчується розширенням `.py`.
  - Розширення `.py` повідомляє всім (операційній системі включно), що цей текстовий файл є програмою Python.
  - Це умовність, а не вимога.

## Створення блокноту Jupyter

Щоб відкрити новий блокнот, натисніть піктограму Python 3 під заголовком _Notebook_ на вкладці Launcher в у головній робочій області. Ви також можете створити новий блокнот, обравши _New -> Notebook_ у меню _File_ на панелі меню.

Додаткові зауваження щодо блокнотів Jupyter.

- Файли, створені в Jupyter Notebook, мають розширення `.ipynb`, щоб відрізнити їх від програм на Python, створених як звичайний текстовий файл.
- Блокноти можна експортувати як скрипти Python, які можна запускати з командного рядка.

Below is a screenshot of a Jupyter notebook running inside JupyterLab. If you are interested in
more details, then see the [official notebook documentation][jupyterlab-notebook-docs].

<p align='center'>   <img alt="Example Jupyter Notebook" src="fig/0_jupyterlab_notebook_screenshot.png" width="750"/>
</p>

:::::::::::::::::::::::::::::::::::::::::  callout

## Як це зберігається

- Файл блокноту зберігається у форматі JSON.
- Подібно до вебсторінки, те, що зберігається, відрізняється від того, що ви бачите у своєму браузері.
- But this format allows Jupyter to mix source code, text, and images, all in one file.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Упорядкування документів в панелях вкладок

У головній робочій області JupyterLab ви можете впорядковувати документи на панелі вкладок. Нижче наведено приклад з [офіційної документації][jupyterlab].

<p align='center'>   <img alt="Multi-panel JupyterLab" src="fig/0_multipanel_jupyterlab_screenshot.png" width="750"/>
</p>

Спочатку створіть текстовий файл, консоль Python, та вікно терміналу і розташуйте їх у три
панелі в основній робочій області. Далі створіть блокнот, вікно терміналу, та текстовий файл і розподіліть їх на три панелі в основній робочій зоні. Нарешті, створіть власну комбінацію панелей і вкладок. Яка, на вашу думку, комбінація панелей та вкладок буде найбільш корисною для вашого робочого процесу?

:::::::::::::::  solution

## Рішення

Після створення необхідних вкладок ви можете перетягнути одну з них в центр панелі для переміщення вкладки на панель; потім ви можете розділити панель, перетягнувши вкладку ліворуч, праворуч, вгору або до низу панелі.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Code vs. Text

Jupyter дозволяє змішувати код і текст у різних типах блоків, які називаються комірками. We often use the term
"code" to mean "the source code of software written in a language such as Python".
A "code cell" in a Notebook is a cell that contains software;
a "text cell" is one that contains ordinary prose written for human beings.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Jupyter Notebook має командний режим та режим редагування.

- If you press <kbd>Esc</kbd> and <kbd>Return</kbd> alternately, the outer border of your code cell will change from gray to blue.
- Існують сірий - **Command** (командний) та синій - **Edit** (редагування) режими вашого блокноту.
- Command mode allows you to edit notebook-level features, and Edit mode changes the content of cells.
- В командному режимі (esc/сірий),
  - Клавіша <kbd>b</kbd> створює нову комірку нижче поточної обраної комірки.
  - Клавіша <kbd>a</kbd> створює одну комірку вище поточної.
  - Клавіша <kbd>x</kbd> видаляє поточну комірку.
  - Клавіша <kbd>z</kbd> скасовує вашу останню операцію з коміркою (це може бути операція видалення, створення тощо).
- Усі дії можна виконувати за допомогою меню, але є багато комбінацій клавіш для прискорення процесу.

:::::::::::::::::::::::::::::::::::::::  challenge

## Командний режим або режим редагування

In the Jupyter notebook page are you currently in Command or Edit mode?\
Switch between the modes.
Use the shortcuts to generate a new cell.
Use the shortcuts to delete a cell.
Use the shortcuts to undo the last cell operation you performed.

:::::::::::::::  solution

## Рішення

Командний режим має сіру рамку, а режим редагування — синю.
Використовуйте <kbd>Esc</kbd> та <kbd>Return</kbd> для перемикання режимів.
Ви маєте бути в командному режимі (Натисніть <kbd>Esc</kbd> якщо ваша комірка синя).  Введіть <kbd>b</kbd> або <kbd>a</kbd>.
Ви маєте бути в командному режимі (Натисніть <kbd>Esc</kbd> якщо ваша клітинка синя).  Введіть <kbd>x</kbd>.
Ви маєте бути в командному режимі (Натисніть <kbd>Esc</kbd> якщо ваша комірка синя).  Введіть <kbd>z</kbd>.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

### Використовуйте клавіатуру та мишу для виділення та редагування комірок.

- Якщо натиснути клавішу <kbd>Return</kbd>, рамка стане синьою та ввімкнеться режим редагування, що дозволяє введення команди в комірку.
- Якщо є необхідність введення кількох рядків кода в одну клітинку, то натискання клавіші <kbd>Return</kbd> в режимі редагування (синя рамка) переміщує курсор на наступний рядок в комірці, як у текстовому редакторі.
- Якщо нам потрібно запустити код, що знаходиться в комірці, нам потрібен інший спосіб повідомити про це Notebook.
- Одночасне натискання клавіш <kbd>Shift</kbd> + <kbd>Return</kbd> призведе до виконання вмісту комірки.
- Зверніть увагу, що клавіші <kbd>Return</kbd> та <kbd>Shift</kbd> розташовані поруч на клавіатурі справа.

### Jupyter Notebook підтримує мову розмітки текстів Markdown.

- Notebooks can also render [Markdown][markdown].
  - A simple plain-text format for writing lists, links,
    and other things that might go into a web page.
  - Власне, це підмножина HTML, яка виглядає у стилі старомодного електронного листа.
- Перетворіть поточну комірку на комірку Markdown, увійшовши в командний режим (<kbd>Esc</kbd>/gray) та натиснувши клавішу <kbd>M</kbd>.
- Позначка `In [ ]:` зникне, щоб показати, що це вже не комірка коду, і ви зможете писати текст у форматі Markdown.
- Перетворіть поточну комірку на комірку з кодом, увійшовши в командний режим (<kbd>Esc</kbd>/gray) та натиснувши клавішу <kbd>y</kbd>.

### Markdown does most of what HTML does.

Table: Showing some markdown syntax and its rendered output.

+---------------------------------------+------------------------------------------------+
\| Код Markdown                  | Виведення                               |
+=======================================+================================================+
+---------------------------------------+------------------------------------------------+
\| `                                  | <p></p>                                        | | *   Використовуйте зірочки                     | -   Використовуйте зірочки                     |           | *   для створення                         | -   для створення                                  | | *   маркованих списків.                     | -   bullet lists.                              |
|`                                   |                                                |
+---------------------------------------+------------------------------------------------+
+---------------------------------------+------------------------------------------------+
\| `                                  | <p></p>                                        | | 1.   Use numbers                      | 1.   Use numbers                               | | 1.   to create                        | 2.   to create                                 | | 1.   bullet lists.                    | 3.   нумеровані списки.                           |
|`                                   |                                                |
+---------------------------------------+------------------------------------------------+
+---------------------------------------+------------------------------------------------+
\| `                                  | <p></p>                                        | | *  You can use indents                | - You can use indents                          | |   *  To create sublists               |   - To create sublists                         | |   *  of the same type                 |   - of the same type                           | | *  Or sublists                        | - Or sublists                                  | |   1. Of different                     |   1. Of different                              | |   1. types                            |   2. types                                     |
|`                                   |                                                |
+---------------------------------------+------------------------------------------------+
+---------------------------------------+------------------------------------------------+
\| `                                  | <p></p>                                        | | # A Level-1 Heading                   | ## A Level-1 Heading                           |
|`                                   |                                                |
+---------------------------------------+------------------------------------------------+
+---------------------------------------+------------------------------------------------+
\| `                                  | <p></p>                                        | | ## A Level-2 Heading (etc.)           | ### A Level-2 Heading (etc.)                   |
|`                                   |                                                |
+---------------------------------------+------------------------------------------------+
+---------------------------------------+------------------------------------------------+
\| `                                  | <p></p>                                        | | Line breaks                           | Line breaks                                    | | don't matter.                         | don't matter.                                  | |                                       |                                                | | But blank lines                       | But blank lines                                | | create new paragraphs.                | create new paragraphs.                         |
|`                                   |                                                |
+---------------------------------------+------------------------------------------------+
+---------------------------------------+------------------------------------------------+
\| ``                                  | <p></p>                                        | | [Links](http://software-carpentry.org)| [Links](https://software-carpentry.org)        | | are created with `[...](...)`.        | are created with `[...](...)`.                 | | Or use [named links][data-carp].      | Or use [named links][data_carpentry].          | |                                       |                                                | | [data-carp]: http://datacarpentry.org |                                                |
|``                                   |                                                |
+---------------------------------------+------------------------------------------------+

:::::::::::::::::::::::::::::::::::::::  challenge

## Створення списків в Markdown

Create a nested list in a Markdown cell in a notebook that looks like this:

1. Знайти фінансування.
2. Виконати роботу.

- Провести експеримент.
- Зібрати дані.
- Провести аналіз.

3. Написати статтю.
4. Опублікувати.

:::::::::::::::  solution

## Рішення

Це завдання поєднує як нумерований, так і маркований списки.
Зверніть увагу, що маркований список має відступ на 2 пробіли, щоб він не збігався з елементами нумерованого списку.

```
1.  Get funding.
2.  Do work.
    *   Design experiment.
    *   Collect data.
    *   Analyze.
3.  Write up.
4.  Publish.
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Більше математики

Що зображується, коли виконується комірка Python в блокноті, що містить декілька обчислень?
For example, what happens when this cell is executed?

```python
7 * 3
2 + 1
```

:::::::::::::::  solution

## Рішення

Python повертає результат останнього розрахунку.

```python
3
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Change an Existing Cell from Code to Markdown

What happens if you write some Python in a code cell
and then you switch it to a Markdown cell?
Наприклад, напишіть наступний вираз в комірці коду:

```python
x = 6 * 7 + 12
print(x)
```

Потім запустіть цей код в комірці за допомогою <kbd>Shift</kbd>\+<kbd>Return</kbd>, щоб переконатися, що ця комірка працює як комірка коду.
Тепер поверніться до комірки та натисніть <kbd>Esc</kbd>, а потім <kbd>m</kbd>, щоб перемкнути комірку на Markdown і "запустити" її за допомогою <kbd>Shift</kbd>\+<kbd>Return</kbd>.
Що сталося, і як це може бути корисним?

:::::::::::::::  solution

## Рішення

Код Python розглядається як текст Markdown.
Рядки виглядають так, ніби вони є частиною одного суміжного абзацу.
This could be useful to temporarily turn on and off cells in notebooks that get used for multiple purposes.

```python
x = 6 * 7 + 12 print(x)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Рівняння

Standard Markdown (such as we're using for these notes) won't render equations,
but the Notebook will.
Створіть нову комірку Markdown і введіть наступне:

```
$\sum_{i=1}^{N} 2^{-i} \approx 1$
```

(Мабуть, це легше скопіювати та вставити.)
Що зображається?
What do you think the underscore, `_`, circumflex, `^`, and dollar sign, `$`, do?

:::::::::::::::  solution

## Рішення

The notebook shows the equation as it would be rendered from LaTeX equation syntax.
The dollar sign, `$`, is used to tell Markdown that the text in between is a LaTeX equation.
If you're not familiar with LaTeX,  underscore, `_`, is used for subscripts and circumflex, `^`, is used for superscripts.
A pair of curly braces, `{` and `}`, is used to group text together so that the statement `i=1` becomes the subscript and `N` becomes the superscript.
Аналогічно, вираз `-i` взятий у фігурні дужки, щоб зробити цей вираз верхнім індексом для `2`.
`\sum` та `\approx` є командами LaTeX для значень "sum over" й "approximate".

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Closing JupyterLab

- На панелі меню оберіть меню "File" і натисніть "Shut Down" внизу спадного меню. Вам буде запропоновано підтвердити, що Ви бажаєте вимкнути сервер JupyterLab (не забудьте зберегти свою роботу!). Натисніть "Shut Down", щоб вимкнути сервер JupyterLab.
- To restart the JupyterLab server you will need to re-run the following command from a shell.

```
$ jupyter lab
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Closing JupyterLab

Потренуйтеся закривати та перезапускати сервер JupyterLab.

::::::::::::::::::::::::::::::::::::::::::::::::::

[jupyterlab]: https://jupyterlab.readthedocs.io/en/stable/
[jupyterlab-ui]: https://jupyterlab.readthedocs.io/en/stable/user/interface.html
[jupyterlab-notebook-docs]: https://jupyterlab.readthedocs.io/en/stable/user/notebook.html
[markdown]: https://en.wikipedia.org/wiki/Markdown
[data_carpentry]: https://datacarpentry.org

:::::::::::::::::::::::::::::::::::::::: keypoints

- Python scripts are plain text files.
- Застосування Jupyter Notebook для редагування та запуску Python
- The Notebook has Command and Edit modes.
- Use the keyboard and mouse to select and edit cells.
- Notebook підтримує мову розмітки текстів Markdown.
- Markdown does most of what HTML does.

::::::::::::::::::::::::::::::::::::::::::::::::::
