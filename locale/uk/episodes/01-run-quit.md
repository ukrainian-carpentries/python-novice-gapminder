---
title: Запуск та завершення роботи
teaching: 15
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives

- Запуск серверу JupyterLab.
- Create a new Python script.
- Створення блокноту Jupyter.
- Зупинка серверу JupyterLab.
- Understand the difference between a Python script and a Jupyter notebook.
- Створення в блокноті комірок типу Markdown.
- Створення та виконання в блокноті комірок Python.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Як запустити програми Python?

::::::::::::::::::::::::::::::::::::::::::::::::::

To run Python, we are going to use \[Jupyter Notebooks]\[jupyter] via [JupyterLab][jupyterlab] for the remainder of this workshop. Jupyter notebooks are common in data science and visualization and serve as a convenient common-denominator experience for running Python code interactively where we can easily view and share the results of our Python code.

Існують й інші способи редагування, управління та виконання коду. Розробники програмного забезпечення часто використовують інтегроване середовище розробки (IDE), подібне до [PyCharm](https://www.jetbrains. om/pycharm/) або [Visual Studio Code](https://code.visualstudio.com/) або текстові редактори такі як Vim або Emacs, щоб створити та відредагувати свої програми Python. Після редагування та збереження ваших програм Python ви можете виконувати ці програми в самому IDE або безпосередньо в командному рядку. На відміну від цього, блокноти Jupyter дозволяють відразу переглянути результати нашого Python коду.

JupyterLab має декілька інших зручних функцій:

- Ви можете легко вводити, редагувати, копіювати та вставляти блоки коду.
- Автодоповнення за допомогою клавіші Tab дозволяє легко отримати доступ до назв об'єктів, які ви використовуєте.
- It allows you to annotate your code with links, different sized text, bullets, etc.
  to make it more accessible to you and your collaborators.
- It allows you to display figures next to the code that produces them
  to tell a complete story of the analysis.

Кожен блокнот містить одну або кілька комірок, що містять код, текст або зображення.

## Початок роботи з JupyterLab

JupyterLab is an application server with a web user interface from [Project Jupyter][jupyter] that
enables one to work with documents and activities such as Jupyter notebooks, text editors, terminals,
and even custom components in a flexible, integrated, and extensible manner. JupyterLab вимагає досить оновлений браузер (в ідеалі – поточна версія Chrome, Safari або Firefox); Інтернет браузер версії 9 і нижче _не_ підтримується.

JupyterLab є частиною інсталяційного пакета Anaconda Python. If you have not already
installed the Anaconda Python distribution, see [the setup instructions](../learners/setup.md)
for installation instructions.

In this lesson we will run JupyterLab locally on our own machines so it will not require an internet connection besides
the initial connection to download and install Anaconda and JupyterLab

- Запустіть сервер JupyterLab на вашому комп'ютері
- Use a web browser to open a special localhost URL that connects to your JupyterLab server
- The JupyterLab server does the work and the web browser renders the result
- Type code into the browser and see the results after your JupyterLab server has finished executing your code

:::::::::::::::::::::::::::::::::::::::::  callout

## JupyterLab? А чому не Jupyter Notebook?

JupyterLab є [подальшим кроком в еволюції Jupyter Notebook](https://jupyterlab.readthedocs.io/en/stable/getting_started/overview.html#overview).
Якщо ви використовували Jupyter Notebook раніше, то ви добре зрозумієте діапазон можливостей JupyterLab.

Experienced users of Jupyter notebooks interested in a more detailed discussion of the similarities and differences
between the JupyterLab and Jupyter notebook user interfaces can find more information in the
[JupyterLab user interface documentation][jupyterlab-ui].

::::::::::::::::::::::::::::::::::::::::::::::::::

## Початок роботи з JupyterLab

Ви можете запустити сервер JupyterLab через командний рядок або через застосунок, що має назву 'Anaconda Navigator'. JupyterLab є частиною інсталяційного пакета Anaconda Python.

### macOS - командний рядок

Для запуску сервера JupyterLab вам потрібно отримати доступ до командного рядка через Terminal.
Існує два способи відкрити термінал на Mac.

1. У директорії Applications відкрийте теку Utilities і двічі натисніть Terminal
2. Натисніть <kbd>Command</kbd> + <kbd>spacebar</kbd> для запуску Spotlight. Введіть `Terminal`, а потім двічі клацніть на результат пошуку або натисніть <kbd>Enter</kbd>

Після запуску Terminal введіть команду для запуску сервера JupyterLab.

```bash
$ jupyter lab
```

### Windows Users - Command Line

To start the JupyterLab server you will need to access the Anaconda Prompt.

Press <kbd>Windows Logo Key</kbd> and search for `Anaconda Prompt`, click the result or press enter.

Після запуску Anaconda Prompt введіть команду:

```bash
$ jupyter lab
```

### Anaconda Navigator

To start a JupyterLab server from Anaconda Navigator you must first [start Anaconda Navigator (click for detailed instructions on macOS, Windows, and Linux)](https://docs.anaconda.com/free/navigator/getting-started/#navigator-starting-navigator). You can search for Anaconda Navigator via Spotlight on macOS (<kbd>Command</kbd> + <kbd>spacebar</kbd>), the Windows search function (<kbd>Windows Logo Key</kbd>) or opening a terminal shell and executing the `anaconda-navigator` executable from the command line.

Після того, як ви запустили Anaconda Navigator, натисніть кнопку `Launch` під JupyterLab. You may need
to scroll down to find it.

Here is a screenshot of an Anaconda Navigator page similar to the one that should open on either macOS
or Windows.

<p align='center'>
  <img alt="Anaconda Navigator landing page" src="fig/0_anaconda_navigator_landing_page.png" width="750"/>
</p>

And here is a screenshot of a JupyterLab landing page that should be similar to the one that opens in your
default web browser after starting the JupyterLab server on either macOS or Windows.

<p align='center'>
  <img alt="JupyterLab landing page" src="fig/0_jupyterlab_landing_page.png" width="750"/>
</p>

## Інтерфейс JupyterLab

JupyterLab has many features found in traditional integrated development environments (IDEs) but
is focused on providing flexible building blocks for interactive, exploratory computing.

The [JupyterLab Interface][jupyterlab-ui]
consists of the Menu Bar, a collapsable Left Side Bar, and the Main Work Area which contains tabs
of documents and activities.

### Панель Меню

The Menu Bar at the top of JupyterLab has the top-level menus that expose various actions
available in JupyterLab along with their keyboard shortcuts (where applicable). Наступні пункти меню наявні за замовчуванням.

- **File:** Actions related to files and directories such as _New_, _Open_, _Close_, _Save_, etc. The _File_ menu also includes the _Shut Down_ action used to shutdown the JupyterLab server.
- **Edit:** Actions related to editing documents and other activities such as _Undo_, _Cut_, _Copy_, _Paste_, etc.
- **View:** Actions that alter the appearance of JupyterLab.
- **Run:** Actions for running code in different activities such as notebooks and code consoles (discussed below).
- **Ядро:** Дії щодо управління ядрами. Kernels in Jupyter will be explained in more detail below.
- **Tabs:** A list of the open documents and activities in the main work area.
- **Settings:** Common JupyterLab settings can be configured using this menu. There is also an _Advanced Settings Editor_ option in the dropdown menu that provides more fine-grained control of JupyterLab settings and configuration options.
- **Help:** A list of JupyterLab and kernel help links.

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

The left sidebar can be collapsed or expanded by selecting "Show Left Sidebar" in the View menu or
by clicking on the active sidebar tab.

### Основна робоча область

Основна робоча область в JupyterLab дозволяє упорядковувати документи (блокноти, текстові файли та ін.)
and other activities (terminals, code consoles, etc.) на панелях вкладок, які можуть бути змінені або
розділені. A screenshot of the default Main Work Area is provided below.

Якщо Ви не бачите вкладку Launcher на панелі запуску, натисніть синій плюс під знаком "Файл" та "Редагувати", і ця вкладка з'явиться.

<p align='center'>   <img alt="JupyterLab Main Work Area" src="fig/0_jupyterlab_main_work_area.png" width="750"/>
</p>

Drag a tab to the center of a tab panel to move the tab to the panel. Розділіть панель вкладок за допомогою перетягування вкладки ліворуч, праворуч, до верху або до низу панелі. Робоча панель має одну поточну дію. Вкладка для поточної дії позначена кольоровою верхньою рамкою (за замовчуванням - синьою).

## Creating a Python script

- To start writing a new Python program click the Text File icon under the _Other_ header in the Launcher tab of the Main Work Area.
  - You can also create a new plain text file by selecting the _New -> Text File_ from the _File_ menu in the Menu Bar.
- To convert this plain text file to a Python program, select the _Save File As_ action from the _File_ menu in the Menu Bar and give your new text file a name that ends with the `.py` extension.
  - The `.py` extension lets everyone (including the operating system) know that this text file is a Python program.
  - Це умовність, а не вимога.

## Створення Jupyter Notebook

To open a new notebook click the Python 3 icon under the _Notebook_ header in the Launcher tab in
the main work area. You can also create a new notebook by selecting _New -> Notebook_ from the _File_ menu in the Menu Bar.

Додаткові зауваження щодо Jupyter notebooks.

- Файли, створені в Jupiter Notebook, мають розширення `.ipynb`, щоб відрізнити їх від програм на Python, створених як звичайний текстовий файл.
- Notebooks can be exported as Python scripts that can be run from the command line.

Нижче наведено скриншот екрана Jupyter Notebook, який працює в JupyterLab. If you are interested in
more details, then see the [official notebook documentation][jupyterlab-notebook-docs].

<p align='center'>   <img alt="Example Jupyter Notebook" src="fig/0_jupyterlab_notebook_screenshot.png" width="750"/>
</p>

:::::::::::::::::::::::::::::::::::::::::  callout

## Як це зберігається

- The notebook file is stored in a format called JSON.
- Just like a webpage, what's saved looks different from what you see in your browser.
- But this format allows Jupyter to mix source code, text, and images, all in one file.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Arranging Documents into Panels of Tabs

In the JupyterLab Main Work Area you can arrange documents into panels of tabs. Here is an
example from the [official documentation][jupyterlab].

<p align='center'>   <img alt="Multi-panel JupyterLab" src="fig/0_multipanel_jupyterlab_screenshot.png" width="750"/>
</p>

First, create a text file, Python console, and terminal window and arrange them into three
panels in the main work area. Next, create a notebook, terminal window, and text file and
arrange them into three panels in the main work area. Finally, create your own combination of
panels and tabs. What combination of panels and tabs do you think will be most useful for your
workflow?

:::::::::::::::  solution

## Solution

After creating the necessary tabs, you can drag one of the tabs to the center of a panel to
move the tab to the panel; next you can subdivide a tab panel by dragging a tab to the left,
right, top, or bottom of the panel.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Code vs. Text

Jupyter mixes code and text in different types of blocks, called cells. We often use the term
"code" to mean "the source code of software written in a language such as Python".
A "code cell" in a Notebook is a cell that contains software;
a "text cell" is one that contains ordinary prose written for human beings.

::::::::::::::::::::::::::::::::::::::::::::::::::

## The Notebook has Command and Edit modes.

- If you press <kbd>Esc</kbd> and <kbd>Return</kbd> alternately, the outer border of your code cell will change from gray to blue.
- These are the **Command** (gray) and **Edit** (blue) modes of your notebook.
- Command mode allows you to edit notebook-level features, and Edit mode changes the content of cells.
- When in Command mode (esc/gray),
  - The <kbd>b</kbd> key will make a new cell below the currently selected cell.
  - The <kbd>a</kbd> key will make one above.
  - The <kbd>x</kbd> key will delete the current cell.
  - The <kbd>z</kbd> key will undo your last cell operation (which could be a deletion, creation, etc).
- All actions can be done using the menus, but there are lots of keyboard shortcuts to speed things up.

:::::::::::::::::::::::::::::::::::::::  challenge

## Command Vs. Edit

In the Jupyter notebook page are you currently in Command or Edit mode?\
Switch between the modes.
Use the shortcuts to generate a new cell.
Use the shortcuts to delete a cell.
Use the shortcuts to undo the last cell operation you performed.

:::::::::::::::  solution

## Solution

Command mode has a grey border and Edit mode has a blue border.
Use <kbd>Esc</kbd> and <kbd>Return</kbd> to switch between modes.
You need to be in Command mode (Press <kbd>Esc</kbd> if your cell is blue).  Type <kbd>b</kbd> or <kbd>a</kbd>.
You need to be in Command mode (Press <kbd>Esc</kbd> if your cell is blue).  Type <kbd>x</kbd>.
You need to be in Command mode (Press <kbd>Esc</kbd> if your cell is blue).  Type <kbd>z</kbd>.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

### Use the keyboard and mouse to select and edit cells.

- Pressing the <kbd>Return</kbd> key turns the border blue and engages Edit mode, which allows
  you to type within the cell.
- Because we want to be able to write many lines of code in a single cell,
  pressing the <kbd>Return</kbd> key when in Edit mode (blue) moves the cursor to the next line
  in the cell just like in a text editor.
- We need some other way to tell the Notebook we want to run what's in the cell.
- Pressing <kbd>Shift</kbd>\+<kbd>Return</kbd> together will execute the contents of the cell.
- Notice that the <kbd>Return</kbd> and <kbd>Shift</kbd> keys on the right of the keyboard are
  right next to each other.

### The Notebook will turn Markdown into pretty-printed documentation.

- Notebooks can also render [Markdown][markdown].
  - A simple plain-text format for writing lists, links,
    and other things that might go into a web page.
  - Equivalently, a subset of HTML that looks like what you'd send in an old-fashioned email.
- Turn the current cell into a Markdown cell by entering the Command mode (<kbd>Esc</kbd>/gray)
  and press the <kbd>M</kbd> key.
- `In [ ]:` will disappear to show it is no longer a code cell and you will be able to write in
  Markdown.
- Turn the current cell into a Code cell by entering the Command mode (<kbd>Esc</kbd>/gray) and
  press the <kbd>y</kbd> key.

### Markdown does most of what HTML does.

Table: Showing some markdown syntax and its rendered output.

+---------------------------------------+------------------------------------------------+
\| Markdown code                         | Rendered output                                |
+=======================================+================================================+
+---------------------------------------+------------------------------------------------+
\| `                                  | <p></p>                                        | | *   Use asterisks                     | -   Use asterisks                              | | *   to create                         | -   to create                                  | | *   bullet lists.                     | -   bullet lists.                              |
|`                                   |                                                |
+---------------------------------------+------------------------------------------------+
+---------------------------------------+------------------------------------------------+
\| `                                  | <p></p>                                        | | 1.   Use numbers                      | 1.   Use numbers                               | | 1.   to create                        | 2.   to create                                 | | 1.   bullet lists.                    | 3.   numbered lists.                           |
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

## Creating Lists in Markdown

Create a nested list in a Markdown cell in a notebook that looks like this:

1. Get funding.
2. Do work.

- Design experiment.
- Collect data.
- Analyze.

3. Write up.
4. Publish.

:::::::::::::::  solution

## Solution

This challenge integrates both the numbered list and bullet list.
Note that the bullet list is indented 2 spaces so that it is inline with the items of the numbered list.

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

## More Math

What is displayed when a Python cell in a notebook
that contains several calculations is executed?
For example, what happens when this cell is executed?

```python
7 * 3
2 + 1
```

:::::::::::::::  solution

## Solution

Python returns the output of the last calculation.

```python
3
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Change an Existing Cell from Code to Markdown

What happens if you write some Python in a code cell
and then you switch it to a Markdown cell?
For example,
put the following in a code cell:

```python
x = 6 * 7 + 12
print(x)
```

And then run it with <kbd>Shift</kbd>\+<kbd>Return</kbd> to be sure that it works as a code cell.
Now go back to the cell and use <kbd>Esc</kbd> then <kbd>m</kbd> to switch the cell to Markdown
and "run" it with <kbd>Shift</kbd>\+<kbd>Return</kbd>.
What happened and how might this be useful?

:::::::::::::::  solution

## Solution

The Python code gets treated like Markdown text.
The lines appear as if they are part of one contiguous paragraph.
This could be useful to temporarily turn on and off cells in notebooks that get used for multiple purposes.

```python
x = 6 * 7 + 12 print(x)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Equations

Standard Markdown (such as we're using for these notes) won't render equations,
but the Notebook will.
Create a new Markdown cell
and enter the following:

```
$\sum_{i=1}^{N} 2^{-i} \approx 1$
```

(It's probably easier to copy and paste.)
What does it display?
What do you think the underscore, `_`, circumflex, `^`, and dollar sign, `$`, do?

:::::::::::::::  solution

## Solution

The notebook shows the equation as it would be rendered from LaTeX equation syntax.
The dollar sign, `$`, is used to tell Markdown that the text in between is a LaTeX equation.
If you're not familiar with LaTeX,  underscore, `_`, is used for subscripts and circumflex, `^`, is used for superscripts.
A pair of curly braces, `{` and `}`, is used to group text together so that the statement `i=1` becomes the subscript and `N` becomes the superscript.
Similarly, `-i` is in curly braces to make the whole statement the superscript for `2`.
`\sum` and `\approx` are LaTeX commands for "sum over" and "approximate" symbols.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Closing JupyterLab

- From the Menu Bar select the "File" menu and then choose "Shut Down" at the bottom of the dropdown menu. You will be prompted to confirm that you wish to shutdown the JupyterLab server (don't forget to save your work!). Click "Shut Down" to shutdown the JupyterLab server.
- To restart the JupyterLab server you will need to re-run the following command from a shell.

```
$ jupyter lab
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Closing JupyterLab

Practice closing and restarting the JupyterLab server.

::::::::::::::::::::::::::::::::::::::::::::::::::

[jupyterlab]: https://jupyterlab.readthedocs.io/en/stable/
[jupyterlab-ui]: https://jupyterlab.readthedocs.io/en/stable/user/interface.html
[jupyterlab-notebook-docs]: https://jupyterlab.readthedocs.io/en/stable/user/notebook.html
[markdown]: https://en.wikipedia.org/wiki/Markdown
[data_carpentry]: https://datacarpentry.org

:::::::::::::::::::::::::::::::::::::::: keypoints

- Python scripts are plain text files.
- Use the Jupyter Notebook for editing and running Python.
- The Notebook has Command and Edit modes.
- Use the keyboard and mouse to select and edit cells.
- The Notebook will turn Markdown into pretty-printed documentation.
- Markdown does most of what HTML does.

::::::::::::::::::::::::::::::::::::::::::::::::::
