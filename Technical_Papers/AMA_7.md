# AMA - 7

---

### **1. What exactly happens when we run `python manage.py runserver`?**

When we run this command, Django starts its development server.
It first checks all the settings and installed apps, then applies URL routing and loads middleware.
After that, it starts listening for incoming requests (by default on port 8000).
This server is used only for testing or local development — not for production.

---

### **2. What is the use of `INSTALLED_APPS` in `settings.py`?**

`INSTALLED_APPS` is a list in the settings file where we mention all the apps that our project will use.
It includes both built-in Django apps (like admin, auth) and the custom apps we create.
If an app is not added here, Django won’t detect its models or migrations.

---

### **3. How does Django handle user authentication?**

Django has a built-in authentication system that manages users, passwords, groups, and permissions.
It provides ready-to-use methods like `login()`, `logout()`, and `authenticate()` to handle user login and logout easily.
We can also use `@login_required` to protect views that should be visible only to logged-in users.

---

### **4. What is the use of the `@login_required` decorator?**

The `@login_required` decorator is used to make sure that only logged-in users can access a particular view.
If someone tries to open that view without logging in, Django automatically redirects them to the login page.
It helps in securing pages like user profile or dashboard.

---

### **5. What are class-based views (CBVs) in Django?**

Class-Based Views are views written as Python classes instead of normal functions.
They help in reusing and organizing code better.
Django already provides some built-in CBVs like `ListView`, `DetailView`, `CreateView`, and `UpdateView`.
They reduce repetitive code and make big projects easier to manage.

---

### **6. What is the use of `@csrf_exempt`?**

`@csrf_exempt` is used to disable CSRF protection for a specific view.
Normally, Django protects all POST requests from CSRF attacks.
But in some cases like APIs or webhook calls, we may need to disable it using this decorator.
It should be used carefully because it removes that layer of security.

---

### **7. What is the difference between `STATICFILES_DIRS` and `STATIC_ROOT`?**

* `STATICFILES_DIRS` is used in development to tell Django where our static files (CSS, JS, images) are located.
* `STATIC_ROOT` is used in production.
  When we run `python manage.py collectstatic`, all static files from different apps are collected into this single folder.

In short:
`STATICFILES_DIRS` → where files are kept during development
`STATIC_ROOT` → where all files are collected for deployment

---

### **8. What is the difference between `__str__()` and `__repr__()` in models?**

In Django models, `__str__()` is used to return a readable name for an object when we print it.
It helps in displaying clear names in the admin panel or shell.

Example:

```python
def __str__(self):
    return self.name
```

`__repr__()` is more for developers. It gives an unambiguous representation of the object (used mostly for debugging).
In short:

* `__str__()` → user-friendly display
* `__repr__()` → developer-friendly display

---

