---
title: "JSE2: Module 4 - Advanced Function Usage"
date: 2025-12-10
draft: false
tags: ["JavaScript", "Functions", "Advanced", "Async"]
categories: ["JavaScript Essentials 2"]
description: "Tìm hiểu về các kỹ thuật nâng cao khi làm việc với Functions"
---

## Giới thiệu

Bài học cuối cùng của khóa JSE2 sẽ đi sâu vào các kỹ thuật nâng cao khi làm việc với functions, bao gồm: callbacks, promises, async/await, generators, và functional programming patterns.

## Callback Functions

### Callback Pattern

```javascript
// Synchronous callback
function processArray(arr, callback) {
    let result = [];
    for (let item of arr) {
        result.push(callback(item));
    }
    return result;
}

let numbers = [1, 2, 3, 4, 5];
let doubled = processArray(numbers, x => x * 2);
console.log(doubled); // [2, 4, 6, 8, 10]

// Asynchronous callback
function fetchData(url, onSuccess, onError) {
    setTimeout(() => {
        if (url) {
            onSuccess({ data: "Some data from " + url });
        } else {
            onError("Invalid URL");
        }
    }, 1000);
}

fetchData(
    "api.example.com",
    (data) => console.log("Success:", data),
    (error) => console.error("Error:", error)
);
```

### Callback Hell

```javascript
// Anti-pattern: Callback hell (Pyramid of Doom)
getData(function(a) {
    getMoreData(a, function(b) {
        getEvenMoreData(b, function(c) {
            getYetMoreData(c, function(d) {
                // Quá nhiều nested callbacks!
                console.log(d);
            });
        });
    });
});
```

## Promises

### Creating Promises

```javascript
// Promise creation
let promise = new Promise((resolve, reject) => {
    let success = true;
    
    setTimeout(() => {
        if (success) {
            resolve("Operation successful!");
        } else {
            reject("Operation failed!");
        }
    }, 1000);
});

// Consuming promise
promise
    .then(result => {
        console.log(result);
        return "Next step";
    })
    .then(result => {
        console.log(result);
    })
    .catch(error => {
        console.error(error);
    })
    .finally(() => {
        console.log("Cleanup");
    });
```

### Promise Chaining

```javascript
// Clean promise chain
function fetchUser(userId) {
    return new Promise((resolve) => {
        setTimeout(() => resolve({ id: userId, name: "Hải" }), 500);
    });
}

function fetchPosts(user) {
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve([
                { id: 1, title: "Post 1" },
                { id: 2, title: "Post 2" }
            ]);
        }, 500);
    });
}

function fetchComments(post) {
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve([
                { id: 1, text: "Comment 1" },
                { id: 2, text: "Comment 2" }
            ]);
        }, 500);
    });
}

// Chain promises
fetchUser(1)
    .then(user => {
        console.log("User:", user);
        return fetchPosts(user);
    })
    .then(posts => {
        console.log("Posts:", posts);
        return fetchComments(posts[0]);
    })
    .then(comments => {
        console.log("Comments:", comments);
    })
    .catch(error => {
        console.error("Error:", error);
    });
```

### Promise Static Methods

```javascript
// Promise.all - Chờ tất cả hoàn thành
let promise1 = Promise.resolve(1);
let promise2 = Promise.resolve(2);
let promise3 = Promise.resolve(3);

Promise.all([promise1, promise2, promise3])
    .then(results => {
        console.log(results); // [1, 2, 3]
    });

// Promise.race - Lấy kết quả đầu tiên
Promise.race([
    new Promise(resolve => setTimeout(() => resolve(1), 1000)),
    new Promise(resolve => setTimeout(() => resolve(2), 500))
])
.then(result => {
    console.log(result); // 2 (faster)
});

// Promise.allSettled - Chờ tất cả (dù success hay fail)
Promise.allSettled([
    Promise.resolve(1),
    Promise.reject("Error"),
    Promise.resolve(3)
])
.then(results => {
    console.log(results);
    // [
    //   { status: "fulfilled", value: 1 },
    //   { status: "rejected", reason: "Error" },
    //   { status: "fulfilled", value: 3 }
    // ]
});

// Promise.any - Lấy fulfilled đầu tiên
Promise.any([
    Promise.reject("Error 1"),
    Promise.resolve(2),
    Promise.resolve(3)
])
.then(result => {
    console.log(result); // 2
});
```

## Async/Await

### Basic Async/Await

