# Synchronous JavaScript Concepts 

## Data Types

JavaScript has two main categories of data types:

### Primitive Types
- **Number**: `42`, `3.14`, `NaN`, `Infinity`
- **String**: `"Hello"`, `'World'`, `` `Template` ``
- **Boolean**: `true`, `false`
- **Undefined**: `undefined`
- **Null**: `null`
- **Symbol**: `Symbol('description')`
- **BigInt**: `123n`

### Reference Types
- **Object**: `{}`, `[]`, `new Date()`
- **Function**: `function() {}`
- **Array**: `[1, 2, 3]`

```javascript
// Examples
let num = 42;
let str = "Hello";
let bool = true;
let obj = { name: "Ravindra" };
let arr = [1, 2, 3];
let func = function() { return "Hello"; };
```

---

## Variable Declarations

### let, var, const

#### `let`
- Block-scoped
- Cannot be redeclared in same scope
- Hoisted but not initialized (Temporal Dead Zone)

```javascript
let name = "Ravindra";
// let name = "Ravindra"; // Error: Identifier 'name' has already been declared
```

#### `var`
- Function-scoped or globally-scoped
- Can be redeclared
- Hoisted and initialized with `undefined`

```javascript
var age = 25;
var age = 25; // No error, redeclaration allowed
```

#### `const`
- Block-scoped
- Cannot be reassigned
- Must be initialized at declaration
- For objects/arrays, the reference is constant but content can change

```javascript
const PI = 3.14159;
// PI = 3.14; // Error: Assignment to constant variable

const person = { name: "Ravindra" };
person.name = "Ravindra"; // OK - modifying object content
// person = {}; // Error - cannot reassign the reference
```

### Why We Must Not Use `var`

1. **Function Scope Issues**: `var` is function-scoped, not block-scoped
2. **Hoisting Problems**: Variables are hoisted and initialized with `undefined`
3. **Redeclaration**: Can be redeclared without error
4. **Loop Issues**: Creates closure problems in loops

```javascript
// Problem with var in loops
for (var i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 100); // Prints 3, 3, 3
}

// Solution with let
for (let i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 100); // Prints 0, 1, 2
}
```

### Why Global Variables Are Bad

1. **Namespace Pollution**: Can conflict with other variables
2. **Debugging Difficulty**: Hard to track where variables are modified
3. **Memory Issues**: Stay in memory longer than needed
4. **Security Risks**: Can be accessed and modified by any code
5. **Testing Problems**: Make unit testing difficult

```javascript
// Bad - Global variable
var globalCounter = 0;

// Good - Encapsulated in module/function
const counterModule = (() => {
    let counter = 0;
    return {
        increment: () => ++counter,
        getValue: () => counter
    };
})();
```

---

## Truthy and Falsy Values

### Falsy Values
- `false`
- `0`
- `-0`
- `0n` (BigInt)
- `""` (empty string)
- `null`
- `undefined`
- `NaN`

### Truthy Values
Everything else is truthy, including:
- `"0"` (string zero)
- `"false"` (string false)
- `[]` (empty array)
- `{}` (empty object)
- `function() {}` (empty function)

```javascript
// Falsy examples
if (false) console.log("won't print");
if (0) console.log("won't print");
if ("") console.log("won't print");
if (null) console.log("won't print");
if (undefined) console.log("won't print");

// Truthy examples
if ("0") console.log("will print");
if ([]) console.log("will print");
if ({}) console.log("will print");
```

---

## Function Hoisting

Function declarations are hoisted completely, meaning they can be called before they are declared.

```javascript
// This works - function is hoisted
sayHello(); // "Hello!"

function sayHello() {
    console.log("Hello!");
}

// This doesn't work - variable is hoisted but not initialized
sayGoodbye(); // TypeError: sayGoodbye is not a function

var sayGoodbye = function() {
    console.log("Goodbye!");
};
```

---

## Function Declarations

### What Happens When Function Has No Return Statement

Functions without explicit return statements return `undefined`.

```javascript
function noReturn() {
    console.log("Hello");
    // No return statement
}

let result = noReturn(); // undefined
console.log(result); // undefined
```

