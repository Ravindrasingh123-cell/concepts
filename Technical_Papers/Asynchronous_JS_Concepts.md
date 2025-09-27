# Asynchronous JavaScript Concepts

---

## How JavaScript Executes Code

JavaScript is a **single-threaded** language, meaning it can only execute one piece of code at a time. However, it uses an **event loop** to handle asynchronous operations efficiently.

### JavaScript Execution Model

```javascript
console.log("1. Start");

setTimeout(() => {
    console.log("2. Timeout");
}, 0);

console.log("3. End");

// Output:
// 1. Start
// 3. End
// 2. Timeout
```

### Call Stack
- JavaScript uses a **call stack** to keep track of function calls
- Functions are added to the stack when called and removed when completed
- The stack follows **LIFO** (Last In, First Out) principle

```javascript
function first() {
    console.log("First function");
    second();
}

function second() {
    console.log("Second function");
    third();
}

function third() {
    console.log("Third function");
}

first();
// Output:
// First function
// Second function
// Third function
```

---

## Synchronous vs Asynchronous

### Synchronous Code
- Code executes **line by line**
- Each line must complete before the next line runs
- **Blocking** - if one operation takes time, everything waits

```javascript
// Synchronous example
console.log("Step 1");
console.log("Step 2");
console.log("Step 3");

// Output:
// Step 1
// Step 2
// Step 3
```

### Asynchronous Code
- Code doesn't wait for slow operations
- **Non-blocking** - other code can run while waiting
- Uses callbacks, promises, or async/await

```javascript
// Asynchronous example
console.log("Step 1");

setTimeout(() => {
    console.log("Step 2 (async)");
}, 1000);

console.log("Step 3");

// Output:
// Step 1
// Step 3
// Step 2 (async) (after 1 second)
```

### Key Differences

- Synchronous

1. Blocking

2. Executes code sequentially, one line after another

3. Simple to understand and debug

4. Can freeze the UI during long operations

- Asynchronous

1. Non-blocking

2. Executes code concurrently using callbacks, promises, or async/await

3. More complex to manage and debug

4. Offers better user experience by keeping the UI responsive

---

## Ways to Make Code Async

### 1. setTimeout() and setInterval()
```javascript
// setTimeout - execute once after delay
setTimeout(() => {
    console.log("This runs after 2 seconds");
}, 2000);

// setInterval - execute repeatedly
const intervalId = setInterval(() => {
    console.log("This runs every 1 second");
}, 1000);

// Clear interval after 5 seconds
setTimeout(() => {
    clearInterval(intervalId);
}, 5000);
```

### 2. Callbacks
```javascript
function fetchData(callback) {
    setTimeout(() => {
        const data = { name: "Ravindra", age: 25 };
        callback(data);
    }, 1000);
}

fetchData((data) => {
    console.log("Received:", data);
});
```

### 3. Promises
```javascript
function fetchData() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            const data = { name: "Ravindra", age: 25 };
            resolve(data);
        }, 1000);
    });
}

fetchData()
    .then(data => console.log("Received:", data))
    .catch(error => console.error("Error:", error));
```

### 4. Async/Await
```javascript
async function fetchData() {
    try {
        const data = await new Promise((resolve) => {
            setTimeout(() => {
                resolve({ name: "Ravindra", age: 25 });
            }, 1000);
        });
        console.log("Received:", data);
    } catch (error) {
        console.error("Error:", error);
    }
}

fetchData();
```

---

## Web Browser APIs

Web Browser APIs are interfaces provided by browsers to interact with browser features and external resources.

### Common Web APIs

#### 1. DOM API
```javascript
// Document Object Model
const element = document.getElementById('myButton');
element.addEventListener('click', () => {
    console.log('Button clicked!');
});
```

