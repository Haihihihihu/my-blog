---
title: "JSE2: Module 3 - Built-In Objects trong JavaScript"
date: 2025-12-11
draft: false
tags: ["JavaScript", "Built-In Objects", "Array", "String"]
categories: ["JavaScript Essentials 2"]
description: "Tìm hiểu về các Built-In Objects quan trọng trong JavaScript"
---

## Giới thiệu

JavaScript cung cấp nhiều built-in objects giúp làm việc với dữ liệu dễ dàng hơn. Trong bài này, chúng ta sẽ tìm hiểu các objects quan trọng nhất.

## String Object

### String Methods

```javascript
let text = "JavaScript là tuyệt vời";

// Length
console.log(text.length); // 23

// toUpperCase / toLowerCase
console.log(text.toUpperCase()); // "JAVASCRIPT LÀ TUYỆT VỜI"
console.log(text.toLowerCase()); // "javascript là tuyệt vời"

// indexOf / lastIndexOf
console.log(text.indexOf("là"));      // 11
console.log(text.indexOf("Python"));  // -1 (không tìm thấy)
console.log(text.lastIndexOf("à"));   // 20

// includes / startsWith / endsWith
console.log(text.includes("Script")); // true
console.log(text.startsWith("Java")); // true
console.log(text.endsWith("vời"));    // true

// slice / substring / substr
console.log(text.slice(0, 10));       // "JavaScript"
console.log(text.substring(0, 10));   // "JavaScript"
console.log(text.slice(-7));          // "tuyệt vời"

// replace / replaceAll
let str = "Tôi học Java. Java rất hay";
console.log(str.replace("Java", "JavaScript"));    // Thay đổi đầu tiên
console.log(str.replaceAll("Java", "JavaScript")); // Thay đổi tất cả

// split
let sentence = "HTML,CSS,JavaScript";
let arr = sentence.split(",");
console.log(arr); // ["HTML", "CSS", "JavaScript"]

// trim / trimStart / trimEnd
let messy = "   hello   ";
console.log(messy.trim());      // "hello"
console.log(messy.trimStart()); // "hello   "
console.log(messy.trimEnd());   // "   hello"

// repeat
console.log("Ha".repeat(3)); // "HaHaHa"

// padStart / padEnd
let num = "5";
console.log(num.padStart(3, "0")); // "005"
console.log(num.padEnd(3, "0"));   // "500"

// charAt / charCodeAt
console.log(text.charAt(0));     // "J"
console.log(text.charCodeAt(0)); // 74 (ASCII code)
```

### Template Literals

```javascript
let name = "Hải";
let age = 22;

// Multiline
let html = `
    <div>
        <h1>${name}</h1>
        <p>Age: ${age}</p>
    </div>
`;

// Expressions
let price = 100;
let tax = 0.1;
console.log(`Total: ${price * (1 + tax)}`); // "Total: 110"

// Tagged templates
function highlight(strings, ...values) {
    return strings.reduce((result, str, i) => {
        return result + str + (values[i] ? `<mark>${values[i]}</mark>` : '');
    }, '');
}

let result = highlight`Name: ${name}, Age: ${age}`;
```

## Array Object

### Basic Array Methods

```javascript
let fruits = ["apple", "banana", "orange"];

// push / pop (cuối array)
fruits.push("grape");     // Thêm vào cuối
console.log(fruits);      // [..., "grape"]
fruits.pop();             // Xóa ở cuối
console.log(fruits);      // ["apple", "banana", "orange"]

// unshift / shift (đầu array)
fruits.unshift("mango");  // Thêm vào đầu
fruits.shift();           // Xóa ở đầu

// splice - Thêm/xóa elements
let arr = [1, 2, 3, 4, 5];
arr.splice(2, 1);         // Xóa 1 element ở index 2
console.log(arr);         // [1, 2, 4, 5]

arr.splice(2, 0, 99, 100); // Thêm 99, 100 ở index 2
console.log(arr);          // [1, 2, 99, 100, 4, 5]

// slice - Trích xuất phần array
let numbers = [1, 2, 3, 4, 5];
let sliced = numbers.slice(1, 4); // Từ index 1 đến 3
console.log(sliced);              // [2, 3, 4]

// concat - Nối arrays
let arr1 = [1, 2];
let arr2 = [3, 4];
let combined = arr1.concat(arr2);
console.log(combined); // [1, 2, 3, 4]

// join - Array thành string
let words = ["Hello", "World"];
console.log(words.join(" ")); // "Hello World"
console.log(words.join("-")); // "Hello-World"

// reverse - Đảo ngược
let nums = [1, 2, 3];
nums.reverse();
console.log(nums); // [3, 2, 1]

// sort - Sắp xếp
let names = ["Charlie", "Alice", "Bob"];
names.sort();
console.log(names); // ["Alice", "Bob", "Charlie"]

// Sắp xếp số
let numbers2 = [10, 5, 40, 25, 1000, 1];
numbers2.sort((a, b) => a - b); // Tăng dần
console.log(numbers2);           // [1, 5, 10, 25, 40, 1000]
```

