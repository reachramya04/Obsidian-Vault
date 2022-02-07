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

### CLI Options
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
	if name == "World":
		print("Hello World")
	else:
		print(f"Hello {name}")

if __name__ == "__main__":
	app()
```

Here `name` is an option which lets the user add in their name to the hello command.


### Terminating CLI 
There are some cases where you might want to terminate a command at some point, and stop all subsequent execution.
It could be that your code determined that the program completed successfully, or it could be an operation aborted.

To stop or abort the execution of the program raise a `Typer.exit()` exception.
Here's an example:
```python
import typer

app = typer.Typer()
passwords = {"gmail" : "Yeetus1234" , "github" : "Feetus1234" , "discord" : "G sus1234"}

@app.command()
def mknewpass(acc : str , new_pass : str):
	if new_pass in passwords.values():
		print("The password already exists")
		raise typer.Exit()
	else:
		passwords[acc] = new_pass 

if __name__ == "__main__":
	app()
```


### Optional CLI Arguments 
By default CLI options are **optional** and CLI arguments are **required**.
Again, that's how they work _by default_, and that's the convention in many CLI programs and systems.
But you can change that.
In fact, it's very common to have **optional** _CLI arguments_, it's way more common than having **required** _CLI options_.

Example: 
```bash
ls ./dir
```
Here `dir` is an optional argument.
The above command is used to list the sub-directories within `dir`.
If `dir` isn't passed to `ls` then it defaults to the current directory.

#### CLI Argument Declaration
Now let's see an alternative way to create the same _CLI argument_:
```python
import typer

app = typer.Typer()
passwords = {"gmail" : "Yeetus1234" , "github" : "Feetus1234" , "discord" : "G sus1234"}

@app.command()
def mknewpass(acc : str = typer.Argument(), new_pass : str = typer.Argument()):
	if new_pass in passwords.values():
		print("The password already exists")
		raise typer.Exit()
	else:
		passwords[acc] = new_pass 

if __name__ == "__main__":
	app()
```

Before `acc` and `new_pass` were required as they didnt have default values.
But now as `typer.Argument()` is the "default value" of the function's parameter, it would mean that "it is no longer required" (in Python terms).
**To make the value required** we can pass in `...` in `typer.Argument(...)`

#### Make an optional CLI Argument 
To make a _CLI argument_ optional, use `typer.Argument()` and pass a different "default" as the first parameter to `typer.Argument()`, for example `None`:
```python
import typer

app = typer.Typer()
passwords = {"gmail" : "Yeetus1234" , "github" : "Feetus1234" , "discord" : "G sus1234"}

@app.command()
def mknewpass(acc : str = typer.Argument(None), new_pass : str = typer.Argument(None)):
	if new_pass in passwords.values():
		print("The password already exists")
		raise typer.Exit()
	elif None in [acc,new_pass]:
		print("No input  passed in")
		raise typer.Exit()
	else:
		passwords[acc] = new_pass
		print(passwords)

if __name__ == "__main__":
	app()
```

Here we pass in a default value to `typer.Argument()` which is `None` .
If no input is given the value is set to `None`.
This gives us the functionality to set a default value for an optional argument.
### CLI Arguments with Defaults 
We can also use the same `typer.Argument()` to set a default value.
That way the _CLI argument_ will be optional _and also_ have a default value.

#### Optional CLI Argument with Default
```python
import typer 
def main(name: str = typer.Argument("G sus")): 
	typer.echo(f"Hello {name}") 
if __name__ == "__main__": 
	typer.run(main)
```

#### Dynamic Default Value 

