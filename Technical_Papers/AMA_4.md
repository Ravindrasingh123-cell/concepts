# AMA 

## AMA QUESTIONS
1. What is the Event Loop in JavaScript?
2. What is "Strict Mode" in JavaScript?
3. What is the purpose of call, apply, and bind?
4. Explain the concept of higher-order functions
5. What is garbage collection in JavaScript?
6. How do async/await simplify working with Promises?

---

## 1. What is the Event Loop in JavaScript?

The Event Loop is what makes JavaScript work with asynchronous code. Even though JavaScript runs on a single thread, the event loop allows it to handle multiple operations without blocking.

### How it Works

JavaScript has four main parts:
- **Call Stack**: Keeps track of function calls
- **Heap**: Stores objects in memory
- **Callback Queue**: Holds functions waiting to run
- **Event Loop**: Moves functions from the queue to the stack

The event loop constantly checks if the call stack is empty. When it is, it takes the first function from the callback queue and puts it on the stack to run.

### Why This Matters

Without the event loop, JavaScript would freeze every time it waits for something like a network request. The event loop lets JavaScript start other tasks while waiting, making the app feel responsive.

### Types of Tasks

There are two types of tasks:
- **Microtasks**: Promises and similar operations (higher priority)
- **Macrotasks**: setTimeout, setInterval, and DOM events (lower priority)

The event loop always runs all microtasks before any macrotasks.

---

## 2. What is "Strict Mode" in JavaScript?

Strict mode is a special way to run JavaScript that makes the language stricter and catches more errors. It was added to help developers write better code.

### How to Use It

I turn on strict mode by writing `"use strict";` at the top of my file or function.

### What It Does

Strict mode prevents many common mistakes:

- **No accidental global variables**: If I forget to declare a variable, it throws an error instead of creating a global one
- **No duplicate property names**: Objects can't have the same property name twice
- **Stricter `this` behavior**: Functions called without an object context have `this` as undefined instead of the global object
- **No `with` statements**: The `with` statement is not allowed
- **No octal numbers**: Numbers starting with 0 are not allowed
- **Eliminates silent errors**: Many silent failures become errors

### Why Use It

Strict mode helps me catch bugs before they become problems. It makes my code more predictable and prepares it for future JavaScript versions. Most modern JavaScript code should use strict mode.

---

## 3. What is the purpose of call, apply, and bind?

These three methods help me control what `this` means inside a function. They let me borrow methods from one object and use them on another object.

### call()

The `call()` method lets me call a function with a specific `this` value and pass arguments one by one.

When I use `call()`, I tell the function what object should be `this` inside it. This is useful when I want to use a method from one object on a different object.

### apply()

The `apply()` method works like `call()` but takes arguments as an array instead of individual arguments.

This is helpful when I have an array of values that I want to pass to a function, or when I don't know how many arguments I'll have ahead of time.

### bind()

The `bind()` method creates a new function with a fixed `this` value. Unlike `call()` and `apply()`, `bind()` doesn't call the function immediately - it returns a new function that I can call later.

This is useful for event handlers where I want to make sure `this` refers to the right object when the event happens.

### Why These Matter

These methods solve the problem of `this` being unpredictable in JavaScript. They let me:
- Borrow methods from one object to use on another
- Fix `this` context for event handlers
- Create new functions with preset arguments
- Use array methods on objects that look like arrays

Without these methods, I'd have trouble controlling what `this` means inside my functions.

---

## 4. Explain the concept of higher-order functions

A higher-order function is a function that either takes other functions as arguments or returns a function as its result. This is a key idea in functional programming.

### What Makes Functions Special in JavaScript

In JavaScript, functions are treated like any other value. I can:
- Store them in variables
- Pass them to other functions
- Return them from functions
- Put them in arrays or objects

This makes functions "first-class citizens" in the language.

### Two Types of Higher-Order Functions

**Functions that take other functions as arguments:**
These are common in array methods like `map()`, `filter()`, and `reduce()`. They let me tell the function how to behave by passing in another function.

**Functions that return other functions:**
These create new functions for me. I might use this to create specialized versions of a general function.

### Why Higher-Order Functions Matter

They help me write code that is:
- **More reusable**: Write a function once, use it many ways
- **More flexible**: Change behavior by passing different functions
- **Easier to understand**: Break complex problems into smaller pieces
- **More powerful**: Combine simple functions to create complex behavior

### Common Examples

Many built-in JavaScript methods are higher-order functions:
- Array methods like `map()`, `filter()`, `forEach()`
- Timer functions like `setTimeout()`
- Promise methods like `then()`

The idea is that instead of writing the same logic over and over, I write a general function that takes another function to tell it what to do.

---

## 5. What is garbage collection in JavaScript?

Garbage collection is how JavaScript automatically manages memory. When I create objects, JavaScript uses memory to store them. When I'm done with those objects, garbage collection frees up that memory so it can be used again.

### How It Works

JavaScript keeps track of which objects are still being used by my program. When an object is no longer referenced anywhere, the garbage collector removes it from memory.

The main algorithm used is called "mark and sweep":
1. **Mark**: The garbage collector looks at all objects and marks which ones are still reachable
2. **Sweep**: It removes all the unmarked objects that are no longer needed

### What Gets Collected

Objects become eligible for garbage collection when:
- No variables point to them
- No other objects reference them
- They're not reachable from the global scope


---

## 6. How do async/await simplify working with Promises?

async/await is a way to write asynchronous code that looks more like regular synchronous code. It makes working with Promises much easier and cleaner.

### The Problem with Promises

Before async/await, I had to use `.then()` chains to handle asynchronous operations. This could get messy and hard to read, especially when I had multiple async operations that depended on each other.

### How async/await Works

**async** marks a function as asynchronous. Inside an async function, I can use **await** to pause execution until a Promise resolves.

When I use `await`, the function waits for the Promise to complete and then continues with the result. If the Promise rejects, it throws an error that I can catch with try/catch.


### Why It Matters

async/await makes asynchronous programming in JavaScript much more approachable. It reduces the complexity of working with Promises and makes my code more maintainable. Most modern JavaScript code uses async/await instead of Promise chains.

---