#### 2. Fetch API
```javascript
// Making HTTP requests
fetch('https://api.example.com/users')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

#### 3. Geolocation API
```javascript
// Get user's location
navigator.geolocation.getCurrentPosition(
    (position) => {
        console.log('Latitude:', position.coords.latitude);
        console.log('Longitude:', position.coords.longitude);
    },
    (error) => {
        console.error('Error getting location:', error);
    }
);
```

#### 4. Web Storage API
```javascript
// Local Storage
localStorage.setItem('username', 'Ravindra');
const username = localStorage.getItem('username');

// Session Storage
sessionStorage.setItem('theme', 'dark');
const theme = sessionStorage.getItem('theme');
```

#### 5. Web Workers
```javascript
// Main thread
const worker = new Worker('worker.js');
worker.postMessage({ data: 'Hello Worker' });

worker.onmessage = (event) => {
    console.log('Message from worker:', event.data);
};

// worker.js
self.onmessage = (event) => {
    const result = event.data.data.toUpperCase();
    self.postMessage(result);
};
```

---

## Event Loop

The **Event Loop** is the mechanism that allows JavaScript to handle asynchronous operations despite being single-threaded.

### Event Loop Components

#### 1. Call Stack
- Where synchronous code executes
- Functions are pushed and popped from the stack

#### 2. Web APIs
- Browser APIs that handle asynchronous operations
- Examples: setTimeout, DOM events, HTTP requests

#### 3. Callback Queue (Task Queue)
- Stores callbacks from completed async operations
- FIFO (First In, First Out) structure

#### 4. Microtask Queue
- Higher priority than callback queue
- Stores promise callbacks and queueMicrotask callbacks

### Event Loop Process

```javascript
console.log("1. Start");

setTimeout(() => console.log("2. Timeout"), 0);

Promise.resolve().then(() => console.log("3. Promise"));

console.log("4. End");

// Output:
// 1. Start
// 4. End
// 3. Promise (microtask - higher priority)
// 2. Timeout (callback queue)
```

### Event Loop Visualization

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│ Call Stack  │    │ Web APIs    │    │ Callback    │
│             │    │             │    │ Queue       │
│             │    │ setTimeout  │───▶│             │
│             │    │ DOM events  │    │             │
│             │    │ HTTP req    │    │             │
└─────────────┘    └─────────────┘    └─────────────┘
       ▲                   │                   │
       │                   │                   │
       └───────────────────┼───────────────────┘
                           │
                   ┌─────────────┐
                   │ Microtask  │
                   │ Queue      │
                   │ (Promises) │
                   └─────────────┘
```

---

## Callback Hell

**Callback Hell** (also called "Pyramid of Doom") occurs when you have multiple nested callbacks, making code hard to read and maintain.

### Example of Callback Hell

```javascript
// Callback Hell Example
getUserData('Ravindra', (user) => {
    console.log('User:', user);
    
    getUserPosts(user.id, (posts) => {
        console.log('Posts:', posts);
        
        getPostComments(posts[0].id, (comments) => {
            console.log('Comments:', comments);
            
            getCommentReplies(comments[0].id, (replies) => {
                console.log('Replies:', replies);
                
                // More nested callbacks...
                getReplyLikes(replies[0].id, (likes) => {
                    console.log('Likes:', likes);
                    // This becomes unreadable and unmaintainable
                });
            });
        });
    });
});
```

### Problems with Callback Hell

1. **Hard to Read**: Code becomes deeply nested
2. **Hard to Debug**: Difficult to trace errors
3. **Hard to Maintain**: Adding features becomes complex
4. **Error Handling**: Difficult to handle errors at each level
5. **Code Reusability**: Hard to reuse callback functions

### Solutions to Callback Hell

#### 1. Named Functions
```javascript
function handleUserData(user) {
    console.log('User:', user);
    getUserPosts(user.id, handleUserPosts);
}

function handleUserPosts(posts) {
    console.log('Posts:', posts);
    getPostComments(posts[0].id, handlePostComments);
}

function handlePostComments(comments) {
    console.log('Comments:', comments);
}

getUserData('Ravindra', handleUserData);
```

