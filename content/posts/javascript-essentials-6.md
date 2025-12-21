---
title: "JSE: Module 6 - Errors, Exceptions, Debugging và Troubleshooting"
date: 2025-12-14
draft: false
tags: ["JavaScript", "Debugging", "Error Handling"]
categories: ["JavaScript Essentials"]
description: "Tìm hiểu về xử lý lỗi, debug và troubleshoot trong JavaScript"
---

## Giới thiệu

Trong quá trình lập trình, lỗi là điều không thể tránh khỏi. Bài học này sẽ giúp bạn hiểu về các loại lỗi, cách xử lý exception, và kỹ thuật debugging.

## Các loại Errors

### Syntax Errors

Lỗi cú pháp - code không đúng cú pháp JavaScript.

```javascript
// Syntax Error: thiếu dấu ngoặc
function greet() {
    console.log("Hello"
// Error: missing )

// Syntax Error: từ khóa sai
const let = 5; // Error: 'let' is a reserved keyword

// Syntax Error: thiếu dấu }
if (true) {
    console.log("test");
// Error: missing }
```

### Runtime Errors

Lỗi xảy ra khi code đang chạy.

```javascript
// ReferenceError: biến không tồn tại
console.log(nonExistentVariable);
// ReferenceError: nonExistentVariable is not defined

// TypeError: gọi method không tồn tại
let num = 5;
num.toUpperCase();
// TypeError: num.toUpperCase is not a function

// RangeError: giá trị ngoài phạm vi
let arr = new Array(-1);
// RangeError: Invalid array length
```

### Logical Errors

Lỗi logic - code chạy được nhưng kết quả sai.

```javascript
// Tính trung bình sai
function average(a, b) {
    return a + b / 2; // Bug! Nên là (a + b) / 2
}

console.log(average(10, 20)); // 20, sai! Đáng ra là 15

// Vòng lặp sai điều kiện
for (let i = 10; i > 0; i++) { // Bug! i++ nên là i--
    console.log(i); // Infinite loop!
}
```

## Try...Catch...Finally

### Cú pháp cơ bản

```javascript
try {
    // Code có thể gây lỗi
    let result = riskyOperation();
    console.log(result);
} catch (error) {
    // Xử lý lỗi
    console.error("Có lỗi xảy ra:", error.message);
} finally {
    // Luôn chạy dù có lỗi hay không
    console.log("Cleanup code");
}
```

### Ví dụ thực tế

```javascript
// Parse JSON
function parseJSON(jsonString) {
    try {
        let data = JSON.parse(jsonString);
        return data;
    } catch (error) {
        console.error("Invalid JSON:", error.message);
        return null;
    }
}

let result = parseJSON('{"name": "Hải"}'); // OK
let invalid = parseJSON('invalid json');   // Lỗi, nhưng không crash

// Chia số
function divide(a, b) {
    try {
        if (b === 0) {
            throw new Error("Không thể chia cho 0");
        }
        return a / b;
    } catch (error) {
        console.error(error.message);
        return null;
    } finally {
        console.log("Phép chia hoàn tất");
    }
}
```

## Throwing Errors

### throw statement

```javascript
// Throw Error object
function checkAge(age) {
    if (age < 0) {
        throw new Error("Tuổi không thể âm");
    }
    if (age < 18) {
        throw new Error("Chưa đủ tuổi");
    }
    return "OK";
}

try {
    checkAge(-5);
} catch (error) {
    console.error(error.message); // "Tuổi không thể âm"
}

// Throw custom value
function validateUsername(username) {
    if (username.length < 3) {
        throw "Username quá ngắn";
    }
    if (username.length > 20) {
        throw "Username quá dài";
    }
    return true;
}
```

### Custom Error Types

```javascript
// Tạo custom error class
class ValidationError extends Error {
    constructor(message) {
        super(message);
        this.name = "ValidationError";
    }
}

class NetworkError extends Error {
    constructor(message) {
        super(message);
        this.name = "NetworkError";
    }
}

// Sử dụng
function validateEmail(email) {
    if (!email.includes("@")) {
        throw new ValidationError("Email không hợp lệ");
    }
    return true;
}

try {
    validateEmail("invalid-email");
} catch (error) {
    if (error instanceof ValidationError) {
        console.error("Validation lỗi:", error.message);
    } else {
        console.error("Lỗi khác:", error.message);
    }
}
```

## Debugging Techniques

### console Methods