### Iteration Methods

```javascript
let numbers = [1, 2, 3, 4, 5];

// forEach - Lặp qua elements
numbers.forEach((num, index) => {
    console.log(`Index ${index}: ${num}`);
});

// map - Transform mỗi element
let doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8, 10]

// filter - Lọc elements
let evens = numbers.filter(num => num % 2 === 0);
console.log(evens); // [2, 4]

// find - Tìm element đầu tiên thỏa mãn
let found = numbers.find(num => num > 3);
console.log(found); // 4

// findIndex - Tìm index
let index = numbers.findIndex(num => num > 3);
console.log(index); // 3

// some - Kiểm tra có ít nhất 1 element thỏa mãn
let hasEven = numbers.some(num => num % 2 === 0);
console.log(hasEven); // true

// every - Kiểm tra TẤT CẢ elements thỏa mãn
let allPositive = numbers.every(num => num > 0);
console.log(allPositive); // true

// reduce - Gộp array thành 1 giá trị
let sum = numbers.reduce((total, num) => total + num, 0);
console.log(sum); // 15

// reduceRight - reduce từ phải sang trái
let result = [1, 2, 3].reduceRight((acc, num) => acc + num, 0);
```

### Modern Array Methods

```javascript
// flat - Làm phẳng nested arrays
let nested = [1, [2, 3], [4, [5, 6]]];
console.log(nested.flat());    // [1, 2, 3, 4, [5, 6]]
console.log(nested.flat(2));   // [1, 2, 3, 4, 5, 6]

// flatMap - map + flat
let arr = [1, 2, 3];
let result = arr.flatMap(x => [x, x * 2]);
console.log(result); // [1, 2, 2, 4, 3, 6]

// includes
console.log([1, 2, 3].includes(2)); // true

// Array.from - Tạo array
let str = "Hello";
let chars = Array.from(str);
console.log(chars); // ["H", "e", "l", "l", "o"]

// Array.of
let arr = Array.of(1, 2, 3);
console.log(arr); // [1, 2, 3]
```

## Math Object

```javascript
// Constants
console.log(Math.PI);     // 3.141592653589793
console.log(Math.E);      // 2.718281828459045

// Rounding
console.log(Math.round(4.7));  // 5
console.log(Math.round(4.4));  // 4
console.log(Math.ceil(4.1));   // 5 (làm tròn lên)
console.log(Math.floor(4.9));  // 4 (làm tròn xuống)
console.log(Math.trunc(4.9));  // 4 (bỏ phần thập phân)

// Min / Max
console.log(Math.min(5, 10, 2, 8));  // 2
console.log(Math.max(5, 10, 2, 8));  // 10

// Power / Square root
console.log(Math.pow(2, 3));  // 8 (2^3)
console.log(2 ** 3);          // 8 (ES7 operator)
console.log(Math.sqrt(16));   // 4
console.log(Math.cbrt(27));   // 3 (căn bậc 3)

// Absolute value
console.log(Math.abs(-5));    // 5

// Random
console.log(Math.random());   // 0 đến 1 (không bao gồm 1)

// Random integer trong range
function randomInt(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}
console.log(randomInt(1, 10)); // Số từ 1 đến 10

// Trigonometry
console.log(Math.sin(Math.PI / 2));  // 1
console.log(Math.cos(0));            // 1
console.log(Math.tan(Math.PI / 4));  // 1
```

## Date Object

