# CHEATSHEET (SETS)
```
| Method                       | Description 
|------------------------------|-------------
| `add(item)`                  | Adds an element to the set.
| `clear()`                    | Removes all elements from the set.
| `copy()`                     | Returns a shallow copy of the set.
| `difference(set)`            | Returns elements in current set but not in another.
| `difference_update(set)`     | Removes elements found in another set.
| `discard(item)`              | Removes an element if it exists (no error if not).
| `intersection(set)`          | Returns elements common to both sets.
| `intersection_update(set)`   | Updates current set with common elements.
| `isdisjoint(set)`            | Returns True if sets have no common elements.
| `issubset(set)`              | Returns True if current set is subset of another.
| `issuperset(set)`            | Returns True if current set is superset of another.
| `pop()`                      | Removes and returns an arbitrary element.
| `remove(item)`               | Removes an element (raises error if not found).
| `symmetric_difference(set)`  | Returns elements in either set but not both.
| `symmetric_difference_update(set)` | Updates set with symmetric difference.
| `union(set)`                 | Returns all elements from both sets.
| `update(set)`                | Adds elements from another set.
| `in`                         | Checks if element exists in set.
| `len(set)`                   | Returns number of elements.
| `set()`                      | Creates a set.
```
## Method Examples
### 1. add()
```python
s = {1, 2}
s.add(3)
print(s)  # {1, 2, 3}
```
### 2. clear()
```python
s = {1, 2, 3}
s.clear()
print(s)  # set()
```
### 3. copy()
```python
s1 = {1, 2}
s2 = s1.copy()
print(s2)  # {1, 2}
```
### 4. difference()
```python
a = {1, 2, 3}
b = {2, 3, 4}
print(a.difference(b))  # {1}
```
### 5. difference_update()
```python
a = {1, 2, 3}
b = {2, 3}
a.difference_update(b)
print(a)  # {1}
```
### 6. discard()
```python
s = {1, 2, 3}
s.discard(2)
print(s)  # {1, 3}
```
### 7. intersection()
```python
a = {1, 2, 3}
b = {2, 3, 4}
print(a.intersection(b))  # {2, 3}
```
### 8. intersection_update()
```python
a = {1, 2, 3}
b = {2, 3, 4}
a.intersection_update(b)
print(a)  # {2, 3}
```
### 9. isdisjoint()
```python
a = {1, 2}
b = {3, 4}
print(a.isdisjoint(b))  # True
```
### 10. issubset()
```python
a = {1, 2}
b = {1, 2, 3}
print(a.issubset(b))  # True
```
### 11. issuperset()
```python
a = {1, 2, 3}
b = {1, 2}
print(a.issuperset(b))  # True
```
### 12. pop()
```python
s = {1, 2, 3}
print(s.pop())  # Removes and returns random element
```
### 13. remove()
```python
s = {1, 2, 3}
s.remove(2)
print(s)  # {1, 3}
```
### 14. symmetric_difference()
```python
a = {1, 2, 3}
b = {3, 4}
print(a.symmetric_difference(b))  # {1, 2, 4}
```
### 15. symmetric_difference_update()
```python
a = {1, 2, 3}
b = {3, 4}
a.symmetric_difference_update(b)
print(a)  # {1, 2, 4}
```
### 16. union()
```python
a = {1, 2}
b = {2, 3}
print(a.union(b))  # {1, 2, 3}
```
### 17. update()
```python
a = {1, 2}
a.update({3, 4})
print(a)  # {1, 2, 3, 4}
```
### 18. in
```python
s = {1, 2, 3}
print(2 in s)  # True
```
### 19. len()
```python
s = {1, 2, 3}
print(len(s))  # 3
```
### 20. set()
```python
chars = "hello"
print(set(chars))  # {'h', 'e', 'l', 'o'}
```

## References


- [Python String Methods – Official Docs](https://docs.python.org/3/library/stdtypes.html#string-methods)
- [W3Schools – Python String Methods](https://www.w3schools.com/python/python_ref_string.asp)
- [GeeksforGeeks – Python String Methods](https://www.geeksforgeeks.org/python-string-methods/)

## Author
```
Ravindra Singh Nagarkoti
```