```javascript
// Async function luôn return Promise
async function getData() {
    return "Hello"; // Tự động wrap trong Promise
}

getData().then(data => console.log(data)); // "Hello"

// Await chỉ dùng trong async function
async function fetchData() {
    try {
        let response = await fetch("https://api.example.com/data");
        let data = await response.json();
        return data;
    } catch (error) {
        console.error("Error:", error);
        throw error;
    }
}
```

### Sequential vs Parallel

```javascript
// Sequential - chạy lần lượt
async function sequential() {
    let user = await fetchUser(1);     // Đợi xong
    let posts = await fetchPosts(user); // Mới chạy
    let comments = await fetchComments(posts[0]);
    return comments;
}

// Parallel - chạy đồng thời
async function parallel() {
    let [user, posts] = await Promise.all([
        fetchUser(1),
        fetchPosts({ id: 1 })
    ]);
    return { user, posts };
}

// Đo thời gian
async function comparePerformance() {
    console.time("Sequential");
    await sequential();
    console.timeEnd("Sequential"); // ~1500ms
    
    console.time("Parallel");
    await parallel();
    console.timeEnd("Parallel");   // ~500ms
}
```

### Error Handling với Async/Await

```javascript
async function fetchUserData(userId) {
    try {
        let response = await fetch(`/api/users/${userId}`);
        
        if (!response.ok) {
            throw new Error(`HTTP ${response.status}`);
        }
        
        let data = await response.json();
        return data;
        
    } catch (error) {
        console.error("Fetch failed:", error);
        
        // Re-throw hoặc return default
        return null;
    }
}

// Hoặc handle ở caller
async function main() {
    try {
        let user = await fetchUserData(1);
        console.log(user);
    } catch (error) {
        console.error("Main error:", error);
    }
}
```

## Generator Functions

```javascript
// Generator function - dùng function*
function* numberGenerator() {
    yield 1;
    yield 2;
    yield 3;
}

let gen = numberGenerator();
console.log(gen.next()); // { value: 1, done: false }
console.log(gen.next()); // { value: 2, done: false }
console.log(gen.next()); // { value: 3, done: false }
console.log(gen.next()); // { value: undefined, done: true }

// Iterate generator
for (let num of numberGenerator()) {
    console.log(num); // 1, 2, 3
}

// Infinite generator
function* idGenerator() {
    let id = 1;
    while (true) {
        yield id++;
    }
}

let idGen = idGenerator();
console.log(idGen.next().value); // 1
console.log(idGen.next().value); // 2
console.log(idGen.next().value); // 3

// Generator với parameters
function* range(start, end) {
    for (let i = start; i <= end; i++) {
        yield i;
    }
}

console.log([...range(1, 5)]); // [1, 2, 3, 4, 5]
```

## Higher-Order Functions

### Function Composition

```javascript
// Compose functions
const compose = (...fns) => x => fns.reduceRight((v, f) => f(v), x);

const double = x => x * 2;
const square = x => x * x;
const addOne = x => x + 1;

const doMath = compose(addOne, square, double);
console.log(doMath(3)); // ((3 * 2) ^ 2) + 1 = 37

// Pipe (ngược lại với compose)
const pipe = (...fns) => x => fns.reduce((v, f) => f(v), x);

const doMathPipe = pipe(double, square, addOne);
console.log(doMathPipe(3)); // ((3 * 2) ^ 2) + 1 = 37
```

### Currying

```javascript
// Currying - transform f(a, b, c) thành f(a)(b)(c)
function curry(fn) {
    return function curried(...args) {
        if (args.length >= fn.length) {
            return fn.apply(this, args);
        } else {
            return function(...args2) {
                return curried.apply(this, args.concat(args2));
            };
        }
    };
}

function sum(a, b, c) {
    return a + b + c;
}

let curriedSum = curry(sum);
console.log(curriedSum(1)(2)(3));     // 6
console.log(curriedSum(1, 2)(3));     // 6
console.log(curriedSum(1)(2, 3));     // 6

// Practical example
const multiply = (a) => (b) => a * b;
const double = multiply(2);
const triple = multiply(3);

console.log(double(5));  // 10
console.log(triple(5));  // 15
```

### Partial Application

```javascript
function partial(fn, ...fixedArgs) {
    return function(...remainingArgs) {
        return fn(...fixedArgs, ...remainingArgs);
    };
}

function greet(greeting, name) {
    return `${greeting}, ${name}!`;
}

const sayHello = partial(greet, "Hello");
console.log(sayHello("Hải"));  // "Hello, Hải!"

const sayHi = partial(greet, "Hi");
console.log(sayHi("Nam"));     // "Hi, Nam!"
```

