## CSS Box Model

The CSS Box Model explains how space is used around elements:
```
+-------------------------+ ← Margin (outside)
|  +-------------------+  |
|  |     Border        |  |
|  |  +-------------+  |  |
|  |  |  Padding    |  |  |
|  |  | +--------+  |  |  |
|  |  | |Content |  |  |  |
|  |  | +--------+  |  |  |
|  |  +-------------+  |  |
|  +-------------------+  |
+-------------------------+
```

Parts:

Content: The actual text/image

Padding: Space between content and border

Border: Edge around the padding

Margin: Space outside the border

## What’s the difference between var, let, and const?

These are JavaScript keywords used to declare variables:

**var**

- Function-scoped

- Can be reassigned

- Can be redeclared

- Hoisted (initialized as undefined)

- Avoid in modern code

**let**

- Block-scoped

- Can be reassigned

- Cannot be redeclared in the same scope

- Hoisted (but not initialized)

**const**

- Block-scoped

- Cannot be reassigned

- Cannot be redeclared

- Hoisted (but not initialized)

*Use let when the value might change.*

*Use const when the value should stay constant.*

## Explain Dummy Table in SQL

A dummy table is used when you want to run a SQL query that doesn't involve real tables.

In Oracle, the dummy table is called DUAL.
```sql
SELECT SYSDATE FROM DUAL;

```
In MySQL/PostgreSQL, you can skip FROM or use:
```sql
SELECT NOW();
```

Use cases:

- Testing expressions

- Getting system date/time

- Performing simple calculations

## What are branches in Git?

Branches in Git are used to manage different versions or features of your project.

- main or master: Default/main production branch

- feature/xyz: For new features

- bugfix/abc: For fixing bugs

- develop: For testing before merging into main

Why use branches?

- Isolate work

- Avoid breaking the main code

- Collaborate efficiently

- Merge when changes are ready

## Different types of constraints in SQL

SQL constraints are rules to protect the data in a table.

- PRIMARY KEY: Uniquely identifies each row; cannot be null

- FOREIGN KEY: Links to a key in another table

- NOT NULL: Value must not be empty

- UNIQUE: All values must be different

- CHECK: Checks a condition (e.g., age >= 18)


Example:
```sql
CREATE TABLE students (
  id INT PRIMARY KEY,
  age INT CHECK (age >= 18)
);
```

## What is pickling and unpickling in Python?

- Pickling: Convert a Python object into a byte stream (to save it to a file).

- Unpickling: Convert the byte stream back into the original Python object.

Example:

import pickle

*Pickling*
```python
data = {'name': 'Alice', 'age': 25}
with open('data.pkl', 'wb') as f:
    pickle.dump(data, f)
```
*Unpickling*
```python
with open('data.pkl', 'rb') as f:
    loaded_data = pickle.load(f)
```
## CSS Position – static, relative, absolute, fixed, sticky

CSS positioning defines how an element is placed on the page.

- static: Default, follows normal flow

- relative: Moved relative to its normal position

- absolute: Positioned relative to nearest ancestor with position set

- fixed: Positioned relative to the screen (stays in place on scroll)

- sticky: Starts as relative, becomes fixed on scroll

Example:

.positioned {
  position: absolute;
  top: 20px;
  left: 30px;
}

## File Handling in Python

Python lets you read, write, and manage files easily.

File modes:

- 'r': Read

- 'w': Write (overwrites)

- 'a': Append

- 'rb' / 'wb': Binary read/write

Example:

*Writing*
with open('file.txt', 'w') as f:
    f.write("Hello, world!")

*Reading*
with open('file.txt', 'r') as f:
    content = f.read()

## Difference between CHAR, VARCHAR, and VARCHAR2 in SQL

- CHAR(n):
Fixed length. Always takes n characters. Pads with spaces if shorter.

- VARCHAR(n):
Variable length. Uses only required space. (Not standard in Oracle)

- VARCHAR2(n):
Oracle’s preferred variable-length type. Safer than VARCHAR.

Example:

name CHAR(10);       -- Always 10 characters
name VARCHAR2(10);   -- Only uses what’s needed

