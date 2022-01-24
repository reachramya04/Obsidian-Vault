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
c.execute('CREATE TABLE IF NOT EXISTS characters (Name text , Power text , Bounty integer)')
conn.commit()
```

`conn.commit()` is used to write those changes in the `.db` file.
If we don't commit to the database then the commands executed wont affect the `.db` file and no changes would be made.

**Inserting Values Method 1**
```python 
c.execute("INSERT INTO characters VALUES ('Monke D. Luffy' , 'Gum Gum Fruit' , 1500000000)")

c.execute("INSERT INTO characters VALUES ('Vinsmoke Sanji' , 'Black Legs' , 330000000)")

c.execute("INSERT INTO characters VALUES ('Roronora Zoro' , 'Swordsman' , 320000000)")
conn.commit()
```

This will insert the values for some characters.

**Inserting Values Method 2**
```python
more_characters = [("Nami" , "Weather Manipulation" , 66000000) , ("Usopp" , "Sniper" , 200000000) , ("Chopper" , "Pharamaceuticals Specialist" , 100) , ("Nico Robin" , "Flower Flower Fruit" , 100000000)]

c.execute("INSERT INTO characters VALUES (?,?,?)", more_characters)
conn.commit()
```

**Getting Data From Tables**
```python
c.execute("SELECT * FROM characters*")
data = c.fetchall()
print(data)
```

`c.fetchall()` gets all the output from the command executed before it.

**Updating A Table**
```python
c.execute("UPDATE characters SET Bounty=130000000 WHERE Name='%Robin'")
conn.commit()
```

**Deleting Data From The Table**
```python
c.execute("DELETE FROM characters WHERE name='%per'")
conn.commit()
```


# For more please [check this](https://www.sqlitetutorial.net/)

