

# Django Review Points

---

## 1. Settings File

### What is `SECRET_KEY`?

* `SECRET_KEY` is **a random string** that Django uses to make your website secure.
* It’s used in things like:

  1. **Session cookies** – Keeps track of logged-in users
  2. **CSRF tokens** – Prevents other websites from sending fake requests
  3. **Password reset links** – Makes sure links are valid and secure
* **Important:**

  * Never share it publicly
  * Never commit it to GitHub
  * For production, use **environment variables**

**Example:**

```python
import os

SECRET_KEY = os.environ.get('DJANGO_SECRET_KEY', 'dev-secret-key')
```

> Tip: Use long, random strings like `"2dj!3#ksdlf@...$kdkf"` for real projects.

---

### Default Django Apps in `INSTALLED_APPS`

When you create a project, Django automatically adds some apps:

| App                           | What it does                              |
| ----------------------------- | ----------------------------------------- |
| `django.contrib.admin`        | Admin panel for managing models and data  |
| `django.contrib.auth`         | Handles users, groups, and permissions    |
| `django.contrib.contenttypes` | Keeps track of all models in the project  |
| `django.contrib.sessions`     | Stores session data (cookies, DB, etc.)   |
| `django.contrib.messages`     | Shows temporary messages to users         |
| `django.contrib.staticfiles`  | Handles static files like CSS, JS, images |

> You can also add extra apps if needed:
>
> * `django.contrib.sites` → Multiple sites
> * Third-party apps → `rest_framework` for APIs

---

### What is Middleware?

* Middleware is like a **layer that sits between request and response**.
* Every request goes through middleware before reaching your view, and every response goes through it before going to the user.
* You can **modify requests or responses**, block requests, or add extra security.

**Common Middleware in Django:**

* `SecurityMiddleware` → Adds security headers
* `SessionMiddleware` → Manages user sessions
* `AuthenticationMiddleware` → Checks logged-in user
* `MessageMiddleware` → Stores flash messages
* `CsrfViewMiddleware` → Prevents CSRF attacks
* `XFrameOptionsMiddleware` → Prevents clickjacking

**Example in `settings.py`:**

```python
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```

**How it works:**

1. Request enters → top middleware runs first
2. Request reaches view → view returns response
3. Response passes back through middleware → sent to browser

> Middleware can also be custom. For example, you can make one that logs every request.

---

### Django Security

1. **CSRF (Cross-Site Request Forgery)**

   * Attack: Makes a logged-in user unknowingly submit forms.
   * Django adds **CSRF tokens** to forms. Always use:

```html
<form method="POST">
  {% csrf_token %}
  ...
</form>
```

2. **XSS (Cross-Site Scripting)**

   * Attack: Malicious script in input field runs in user’s browser.
   * Django **escapes HTML automatically** in templates.
   * Safe way to show user input: `{{ user_input }}`

3. **Clickjacking**

   * Attack: Hides your site in a frame and tricks users to click.
   * Fix:

```python
X_FRAME_OPTIONS = 'DENY'
```

4. **Other security tips:**

   * Always set `DEBUG = False` in production
   * Use `SecurityMiddleware` to force HTTPS and HSTS
   * Regularly update Django to latest version

---

### WSGI

* WSGI = **Web Server Gateway Interface**
* It’s a **bridge** between your Django app and web server like Nginx, Apache, or Gunicorn.
* In production, server calls `wsgi.py` to run your Django app.

**Example `wsgi.py`:**

```python
from django.core.wsgi import get_wsgi_application

application = get_wsgi_application()
```

> Note: Django 5+ also supports **ASGI** for async requests.

---

## 2. Models

### `on_delete=models.CASCADE`

* When you delete a record, related records are **also deleted** automatically.
* Example:

```python
class Author(models.Model):
    name = models.CharField(max_length=100)

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
```

* If an Author is deleted, all their Books are deleted too.

**Other options:**

* `SET_NULL` → Set FK to NULL if parent deleted
* `PROTECT` → Prevent deletion if related objects exist
* `DO_NOTHING` → Does nothing (may break DB integrity)

---

### Fields & Validators

**Common fields:**

| Field         | Description                       |
| ------------- | --------------------------------- |
| CharField     | Short text, must set `max_length` |
| TextField     | Long text                         |
| IntegerField  | Whole numbers                     |
| BooleanField  | True/False                        |
| DateTimeField | Stores date + time                |
| EmailField    | Validates email                   |
| URLField      | Validates URLs                    |

**Validators:** Ensure data is correct

```python
from django.core.validators import MinValueValidator, MaxValueValidator

age = models.IntegerField(validators=[MinValueValidator(0), MaxValueValidator(120)])
```

**Tips:** You can also make **custom validators** by writing a Python function.

---

### Python Module vs Class

* **Module:** Python file containing code (`models.py`)
* **Class:** Blueprint for objects

```python
class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
```

* Models are always classes inheriting from `models.Model`.

---

## 3. Django ORM

### Basic Queries

```python
from myapp.models import Book


books = Book.objects.all()


books_by_john = Book.objects.filter(author__name="John")


book = Book.objects.get(id=1)
```

**Notes:**

* `all()` → Returns all records
* `filter()` → Returns queryset matching condition
* `get()` → Returns single object, raises error if not found

---

### Turning ORM into SQL

```python
qs = Book.objects.filter(author__name="John")
print(qs.query)
```

* Useful to see what SQL Django runs in the background.

---

### Aggregations

* Count, sum, average, min, max:

```python
from django.db.models import Avg, Count, Sum, Min, Max

Book.objects.aggregate(Avg('price'))  
Book.objects.aggregate(Sum('pages')) 
Author.objects.annotate(num_books=Count('book'))  
```

* `annotate()` adds **new fields** to each object in queryset.

---

### Migrations

* Migration = **file that tracks changes in models**
* Commands:

```bash
python manage.py makemigrations  
python manage.py migrate         
```

* Always run migrations after **adding/changing models or fields**.

---

### SQL Transactions

* A **transaction** = a group of DB operations executed as a unit.
* Either all succeed or all fail → called **atomicity**.

---

### Atomic Transactions

```python
from django.db import transaction

@transaction.atomic
def create_order(user, items):
    order = Order.objects.create(user=user)
    for item in items:
        OrderItem.objects.create(order=order, product=item)
```

* If anything fails, **everything rolls back automatically**.
* Useful for payment processing or critical DB updates.

---
