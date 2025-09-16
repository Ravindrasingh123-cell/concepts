# AMA - 1

## Foreign Keys In SQL :

A foreign key in SQL is a constraint that establishes a relationship between two tables. It ensures referential integrity, meaning values in one table must correspond to values in another.

- A foreign key in one table points to the primary key in another table.

- It enforces a link between related data in two tables.

**Syntax : **
```sql
CREATE TABLE ChildTable (
    column1 datatype,
    column2 datatype,
    ...,
    foreign_key_column datatype,
    FOREIGN KEY (foreign_key_column) REFERENCES ParentTable(parent_key_column)
);
```


---






## Membership operators in python :

 Membership Operators
Operator	Meaning	Example	Result
in	True if value is present	'a' in 'cat'	True
not in	True if value is not present	'x' not in 'cat'	True
***Examples by Data Type***
**1. String**
```python
'a' in 'apple'        # True
'z' not in 'pizza'    # False
```
**2. List**
```python
5 in [1, 2, 3, 5]     # True
10 not in [1, 2, 3]   # True
```
**3. Tuple**
```python
'cat' in ('dog', 'cat', 'mouse')  # True
```
**4. Set**
```python
10 in {1, 3, 5, 10}   # True
```
**5. Dictionary**
```python
d = {'a': 1, 'b': 2}
'a' in d              # True (checks keys, not values)
2 in d                # False
2 in d.values()       # True
```

---








## Deep Copy and Shallow Copy :

**Shallow Copy:**

Creates a new object, but does not copy nested objects — it only copies references to them.

So, changes to nested (inner) objects will affect both the original and the copy.

**Deep Copy:**

Creates a new object, and recursively copies all nested objects.

The original and the copy are fully independent, even at nested levels.

*Examples in Python*


```python
import copy

original = [[1, 2], [3, 4]]

# Shallow Copy
shallow = copy.copy(original)

# Deep Copy
deep = copy.deepcopy(original)
```
```
original:  [[1, 2], [3, 4]]
shallow:   [[1, 2], [3, 4]]  ← shares inner lists with original
deep:      [[1, 2], [3, 4]]  ← independent copy
```

**Modifying a nested element:**
```python
original[0][0] = 99
```
**Result:**
```python
print(original)  # [[99, 2], [3, 4]]
print(shallow)   # [[99, 2], [3, 4]] ← affected
print(deep)      # [[1, 2], [3, 4]]  ← not affected
```


---





## DCL in SQL :

DCL (Data Control Language) in SQL is used to control access to data in a database. It includes commands that grant or revoke privileges to users over database objects like tables, views, procedures, etc.

**DCL Commands**
Command	                    Description
GRANT	          Gives specific privileges to users
REVOKE	          Removes previously granted privileges
**1. GRANT** – Give Permissions

Used to allow a user to perform certain actions.

*Syntax:*
GRANT privilege_name ON object_name TO user_name;

*Example:*
GRANT SELECT, INSERT ON employees TO john;


- Gives user john permission to SELECT and INSERT data in the employees table.

**2. REVOKE** – Take Back Permissions

Used to take away granted permissions from a user.

*Syntax:*
REVOKE privilege_name ON object_name FROM user_name;

*Example:*
REVOKE INSERT ON employees FROM john;


Removes the INSERT permission from user john for the employees table.

**Common Privileges**
```
Privilege	                Description
SELECT	           Read data from a table/view
INSERT	               Add data to a table
UPDATE	              Modify existing data
DELETE	            Remove data from a table
ALL PRIVILEGES	       Grant all permissions
```

---






## Time and Space complexity : 

**Time Complexity**

Time complexity measures how the runtime of a program or algorithm increases as the size of the input grows. It's commonly expressed using Big O notation, which describes the upper bound of the growth rate.

*Common Time Complexities*
```
Big O	           Name	                   Example
O(1)	         Constant	    Accessing an element in a list: arr[0]
O(log n)	    Logarithmic	       Binary search on a sorted list
O(n)	          Linear	        Looping through a list
O(n log n)	    Log-linear	    Merge sort, quicksort (average case)
O(n²)	         Quadratic	       Nested loops over a list
O(2ⁿ)	        Exponential	     Solving the Fibonacci recursively
```
*Time complexity*: O(n) — in the worst case, it checks every element.

**Space Complexity**

Space complexity measures how much additional memory (other than the input) an algorithm needs as input size increases.

It also uses Big O notation to describe memory usage relative to the input size.


**Time complexity:** O(n) — it loops n times.

**Space complexity:** O(n) — it stores n items in the result list.

--- 





## Strings in python :

A string is a sequence of Unicode characters enclosed in quotes. Strings are immutable, meaning they cannot be changed after they are created.

**Examples:**
s1 = "Hello"
s2 = 'World'
s3 = """This is 
a multi-line string"""

*Features*
1. Immutability

You can't change a string once it's created:
```python
s = "hello"
# s[0] = 'H'  This will raise an error
```
2. Indexing and Slicing

Strings support zero-based indexing:
```python
s = "Python"
print(s[0])    # 'P'
print(s[-1])   # 'n'
print(s[0:3])  # 'Pyt'
print(s[::2])  # 'Pto'
```
*String Operations*

**Concatenation:**
```python
a = "Hello"
b = "World"
c = a + " " + b
print(c)  # "Hello World"
```

**Repetition:**
```python
print("ha" * 3)  # "hahaha"
```

**Length:**
```python
len("hello")  # 5
```

---





## Constructors in Python : 

A constructor is a method that runs automatically when you create a new object from a class. In Python, the constructor method is:

__init__()


It’s used to set up initial state (like setting default values or initializing variables).

**Constructor Example :**
```python
class Person:
    def __init__(self, name, age):
        self.name = name   # instance variable
        self.age = age

# Create object
p1 = Person("Ravindra", 25)

print(p1.name)  # Output: Ravindra
print(p1.age)   # Output: 25
```

-  __init__ is called automatically when Person() is used to create an object.


**Types of Constructors :**

Python technically only has one constructor (__init__), but conceptually you can think of:

- Default constructor (no arguments except self)

- Parameterized constructor (takes arguments to initialize variables)

---
