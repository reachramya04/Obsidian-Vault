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