### Different Ways of Declaring Functions

#### 1. Function Declaration
```javascript
function add(a, b) {
    return a + b;
}
```

#### 2. Function Expression
```javascript
const add = function(a, b) {
    return a + b;
};
```

#### 3. Arrow Function
```javascript
const add = (a, b) => a + b;
const addWithBraces = (a, b) => {
    return a + b;
};
```

#### 4. Named Function Expression
```javascript
const add = function addNumbers(a, b) {
    return a + b;
};
```

#### 5. Constructor Function
```javascript
const add = new Function('a', 'b', 'return a + b');
```

---

## Pass by Reference vs Pass by Value

### Primitive Types (Pass by Value)
```javascript
let a = 5;
let b = a;
b = 10;
console.log(a); // 5 (unchanged)
console.log(b); // 10
```

### Reference Types (Pass by Reference)
```javascript
let obj1 = { value: 5 };
let obj2 = obj1;
obj2.value = 10;
console.log(obj1.value); // 10 (changed)
console.log(obj2.value); // 10
```

### Function Parameters
```javascript
// Primitive - value is copied
function changeNumber(num) {
    num = 10;
}
let x = 5;
changeNumber(x);
console.log(x); // 5 (unchanged)

// Object - reference is copied
function changeObject(obj) {
    obj.value = 10;
}
let myObj = { value: 5 };
changeObject(myObj);
console.log(myObj.value); // 10 (changed)
```

---

## Loops

### 1. Traditional For Loop (with numbers)
```javascript
for (let i = 0; i < 5; i++) {
    console.log(i); // 0, 1, 2, 3, 4
}
```

### 2. For...in Loop (object properties)
```javascript
const person = { name: "Ravindra", age: 25, city: "Bangalore" };
for (let key in person) {
    console.log(key + ": " + person[key]);
}
// name: Ravindra
// age: 25
// city: Bangalore
```

### 3. For...of Loop (iterable values)
```javascript
const fruits = ["apple", "banana", "orange"];
for (let fruit of fruits) {
    console.log(fruit);
}
// apple
// banana
// orange
```

### 4. forEach Method
```javascript
const numbers = [1, 2, 3, 4, 5];
numbers.forEach((num, index) => {
    console.log(`Index ${index}: ${num}`);
});
```

---

## Array Methods

### Popular Array Utility Methods

#### Immutable Methods (return new array)
```javascript
const numbers = [1, 2, 3, 4, 5];

// map - transform each element
const doubled = numbers.map(x => x * 2);
console.log(doubled); // [2, 4, 6, 8, 10]

// filter - select elements based on condition
const evens = numbers.filter(x => x % 2 === 0);
console.log(evens); // [2, 4]

// reduce - reduce array to single value
const sum = numbers.reduce((acc, curr) => acc + curr, 0);
console.log(sum); // 15

// slice - extract portion of array
const middle = numbers.slice(1, 4);
console.log(middle); // [2, 3, 4]

// concat - combine arrays
const combined = numbers.concat([6, 7, 8]);
console.log(combined); // [1, 2, 3, 4, 5, 6, 7, 8]
```

#### Mutable Methods (modify original array)
```javascript
const numbers = [1, 2, 3, 4, 5];

// push - add to end
numbers.push(6);
console.log(numbers); // [1, 2, 3, 4, 5, 6]

// pop - remove from end
numbers.pop();
console.log(numbers); // [1, 2, 3, 4, 5]

// shift - remove from beginning
numbers.shift();
console.log(numbers); // [2, 3, 4, 5]

// unshift - add to beginning
numbers.unshift(1);
console.log(numbers); // [1, 2, 3, 4, 5]

// splice - add/remove elements at specific position
numbers.splice(2, 1, 10); // Remove 1 element at index 2, insert 10
console.log(numbers); // [1, 2, 10, 4, 5]
```

### When to Use forEach vs Array Methods

#### Use forEach when:
- You need to perform side effects
- You don't need to return a new array
- You want to iterate without transformation

```javascript
const numbers = [1, 2, 3, 4, 5];
numbers.forEach(num => console.log(num)); // Side effect: logging
```

