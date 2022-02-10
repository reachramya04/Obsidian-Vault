# Introduction 
Rich is a Python library for _rich_ text and beautiful formatting in the terminal.

The [Rich API](https://rich.readthedocs.io/en/latest/) makes it easy to add color and style to terminal output. Rich can also render pretty tables, progress bars, markdown, syntax highlighted source code, tracebacks, and more — out of the box.

# Installing 
```bash
pip install rich
```
**or**
```bash
python -m pip install rich
```

**For an example run**
```bash
python -m rich
```

# Getting Started
###  rich print function 
To effortlessly add rich output to your application, you can import the [rich print](https://rich.readthedocs.io/en/latest/introduction.html#quick-start) method, which has the same signature as the builtin Python function.

**Note :** The builtin print function will be overridden with rich print function
```python 
from rich import print

print("Hello, [bold magenta]World[/bold magenta]!")
```
>  `>>>`  Hello <font color="magenta"  style = "font-weight:bold">World!</font>


###  rich Console
For more control over rich terminal content, import and construct a [Console](https://rich.readthedocs.io/en/latest/reference/console.html#rich.console.Console) object.

```python
from rich.console import Console

console = Console()
```

The Console object has a `print` method which has an intentionally similar interface to the builtin `print` function. Here's an example of use:

```python
console.print("Hello", "World!")
```

As you might expect, this will print `"Hello World!"` to the terminal. Note that unlike the builtin `print` function, Rich will word-wrap your text to fit within the terminal width.

There are a few ways of adding color and style to your output. You can set a style for the entire output by adding a `style` keyword argument. Here's an example:
```python
console.print("Hello", "World!", style="bold red")
```
>  `>>>`  <font color="red" style="font-weight:bold">Hello World!</font>


###  rich Inspect function
Rich has an [inspect](https://rich.readthedocs.io/en/latest/reference/init.html?highlight=inspect#rich.inspect) function which can produce a report on any Python object, such as class, instance, or builtin.
```python 
my_list = ["foo", "bar"]
from rich import inspect
inspect(my_list, methods=True)
```
![[Pasted image 20220127002006.png]]

# Styles
In various places in the Rich API you can set a “style” which defines the color of the text and various attributes such as bold, italic etc. A style may be given as a string containing a _style definition_ or as an instance of a [`Style`](https://rich.readthedocs.io/en/latest/reference/style.html#rich.style.Style "rich.style.Style") class.

### Defining Styles
- A style definition is a string containing one or more words to set colors and attributes.
To specify a foreground color use one of the 256 [Standard Colors](https://rich.readthedocs.io/en/latest/appendix/colors.html#appendix-colors). 
For example, to print “Hello” in magenta:
```python 
console.print("Hello", style="magenta")
```
>  `>>>`  <font color="magenta">Hello</font>

- Alteratively you can use a CSS-like syntax to specify a color with a “#” followed by three pairs of hex characters, or in RGB form with three decimal integers.
```python
console.print("Hello", style="#af00ff")
console.print("Hello", style="rgb(175,0,255)")
```
> `>>>`  <font color="#af00ff">Hello</font>
> `>>>`  <font color="#af00ff">Hello</font>

**Note :** Some terminals only support 256 colors. Rich will attempt to pick the closest color it can if your color isn’t available.

- You can also set a background color , precede the color with word "on ".
```python
console.print("DANGER!", style="red on white")
```
>  `>>>`  <font color="red" style="background-color:white">DANGER!</font>

- **You can set a style attribute by adding one or more of the following words:**
	- `"bold"` or `"b"` for bold text.
	-   `"blink"` for text that flashes (use this one sparingly).
  -   `"blink2"` for text that flashes rapidly (not supported by most terminals).
	-   `"conceal"` for _concealed_ text (not supported by most terminals).
	-   `"italic"` or `"i"` for italic text (not supported on Windows).
	-   `"reverse"` or `"r"` for text with foreground and background colors reversed.
	-   `"strike"` or `"s"` for text with a line through it.    
	-   `"underline"` or `"u"` for underlined text.

- Styles may be negated by prefixing the attribute with the word “not”. This can be used to turn off styles if they overlap. For example:
```python
console.print("foo [not bold]bar[/not bold] baz", style="bold")
```
> `>>>`   **foo** bar **baz**


- To add a link to a style, the definition should contain the word `"link"` followed by a URL. The following example will make a clickable link:
```python
console.print("[yellow underline]Google", style="link https://google.com")
```
> `>>>`   [Google](www.google.com)



### Style Themes
Rich provides a [`Theme`](https://rich.readthedocs.io/en/latest/reference/theme.html#rich.theme.Theme "rich.theme.Theme") class which you can use to define custom styles that you can refer to by name. That way you only need to update your styles in one place.

To use a style theme, construct a [`Theme`](https://rich.readthedocs.io/en/latest/reference/theme.html#rich.theme.Theme "rich.theme.Theme") instance and pass it to the [`Console`](https://rich.readthedocs.io/en/latest/reference/console.html#rich.console.Console "rich.console.Console") constructor. 
Here’s an example:
```Python
from rich.console import Console
from rich.theme import Theme
custom_theme = Theme({
    "info": "dim cyan",
    "warning": "magenta",
    "danger": "bold red"
})
console = Console(theme=custom_theme)
console.print("This is information", style="info")
console.print("[warning]The pod bay doors are locked[/warning]")
console.print("Something terrible happened!", style="danger")
```
>  `>>>`  <font color="cyan">This is information</font>
>  `>>>`  <font color="magenta" >The pod bay doors are locked</font>
>  `>>>`  <font color="red"  style = "font-weight:bold">Something terrible happened</font>

### bbcode Styles
Styles can also be added to strings with bbcode like syntax .
Here's an example:
```Python
from rich.console import Console

console = Console()
console.print("Initiating [bold cyan]drop[/bold cyan] sequence in....")
```
> `>>>`  Initiating <font color = "cyan" style="font-weight:bold">drop</font> sequence in...  



# Emojis
To insert an emoji in to console output place the name between two colons.
Here's an example:
```python 
from rich.console import Console

console = Console()
console.print("The logo of dracula theme is :vampire:")
```
>   `>>>`  The logo of dracula theme is 🧛



# Tracebacks
Rich can render Python tracebacks with syntax highlighting and formatting. Rich tracebacks are easier to read and show more code than standard Python tracebacks.

To see an example of a Rich traceback, running the following command:
```bash
python -m rich.traceback
```

### Printing Tracebacks
The [`print_exception()`](https://rich.readthedocs.io/en/latest/reference/console.html#rich.console.Console.print_exception "rich.console.Console.print_exception") method will print a traceback for the current exception being handled.
Here’s an example:
```Python
from rich.console import Console
console = Console()

try:
    do_something()
except Exception:
    console.print_exception(show_locals=True)
```

### Traceback Handler
Rich can be installed as the default traceback handler so that all uncaught exceptions will be rendered with highlighting. 
Here’s how:
```Python
from rich.traceback import install
install(show_locals=True)
```


# Prompt 
Rich has a number of [`Prompt`](https://rich.readthedocs.io/en/latest/reference/prompt.html#rich.prompt.Prompt "rich.prompt.Prompt") classes which ask a user for input and loop until a valid response is received . Here’s a simple example:
```Python
>>> from rich.prompt import Prompt
>>> name = Prompt.ask("Enter your name")
```
>  `>>>`  Enter your name 

It might look pretty similar to the `input()` function , but it also offers many other functionalities that `input()` function doesn't have.

### Default Values 
You can set a default value which will be returned if the user presses return without entering any text.
Here's an example:
```Python
>>> from rich.prompt import Prompt
>>> name = Prompt.ask("Enter your name", default="Roronoa Zoro")
```
>  `>>>`  Enter your name <font color="cyan" style="font-weight:bold">(Roronoa Zoro)</font> : 

### Choices
If you supply a list of choices, the prompt will loop until the user enters one of the choices.
Here's an example:
```Python
>>> from rich.prompt import Prompt
>>> name = Prompt.ask("Enter your name", choices=["Luffy", "Zoro", "Brooke"], default="Unknown")
```
>  `>>>`  Enter your name <font color="magenta" style="font-weight:bold;">[Luffy , Zoro , Brooke]</font>  <font color="cyan" style="font-weight:bold">(Unknown)</font> :

In addition to `Prompt` which returns strings, you can also use `IntPrompt` which asks the user for an integer, and `FloatPrompt` for floats.

### Confirm 
The [`Confirm`](https://rich.readthedocs.io/en/latest/reference/prompt.html#rich.prompt.Confirm "rich.prompt.Confirm") class is a specialized prompt which may be used to ask the user a simple yes / no question. Here’s an example:
```Python
>>> from rich.prompt import Confirm
>>> is_rich_great = Confirm.ask("Do you like rich?")
```
>  `>>>`  Do you like rich? <font color="magenta" style="font-weight:bold;">[y,n]</font> : 


# Markdown
Rich can render Markdown to the console. To render markdown, construct a [`Markdown`](https://rich.readthedocs.io/en/latest/reference/markdown.html#rich.markdown.Markdown "rich.markdown.Markdown") object then print it to the console.
Here’s an example of use:

```Python
MARKDOWN = """
# This is an h1

Rich can do a pretty *decent* job of rendering markdown.

1. This is a list item
2. This is another list item
"""
from rich.console import Console
from rich.markdown import Markdown

console = Console()
md = Markdown(MARKDOWN)
console.print(md)
```

Markdown can also be rendered from files.
Here's an example:
```Python
from rich.markdown import Markdown 
from rich.console import Console

with open("/hdd/Obsidian/JavetsM/Programming/rich.md") as file:
    md = Markdown(file.read())
console = Console()
console.print(md)
```



# Padding
The [`Padding`](https://rich.readthedocs.io/en/latest/reference/padding.html#rich.padding.Padding "rich.padding.Padding") class may be used to add whitespace around text or other renderable. The following example will print the word “Hello” with a padding of 1 character, so there will be a blank line above and below, and a space on the left and right edges:
```Python
from rich import print
from rich.padding import Padding
test = Padding("Hello", 1)
print(test)
```

A tuple of 2 values sets the top/bottom and left/right padding, whereas a tuple of 4 values sets the padding for top, right, bottom, and left sides.
Here's an example:
```Python
from rich import print
from rich.padding import Padding
test = Padding("Hello", (2, 4))
test2 = Padding("Hello" , (2, 4 , 2 , 4))
print(test)
print(test2)
```

The Padding class can also accept a `style` argument which applies a style to the padding and contents, and an `expand` switch which can be set to False to prevent the padding from extending to the full width of the terminal.
Here's an example:
```Python
from rich import print
from rich.padding import Padding
test = Padding("Hello", (2, 4), style="on blue", expand=False)
test = Padding("Hello", (2, 4) , style="on magenta")
print(test)
```


# Panel
To draw a border around text or other renderable, construct a [`Panel`](https://rich.readthedocs.io/en/latest/reference/panel.html#rich.panel.Panel "rich.panel.Panel") with the renderable as the first positional argument.
Here’s an example:
```Python
from rich import print
from rich.panel import Panel
print(Panel("Hello, [red]World!"))
```

You can change the style of the panel by setting the [box](https://rich.readthedocs.io/en/latest/appendix/box.html#appendix-box) argument to the Panel constructor.
Rich has a number of constants that set the box characters used to draw tables and panels. To select a box style import one of the constants below from `rich.box`
```bash
python -m rich.box
```

Panels will extend to the full width of the terminal. You can make panel _fit_ the content by setting `expand=False` on the constructor, or by creating the Panel with [`fit()`](https://rich.readthedocs.io/en/latest/reference/panel.html#rich.panel.Panel.fit "rich.panel.Panel.fit").
For example:
```Python
from rich import print
from rich.panel import Panel
print(Panel.fit("Hello, [red]World!"))
print(Panel("Hello, [red]World!" , expand=False))
```


# Syntax
Rich can syntax highlight various programming languages with line numbers.
To syntax highlight code, construct a [`Syntax`](https://rich.readthedocs.io/en/latest/reference/syntax.html#rich.syntax.Syntax "rich.syntax.Syntax") object and print it to the console.
Here’s an example:
```Python
from rich.console import Console
from rich.syntax import Syntax

console = Console()
with open("syntax.py", "r") as code_file:
    syntax = Syntax(code_file.read(), "python")
console.print(syntax)
```
You may also use the [`from_path()`](https://rich.readthedocs.io/en/latest/reference/syntax.html#rich.syntax.Syntax.from_path "rich.syntax.Syntax.from_path") alternative constructor which will load the code from disk and auto-detect the file type.
```Python
from rich.console import Console
from rich.syntax import Syntax

console = Console()
syntax = Syntax.from_path("syntax.py")
console.print(syntax)
```

### Line Numbers
If you set `line_numbers=True`, Rich will render a column for line numbers:
```Python
code = Syntax.from_path("./code.py" , line_numbers=True)
```

### Themes
The Syntax constructor (and [`from_path()`](https://rich.readthedocs.io/en/latest/reference/syntax.html#rich.syntax.Syntax.from_path "rich.syntax.Syntax.from_path")) accept a `theme` attribute which should be the name of a [Pygments theme](https://pygments.org/styles/). It may also be one of the special case theme names “ansi_dark” or “ansi_light” which will use the color theme configured by the terminal.
```Python
code = Syntax.from_path("./code.py" , theme="one-dark")
```

### Background Color 
You can override the background color from the theme by supplying a `background_color` argument to the constructor. This should be a string in the same format a style definition accepts, .e.g “red”, “#ff0000”, “rgb(255,0,0)” etc.
```Python
code = Syntax.from_path("./code.py" , background_color="rgb(255,255,255)")
```


# Tables
Rich’s [`Table`](https://rich.readthedocs.io/en/latest/reference/table.html#rich.table.Table "rich.table.Table") class offers a variety of ways to render tabular data to the terminal.

To render a table, construct a [`Table`](https://rich.readthedocs.io/en/latest/reference/table.html#rich.table.Table "rich.table.Table") object, add columns with [`add_column()`](https://rich.readthedocs.io/en/latest/reference/table.html#rich.table.Table.add_column "rich.table.Table.add_column"), and rows with [`add_row()`](https://rich.readthedocs.io/en/latest/reference/table.html#rich.table.Table.add_row "rich.table.Table.add_row") – then print it to the console.

```Python
from rich.console import Console
from rich.table import Table

table = Table(title="Characters From One Piece")

table.add_column("Names", justify="right", style="cyan", no_wrap=True)
table.add_column("AKA", style="magenta")
table.add_column("Powers", justify="right", style="green")

table.add_row("Luffy" , "Mugiwara" , "Rubber Body")
table.add_row("Zoro" , "Swordsman" , "Pirate Hunter")
table.add_row("Usopp" , "Sniper" , "Sogeking")
table.add_row("Nami" , "Navigator" , "Cat Burglar")

console = Console()
console.print(table)
```

### Table Options
-   `title` Sets the title of the table (text show above the table).
-   `caption` Sets the table caption (text show below the table).
-   `width` Sets the desired width of the table (disables automatic width calculation).
-   `min_width` Sets a minimum width for the table.
-   `box` Sets one of the [Box](https://rich.readthedocs.io/en/latest/appendix/box.html#appendix-box) styles for the table grid, or `None` for no grid.
-   `safe_box` Set to `True` to force the table to generate ASCII characters rather than unicode.
-   `padding` A integer, or tuple of 1, 2, or 4 values to set the padding on cells.
-   `collapse_padding` If True the padding of neighboring cells will be merged.
-   `pad_edge` Set to False to remove padding around the edge of the table.
-   `expand` Set to True to expand the table to the full available size.
-   `show_header` Set to True to show a header, False to disable it.
-   `show_footer` Set to True to show a footer, False to disable it.
-   `show edge` Set to False to disable the edge line around the table.
-   `show_lines` Set to True to show lines between rows as well as header / footer.
-   `leading` Additional space between rows.
-   `style` A Style to apply to the entire table, e.g. "on blue".
-   `row_styles` Set to a list of styles to style alternating rows. e.g. `["dim", ""]` to create _zebra stripes_
-   `header_style` Set the default style for the header.
-   `footer_style` Set the default style for the footer.
-   `border style` Set a style for border characters.
-   `title_style` Set a style for the title.
-   `caption_style` Set a style for the caption.
-   `title_justify` Set the title justify method (“left”, “right”, “center”, or “full”)
-   `caption_justify` Set the caption justify method (“left”, “right”, “center”, or “full”)
-   `highlight` Set to True to enable automatic highlighting of cell contents.

### Border Styles
You can set the border style by importing one of the preset `Box` objects and setting the `box` argument in the table constructor.
Here’s an example:
```Python
from rich import box
table = Table(title="Star Wars Movies", box=box.MINIMAL_DOUBLE_HEAD)
```
See [Box](https://rich.readthedocs.io/en/latest/appendix/box.html#appendix-box) for other box styles.
**You can also set `box=None` to remove borders entirely.**

### Grids
The Table class can also make a great layout tool. If you disable headers and borders you can use it to position content within the terminal. The alternative constructor [`grid()`](https://rich.readthedocs.io/en/latest/reference/table.html#rich.table.Table.grid "rich.table.Table.grid") can create such a table for you.
For instance, the following code displays two pieces of text aligned to both the left and right edges of the terminal on a single line:
```Python
from rich import print
from rich.table import Table

grid = Table.grid(expand=True)
grid.add_column()
grid.add_column(justify="right")
grid.add_row("Raising shields", "[bold magenta]COMPLETED [green]:heavy_check_mark:")

print(grid)
```


# Tree
Rich has a [`Tree`](https://rich.readthedocs.io/en/latest/reference/tree.html#rich.tree.Tree "rich.tree.Tree") class which can generate a tree view in the terminal.Each branch of the tree can have a label which may be text or any other Rich renderable.
```bash
python -m rich.tree
```
With only a single `Tree` instance this will output nothing more than the text “Rich Tree”. Things get more interesting when we call [`add()`](https://rich.readthedocs.io/en/latest/reference/tree.html#rich.tree.Tree.add "rich.tree.Tree.add") to add more branches to the Tree. The following code adds two more branches:

```Python
tree.add("foo")
tree.add("bar")
print(tree)
```

The tree will now have two branches connected to the original tree with guide lines.
When you call [`add()`](https://rich.readthedocs.io/en/latest/reference/tree.html#rich.tree.Tree.add "rich.tree.Tree.add") a new Tree instance is returned. You can use this instance to add more branches to, and build up a more complex tree..

```Python
baz_tree = tree.add("baz")
baz_tree.add("[red]Red").add("[green]Green").add("[blue]Blue")
print(tree)
```

### Tree Styles
The Tree constructor and [`add()`](https://rich.readthedocs.io/en/latest/reference/tree.html#rich.tree.Tree.add "rich.tree.Tree.add") method allows you to specify a `style` argument which sets a style for the entire branch, and `guide_style` which sets the style for the guide lines. These styles are inherited by the branches and will apply to any sub-trees as well.
If you set `guide_style` to bold, Rich will select the thicker variations of unicode line characters. Similarly, if you select the “underline2” style you will get double line style of unicode characters.


```javascript
var foo = function (bar) { 
	return bar++; 
}; 
console.log(foo(5));
```
H^ello