#### 2. Promises (Better Solution)
```javascript
getUserData('Ravindra')
    .then(user => {
        console.log('User:', user);
        return getUserPosts(user.id);
    })
    .then(posts => {
        console.log('Posts:', posts);
        return getPostComments(posts[0].id);
    })
    .then(comments => {
        console.log('Comments:', comments);
        return getCommentReplies(comments[0].id);
    })
    .then(replies => {
        console.log('Replies:', replies);
    })
    .catch(error => {
        console.error('Error:', error);
    });
```

#### 3. Async/Await (Best Solution)
```javascript
async function fetchUserData() {
    try {
        const user = await getUserData('Ravindra');
        console.log('User:', user);
        
        const posts = await getUserPosts(user.id);
        console.log('Posts:', posts);
        
        const comments = await getPostComments(posts[0].id);
        console.log('Comments:', comments);
        
        const replies = await getCommentReplies(comments[0].id);
        console.log('Replies:', replies);
        
    } catch (error) {
        console.error('Error:', error);
    }
}

fetchUserData();
```

---

## Inversion of Control in Callbacks

**Inversion of Control** occurs when you pass control of your function's execution to another function (the callback).

### The Problem

```javascript
// Your function depends on another function's behavior
function processData(data, callback) {
    // You don't control when or how many times callback is called
    callback(data);
    callback(data); // Called twice 
    callback(data); // Called three times - unexpected!
}

processData('Ravindra', (result) => {
    console.log('Processing:', result);
    // This might run multiple times unexpectedly
});
```

### Problems with Inversion of Control

1. **Unpredictable Execution**: You don't control when callbacks run
2. **Multiple Calls**: Callback might be called multiple times
3. **No Error Handling**: No guarantee of error handling
4. **Trust Issues**: You must trust the callback function

### Example of Trust Issues

```javascript
// You trust this function to call your callback correctly
function trustedFunction(callback) {
    // But what if it doesn't?
    // What if it calls callback multiple times?
    // What if it never calls callback?
    // What if it throws an error?
}

// Your code depends on the callback being called correctly
trustedFunction((result) => {
    console.log('Result:', result);
    // This might never execute or execute multiple times
});
```

### How Promises Solve This

```javascript
// Promises provide better control
function createPromise() {
    return new Promise((resolve, reject) => {
        // You control the execution
        // resolve() can only be called once
        // reject() can only be called once
        setTimeout(() => {
            resolve('Success');
        }, 1000);
    });
}

createPromise()
    .then(result => {
        console.log('Result:', result);
        // This will only run once
        // You have control over error handling
    })
    .catch(error => {
        console.error('Error:', error);
    });
```

---

## Promises

A **Promise** is an object representing the eventual completion or failure of an asynchronous operation.

### What is a Promise?

A Promise is a proxy for a value not necessarily known when the promise is created. It allows you to associate handlers with an asynchronous action's eventual success value or failure reason.

### Creating a New Promise

```javascript
const myPromise = new Promise((resolve, reject) => {
    // Asynchronous operation
    setTimeout(() => {
        const success = true;
        
        if (success) {
            resolve('Operation successful!');
        } else {
            reject('Operation failed!');
        }
    }, 1000);
});
```

### Promise States

#### 1. Pending
- Initial state, neither fulfilled nor rejected
- Promise is still executing

```javascript
const pendingPromise = new Promise((resolve, reject) => {
    // This promise is in pending state
    // until resolve() or reject() is called
});
```

#### 2. Fulfilled (Resolved)
- Operation completed successfully
- Promise has a resulting value

```javascript
const fulfilledPromise = new Promise((resolve, reject) => {
    resolve('Success!'); // Promise is now fulfilled
});
```

#### 3. Rejected
- Operation failed
- Promise has a reason for failure

```javascript
const rejectedPromise = new Promise((resolve, reject) => {
    reject('Error occurred!'); // Promise is now rejected
});
```

### Consuming an Existing Promise

#### Using .then() and .catch()
```javascript
const userPromise = fetchUserData('Ravindra');

userPromise
    .then(user => {
        console.log('User data:', user);
        return user.id;
    })
    .then(userId => {
        console.log('User ID:', userId);
    })
    .catch(error => {
        console.error('Error:', error);
    });
```

