
### 1. How is MVT different from MVC architecture?
MVT (Model-View-Template) is similar to MVC (Model-View-Controller), but Django handles the **controller part automatically**.  
In Django:
- **Model** → handles database structure and data.  
- **View** → contains business logic and interacts with the model.  
- **Template** → handles the presentation (HTML).  
The **Django framework itself acts as the controller**, managing how requests are routed between models, views, and templates.

---

### 2. What is the purpose of the Template in Django?
The **Template** in Django is responsible for the **presentation layer**.  
It defines how data sent from the view is displayed on the webpage using **HTML mixed with Django Template Language (DTL)**.  
Templates help separate the logic from the design, making the code cleaner and more maintainable.

---

### 3. How does JavaScript interact with the DOM?
JavaScript interacts with the DOM by **accessing and manipulating HTML elements dynamically**.  
Using JavaScript, developers can:
- Read or modify content and attributes.  
- Change styles and structure.  
- Handle events like clicks or key presses.  
This allows web pages to become interactive and dynamic without reloading.

---

### 4. What is the purpose of innerHTML and textContent in the DOM?
- **innerHTML**: Returns or sets the **HTML content** (including tags) inside an element.  
- **textContent**: Returns or sets only the **text inside an element**, ignoring HTML tags.  
Example:
```javascript
element.innerHTML = "<b>Hello</b>"; 
element.textContent = "<b>Hello</b>"; 
````

---

### 5. How can you dynamically change the content of a webpage using the DOM?

You can change webpage content dynamically by **selecting an element** and **modifying its properties** using JavaScript.
Example:

```javascript
document.getElementById("demo").textContent = "New content added!";
```

You can also update attributes, add styles, or create/remove elements to modify the page structure in real time.

---

### 6. What does the classList property do?

The **classList** property provides an easy way to **add, remove, toggle, or check CSS classes** on an element.
Example:

```javascript
element.classList.add("active");
element.classList.remove("hidden");
element.classList.toggle("dark-mode");
```

It helps manage CSS classes dynamically without manually editing the `class` attribute string.

---

### 7. What is the purpose of the removeChild() method?

The `removeChild()` method is used to **remove a specific child node** from a parent element in the DOM.
Example:

```javascript
let parent = document.getElementById("list");
let child = document.getElementById("item1");
parent.removeChild(child);
```

After execution, the specified child (`item1`) will be deleted from the DOM.

---

### 8. How can you replace an existing DOM element with another element?

You can replace an existing element using the **replaceChild()** method.
Example:

```javascript
let newElem = document.createElement("p");
newElem.textContent = "This is a new paragraph.";

let oldElem = document.getElementById("oldPara");
oldElem.parentNode.replaceChild(newElem, oldElem);
```

This replaces the old element (`oldPara`) with the new one in the DOM.


