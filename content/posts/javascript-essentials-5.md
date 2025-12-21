---
title: "JSE: Module 5 - Functions"
date: 2025-12-15
draft: false
tags: ["JavaScript", "Functions", "Parameters"]
categories: ["JavaScript Essentials"]
description: "Tìm hiểu chi tiết về Functions trong JavaScript"
---

## Giới thiệu

Functions (hàm) là khối code có thể tái sử dụng để thực hiện một tác vụ cụ thể. Đây là một trong những khái niệm quan trọng nhất trong JavaScript.

## Function Declaration

```javascript
// Cú pháp cơ bản
function greet() {
    console.log("Xin chào!");
}

// Gọi hàm
greet(); // "Xin chào!"

// Function với parameters
function greetUser(name) {
    console.log(`Xin chào ${name}!`);
}

greetUser("Hải"); // "Xin chào Hải!"

// Multiple parameters
function add(a, b) {
    return a + b;
}

let result = add(5, 3);
console.log(result); // 8
```

## Function Expression

```javascript
// Anonymous function expression
const multiply = function(a, b) {
    return a * b;
};

console.log(multiply(4, 5)); // 20

// Named function expression
const factorial = function fact(n) {
    if (n <= 1) return 1;
    return n * fact(n - 1);
};

console.log(factorial(5)); // 120
```

## Arrow Functions (ES6)

```javascript
// Cú pháp ngắn gọn
const square = (x) => x * x;
console.log(square(5)); // 25

// Với multiple parameters
const add = (a, b) => a + b;

// Với body nhiều dòng
const greet = (name) => {
    let message = `Hello ${name}!`;
    return message;
};

// Không có parameters
const sayHi = () => console.log("Hi!");

// Một parameter (có thể bỏ ngoặc)
const double = x => x * 2;
```

## Parameters và Arguments

### Default Parameters

```javascript
function greet(name = "Guest") {
    console.log(`Hello ${name}!`);
}

greet();        // "Hello Guest!"
greet("Hải");   // "Hello Hải!"

// Multiple defaults
function createUser(name = "Anonymous", age = 18, role = "User") {
    return { name, age, role };
}
```

### Rest Parameters

```javascript
// Thu thập tất cả arguments còn lại
function sum(...numbers) {
    let total = 0;
    for (let num of numbers) {
        total += num;
    }
    return total;
}

console.log(sum(1, 2, 3));        // 6
console.log(sum(1, 2, 3, 4, 5));  // 15

// Rest parameters phải ở cuối
function introduce(firstName, lastName, ...hobbies) {
    console.log(`Name: ${firstName} ${lastName}`);
    console.log(`Hobbies: ${hobbies.join(", ")}`);
}

introduce("Nguyễn", "Hải", "Coding", "Reading", "Gaming");
```

### Spread Operator

```javascript
let numbers = [1, 2, 3, 4, 5];

// Spread array thành arguments
console.log(Math.max(...numbers)); // 5

// Kết hợp arrays
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];
let combined = [...arr1, ...arr2]; // [1,2,3,4,5,6]

// Copy array
let original = [1, 2, 3];
let copy = [...original];
```

## Return Statement

```javascript
// Return value
function multiply(a, b) {
    return a * b;
}

// Return object
function createPerson(name, age) {
    return {
        name: name,
        age: age,
        greet: function() {
            console.log(`Hi, I'm ${this.name}`);
        }
    };
}

// Early return
function checkAge(age) {
    if (age < 0) {
        return "Invalid age";
    }
    if (age < 18) {
        return "Minor";
    }
    return "Adult";
}

// Return undefined (implicit)
function doSomething() {
    console.log("Done");
    // No return statement = returns undefined
}
```

## Function Scope

```javascript
// Global scope
let globalVar = "global";