#### Using async/await
```javascript
async function getUserInfo() {
    try {
        const user = await fetchUserData('Ravindra');
        console.log('User data:', user);
        
        const userId = user.id;
        console.log('User ID:', userId);
    } catch (error) {
        console.error('Error:', error);
    }
}

getUserInfo();
```

---

## Promise Chaining

Promise chaining allows you to perform multiple asynchronous operations in sequence.

### Basic Promise Chaining

```javascript
fetchUserData('Ravindra')
    .then(user => {
        console.log('Step 1:', user);
        return getUserPosts(user.id);
    })
    .then(posts => {
        console.log('Step 2:', posts);
        return getPostComments(posts[0].id);
    })
    .then(comments => {
        console.log('Step 3:', comments);
        return getCommentReplies(comments[0].id);
    })
    .then(replies => {
        console.log('Final result:', replies);
    })
    .catch(error => {
        console.error('Error in chain:', error);
    });
```

### Error Handling in Promise Chain

#### Using .catch()
```javascript
fetchUserData('Ravindra')
    .then(user => {
        if (!user) {
            throw new Error('User not found');
        }
        return getUserPosts(user.id);
    })
    .then(posts => {
        console.log('Posts:', posts);
    })
    .catch(error => {
        console.error('Error caught:', error);
        // This catches errors from any .then() in the chain
    });
```

#### Using try/catch with async/await
```javascript
async function fetchUserDataChain() {
    try {
        const user = await fetchUserData('Ravindra');
        if (!user) {
            throw new Error('User not found');
        }
        
        const posts = await getUserPosts(user.id);
        console.log('Posts:', posts);
        
    } catch (error) {
        console.error('Error caught:', error);
    }
}
```

### Finally Block in Promise Chain

```javascript
fetchUserData('Ravindra')
    .then(user => {
        console.log('User:', user);
        return getUserPosts(user.id);
    })
    .then(posts => {
        console.log('Posts:', posts);
    })
    .catch(error => {
        console.error('Error:', error);
    })
    .finally(() => {
        console.log('This always runs, regardless of success or failure');
        // Cleanup code, logging, etc.
    });
```

### Error Handling Scenarios

#### Error in .then() with .catch()
```javascript
fetchUserData('Ravindra')
    .then(user => {
        console.log('User:', user);
        throw new Error('Something went wrong in .then()');
    })
    .then(posts => {
        console.log('This will not run');
    })
    .catch(error => {
        console.error('Error caught:', error); // This will catch the error
    });
```

#### Error in .then() without .catch()
```javascript
fetchUserData('Ravindra')
    .then(user => {
        console.log('User:', user);
        throw new Error('Something went wrong in .then()');
    })
    .then(posts => {
        console.log('This will not run');
    });
// Error will be unhandled and logged to console
```

### Why .catch() Must Be at the End

```javascript
// Good - .catch() at the end catches all errors
fetchUserData('Ravindra')
    .then(user => getUserPosts(user.id))
    .then(posts => getPostComments(posts[0].id))
    .then(comments => getCommentReplies(comments[0].id))
    .catch(error => {
        console.error('Any error in the chain:', error);
    });

// Bad - .catch() in the middle only catches errors before it
fetchUserData('Ravindra')
    .then(user => getUserPosts(user.id))
    .catch(error => console.error('Only catches errors up to here'))
    .then(posts => getPostComments(posts[0].id)) // Errors here won't be caught
    .then(comments => getCommentReplies(comments[0].id));
```

### Consuming Multiple Promises

#### By Chaining (Sequential)
```javascript
async function fetchUserDataSequentially() {
    try {
        const user = await fetchUserData('Ravindra');
        const posts = await getUserPosts(user.id);
        const comments = await getPostComments(posts[0].id);
        
        return { user, posts, comments };
    } catch (error) {
        console.error('Error:', error);
    }
}
```

