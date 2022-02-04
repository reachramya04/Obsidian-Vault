# Introduction
Typer is a library for building CLI applications that users will **love using** and developers will **love creating**. Based on Python 3.6+ type hints.

The key features are:

-   **Intuitive to write**: Great editor support. Completion everywhere. Less time debugging. Designed to be easy to use and learn. Less time reading docs.
-   **Easy to use**: It's easy to use for the final users. Automatic help, and automatic completion for all shells.
-   **Short**: Minimize code duplication. Multiple features from each parameter declaration. Fewer bugs.
-   **Start simple**: The simplest example adds only 2 lines of code to your app: **1 import, 1 function call**.
-   **Grow large**: Grow in complexity as much as you want, create arbitrarily complex trees of commands and groups of subcommands, with options and arguments.

### Installation
```bash
pip install typer
```

### Example
```python
import typer 

def main(name: str): 
	typer.echo(f"Hello {name}") 

if __name__ == "__main__": 
	typer.run(main)
```


# CLI Argument
Parameters passed in some specific order to the CLI application. By default, they are _required_.
**Note** : CLI arguments are different from CLI options

Example:
```bash
ls
```
It would list all the directories present in the current directory.

### Add an argument
Example:
```bash
rm file_name
```
Here `file_name` is the argument for the `rm` (remove command)

Python code:
```python
import typer

app = typer.Typer()
@app.command()
def hello(string:str):
	print(f"Hello {string}")

if __name__ == "__main__":
	app()
```

# CLI Options
CLI parameters passed to the CLI application with a specific name.
Example:
```bash
ls --help
```
The main visual difference between a _CLI option_ and and a _CLI argument_ is that the _CLI option_ has `--` prepended to the name, like in `--help`.

Python Code:
```python
import typer

app = typer.Typer()
@app.command()
def hello(name:str = 'World'):
	if string == "World":
		print("Hello World")
	else:
		print(f"Hello {name}")

if __name__ == "__main__":
	app()
```


