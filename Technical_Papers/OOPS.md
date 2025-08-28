# Objects and Object-Oriented Programming (OOP) in Python

## Introduction

Object-Oriented Programming (OOP) is a programming paradigm based on the concept of "objects". Objects are instances of classes, which bundle data (attributes) and behavior (methods) together. OOP helps to organize code, making it reusable, modular, and easier to maintain.

This paper explains key OOP concepts using a real-world example of a 

**Training Employee**.

---

## Key Concepts of OOP

### 1. Class

A **class** is a blueprint or template for creating objects. It defines attributes (data) and methods (functions) that its objects will have.

#### Example:

```python
class TrainingEmployee:
    def __init__(self, name, role, experience):
        self.name = name
        self.role = role
        self.experience = experience  # in years
```
Here, TrainingEmployee is a class with attributes name, role, and experience.

### 2. Object (Instance)
An object is an individual instance of a class. Each object has its own values for the attributes defined in the class.

Example:
```python

emp1 = TrainingEmployee("Alice", "Data Analyst", 2)
emp2 = TrainingEmployee("Bob", "Software Developer", 3)
```
emp1 and emp2 are two objects of the TrainingEmployee class with different attribute values.

### 3. Methods
Methods are functions defined inside a class that describe the behaviors or actions that an object can perform.

Example:
```python

class TrainingEmployee:
    def __init__(self, name, role, experience):
        self.name = name
        self.role = role
        self.experience = experience

    def introduce(self):
        print(f"Hello, my name is {self.name} and I work as a {self.role}.")

    def years_of_experience(self):
        print(f"I have {self.experience} years of experience.")
```
You can call these methods on the object:

```python

emp1.introduce()          # Output: Hello, my name is Alice and I work as a Data Analyst.
emp2.years_of_experience() # Output: I have 3 years of experience.
```
### 4. Encapsulation
Encapsulation means bundling the data (attributes) and methods into a single unit (class), and restricting access to some components. This protects the internal state of the object.

Example of private attribute:

```python

class TrainingEmployee:
    def __init__(self, name, salary):
        self.name = name
        self.__salary = salary  # private attribute

    def get_salary(self):
        return self.__salary
```
Here, __salary is private and cannot be accessed directly outside the class:

```python

emp = TrainingEmployee("Alice", 70000)
print(emp.get_salary())  # Works fine
print(emp.__salary)      # Raises AttributeError
```
### 5. Inheritance
Inheritance allows a class (child class) to inherit attributes and methods from another class (parent class), promoting code reuse.

Example:

```python

class Employee:
    def __init__(self, name, role):
        self.name = name
        self.role = role

    def work(self):
        print(f"{self.name} is working as a {self.role}.")

class Trainer(Employee):
    def conduct_training(self):
        print(f"{self.name} is conducting training sessions.")
```
```python

trainer = Trainer("Bob", "Trainer")
trainer.work()               # Output: Bob is working as a Trainer.
trainer.conduct_training()   # Output: Bob is conducting training sessions.
```
### 6. Polymorphism
Polymorphism means the ability to use the same method name in different classes with different behaviors.

Example:

```python

class Employee:
    def work(self):
        print("Employee is working.")

class Trainer(Employee):
    def work(self):
        print("Trainer is conducting a training session.")

class Developer(Employee):
    def work(self):
        print("Developer is writing code.")

employees = [Trainer(), Developer()]

for emp in employees:
    emp.work()
```
Output:

```python

Trainer is conducting a training session.
Developer is writing code.
```
## Summary
- **Class**  
  A class is a blueprint or template for creating objects. It defines the properties (attributes) and behaviors (methods) that the objects created from it will have.  
  *Example:* `TrainingEmployee` class defines what a training employee is.

- **Object**  
  An object is a specific instance of a class with its own unique data. When you create an object, you are creating a real-world entity based on the class blueprint.  
  *Example:* `emp1 = TrainingEmployee("Alice", "Analyst")` creates an object representing Alice.

- **Methods**  
  Methods are functions defined inside a class that describe the actions or behaviors an object can perform.  
  *Example:* Methods like `introduce()` and `years_of_experience()` allow a TrainingEmployee object to perform actions like introducing themselves.

- **Encapsulation**  
  Encapsulation is the practice of hiding internal object details (data) and only exposing what is necessary through methods, protecting the object's internal state.  
  *Example:* The private attribute `__salary` is not accessible directly from outside the class but can be accessed through a method like `get_salary()`.

- **Inheritance**  
  Inheritance allows a child class to inherit attributes and methods from a parent class, promoting code reuse and hierarchical relationships.  
  *Example:* The `Trainer` class inherits from the `Employee` class and can add or override methods.

- **Polymorphism**  
  Polymorphism lets methods in different classes have the same name but behave differently depending on the class of the object calling the method.  
  *Example:* The `work()` method behaves differently for `Trainer` and `Developer` objects even though it shares the same name.

## References
- [Python Classes and Objects – Official Docs](https://docs.python.org/3/tutorial/classes.html)
- [Real Python – OOP in Python](https://realpython.com/python3-object-oriented-programming/)
- [GeeksforGeeks – Object Oriented Programming in Python](https://www.geeksforgeeks.org/python-object-oriented-programming/)


## Author

```
Ravindra Singh Nagarkoti
```