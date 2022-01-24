# What to do first
1. Connect to the database
2. Initialize the cursor

# Connecting to the database
```python
import sqlite3
conn = sqlite3.connect('testing.db') #connection
```

The `sqlite3.connect()` is used to connect to the database name given in the parenthesis. If the database doesn't exist in the current directory then a new database is created with the name given in the parenthesis.

# Initializing the cursor
```python
import sqlite3
conn = sqlite3.connect('testing.db') #connection
c = conn.cursor()
```

The `conn.cursor()` is initialized to execute SQL code within python.

# Executing SQL Code
```python
import sqlite3
conn = sqlite3.connect('testing.db') #connection
c = conn.cursor()

c.execute("CREATE TABLE characters") # The SQL command is always in capital letters 
```

The `c.execute()` is used to execute the SQL code.

# Creating and Manipulating Tables
```python
import sqlite3
conn = sqlite3.connect('testing.db') #connection
c = conn.cursor()
c.execute('CREATE TABLE characters')
conn.commit()
```

`conn.commit()` is used to write those changes in the `.db` file.
If we don't commit to the database then the commands executed wont affect the `.db` file and no changes would be made.