## Memoization

```javascript
// Cache function results
function memoize(fn) {
    const cache = {};
    
    return function(...args) {
        const key = JSON.stringify(args);
        
        if (key in cache) {
            console.log("From cache");
            return cache[key];
        }
        
        console.log("Calculating...");
        const result = fn(...args);
        cache[key] = result;
        return result;
    };
}

// Expensive function
function fibonacci(n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

const memoizedFib = memoize(fibonacci);
console.log(memoizedFib(40)); // Calculating... 102334155
console.log(memoizedFib(40)); // From cache 102334155
```

## Function Decorators

```javascript
// Decorator pattern
function timer(fn) {
    return function(...args) {
        console.time(fn.name);
        const result = fn(...args);
        console.timeEnd(fn.name);
        return result;
    };
}

function logger(fn) {
    return function(...args) {
        console.log(`Calling ${fn.name} with`, args);
        const result = fn(...args);
        console.log(`${fn.name} returned`, result);
        return result;
    };
}

// Apply decorators
function add(a, b) {
    return a + b;
}

const timedAdd = timer(add);
const loggedAdd = logger(add);
const bothDecorated = timer(logger(add));

bothDecorated(5, 3);
// Calling add with [5, 3]
// add returned 8
// add: 0.123ms
```

## Debounce và Throttle

```javascript
// Debounce - chỉ chạy sau khi ngừng gọi trong delay ms
function debounce(fn, delay) {
    let timeoutId;
    
    return function(...args) {
        clearTimeout(timeoutId);
        timeoutId = setTimeout(() => fn(...args), delay);
    };
}

// Sử dụng cho search input
const search = debounce((query) => {
    console.log("Searching for:", query);
}, 500);

// Throttle - chỉ chạy 1 lần trong delay ms
function throttle(fn, delay) {
    let lastCall = 0;
    
    return function(...args) {
        const now = Date.now();
        
        if (now - lastCall >= delay) {
            lastCall = now;
            fn(...args);
        }
    };
}

// Sử dụng cho scroll event
const handleScroll = throttle(() => {
    console.log("Scrolled!");
}, 1000);
```

## Real-World Example: API Client

```javascript
class APIClient {
    constructor(baseURL) {
        this.baseURL = baseURL;
    }
    
    async request(endpoint, options = {}) {
        const url = `${this.baseURL}${endpoint}`;
        
        try {
            const response = await fetch(url, {
                headers: {
                    'Content-Type': 'application/json',
                    ...options.headers
                },
                ...options
            });
            
            if (!response.ok) {
                throw new Error(`HTTP ${response.status}`);
            }
            
            return await response.json();
        } catch (error) {
            console.error(`Request failed: ${url}`, error);
            throw error;
        }
    }
    
    get(endpoint) {
        return this.request(endpoint, { method: 'GET' });
    }
    
    post(endpoint, data) {
        return this.request(endpoint, {
            method: 'POST',
            body: JSON.stringify(data)
        });
    }
    
    put(endpoint, data) {
        return this.request(endpoint, {
            method: 'PUT',
            body: JSON.stringify(data)
        });
    }
    
    delete(endpoint) {
        return this.request(endpoint, { method: 'DELETE' });
    }
}

// Usage
const api = new APIClient('https://api.example.com');

async function main() {
    try {
        // Get all users
        const users = await api.get('/users');
        console.log(users);
        
        // Create new user
        const newUser = await api.post('/users', {
            name: 'Hải',
            email: 'hai@example.com'
        });
        
        // Update user
        await api.put(`/users/${newUser.id}`, {
            name: 'Nguyễn Hải'
        });
        
    } catch (error) {
        console.error('Main error:', error);
    }
}
```

## Best Practices

1. **Prefer async/await over promises** cho code dễ đọc
2. **Sử dụng Promise.all** cho parallel operations
3. **Always handle errors** trong async functions
4. **Memoize expensive functions** để improve performance
5. **Debounce/throttle** cho event handlers
6. **Use generators** cho lazy evaluation
7. **Function composition** thay vì nested function calls

## Kết luận

Advanced function techniques giúp bạn viết code JavaScript hiệu quả và elegant hơn. Nắm vững callbacks, promises, async/await, generators, và functional programming patterns là bước quan trọng để trở thành JavaScript developer giỏi.

**Chúc mừng bạn đã hoàn thành khóa JavaScript Essentials! 🎉**
