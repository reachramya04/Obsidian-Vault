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
#### Output
Hello <font color="magenta"  style = "font-weight:bold">World!</font>



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

#### Output
<font color="red" style="font-weight:bold">Hello World!</font>


# rich Inspect function
Rich has an [inspect](https://rich.readthedocs.io/en/latest/reference/init.html?highlight=inspect#rich.inspect) function which can produce a report on any Python object, such as class, instance, or builtin.
```python 
my_list = ["foo", "bar"]
from rich import inspect
inspect(my_list, methods=True)
```
![[Pasted image 20220127002006.png]]