#### Use map when:
- You need to transform each element
- You want a new array with same length

```javascript
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(x => x * 2);
```

#### Use filter when:
- You need to select elements based on condition
- You want a subset of the original array

```javascript
const numbers = [1, 2, 3, 4, 5];
const evens = numbers.filter(x => x % 2 === 0);
```

#### Use reduce when:
- To reduce array to single value
- Need custom accumulation logic

```javascript
const numbers = [1, 2, 3, 4, 5];
const sum = numbers.reduce((acc, curr) => acc + curr, 0);
```

### Array Method Chaining
```javascript
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

const result = numbers
    .filter(x => x % 2 === 0)    // [2, 4, 6, 8, 10]
    .map(x => x * 2)              // [4, 8, 12, 16, 20]
    .reduce((acc, curr) => acc + curr, 0); // 60

console.log(result); // 60
```

---

## String Methods

### Popular String Utility Methods

```javascript
const str = "  Hello World  ";

// Basic methods
console.log(str.length);           // 15
console.log(str.toUpperCase());    // "  HELLO WORLD  "
console.log(str.toLowerCase());    // "  hello world  "
console.log(str.trim());           // "Hello World"

// Search methods
console.log(str.includes("World"));    // true
console.log(str.indexOf("World"));     // 8
console.log(str.startsWith("Hello")); // false (due to spaces)
console.log(str.endsWith("World"));    // false (due to spaces)

// Substring methods
console.log(str.substring(2, 7));      // "Hello"
console.log(str.slice(2, 7));          // "Hello"

// Replace methods
console.log(str.replace("World", "JavaScript")); // "  Hello JavaScript  "
console.log(str.replaceAll("l", "L"));           // "  HeLLo WorLd  "

// Split and join
const words = str.trim().split(" ");
console.log(words); // ["Hello", "World"]
console.log(words.join("-")); // "Hello-World"
```

---

## Object Methods

### Popular Object Utility Methods

```javascript
const person = { name: "Ravindra", age: 25, city: "Bangalore" };

// Object.keys() - get property names
console.log(Object.keys(person)); // ["name", "age", "city"]

// Object.values() - get property values
console.log(Object.values(person)); // ["Ravindra", 25, "Bangalore"]

// Object.entries() - get key-value pairs
console.log(Object.entries(person)); // [["name", "Ravindra"], ["age", 25], ["city", "Bangalore"]]

// Object.assign() - copy properties
const newPerson = Object.assign({}, person, { age: 25 });
console.log(newPerson); // { name: "Ravindra", age: 25, city: "Bangalore" }

// Object.freeze() - make object immutable
Object.freeze(person);
person.age = 25; // Won't work in strict mode
console.log(person.age); // 25 (unchanged)

// Object.hasOwnProperty() - check if property exists
console.log(person.hasOwnProperty("name")); // true
console.log(person.hasOwnProperty("salary")); // false

// Object.defineProperty() - define property with descriptors
Object.defineProperty(person, "id", {
    value: 123,
    writable: false,
    enumerable: true,
    configurable: false
});
```

---

## Error Handling

### Try-Catch Block
```javascript
try {
    // Code that might throw an error
    const result = riskyOperation();
    console.log(result);
} catch (error) {
    // Handle the error
    console.error("An error occurred:", error.message);
} finally {
    // Code that always runs
    console.log("Cleanup code here");
}
```

### Throwing Errors

#### Difference between `throw new Error()` and `throw "string"`

```javascript
// Using Error object (recommended)
try {
    throw new Error("Something went wrong");
} catch (error) {
    console.log(error instanceof Error); // true
    console.log(error.message);         // "Something went wrong"
    console.log(error.stack);           // Stack trace
}

// Using string (not recommended)
try {
    throw "Something went wrong";
} catch (error) {
    console.log(error instanceof Error); // false
    console.log(error);                 // "Something went wrong"
    console.log(error.stack);           // undefined
}
```

### Reading Error Messages and Stack Traces

```javascript
function outerFunction() {
    middleFunction();
}

function middleFunction() {
    innerFunction();
}

function innerFunction() {
    throw new Error("Error in inner function");
}

try {
    outerFunction();
} catch (error) {
    console.log("Error message:", error.message);
    console.log("Stack trace:");
    console.log(error.stack);
}
```

