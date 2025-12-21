---
title: "JSE: Module 3 - Operators và User Interaction"
date: 2025-12-17
draft: false
tags: ["JavaScript", "Operators", "User Input"]
categories: ["JavaScript Essentials"]
description: "Tìm hiểu về các toán tử và tương tác người dùng trong JavaScript"
---

## Giới thiệu

Trong bài này, chúng ta sẽ học về các toán tử (operators) trong JavaScript và cách tương tác với người dùng.

## Arithmetic Operators (Toán tử số học)

```javascript
let a = 10;
let b = 3;

console.log(a + b);  // 13 - Cộng
console.log(a - b);  // 7  - Trừ
console.log(a * b);  // 30 - Nhân
console.log(a / b);  // 3.333... - Chia
console.log(a % b);  // 1  - Chia lấy dư
console.log(a ** b); // 1000 - Lũy thừa (ES2016)

// Increment và Decrement
let x = 5;
x++;  // x = 6 (post-increment)
++x;  // x = 7 (pre-increment)
x--;  // x = 6 (post-decrement)
--x;  // x = 5 (pre-decrement)
```

## Assignment Operators (Toán tử gán)

```javascript
let x = 10;

x += 5;  // x = x + 5  (15)
x -= 3;  // x = x - 3  (12)
x *= 2;  // x = x * 2  (24)
x /= 4;  // x = x / 4  (6)
x %= 4;  // x = x % 4  (2)
x **= 3; // x = x ** 3 (8)
```

## Comparison Operators (Toán tử so sánh)

```javascript
let a = 5;
let b = "5";

// So sánh bằng (loose equality)
console.log(a == b);   // true (chỉ so giá trị)

// So sánh bằng strict (strict equality)
console.log(a === b);  // false (so cả giá trị và kiểu)

// Không bằng
console.log(a != b);   // false
console.log(a !== b);  // true

// So sánh lớn hơn, nhỏ hơn
console.log(10 > 5);   // true
console.log(10 < 5);   // false
console.log(10 >= 10); // true
console.log(10 <= 5);  // false
```

## Logical Operators (Toán tử logic)

```javascript
let age = 22;
let isStudent = true;

// AND (&&) - Cả hai đều true
console.log(age > 18 && isStudent);  // true

// OR (||) - Một trong hai true
console.log(age < 18 || isStudent);  // true

// NOT (!) - Đảo ngược
console.log(!isStudent);  // false

// Short-circuit evaluation
let name = username || "Guest"; // Nếu username falsy, dùng "Guest"
let value = isValid && getValue(); // Chỉ gọi getValue() nếu isValid true
```

## String Operators

```javascript
// Concatenation (Nối chuỗi)
let firstName = "Nguyễn";
let lastName = "Hải";
let fullName = firstName + " " + lastName; // "Nguyễn Hải"

// += với string
let message = "Hello";
message += " World"; // "Hello World"

// Template literals (cách tốt hơn)
let greeting = `${firstName} ${lastName}`;
```

## Ternary Operator (Toán tử 3 ngôi)

```javascript
// Cú pháp: condition ? valueIfTrue : valueIfFalse

let age = 20;
let status = age >= 18 ? "Người lớn" : "Trẻ em";
console.log(status); // "Người lớn"

// Nested ternary
let score = 85;
let grade = score >= 90 ? "A" :
            score >= 80 ? "B" :
            score >= 70 ? "C" : "D";
```

## Operator Precedence (Độ ưu tiên)

```javascript
// Phép nhân có độ ưu tiên cao hơn cộng
let result = 5 + 3 * 2;  // 11, không phải 16

// Dùng ngoặc để thay đổi thứ tự
let result2 = (5 + 3) * 2;  // 16

// Độ ưu tiên (cao -> thấp):
// 1. () - Ngoặc đơn
// 2. ++, -- - Increment/Decrement
// 3. **, *, /, % - Số học
// 4. +, - - Cộng trừ
// 5. <, >, <=, >= - So sánh
// 6. ==, !=, ===, !== - Bằng/Không bằng
// 7. && - AND logic
// 8. || - OR logic
// 9. = - Gán
```

## User Interaction

### alert() - Hiển thị thông báo

```javascript
alert("Xin chào!");
alert("Đây là một thông báo");
```

### prompt() - Nhập liệu

```javascript
// Cú pháp: prompt(message, defaultValue)
let name = prompt("Tên bạn là gì?", "");
console.log(`Xin chào ${name}!`);

let age = prompt("Bạn bao nhiêu tuổi?", "18");
let ageNumber = Number(age); // Convert sang số
```

### confirm() - Xác nhận

```javascript
let isConfirmed = confirm("Bạn có chắc chắn?");

if (isConfirmed) {
    console.log("User nhấn OK");
} else {
    console.log("User nhấn Cancel");
}
```

## Ví dụ thực tế

### Calculator đơn giản

```javascript
let num1 = Number(prompt("Nhập số thứ nhất:"));
let operator = prompt("Nhập toán tử (+, -, *, /):");
let num2 = Number(prompt("Nhập số thứ hai:"));

let result;

if (operator === "+") {
    result = num1 + num2;
} else if (operator === "-") {
    result = num1 - num2;
} else if (operator === "*") {
    result = num1 * num2;
} else if (operator === "/") {
    result = num1 / num2;
} else {
    result = "Toán tử không hợp lệ";
}

alert(`Kết quả: ${result}`);
```

### Kiểm tra tuổi

```javascript
let age = Number(prompt("Bạn bao nhiêu tuổi?"));

let message = age >= 18 
    ? "Bạn đã đủ tuổi" 
    : "Bạn chưa đủ tuổi";

alert(message);
```

## Best Practices

1. **Dùng `===` thay vì `==`** để tránh lỗi type coercion
2. **Dùng template literals** thay vì nối chuỗi với `+`
3. **Validate input** từ người dùng
4. **Dùng ngoặc** để làm rõ thứ tự tính toán
5. **Tránh nested ternary** quá phức tạp

## Kết luận

Operators là công cụ cơ bản để xử lý dữ liệu trong JavaScript. Hiểu rõ các toán tử và cách tương tác với người dùng sẽ giúp bạn xây dựng các ứng dụng tương tác hiệu quả.

Bài tiếp theo, chúng ta sẽ học về **Control Flow - Conditional Execution và Loops**.
