# Python Technical Paper: Array Methods

## Introduction

In Python, arrays are used to store multiple values in a single variable. The most commonly used sequence type is the **list**, which behaves like a dynamic array. Python also offers the `array` module and third-party libraries like `NumPy` for more specialized array operations.

This paper explores built-in list methods (array-like), common array manipulations, and relevant examples.

---

## 1. Built-in Array Type: `list`

Python does not have a built-in array type like other languages (e.g., Java or C++). Instead, it uses `list` as a general-purpose dynamic array.

```python
fruits = ['apple', 'banana', 'cherry']
```
## 2. Common List (Array) Methods

### Method	Description
```
append(x)	        Adds an item to the end of the list.
extend(iterable)	Adds all items from an iterable.
insert(i, x)       	Inserts an item at a given position.
remove(x)       	Removes the first item with the value x.
pop([i])        	Removes and returns item at index (last if none).

clear()	            Removes all items.
index(x)        	Returns index of the first occurrence of x.
count(x)	        Returns number of times x appears.
sort()	            Sorts the list in-place.
reverse()	        Reverses the list in-place.
copy()	            Returns a shallow copy of the list.
```
## 3. Example Usage

#### append() and extend()

```python

numbers = [1, 2, 3]
numbers.append(4)          # [1, 2, 3, 4]
numbers.extend([5, 6])     # [1, 2, 3, 4, 5, 6]

```
#### insert() and remove()
```python
numbers.insert(1, 10)      # [1, 10, 2, 3, 4, 5, 6]
numbers.remove(10)         # [1, 2, 3, 4, 5, 6]
```
#### pop() and clear()
```python

last = numbers.pop()       # Removes 6
numbers.clear()            # []
```

#### index(x)
```python
fruits = ['apple', 'banana', 'cherry', 'banana']
index_of_banana = fruits.index('banana')
print(index_of_banana)  # Output: 1
```
#### count(x)
```python
numbers = [1, 2, 3, 2, 2, 4]
count_of_2 = numbers.count(2)
print(count_of_2)  # Output: 3
```
#### sort()
```python
scores = [50, 20, 90, 70]
scores.sort()
print(scores)  # Output: [20, 50, 70, 90]
```

You can also sort in descending order:
```python
scores.sort(reverse=True)
print(scores)  # Output: [90, 70, 50, 20]
```
#### reverse()
```python
colors = ['red', 'green', 'blue']
colors.reverse()
print(colors)  # Output: ['blue', 'green', 'red']
```
#### copy()
```python
original = [1, 2, 3]
duplicate = original.copy()
duplicate.append(4)

print(original)  # Output: [1, 2, 3]
print(duplicate) # Output: [1, 2, 3, 4]
```
## 4. Iterating Over Lists
```python

colors = ['red', 'green', 'blue']
for color in colors:
    print(color.upper())
```
## 5. List Comprehension (Array-Like Feature)

List comprehensions offer a concise way to create arrays:

```python

squares = [x**2 for x in range(5)]  # [0, 1, 4, 9, 16]
```
## 6. Alternatives: array Module
For numerical data, Python’s array module provides more memory-efficient arrays.

```python

from array import array

a = array('i', [1, 2, 3])
a.append(4)
print(a)  # array('i', [1, 2, 3, 4])
```
## 7. Third-Party Arrays: NumPy
For large-scale numerical computations, NumPy is widely used:

```python

import numpy as np

arr = np.array([1, 2, 3])
print(arr + 1)  # [2 3 4]
```
## Conclusion
```
Python provides flexible and powerful tools for working with arrays via built-in lists and the array module. Understanding these methods is crucial for effective data manipulation and performance in both general programming and scientific computing.
```
## References


1. [Python Lists – Python Docs](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists)
2. [array — Efficient arrays of numeric values – Python Docs](https://docs.python.org/3/library/array.html)
3. [NumPy Array Creation – NumPy Docs](https://numpy.org/doc/stable/user/basics.creation.html)
4. [Python List Methods – W3Schools](https://www.w3schools.com/python/python_lists_methods.asp)



## Author

```
Ravindra Singh Nagarkoti
```