## 1. What are arrow functions? How are they different from normal functions?

Arrow functions are a shorter syntax for writing functions introduced in ES6.
They differ from normal functions in the following ways:

Arrow functions do not have their own this; they inherit it from the surrounding scope.

They do not have their own arguments object.

They cannot be used as constructors.

They provide a cleaner, more concise syntax.

## 2. What are template literals?

Template literals are string literals that allow embedded expressions and support multi-line strings.
They use backticks (`) and support features like:

String interpolation using ${expression}

Multi-line string formatting

Tagged templates for custom processing

## 3. How do you select an element by id, class, and tag name in JavaScript?

In JavaScript, elements can be selected using:

getElementById for selecting by ID.

getElementsByClassName for selecting by class.

getElementsByTagName for selecting by tag name.

Alternatively, querySelector and querySelectorAll can be used for more flexible selectors.

## 4. Why is block scope important in ES6?

Block scope allows variables to be scoped to the nearest enclosing block using let and const.
This prevents variable leakage outside of blocks, reduces bugs, and makes code more predictable and maintainable compared to var, which is function-scoped.

## 5. How do arrow functions handle the this keyword differently?

Arrow functions do not have their own this.
Instead, they lexically bind this from the surrounding context, which is especially useful in callbacks and class methods where preserving the outer this is important.

## 6. What are rest parameters?

Rest parameters allow a function to accept an indefinite number of arguments as an array.
They are defined using three dots (...) and must be the last parameter in a function.
They are useful for handling variable numbers of arguments.

## 7. What is the difference between named exports and default exports in ES6 modules?

Named exports allow exporting multiple values with their names. They must be imported using the same names.

Default export allows exporting a single value, which can be imported with any name.

A module can have multiple named exports but only one default export.

## 8. What are Set and Map in ES6?

A Set is a collection of unique values that maintains insertion order and automatically removes duplicates.

A Map is a collection of key-value pairs where keys can be of any type, and it maintains insertion order as well.