```javascript
// Tạo Date
let now = new Date();
console.log(now);

let specific = new Date(2024, 0, 1); // Jan 1, 2024 (month 0-indexed!)
let fromString = new Date("2024-12-25");
let fromTimestamp = new Date(1609459200000);

// Get components
console.log(now.getFullYear());   // 2025
console.log(now.getMonth());      // 0-11 (Jan = 0)
console.log(now.getDate());       // 1-31
console.log(now.getDay());        // 0-6 (Sun = 0)
console.log(now.getHours());      // 0-23
console.log(now.getMinutes());    // 0-59
console.log(now.getSeconds());    // 0-59
console.log(now.getMilliseconds()); // 0-999

// Set components
let date = new Date();
date.setFullYear(2025);
date.setMonth(11);      // December
date.setDate(25);

// Format
console.log(now.toDateString());      // "Thu Jan 19 2025"
console.log(now.toTimeString());      // "14:30:45 GMT+0700"
console.log(now.toLocaleDateString()); // "1/19/2025" (locale-dependent)
console.log(now.toISOString());       // "2025-01-19T07:30:45.123Z"

// Timestamp
console.log(now.getTime());        // Milliseconds since Jan 1, 1970
console.log(Date.now());           // Current timestamp

// Calculate time difference
let start = new Date("2024-01-01");
let end = new Date("2024-12-31");
let diff = end - start; // Milliseconds
let days = diff / (1000 * 60 * 60 * 24);
console.log(`${days} days`);
```

## JSON Object

```javascript
// Object to JSON
let person = {
    name: "Hải",
    age: 22,
    skills: ["JavaScript", "Python", "Linux"]
};

let json = JSON.stringify(person);
console.log(json);
// '{"name":"Hải","age":22,"skills":["JavaScript","Python","Linux"]}'

// Pretty print
let prettyJson = JSON.stringify(person, null, 2);
console.log(prettyJson);

// JSON to Object
let jsonString = '{"name":"Hải","age":22}';
let obj = JSON.parse(jsonString);
console.log(obj.name); // "Hải"

// Error handling
try {
    let invalid = JSON.parse("invalid json");
} catch (error) {
    console.error("Parse error:", error.message);
}
```

## RegExp Object

```javascript
// Tạo RegExp
let pattern1 = /abc/;
let pattern2 = new RegExp("abc");

// test - Kiểm tra match
let emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
console.log(emailPattern.test("hai@example.com")); // true
console.log(emailPattern.test("invalid-email"));   // false

// match - Tìm matches
let text = "Số điện thoại: 0123456789, 0987654321";
let phonePattern = /\d{10}/g;
let phones = text.match(phonePattern);
console.log(phones); // ["0123456789", "0987654321"]

// replace với RegExp
let str = "Hello World! Hello Everyone!";
let newStr = str.replace(/Hello/g, "Hi");
console.log(newStr); // "Hi World! Hi Everyone!"

// Capturing groups
let datePattern = /(\d{2})\/(\d{2})\/(\d{4})/;
let match = "25/12/2024".match(datePattern);
console.log(match[1]); // "25" (day)
console.log(match[2]); // "12" (month)
console.log(match[3]); // "2024" (year)
```

## Set Object (ES6)

```javascript
// Tạo Set - unique values only
let set = new Set([1, 2, 3, 3, 4, 4, 5]);
console.log(set); // Set(5) {1, 2, 3, 4, 5}

// Methods
set.add(6);
set.delete(1);
console.log(set.has(2));  // true
console.log(set.size);    // 5

// Iterate
for (let value of set) {
    console.log(value);
}

// Convert to array
let arr = [...set];
let arr2 = Array.from(set);

// Remove duplicates from array
let numbers = [1, 2, 2, 3, 3, 4, 5, 5];
let unique = [...new Set(numbers)];
console.log(unique); // [1, 2, 3, 4, 5]
```

## Map Object (ES6)

```javascript
// Tạo Map - key-value pairs
let map = new Map();

// set / get / has / delete
map.set("name", "Hải");
map.set("age", 22);
map.set(1, "one");

console.log(map.get("name")); // "Hải"
console.log(map.has("age"));  // true
console.log(map.size);        // 3

map.delete("age");

// Iterate
for (let [key, value] of map) {
    console.log(`${key}: ${value}`);
}

// Object to Map
let obj = { a: 1, b: 2 };
let mapFromObj = new Map(Object.entries(obj));

// Map to Object
let objFromMap = Object.fromEntries(map);
```

## Best Practices

1. **Chọn đúng data structure**: Array vs Set, Object vs Map
2. **Sử dụng built-in methods** thay vì tự implement
3. **Chain array methods** cho code clean hơn
4. **Immutable operations** với map, filter thay vì mutate
5. **Validate RegExp patterns** carefully
6. **Handle JSON parse errors** với try...catch

## Kết luận

Built-in objects là công cụ mạnh mẽ giúp bạn làm việc với dữ liệu hiệu quả. Hiểu rõ String, Array, Math, Date, JSON, RegExp, Set, và Map sẽ giúp bạn giải quyết hầu hết các tác vụ thường gặp trong JavaScript.

Bài cuối cùng: **Advanced Function Usage**!
