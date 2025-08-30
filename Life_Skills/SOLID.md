# Technical Paper: Understanding and Applying SOLID Principles

## Scenario

After joining a new project, I found the codebase to be difficult to read, test, and maintain. My team lead advised me to study design principles that could help improve the structure and scalability of the code. I was introduced to the **SOLID** principles of object-oriented design. This technical paper summarizes these principles and provides example code to help guide our refactoring efforts.

---

## What is SOLID?

SOLID stands for five ideas that help me write code that’s easy to maintain and grow. Robert C. Martin introduced these, and they’re really useful for object-oriented programming.SOLID stands for five ideas that help me write code that’s easy to maintain and grow. Robert C. Martin introduced these, and they’re really useful for object-oriented programming.


![SOLID](https://media.geeksforgeeks.org/wp-content/uploads/20220910005416/SingleResponsibility2.png)

---

## SOLID Principles Overview

#### 1. Single Responsibility Principle (SRP)

    Every class should have just one job. If a class does too many things, it’s tough to change without messing something up.

#### Example:

    A trainee is assigned to write unit tests. If they're also responsible for fixing production bugs and writing documentation at the same time, it becomes chaotic and hard to manage.


#### In code:

### Bad ❌ : One class handles both training progress and HR-related tasks

```python

class Trainee:
    def __init__(self, name):
        self.name = name

    def complete_module(self, module):
        print(f"{self.name} completed {module}")

    def apply_for_leave(self, days):
        print(f"{self.name} applied for {days} days leave")


```

### Good ✅ : Separate responsibilities

```python

class TraineeProgress:

    def __init__(self, trainee_name):
        self.trainee_name = trainee_name

    def complete_module(self, module):
        print(f"{self.trainee_name} completed {module}")

class TraineeLeave:
    def __init__(self, trainee_name):
        self.trainee_name = trainee_name

    def apply_for_leave(self, days):
        print(f"{self.trainee_name} applied for {days} days leave")

```

---


#### 2. Open/Closed Principle (OCP)

    Classes should let me add new features without changing their code. I should extend, not edit.

#### Example:

    A trainee is creating reports for different departments. If they have to change the same report generator every time a new department is added, it violates OCP.

#### In code:

### Bad ❌ : TraineeReport needs to change for each department
```python
class TraineeReport:
    def generate(self, department):
        if department == "HR":
            return "HR Report"
        elif department == "Tech":
            return "Tech Report"
```

### Good ✅ : Extend using inheritance or strategy
```python
class Report:
    def generate(self):
        pass

class HRReport(Report):
    def generate(self):
        return "HR Report"

class TechReport(Report):
    def generate(self):
        return "Tech Report"

def print_report(report: Report):
    print(report.generate())
```

#### 3. Liskov Substitution Principle (LSP)

    If I have a parent class, any child class should work in its place without causing problems.

#### Example:

    Suppose trainees are divided into interns and full-time trainees. All trainees should attend sessions, but only full-time trainees submit daily reports.

#### In code:


### Bad ❌ : Not all subclasses behave like the base class

```python
class Trainee:
    def attend_training(self):
        pass

    def submit_daily_report(self):
        pass  # Interns don’t do this — violates LSP

class Intern(Trainee):
    def submit_daily_report(self):
        raise Exception("Interns do not submit reports")

```

### Good ✅ : Split into proper class hierarchy

```python
class Trainee:
    def attend_training(self):
        pass

class ReportableTrainee(Trainee):
    def submit_daily_report(self):
        pass

class Intern(Trainee):
    pass

class FullTimeTrainee(ReportableTrainee):
    def submit_daily_report(self):
        print("Report submitted")
```

#### 4. Interface Segregation Principle (ISP)

    Don’t make a class use stuff it doesn’t need. Keep interfaces small and specific.

#### Example:

    A trainee shouldn't be forced to implement features like code deployment if their job is just to write test cases.

#### In code:

### Bad ❌ : One interface forces implementation of all duties
```python
class TraineeDuties:
    def write_tests(self): pass
    def deploy_code(self): pass
    def monitor_logs(self): pass

class QAIntern(TraineeDuties):
    def write_tests(self): print("Writing tests")
    def deploy_code(self): pass  # Not needed
    def monitor_logs(self): pass  # Not needed
```

### Good ✅ : Split into smaller interfaces
```python
class TestWriter:
    def write_tests(self): pass

class Deployer:
    def deploy_code(self): pass

class QATrainee(TestWriter):
    def write_tests(self): print("Writing tests")
```

#### 5. Dependency Inversion Principle (DIP)

    High-level modules should not depend on low-level modules.

#### Example:

    A trainee is assigned a task to log training activities. Instead of hardcoding the logging to a text file, the code should depend on an abstraction like a Logger, which can later be swapped to log to a database or cloud service.

#### In code:

### Bad ❌ : Direct dependency on FileLogger
```python
class FileLogger:
    def log(self, message):
        with open("log.txt", "a") as f:
            f.write(message + "\n")

class TraineeActivity:
    def __init__(self):
        self.logger = FileLogger()

    def complete_task(self, task):
        self.logger.log(f"Completed task: {task}")
```

### Good ✅ : Depend on abstraction
```python
class Logger:
    def log(self, message):
        pass

class FileLogger(Logger):
    def log(self, message):
        with open("log.txt", "a") as f:
            f.write(message + "\n")

class ConsoleLogger(Logger):
    def log(self, message):
        print(message)

class TraineeActivity:
    def __init__(self, logger: Logger):
        self.logger = logger

    def complete_task(self, task):
        self.logger.log(f"Completed task: {task}")
```

## Summary 📖

    Using SOLID principles, even in small projects like tracking a trainee’s tasks, helps us write cleaner code that’s easier to understand and update. It also teaches trainees how to write better code and work well with others on a team.


## References 🔗

* [Grammarly](https://www.grammarly.com/)
  
* [Markdown Guide - GitHub](https://guides.github.com/features/mastering-markdown/)
  
* [SOLID Principles - GeeksforGeeks](https://www.geeksforgeeks.org/solid-principle-in-programming-understand-with-real-life-examples/)

* [Digital Ocean](https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design)

* [SOLID Design Principles by Kudvenkat](https://www.youtube.com/playlist?list=PL6n9fhu94yhXjG1w2blMXUzyDrZ_eyOme)