function testScope() {
    // Function scope
    let functionVar = "function";
    
    if (true) {
        // Block scope
        let blockVar = "block";
        console.log(globalVar);   // ✓ Accessible
        console.log(functionVar); // ✓ Accessible
        console.log(blockVar);    // ✓ Accessible
    }
    
    console.log(globalVar);   // ✓ Accessible
    console.log(functionVar); // ✓ Accessible
    // console.log(blockVar); // ✗ Error!
}

console.log(globalVar); // ✓ Accessible
// console.log(functionVar); // ✗ Error!
```

## Closure

```javascript
// Function nhớ scope của nó
function createCounter() {
    let count = 0;
    
    return function() {
        count++;
        return count;
    };
}

let counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3

// Private variables với closure
function bankAccount(initialBalance) {
    let balance = initialBalance;
    
    return {
        deposit: function(amount) {
            balance += amount;
            return balance;
        },
        withdraw: function(amount) {
            if (amount <= balance) {
                balance -= amount;
                return balance;
            }
            return "Insufficient funds";
        },
        getBalance: function() {
            return balance;
        }
    };
}

let account = bankAccount(1000);
console.log(account.deposit(500));  // 1500
console.log(account.withdraw(200)); // 1300
console.log(account.getBalance());  // 1300
```

## Callback Functions

```javascript
// Function as argument
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

// Real-world example
function fetchData(url, onSuccess, onError) {
    // Simulate API call
    setTimeout(() => {
        if (url) {
            onSuccess({ data: "Some data" });
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

## Higher-Order Functions

```javascript
// Function trả về function
function multiplier(factor) {
    return function(number) {
        return number * factor;
    };
}

let double = multiplier(2);
let triple = multiplier(3);

console.log(double(5));  // 10
console.log(triple(5));  // 15

// Built-in higher-order functions
let numbers = [1, 2, 3, 4, 5];

// map
let squared = numbers.map(x => x * x);
console.log(squared); // [1, 4, 9, 16, 25]

// filter
let evens = numbers.filter(x => x % 2 === 0);
console.log(evens); // [2, 4]

// reduce
let sum = numbers.reduce((acc, curr) => acc + curr, 0);
console.log(sum); // 15
```

## Recursion

```javascript
// Factorial
function factorial(n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}

console.log(factorial(5)); // 120

// Fibonacci
function fibonacci(n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

console.log(fibonacci(7)); // 13

// Countdown
function countdown(n) {
    console.log(n);
    if (n > 0) {
        countdown(n - 1);
    } else {
        console.log("Done!");
    }
}

countdown(5);
```

## IIFE (Immediately Invoked Function Expression)

```javascript
// Execute ngay khi định nghĩa
(function() {
    console.log("IIFE executed!");
})();

// Với parameters
(function(name) {
    console.log(`Hello ${name}!`);
})("Hải");

// Arrow function IIFE
(() => {
    console.log("Arrow IIFE!");
})();

// Sử dụng để tạo scope riêng
(function() {
    let privateVar = "secret";
    // privateVar chỉ tồn tại trong scope này
})();
```

## Best Practices

1. **Đặt tên hàm có ý nghĩa**: `calculateTotal()` thay vì `calc()`
2. **Một hàm một nhiệm vụ**: Function nên làm một việc và làm tốt việc đó
3. **Sử dụng arrow functions** cho callback ngắn
4. **Tránh quá nhiều parameters** (> 3-4)
5. **Document phức tạp functions** với JSDoc
6. **Sử dụng default parameters** thay vì check undefined

```javascript
// Good
function createUser(name, age = 18, role = "user") {
    return { name, age, role };
}

// Avoid
function createUser(name, age, role) {
    age = age || 18;
    role = role || "user";
    return { name, age, role };
}
```

## Kết luận

Functions là nền tảng của JavaScript programming. Hiểu rõ về functions, closure, callbacks, và higher-order functions sẽ giúp bạn viết code hiệu quả và dễ bảo trì.

Bài tiếp theo: **Errors, Exceptions, Debugging, và Troubleshooting**!
