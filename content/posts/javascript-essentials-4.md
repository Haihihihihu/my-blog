---
title: "JSE: Module 4 - Control Flow: Conditional Execution và Loops"
date: 2025-12-16
draft: false
tags: ["JavaScript", "Control Flow", "Loops"]
categories: ["JavaScript Essentials"]
description: "Tìm hiểu về cấu trúc điều khiển và vòng lặp trong JavaScript"
---

## Giới thiệu

Control Flow (luồng điều khiển) cho phép chúng ta quyết định code nào sẽ được thực thi dựa trên điều kiện, hoặc lặp lại một đoạn code nhiều lần.

## Conditional Statements (Câu lệnh điều kiện)

### if Statement

```javascript
let age = 20;

if (age >= 18) {
    console.log("Bạn đã đủ tuổi");
}
```

### if...else

```javascript
let score = 75;

if (score >= 80) {
    console.log("Giỏi");
} else {
    console.log("Cần cố gắng");
}
```

### if...else if...else

```javascript
let score = 85;

if (score >= 90) {
    console.log("Xuất sắc (A)");
} else if (score >= 80) {
    console.log("Giỏi (B)");
} else if (score >= 70) {
    console.log("Khá (C)");
} else if (score >= 60) {
    console.log("Trung bình (D)");
} else {
    console.log("Yếu (F)");
}
```

### switch Statement

```javascript
let day = 3;
let dayName;

switch (day) {
    case 1:
        dayName = "Thứ Hai";
        break;
    case 2:
        dayName = "Thứ Ba";
        break;
    case 3:
        dayName = "Thứ Tư";
        break;
    case 4:
        dayName = "Thứ Năm";
        break;
    case 5:
        dayName = "Thứ Sáu";
        break;
    case 6:
        dayName = "Thứ Bảy";
        break;
    case 7:
        dayName = "Chủ Nhật";
        break;
    default:
        dayName = "Không hợp lệ";
}

console.log(dayName); // "Thứ Tư"
```

### Multiple cases

```javascript
let month = 2;
let season;

switch (month) {
    case 12:
    case 1:
    case 2:
        season = "Mùa đông";
        break;
    case 3:
    case 4:
    case 5:
        season = "Mùa xuân";
        break;
    case 6:
    case 7:
    case 8:
        season = "Mùa hè";
        break;
    case 9:
    case 10:
    case 11:
        season = "Mùa thu";
        break;
    default:
        season = "Tháng không hợp lệ";
}
```

## Loops (Vòng lặp)

### for Loop

```javascript
// In số từ 1 đến 5
for (let i = 1; i <= 5; i++) {
    console.log(i);
}

// Tính tổng từ 1 đến 100
let sum = 0;
for (let i = 1; i <= 100; i++) {
    sum += i;
}
console.log(sum); // 5050
```

### while Loop

```javascript
// In số từ 1 đến 5
let i = 1;
while (i <= 5) {
    console.log(i);
    i++;
}

// Đoán số
let target = 7;
let guess = 0;
while (guess !== target) {
    guess = Math.floor(Math.random() * 10) + 1;
    console.log(`Đoán: ${guess}`);
}
```

### do...while Loop

```javascript
// Chạy ít nhất 1 lần
let count = 0;
do {
    console.log(`Count: ${count}`);
    count++;
} while (count < 5);

// Menu application
let choice;
do {
    choice = prompt(`
        1. Xem thông tin
        2. Cập nhật
        3. Thoát
        Chọn: 
    `);
    
    if (choice === "1") {
        alert("Hiển thị thông tin");
    } else if (choice === "2") {
        alert("Cập nhật thông tin");
    }
} while (choice !== "3");
```

### for...of Loop (Lặp qua array)

```javascript
let colors = ["red", "green", "blue"];

for (let color of colors) {
    console.log(color);
}

// Với string
let name = "JavaScript";
for (let char of name) {
    console.log(char);
}
```

### for...in Loop (Lặp qua object properties)

```javascript
let student = {
    name: "Hải",
    age: 22,
    major: "An ninh mạng"
};

for (let key in student) {
    console.log(`${key}: ${student[key]}`);
}
```

## Loop Control Statements

### break - Thoát khỏi vòng lặp

```javascript
// Tìm số chia hết cho 7
for (let i = 1; i <= 100; i++) {
    if (i % 7 === 0) {
        console.log(`Số đầu tiên chia hết cho 7: ${i}`);
        break; // Thoát vòng lặp
    }
}

// break với label
outerLoop: for (let i = 0; i < 3; i++) {
    for (let j = 0; j < 3; j++) {
        if (i === 1 && j === 1) {
            break outerLoop; // Thoát cả outer loop
        }
        console.log(`i=${i}, j=${j}`);
    }
}
```

### continue - Bỏ qua iteration hiện tại

```javascript
// In số lẻ từ 1-10
for (let i = 1; i <= 10; i++) {
    if (i % 2 === 0) {
        continue; // Bỏ qua số chẵn
    }
    console.log(i); // Chỉ in số lẻ
}

// continue với label
outerLoop: for (let i = 0; i < 5; i++) {
    for (let j = 0; j < 5; j++) {
        if (j === 2) {
            continue outerLoop;
        }
        console.log(`i=${i}, j=${j}`);
    }
}
```

## Nested Loops (Vòng lặp lồng nhau)

```javascript
// In bảng cửu chương
for (let i = 2; i <= 9; i++) {
    console.log(`\nBảng ${i}:`);
    for (let j = 1; j <= 10; j++) {
        console.log(`${i} x ${j} = ${i * j}`);
    }
}

// In hình tam giác
for (let i = 1; i <= 5; i++) {
    let stars = "";
    for (let j = 1; j <= i; j++) {
        stars += "*";
    }
    console.log(stars);
}
/*
*
**
***
****
*****
*/
```

## Ví dụ thực tế

### Kiểm tra số nguyên tố

```javascript
function isPrime(num) {
    if (num <= 1) return false;
    if (num === 2) return true;
    
    for (let i = 2; i <= Math.sqrt(num); i++) {
        if (num % i === 0) {
            return false;
        }
    }
    return true;
}

console.log(isPrime(7));  // true
console.log(isPrime(10)); // false
```

### FizzBuzz

```javascript
for (let i = 1; i <= 100; i++) {
    if (i % 3 === 0 && i % 5 === 0) {
        console.log("FizzBuzz");
    } else if (i % 3 === 0) {
        console.log("Fizz");
    } else if (i % 5 === 0) {
        console.log("Buzz");
    } else {
        console.log(i);
    }
}
```

### Tìm max trong array

```javascript
let numbers = [5, 2, 9, 1, 7, 6];
let max = numbers[0];

for (let num of numbers) {
    if (num > max) {
        max = num;
    }
}

console.log(`Số lớn nhất: ${max}`); // 9
```

## Best Practices

1. **Tránh infinite loops** - Luôn đảm bảo điều kiện dừng
2. **Chọn đúng loại loop** phù hợp với tình huống
3. **Sử dụng break/continue** một cách hợp lý
4. **Tránh nested loops quá sâu** (> 3 levels)
5. **Đặt tên biến có ý nghĩa** thay vì `i`, `j`

## Kết luận

Control Flow và Loops là nền tảng quan trọng giúp bạn điều khiển luồng thực thi của chương trình. Hiểu rõ và sử dụng thành thạo các cấu trúc này sẽ giúp bạn viết code hiệu quả và dễ đọc hơn.

Bài tiếp theo sẽ về **Functions** - một trong những khái niệm quan trọng nhất trong JavaScript!
