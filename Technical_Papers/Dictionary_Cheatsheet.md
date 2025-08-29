# CHEATSHEET (DICTIONARIES)
```
| Method                     | Description 
|----------------------------|-------------
| `clear()`                  | Removes all items from the dictionary.
| `copy()`                   | Returns a shallow copy of the dictionary.
| `fromkeys(seq, value)`     | Creates a new dictionary from a sequence of keys and a value.
| `get(key, default)`        | Returns the value of the specified key; default if not found.
| `items()`                  | Returns a view object with key-value pairs.
| `keys()`                   | Returns a view object of all keys.
| `values()`                 | Returns a view object of all values.
| `pop(key, default)`        | Removes the item with the specified key.
| `popitem()`                | Removes and returns the last inserted key-value pair.
| `setdefault(key, default)` | Returns the value of a key. If not present, inserts key with default.
| `update([other])`          | Updates the dictionary with elements from another dict or iterable.
| `in`                       | Checks if a key exists in the dictionary.
| `del`                      | Deletes a key-value pair by key.
| `len(dict)`                | Returns the number of key-value pairs.
| `dict()`                   | Creates a dictionary from a sequence or keyword args.
```
## Method Examples
### 1. clear()
```python
d = {'a': 1, 'b': 2}
d.clear()
print(d)  # {}
```
### 2. copy()
```python
original = {'x': 10}
cloned = original.copy()
print(cloned)  # {'x': 10}
```
### 3. fromkeys()
```python
keys = ['a', 'b']
print(dict.fromkeys(keys, 0))  # {'a': 0, 'b': 0}
```
### 4. get()
```python
d = {'a': 1}
print(d.get('a'))        # 1
print(d.get('b', 'N/A')) # N/A
```
### 5. items()
```python
d = {'x': 1, 'y': 2}
for k, v in d.items():
    print(k, v)
# x 1
# y 2
```
### 6. keys()
```python
d = {'name': 'Alice'}
print(d.keys())  # dict_keys(['name'])
```
### 7. values()
```python
d = {'a': 1, 'b': 2}
print(d.values())  # dict_values([1, 2])
```
### 8. pop()
```python
d = {'a': 10, 'b': 20}
print(d.pop('a'))  # 10
print(d)           # {'b': 20}
```
### 9. popitem()
```python
d = {'x': 1, 'y': 2}
print(d.popitem())  # ('y', 2)
print(d)            # {'x': 1}
```
### 10. setdefault()
```python
d = {'x': 1}
print(d.setdefault('x', 100))  # 1
print(d.setdefault('y', 200))  # 200
print(d)  # {'x': 1, 'y': 200}
```
### 11. update()
```python
d1 = {'a': 1}
d2 = {'b': 2}
d1.update(d2)
print(d1)  # {'a': 1, 'b': 2}
```
### 12. in
```python
d = {'name': 'Ravi'}
print('name' in d)  # True
```
### 13. del
```python
d = {'x': 1, 'y': 2}
del d['x']
print(d)  # {'y': 2}
```
### 14. len()
```python
d = {'a': 1, 'b': 2}
print(len(d))  # 2
```
### 15. dict()
```python
pairs = [('a', 1), ('b', 2)]
print(dict(pairs))  # {'a': 1, 'b': 2}
```

## References


- [Python String Methods – Official Docs](https://docs.python.org/3/library/stdtypes.html#string-methods)
- [W3Schools – Python String Methods](https://www.w3schools.com/python/python_ref_string.asp)
- [GeeksforGeeks – Python String Methods](https://www.geeksforgeeks.org/python-string-methods/)

## Author
```
Ravindra Singh Nagarkoti
```