### Importance of Catch Block

The catch block is crucial because:
1. **Prevents Program Crash**: Without catch, unhandled errors crash the program
2. **Error Logging**: Allows logging errors for debugging
3. **Graceful Degradation**: Provides fallback behavior
4. **User Experience**: Shows user-friendly error messages

```javascript
// Without catch - program crashes
function riskyFunction() {
    throw new Error("Something failed");
}
riskyFunction(); // Uncaught Error: Something failed

// With catch - program continues
try {
    riskyFunction();
} catch (error) {
    console.log("Error handled:", error.message);
    // Program continues execution
}
```

---

## ES6+ Features

### Spread Operator
```javascript
// Array spreading
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const combined = [...arr1, ...arr2]; // [1, 2, 3, 4, 5, 6]

// Object spreading
const obj1 = { a: 1, b: 2 };
const obj2 = { c: 3, d: 4 };
const merged = { ...obj1, ...obj2 }; // { a: 1, b: 2, c: 3, d: 4 }

// Function arguments
function sum(...numbers) {
    return numbers.reduce((acc, curr) => acc + curr, 0);
}
console.log(sum(1, 2, 3, 4)); // 10
```

### Template Literals
```javascript
const name = "Ravindra";
const age = 25;

// Old way
const message = "Hello, my name is " + name + " and I am " + age + " years old.";

// Template literal way
const message = `Hello, my name is ${name} and I am ${age} years old.`;

// Multi-line strings
const html = `
    <div>
        <h1>${name}</h1>
        <p>Age: ${age}</p>
    </div>
`;
```

### Default Parameters
```javascript
// Old way
function greet(name) {
    name = name || "Guest";
    return `Hello, ${name}!`;
}

// ES6 way
function greet(name = "Guest") {
    return `Hello, ${name}!`;
}

// Complex default values
function createUser(name, options = {}) {
    const defaults = {
        age: 18,
        city: "Unknown",
        isActive: true
    };
    
    return {
        name,
        ...defaults,
        ...options
    };
}
```

### Destructuring
```javascript
// Array destructuring
const numbers = [1, 2, 3, 4, 5];
const [first, second, ...rest] = numbers;
console.log(first, second, rest); // 1, 2, [3, 4, 5]

// Object destructuring
const person = { name: "Ravindra", age: 25, city: "Bangalore" };
const { name, age, city = "Unknown" } = person;
console.log(name, age, city); // Ravindra, 25, Bangalore

// Function parameter destructuring
function greet({ name, age }) {
    return `Hello ${name}, you are ${age} years old.`;
}

// Nested destructuring
const data = {
    user: {
        profile: {
            name: "Ravindra",
            settings: {
                theme: "dark"
            }
        }
    }
};

const { user: { profile: { name, settings: { theme } } } } = data;
console.log(name, theme); // Ravindra, dark
```

---

## Functions and Closures

### Closures
A closure is a function that has access to variables in its outer scope even after the outer function returns.

```javascript
function outerFunction(x) {
    // Outer function's variable
    return function innerFunction(y) {
        // Inner function has access to x
        return x + y;
    };
}

const addFive = outerFunction(5);
console.log(addFive(3)); // 8

// More complex closure example
function createCounter() {
    let count = 0;
    
    return {
        increment: () => ++count,
        decrement: () => --count,
        getCount: () => count
    };
}

const counter = createCounter();
console.log(counter.increment()); // 1
console.log(counter.increment()); // 2
console.log(counter.getCount());  // 2
```

### Difference between Arrow Functions and Regular Functions

#### 1. `this` Binding
```javascript
const obj = {
    name: "Ravindra",
    
    // Regular function - has its own 'this'
    regularFunction: function() {
        console.log(this.name); // "Ravindra"
        
        setTimeout(function() {
            console.log(this.name); // undefined (this refers to global object)
        }, 100);
    },
    
    // Arrow function - inherits 'this' from outer scope
    arrowFunction: function() {
        console.log(this.name); // "Ravindra"
        
        setTimeout(() => {
            console.log(this.name); // "Ravindra" (this refers to obj)
        }, 100);
    }
};
```

