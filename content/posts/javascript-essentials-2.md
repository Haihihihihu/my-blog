---
title: "JSE: Module 2 - Variables, Data Types, Type Casting và Comments"
date: 2025-12-18
draft: false
tags: ["JavaScript", "Variables", "Data Types"]
categories: ["JavaScript Essentials"]
description: "Tìm hiểu về biến, kiểu dữ liệu, ép kiểu và comments trong JavaScript"
---

## Giới thiệu

Trong bài học này, chúng ta sẽ tìm hiểu về các khái niệm cốt lõi của JavaScript: biến, kiểu dữ liệu, ép kiểu và cách viết comments.

## Variables (Biến)

Biến là nơi lưu trữ dữ liệu trong chương trình. JavaScript có 3 cách khai báo biến:

### var, let, và const

```javascript
// var - cách cũ, có function scope
var name = "Hải";

// let - ES6, có block scope, có thể thay đổi
let age = 22;
age = 23; // OK

// const - ES6, có block scope, không thể thay đổi
const PI = 3.14159;
// PI = 3.14; // Error!
```

### Quy tắc đặt tên biến

- Bắt đầu bằng chữ cái, `_` hoặc `$`
- Không được bắt đầu bằng số
- Case-sensitive (phân biệt chữ hoa/thường)
- Không dùng từ khóa của JavaScript

```javascript
// Hợp lệ
let userName = "Hải";
let _temp = 25;
let $price = 100;

// Không hợp lệ
// let 123abc = "test"; // Error
// let let = 5; // Error - từ khóa
```

## Data Types (Kiểu dữ liệu)

JavaScript có 2 nhóm kiểu dữ liệu chính:

### Primitive Types (Kiểu nguyên thủy)

```javascript
// String - Chuỗi
let message = "Hello World";
let name = 'Hải';

// Number - Số
let age = 22;
let price = 99.99;

// Boolean - Logic
let isStudent = true;
let isGraduated = false;

// Undefined - Chưa gán giá trị
let x;
console.log(x); // undefined

// Null - Không có giá trị
let y = null;

// Symbol (ES6)
let id = Symbol('id');

// BigInt (ES2020)
let bigNumber = 9007199254740991n;
```

### Reference Types (Kiểu tham chiếu)

```javascript
// Object
let student = {
    name: "Hải",
    age: 22,
    major: "An ninh mạng"
};

// Array
let numbers = [1, 2, 3, 4, 5];
let colors = ["red", "green", "blue"];

// Function
function greet() {
    console.log("Hello!");
}
```

## Type Checking

```javascript
// typeof operator
console.log(typeof "Hello");     // "string"
console.log(typeof 42);          // "number"
console.log(typeof true);        // "boolean"
console.log(typeof undefined);   // "undefined"
console.log(typeof null);        // "object" (quirk!)
console.log(typeof {});          // "object"
console.log(typeof []);          // "object"
console.log(typeof function(){}); // "function"
```

## Type Casting (Ép kiểu)

### Implicit Coercion (Tự động)

```javascript
// String + Number = String
let result = "5" + 3; // "53"

// Boolean to Number
let x = true + 1; // 2
let y = false + 1; // 1
```

### Explicit Conversion (Tường minh)

```javascript
// String to Number
let str = "123";
let num1 = Number(str);      // 123
let num2 = parseInt(str);    // 123
let num3 = parseFloat("3.14"); // 3.14

// Number to String
let n = 100;
let s1 = String(n);    // "100"
let s2 = n.toString(); // "100"

// To Boolean
Boolean(1);        // true
Boolean(0);        // false
Boolean("");       // false
Boolean("hello");  // true
```

## Comments (Chú thích)

Comments giúp giải thích code và làm cho code dễ đọc hơn.

```javascript
// Comment một dòng
let name = "Hải"; // Comment ở cuối dòng

/*
   Comment nhiều dòng
   Dùng để giải thích
   đoạn code phức tạp
*/
let age = 22;

/**
 * JSDoc comment
 * @param {string} name - Tên người dùng
 * @returns {string} Lời chào
 */
function greet(name) {
    return `Hello ${name}!`;
}
```

## Template Literals (ES6)

```javascript
let name = "Hải";
let age = 22;

// Cách cũ
let message1 = "Tên tôi là " + name + ", " + age + " tuổi";

// Template literals
let message2 = `Tên tôi là ${name}, ${age} tuổi`;

// Multi-line
let html = `
    <div>
        <h1>${name}</h1>
        <p>Age: ${age}</p>
    </div>
`;
```

## Best Practices

1. **Dùng `const` by default**, chỉ dùng `let` khi cần thay đổi giá trị
2. **Tránh dùng `var`** trong code mới
3. **Đặt tên biến có ý nghĩa**: `userName` thay vì `x`
4. **Viết comments cho code phức tạp**
5. **Sử dụng template literals** thay vì nối chuỗi

## Kết luận

Hiểu rõ về variables, data types, type casting và cách viết comments là nền tảng quan trọng để học JavaScript. Trong bài tiếp theo, chúng ta sẽ tìm hiểu về **Operators và User Interaction**.