```javascript
// console.log - In thông tin
console.log("Debug info:", variable);

// console.error - In lỗi (màu đỏ)
console.error("Error occurred!");

// console.warn - Cảnh báo (màu vàng)
console.warn("This is deprecated");

// console.table - Hiển thị array/object dạng bảng
let users = [
    { name: "Hải", age: 22 },
    { name: "Nam", age: 23 }
];
console.table(users);

// console.time / console.timeEnd - Đo thời gian
console.time("myTimer");
for (let i = 0; i < 1000000; i++) {
    // Some operation
}
console.timeEnd("myTimer"); // "myTimer: 5.234ms"

// console.trace - Stack trace
function func1() {
    func2();
}
function func2() {
    console.trace("Trace:");
}
func1();
```

### Breakpoints (Browser DevTools)

```javascript
// debugger statement - Dừng chương trình tại đây
function calculateTotal(items) {
    let total = 0;
    debugger; // Browser sẽ pause ở đây
    
    for (let item of items) {
        total += item.price;
    }
    
    return total;
}
```

### Type Checking

```javascript
// Kiểm tra type để tránh lỗi
function processData(data) {
    // Type guards
    if (typeof data !== "object") {
        throw new TypeError("Data phải là object");
    }
    
    if (!Array.isArray(data.items)) {
        throw new TypeError("items phải là array");
    }
    
    // Safe to process
    return data.items.length;
}
```

## Error Prevention

### Input Validation

```javascript
function createUser(name, age, email) {
    // Validate name
    if (!name || typeof name !== "string") {
        throw new ValidationError("Tên không hợp lệ");
    }
    
    if (name.length < 2 || name.length > 50) {
        throw new ValidationError("Tên phải từ 2-50 ký tự");
    }
    
    // Validate age
    if (typeof age !== "number" || age < 0 || age > 150) {
        throw new ValidationError("Tuổi không hợp lệ");
    }
    
    // Validate email
    if (!email || !email.includes("@")) {
        throw new ValidationError("Email không hợp lệ");
    }
    
    return { name, age, email };
}
```

### Defensive Programming

```javascript
// Kiểm tra null/undefined
function getUserName(user) {
    // Bad
    return user.name; // Error nếu user null!
    
    // Good
    return user?.name ?? "Guest"; // Optional chaining + nullish coalescing
}

// Default values
function greet(name = "Guest") {
    console.log(`Hello ${name}!`);
}

// Type checking
function add(a, b) {
    if (typeof a !== "number" || typeof b !== "number") {
        throw new TypeError("Arguments phải là số");
    }
    return a + b;
}
```

## Common Errors và Solutions

### ReferenceError

```javascript
// Lỗi: biến chưa khai báo
console.log(x); // ReferenceError

// Fix: khai báo trước khi dùng
let x = 5;
console.log(x); // OK
```

### TypeError

```javascript
// Lỗi: gọi method trên null/undefined
let obj = null;
obj.toString(); // TypeError

// Fix: kiểm tra trước
if (obj) {
    obj.toString();
}
// Hoặc dùng optional chaining
obj?.toString();
```

### Infinite Loop

```javascript
// Lỗi: vòng lặp vô hạn
let i = 0;
while (i < 10) {
    console.log(i);
    // Quên tăng i!
}

// Fix: đảm bảo điều kiện dừng
let i = 0;
while (i < 10) {
    console.log(i);
    i++; // Tăng i
}
```

## Best Practices

1. **Luôn validate input** từ user
2. **Sử dụng try...catch** cho code có thể lỗi
3. **Throw meaningful errors** với message rõ ràng
4. **Log errors** để troubleshoot
5. **Test edge cases** (null, undefined, empty, negative)
6. **Sử dụng linter** (ESLint) để tìm lỗi
7. **Debug bằng console và breakpoints**

```javascript
// Good error handling
async function fetchUserData(userId) {
    try {
        // Validate input
        if (!userId) {
            throw new ValidationError("User ID là bắt buộc");
        }
        
        // Fetch data
        const response = await fetch(`/api/users/${userId}`);
        
        if (!response.ok) {
            throw new NetworkError(`HTTP ${response.status}`);
        }
        
        const data = await response.json();
        return data;
        
    } catch (error) {
        // Log error
        console.error("Fetch user failed:", error);
        
        // Re-throw hoặc return default
        if (error instanceof NetworkError) {
            throw error; // Let caller handle
        }
        
        return null; // Return safe default
    }
}
```

## Kết luận

Xử lý lỗi đúng cách và debugging hiệu quả là kỹ năng quan trọng của mọi developer. Hiểu rõ các loại lỗi, cách prevent và handle chúng sẽ giúp bạn viết code robust và dễ maintain hơn.

Tiếp theo: **JavaScript Essentials 2 - Classless Objects**!
