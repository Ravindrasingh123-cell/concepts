# Python Technical Paper: String Methods

## Introduction

Strings are one of the most commonly used data types in Python. They are sequences of characters used for storing and manipulating text. Python provides a rich set of built-in string methods that make text processing easy and efficient.

This paper covers the most frequently used string methods with practical examples.

---

## Common String Methods in Python
```
| Method                  | Description 
|-------------------------|-------------
| `lower()`               | Converts all characters to lowercase. 
| `upper()`               | Converts all characters to uppercase. 
| `capitalize()`          | Capitalizes the first character. 
| `title()`               | Capitalizes the first character of each word. 
| `strip()`               | Removes leading and trailing whitespaces. 
| `replace(old, new)`     | Replaces all occurrences of a substring. 
| `split(separator)`      | Splits the string into a list. 
| `join(iterable)`        | Joins the elements of an iterable into a string. 
| `find(substring)`       | Returns the index of the first occurrence of a substring. 
| `count(substring)`      | Counts occurrences of a substring. 
| `startswith(prefix)`    | Checks if string starts with specified prefix. 
| `endswith(suffix)`      | Checks if string ends with specified suffix. 
| `rfind(substring)`      | Returns highest index of substring. 
| `isalpha()`             | Checks if all characters are alphabetic. 
| `isdigit()`             | Checks if all characters are digits. 
| `isalnum()`             | Checks if all characters are alphanumeric. 
| `isspace()`             | Checks if string contains only whitespaces. 
| `swapcase()`            | Swaps case of each character. 
| `lstrip()`              | Removes leading whitespaces. 
| `rstrip()`              | Removes trailing whitespaces. 
| `zfill(width)`          | Pads string on the left with zeros. 
```

## Method Examples
### 1. lower()
```python
text = "HeLLo WoRLD"
print(text.lower())  # hello world
```

### 2. upper()
```python
text = "hello"
print(text.upper())  # HELLO
```
### 3. capitalize()
```python
text = "python programming"
print(text.capitalize())  # Python programming
```
### 4. title()
```python
text = "welcome to python"
print(text.title())  # Welcome To Python
```
### 5. strip()
```python
text = "  hello  "
print(text.strip())  # "hello"
```
### 6. replace()
```python
text = "I love Java"
print(text.replace("Java", "Python"))  # I love Python
```
### 7. split()
```python
text = "apple,banana,cherry"
print(text.split(","))  # ['apple', 'banana', 'cherry']
```
### 8. join()
```python
items = ['a', 'b', 'c']
print("-".join(items))  # a-b-c
```
### 9. find()
```python
text = "Hello world"
print(text.find("world"))  # 6
```
### 10.  count()
```python
text = "banana"
print(text.count("a"))  # 3
```
### 11.  startswith()
```python
text = "hello world"
print(text.startswith("hello"))  # True
```
### 12.  endswith()
```python
text = "myfile.txt"
print(text.endswith(".txt"))  # True
```
### 13.  rfind()
```python
text = "banana"
print(text.rfind("a"))  # 5
```
### 14.  isalpha()
```python
text = "Python"
print(text.isalpha())  # True
```
### 15.  isdigit()
```python
text = "12345"
print(text.isdigit())  # True
```
### 16.  isalnum()
```python
text = "abc123"
print(text.isalnum())  # True
```
### 17.  isspace()
```python
text = "   "
print(text.isspace())  # True
```
### 18.  swapcase()
```python
text = "HeLLo WoRLd"
print(text.swapcase())  # hEllO wOrlD
```
### 19.  lstrip()
```python
text = "   hello"
print(text.lstrip())  # 'hello'
```
### 20.  rstrip()
```python
text = "hello   "
print(text.rstrip())  # 'hello'
```
### 21.  zfill()
```python
text = "42"
print(text.zfill(5))  # 00042
```
## Conclusion
```
Python provides a comprehensive set of string methods that simplify string handling. Mastering these methods allows developers to write efficient and readable code when dealing with text.
```

## References

- [Python String Methods – Official Docs](https://docs.python.org/3/library/stdtypes.html#string-methods)
- [W3Schools – Python String Methods](https://www.w3schools.com/python/python_ref_string.asp)
- [GeeksforGeeks – Python String Methods](https://www.geeksforgeeks.org/python-string-methods/)


## Author

```
Ravindra Singh Nagarkoti
```