#### By Promise.all() (Parallel)
```javascript
async function fetchUserDataParallel() {
    try {
        const [user, posts, comments] = await Promise.all([
            fetchUserData('Ravindra'),
            getUserPosts('user123'),
            getPostComments('post456')
        ]);
        
        return { user, posts, comments };
    } catch (error) {
        console.error('Error:', error);
    }
}
```

---

## Promise Methods

### Promise.resolve()
Creates a resolved promise with the given value.

```javascript
// Resolve with a value
const resolvedPromise = Promise.resolve('Success!');
resolvedPromise.then(value => console.log(value)); // "Success!"

// Resolve with another promise
const anotherPromise = Promise.resolve(Promise.resolve('Nested promise'));
anotherPromise.then(value => console.log(value)); // "Nested promise"
```

### Promise.reject()
Creates a rejected promise with the given reason.

```javascript
// Reject with an error
const rejectedPromise = Promise.reject('Error occurred!');
rejectedPromise.catch(error => console.error(error)); // "Error occurred!"

// Reject with an Error object
const errorPromise = Promise.reject(new Error('Something went wrong'));
errorPromise.catch(error => console.error(error.message)); // "Something went wrong"
```

### Promise.all()
Waits for all promises to resolve or any to reject.

```javascript
const promise1 = fetchUserData('Ravindra');
const promise2 = getUserPosts('user123');
const promise3 = getPostComments('post456');

Promise.all([promise1, promise2, promise3])
    .then(results => {
        const [user, posts, comments] = results;
        console.log('All data:', { user, posts, comments });
    })
    .catch(error => {
        console.error('One or more promises failed:', error);
    });
```

### Promise.allSettled()
Waits for all promises to settle (resolve or reject).

```javascript
const promise1 = Promise.resolve('Success');
const promise2 = Promise.reject('Error');
const promise3 = Promise.resolve('Another success');

Promise.allSettled([promise1, promise2, promise3])
    .then(results => {
        results.forEach((result, index) => {
            if (result.status === 'fulfilled') {
                console.log(`Promise ${index + 1} succeeded:`, result.value);
            } else {
                console.log(`Promise ${index + 1} failed:`, result.reason);
            }
        });
    });
```

### Promise.any()
Returns the first fulfilled promise, or rejects if all promises reject.

```javascript
const promise1 = Promise.reject('Error 1');
const promise2 = Promise.resolve('Success 2');
const promise3 = Promise.reject('Error 3');

Promise.any([promise1, promise2, promise3])
    .then(result => {
        console.log('First success:', result); // "Success 2"
    })
    .catch(error => {
        console.error('All promises failed:', error);
    });
```

### Promise.race()
Returns the first settled promise (fulfilled or rejected).

```javascript
const promise1 = new Promise(resolve => setTimeout(() => resolve('Fast'), 100));
const promise2 = new Promise(resolve => setTimeout(() => resolve('Slow'), 500));

Promise.race([promise1, promise2])
    .then(result => {
        console.log('Winner:', result); // "Fast"
    });
```

---

## Error Handling with Promises

### Why Error Handling is Most Important

1. **User Experience: Prevents crashes and provides meaningful error messages
2. **Debugging**: Makes it easier to identify and fix issues
3. **Recovery**: Allows graceful handling of failures
4. **User Feedback**: Provides appropriate feedback to users

### Comprehensive Error Handling

```javascript
async function robustDataFetching() {
    try {
        // Primary data source
        const user = await fetchUserData('Ravindra');
        
        // Secondary data with fallback
        let posts;
        try {
            posts = await getUserPosts(user.id);
        } catch (error) {
            console.warn('Failed to fetch posts, using default:', error);
            posts = []; // Fallback to empty array
        }
        
        // Validate data
        if (!user || !user.id) {
            throw new Error('Invalid user data received');
        }
        
        return { user, posts };
        
    } catch (error) {
        console.error('Critical error in data fetching:', error);
        
        // Log error for debugging
        console.error('Error details:', {
            message: error.message,
            stack: error.stack,
            timestamp: new Date().toISOString()
        });
        
        // Return fallback data
        return {
            user: { id: 'unknown', name: 'Guest' },
            posts: []
        };
    }
}
```

