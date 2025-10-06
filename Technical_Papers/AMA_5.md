# AMA - 5


## AMA Questions

### 1. What is the difference between document.getElementById() and document.querySelector()?

- document.getElementById("id") is used to select an element by its unique id. It only works with IDs and directly returns the element.

- document.querySelector("selector") is more flexible. It can select elements using CSS selectors (.class, #id, tag, attribute selectors, etc.).

In short, getElementById is faster and limited to IDs, while querySelector is more powerful and versatile.

### 2. What is the DOM (Document Object Model)? How does JavaScript interact with it?

- The DOM is a tree-like structure that represents the content of a web page. Every HTML element (like ```<div>```, ```<p>```, ```<img>```) becomes a node in this tree.

- JavaScript can access and manipulate the DOM to change content, styles, or structure dynamically.

For example, adding text, updating CSS, creating elements, or listening to events (like clicks) all happen through the DOM.

### 3. Arrow functions were introduced in ES6. They give a shorter syntax to write functions.

The biggest difference is that arrow functions do not have their own this. They take this from the surrounding context (lexical scope).

Also, arrow functions cannot be used as constructors (can’t use new with them).

*Example*:

- normal function
```js
function add(a, b) {
  return a + b;
}
```
- arrow function
```js
const addArrow = (a, b) => a + b;
```

### 4. What is the difference between a web server and an application server?

- A web server (like Apache, Nginx) mainly handles HTTP requests and serves static content such as HTML, CSS, JavaScript, or images.

- An application server (like Node.js, Django, Spring Boot) contains business logic. It processes requests, interacts with databases, and prepares dynamic responses.

- In simple terms:

  - Web server = static content delivery

  - Application server = dynamic logic and data processing

### 5. Explain the request/response cycle in a web application.

- The user enters a URL or clicks a link → Browser sends an HTTP request to the server.

- The request goes through DNS resolution, then reaches a web server or application server.

- The server processes it (may talk to a database) and creates a response.

- The server sends back an HTTP response (status code, headers, body).

- The browser receives it, parses HTML, loads CSS/JS, and finally renders the page for the user.

### 6. What is the difference between inline, internal, and external JavaScript?

- Inline JavaScript: JS code written directly inside an element’s attribute.
*Example*: 
```js
<button onclick="alert('Hello')">Click</button>
```

- Internal JavaScript: JS code written inside ```<script>``` tags in the HTML file.
*Example*:
```js
<script>
  console.log("Internal JS");
</script>
```

- External JavaScript: JS written in a separate .js file and linked using 
  ```js
  <script src="file.js"></script>
  ```
This is the best practice as it keeps code clean and reusable.

### 7. Explain the concept of scope and scope chain in JavaScript.

- Scope defines where variables and functions are accessible in code.

- Global scope: accessible everywhere

- Function scope: variables inside a function are only available inside it

- Block scope (let, const): accessible only within { } block

- Scope chain: If JavaScript can’t find a variable in the current scope, it looks outward in the parent scopes until it reaches the global scope.

*Example*: If a variable is not inside a function, JS searches its parent function and then the global scope.