#### 2. Arguments Object
```javascript
function regularFunction() {
    console.log(arguments); // Arguments object available
}

const arrowFunction = () => {
    console.log(arguments); // ReferenceError: arguments is not defined
};
```

#### 3. Constructor Usage
```javascript
// Regular function can be used as constructor
function Person(name) {
    this.name = name;
}
const person1 = new Person("Ravindra");

// Arrow function cannot be used as constructor
const PersonArrow = (name) => {
    this.name = name;
};
// const person2 = new PersonArrow("Ravindra"); // TypeError: PersonArrow is not a constructor
```

#### 4. Hoisting
```javascript
// Regular function - fully hoisted
console.log(regularFunc()); // "Hello"

function regularFunc() {
    return "Hello";
}

// Arrow function - not hoisted
// console.log(arrowFunc()); // ReferenceError: Cannot access 'arrowFunc' before initialization

const arrowFunc = () => {
    return "Hello";
};
```

---

## Comparison Operators

### Difference between `===` and `==`

#### `==` (Loose Equality)
- Performs type coercion
- Can lead to unexpected results
- Not recommended for most cases

```javascript
console.log(5 == "5");     // true (string "5" converted to number 5)
console.log(true == 1);    // true (boolean true converted to number 1)
console.log(null == undefined); // true
console.log(0 == false);   // true
console.log("" == false);  // true
```

#### `===` (Strict Equality)
- No type coercion
- Compares both value and type
- Recommended for most cases

```javascript
console.log(5 === "5");    // false (different types)
console.log(true === 1);   // false (different types)
console.log(null === undefined); // false
console.log(0 === false);  // false
console.log("" === false); // false
```

### Why `value === undefined` is Better than `!value`

```javascript
const value = 0;

// Using !value - treats 0 as falsy
if (!value) {
    console.log("Value is falsy"); // This will print, but 0 might be a valid value
}

// Using value === undefined - only checks for undefined
if (value === undefined) {
    console.log("Value is undefined"); // This won't print, 0 is a valid value
}

// Better approach for checking if value exists
if (value !== undefined && value !== null) {
    console.log("Value exists and is not null");
}
```

---

## Modules

### CommonJS (Node.js) - require and module.exports

#### Exporting
```javascript
// math.js
const add = (a, b) => a + b;
const subtract = (a, b) => a - b;

// Named exports
module.exports.add = add;
module.exports.subtract = subtract;

// Or export an object
module.exports = {
    add,
    subtract,
    multiply: (a, b) => a * b
};

// Or export individual functions
module.exports.add = add;
module.exports.subtract = subtract;
```

#### Importing
```javascript
// main.js
const math = require('./math');
console.log(math.add(2, 3)); // 5

// Destructuring import
const { add, subtract } = require('./math');
console.log(add(2, 3)); // 5

// Import specific function
const add = require('./math').add;
console.log(add(2, 3)); // 5
```

### ES6 Modules (Modern JavaScript)

#### Exporting
```javascript
// math.js
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// Default export
export default function multiply(a, b) {
    return a * b;
}
```

#### Importing
```javascript
// main.js
import multiply, { add, subtract } from './math.js';
console.log(add(2, 3)); // 5
console.log(multiply(2, 3)); // 6
```

---

## Console Methods

### Different Console Methods

```javascript
// Basic logging
console.log("Regular message");
console.info("Informational message");
console.warn("Warning message");
console.error("Error message");

// Debugging
console.debug("Debug message"); // Same as console.log in most browsers

// Grouping
console.group("Group 1");
console.log("Message 1");
console.log("Message 2");
console.groupEnd();

// Timing
console.time("Timer");
// Some operation
console.timeEnd("Timer"); // Prints elapsed time

// Counting
console.count("Counter"); // 1
console.count("Counter"); // 2
console.countReset("Counter");
console.count("Counter"); // 1

// Table display
const data = [
    { name: "Ravindra", age: 25 },
    { name: "Ravindra", age: 25 }
];
console.table(data);

// Assertion
console.assert(2 + 2 === 5, "Math is broken!"); // Only logs if assertion fails

// Trace
function outer() {
    middle();
}

function middle() {
    inner();
}

function inner() {
    console.trace("Call stack trace");
}
outer(); // Shows the call stack

// Clear
console.clear(); // Clears the console
```

