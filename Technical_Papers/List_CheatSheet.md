# CHEATSHEET (LISTS)
```
| Method                     | Description 
|----------------------------|-------------
| `append(item)`             | Adds an item to the end of the list.
| `extend(iterable)`         | Adds elements of an iterable to the list.
| `insert(index, item)`      | Inserts an item at the given position.
| `remove(item)`             | Removes the first occurrence of the item.
| `pop(index)`               | Removes and returns the item at the index (default: last).
| `clear()`                  | Removes all items from the list.
| `index(item)`              | Returns the index of the first occurrence of the item.
| `count(item)`              | Counts how many times an item appears.
| `sort()`                   | Sorts the list in ascending order.
| `reverse()`                | Reverses the list.
| `copy()`                   | Returns a shallow copy of the list.
| `len(list)`                | Returns the number of items in the list.
| `max(list)`                | Returns the maximum value in the list.
| `min(list)`                | Returns the minimum value in the list.
| `sum(list)`                | Returns the sum of numeric items in the list.
| `all(list)`                | Returns True if all items are truthy.
| `any(list)`                | Returns True if at least one item is truthy.
| `enumerate(list)`          | Returns index-item pairs.
| `sorted(list)`             | Returns a sorted copy (original list unchanged).
| `list()`                   | Converts an iterable to a list.
```

## Method Examples
### 1. append()
```python
colors = ['red', 'green']
colors.append('blue')
print(colors)  # ['red', 'green', 'blue']
```

### 2. extend()
```python
colors = ['red']
colors.extend(['green', 'blue'])
print(colors)  # ['red', 'green', 'blue']
```
### 3. insert()
```python
nums = [1, 3, 4]
nums.insert(1, 2)
print(nums)  # [1, 2, 3, 4]
```
### 4. remove()
```python
letters = ['a', 'b', 'c', 'b']
letters.remove('b')
print(letters)  # ['a', 'c', 'b']
```
### 5. pop()
```python
stack = [10, 20, 30]
print(stack.pop())  # 30
print(stack)        # [10, 20]
```
### 6. clear()
```python
items = [1, 2, 3]
items.clear()
print(items)  # []
```
### 7. index()
```python
fruits = ['apple', 'banana', 'cherry']
print(fruits.index('banana'))  # 1
```
### 8. count()
```python
nums = [1, 2, 2, 3]
print(nums.count(2))  # 2
```
### 9. sort()
```python
numbers = [3, 1, 4, 2]
numbers.sort()
print(numbers)  # [1, 2, 3, 4]
```
### 10. reverse()
```python
values = [1, 2, 3]
values.reverse()
print(values)  # [3, 2, 1]
```
### 11. copy()
```python
original = [1, 2, 3]
cloned = original.copy()
print(cloned)  # [1, 2, 3]
```
### 12. len()
```python
items = ['a', 'b', 'c']
print(len(items))  # 3
```
### 13. max()
```python
nums = [3, 7, 2]
print(max(nums))  # 7
```
### 14. min()
```python
nums = [3, 7, 2]
print(min(nums))  # 2
```
### 15. sum()
```python
nums = [1, 2, 3]
print(sum(nums))  # 6
```
### 16. all()
```python
values = [True, 1, 'hello']
print(all(values))  # True
```
### 17. any()
```python
values = [0, False, 5]
print(any(values))  # True
```
### 18. enumerate()
```python
names = ['Alice', 'Bob']
for index, name in enumerate(names):
    print(index, name)
# Output:
# 0 Alice
# 1 Bob
```
### 19. sorted()
```python
nums = [5, 3, 1]
print(sorted(nums))  # [1, 3, 5]
print(nums)          # [5, 3, 1]
```
### 20. list()
```python
text = "hello"
print(list(text))  # ['h', 'e', 'l', 'l', 'o']
```


## References


- [Python String Methods – Official Docs](https://docs.python.org/3/library/stdtypes.html#string-methods)
- [W3Schools – Python String Methods](https://www.w3schools.com/python/python_ref_string.asp)
- [GeeksforGeeks – Python String Methods](https://www.geeksforgeeks.org/python-string-methods/)

## Author
```
Ravindra Singh Nagarkoti
```