### Promisifying Callback-based Functions

#### setTimeout
```javascript
function delay(ms) {
    return new Promise(resolve => {
        setTimeout(resolve, ms);
    });
}

// Usage
async function example() {
    console.log('Start');
    await delay(2000);
    console.log('After 2 seconds');
}
```

#### fs.readFile (Node.js)
```javascript
const fs = require('fs');

function readFilePromise(filePath) {
    return new Promise((resolve, reject) => {
        fs.readFile(filePath, 'utf8', (error, data) => {
            if (error) {
                reject(error);
            } else {
                resolve(data);
            }
        });
    });
}

// Usage
readFilePromise('data.txt')
    .then(data => console.log('File content:', data))
    .catch(error => console.error('Error reading file:', error));
```

#### XMLHttpRequest
```javascript
function fetchData(url) {
    return new Promise((resolve, reject) => {
        const xhr = new XMLHttpRequest();
        xhr.open('GET', url);
        xhr.onload = () => {
            if (xhr.status === 200) {
                resolve(xhr.responseText);
            } else {
                reject(new Error(`HTTP ${xhr.status}: ${xhr.statusText}`));
            }
        };
        xhr.onerror = () => reject(new Error('Network error'));
        xhr.send();
    });
}

// Usage
fetchData('https://api.example.com/data')
    .then(data => console.log('Data:', data))
    .catch(error => console.error('Error:', error));
```

---

## Best Practices

### 1. Always Handle Errors
```javascript
// Good
fetchUserData('Ravindra')
    .then(user => console.log(user))
    .catch(error => console.error('Error:', error));

// Bad - unhandled promise rejection
fetchUserData('Ravindra')
    .then(user => console.log(user));
```

### 2. Use async/await for Better Readability
```javascript
// Good - async/await
async function fetchData() {
    try {
        const user = await fetchUserData('Ravindra');
        const posts = await getUserPosts(user.id);
        return { user, posts };
    } catch (error) {
        console.error('Error:', error);
        throw error;
    }
}

// Less readable - promise chains
function fetchData() {
    return fetchUserData('Ravindra')
        .then(user => getUserPosts(user.id))
        .then(posts => ({ user, posts }))
        .catch(error => {
            console.error('Error:', error);
            throw error;
        });
}
```

### 3. Use Promise.all() for Parallel Operations
```javascript
// Good - parallel execution
async function fetchAllData() {
    const [user, posts, comments] = await Promise.all([
        fetchUserData('Ravindra'),
        getUserPosts('user123'),
        getPostComments('post456')
    ]);
    return { user, posts, comments };
}

// Less efficient - sequential execution
async function fetchAllDataSequential() {
    const user = await fetchUserData('Ravindra');
    const posts = await getUserPosts('user123');
    const comments = await getPostComments('post456');
    return { user, posts, comments };
}
```

### 4. Provide Meaningful Error Messages
```javascript
// Good - specific error messages
async function fetchUserData(userId) {
    if (!userId) {
        throw new Error('User ID is required');
    }
    
    try {
        const response = await fetch(`/api/users/${userId}`);
        if (!response.ok) {
            throw new Error(`Failed to fetch user: ${response.status} ${response.statusText}`);
        }
        return await response.json();
    } catch (error) {
        if (error.name === 'TypeError') {
            throw new Error('Network error: Unable to connect to server');
        }
        throw error;
    }
}
```

### 5. Use Finally for Cleanup
```javascript
async function processData() {
    let connection = null;
    
    try {
        connection = await openDatabaseConnection();
        const data = await fetchData(connection);
        return await processData(data);
    } catch (error) {
        console.error('Error processing data:', error);
        throw error;
    } finally {
        if (connection) {
            await closeDatabaseConnection(connection);
        }
    }
}
```

---