---

## Best Practices

### Indentation
```javascript
// Good - consistent 2 or 4 spaces
function calculateTotal(items) {
    let total = 0;
    for (let item of items) {
        if (item.price > 0) {
            total += item.price;
        }
    }
    return total;
}

// Bad - inconsistent indentation
function calculateTotal(items) {
let total = 0;
    for (let item of items) {
  if (item.price > 0) {
        total += item.price;
    }
    }
    return total;
}
```

### Variable Naming
```javascript
// Good - descriptive and clear
const userEmailAddress = "john@example.com";
const isUserLoggedIn = true;
const maximumRetryAttempts = 3;

// Bad - unclear or abbreviated
const uea = "john@example.com";
const uli = true;
const mra = 3;
```

### Loop Variable Naming
```javascript
// Good - descriptive loop variables
for (let userIndex = 0; userIndex < users.length; userIndex++) {
    console.log(users[userIndex].name);
}

// For arrays, use descriptive names
for (let product of products) {
    console.log(product.name);
}

// For objects, use key-value pairs
for (let [key, value] of Object.entries(config)) {
    console.log(`${key}: ${value}`);
}

// Bad - generic or unclear
for (let i = 0; i < users.length; i++) {
    console.log(users[i].name);
}
```

### Function Naming
```javascript
// Good - verb-based names that describe what the function does
function calculateTotalPrice(items) { }
function validateUserInput(input) { }
function sendEmailNotification(user) { }

// Bad - unclear or noun-based names
function total(items) { }
function check(input) { }
function email(user) { }
```

### Passing Functions to Other Functions

```javascript
// Higher-order function that accepts a function as parameter
function processArray(array, processor) {
    const result = [];
    for (let item of array) {
        result.push(processor(item));
    }
    return result;
}

// Named function
function double(x) {
    return x * 2;
}
const numbers = [1, 2, 3, 4, 5];
const doubled = processArray(numbers, double);

// Anonymous function
const tripled = processArray(numbers, function(x) {
    return x * 3;
});

// Arrow function
const squared = processArray(numbers, x => x * x);
```

### Named vs Anonymous Functions

#### Named Functions
```javascript
// Named function declaration
function calculateTotal(items) {
    return items.reduce((sum, item) => sum + item.price, 0);
}

// Named function expression
const calculateTotal = function calculateTotal(items) {
    return items.reduce((sum, item) => sum + item.price, 0);
};

// Benefits:
// - Better stack traces
// - Self-referencing capability
// - Easier debugging
```

#### Anonymous Functions
```javascript
// Anonymous function expression
const calculateTotal = function(items) {
    return items.reduce((sum, item) => sum + item.price, 0);
};

// Arrow function (anonymous)
const calculateTotal = (items) => {
    return items.reduce((sum, item) => sum + item.price, 0);
};

// Used as callbacks
setTimeout(function() {
    console.log("Delayed message");
}, 1000);
```

### Variable Number of Arguments

```javascript
// Using arguments object (ES5)
function sum() {
    let total = 0;
    for (let i = 0; i < arguments.length; i++) {
        total += arguments[i];
    }
    return total;
}

// Using rest parameters (ES6+)
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}

// Examples
console.log(sum(1, 2, 3));        // 6
console.log(sum(1, 2, 3, 4, 5));  // 15
console.log(sum());               // 0

// Combining with other parameters
function createUser(name, age, ...hobbies) {
    return {
        name,
        age,
        hobbies
    };
}

const user = createUser("Ravindra", 25, "reading", "gaming", "cooking");
console.log(user);
// { name: "Ravindra", age: 25, hobbies: ["reading", "gaming", "cooking"] }
```

---

## References

1. **JavaScript Reference**: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference
2. **Array Methods**: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array
3. **String Methods**: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
4. **Object Methods**: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object

---

