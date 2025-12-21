---
title: "JSE2: Module 1 - Classless Objects trong JavaScript"
date: 2025-12-13
draft: false
tags: ["JavaScript", "Objects", "OOP"]
categories: ["JavaScript Essentials 2"]
description: "Tìm hiểu về Objects trong JavaScript không cần Classes"
---

## Giới thiệu

JavaScript là ngôn ngữ hướng đối tượng dựa trên prototype (prototype-based), khác với các ngôn ngữ OOP truyền thống như Java hay C++. Trong bài này, chúng ta sẽ học cách làm việc với objects mà không cần classes.

## Object Basics

### Tạo Objects

```javascript
// Object literal - cách đơn giản nhất
let person = {
    name: "Hải",
    age: 22,
    major: "An ninh mạng"
};

// Object constructor
let car = new Object();
car.brand = "Toyota";
car.model = "Camry";
car.year = 2024;

// Object.create()
let animal = {
    eat: function() {
        console.log("Eating...");
    }
};
let dog = Object.create(animal);
dog.bark = function() {
    console.log("Woof!");
};
```

### Truy cập Properties

```javascript
let student = {
    name: "Hải",
    age: 22,
    "favorite subject": "JavaScript"
};

// Dot notation
console.log(student.name); // "Hải"

// Bracket notation
console.log(student["age"]); // 22
console.log(student["favorite subject"]); // Bắt buộc dùng bracket

// Dynamic property access
let prop = "age";
console.log(student[prop]); // 22
```

### Thêm/Sửa/Xóa Properties

```javascript
let user = {
    name: "Hải"
};

// Thêm property
user.age = 22;
user["email"] = "hai@example.com";

// Sửa property
user.age = 23;

// Xóa property
delete user.email;

console.log(user); // { name: "Hải", age: 23 }
```

## Object Methods

```javascript
let calculator = {
    a: 0,
    b: 0,
    
    // Method
    setValues: function(x, y) {
        this.a = x;
        this.b = y;
    },
    
    // Shorthand method (ES6)
    add() {
        return this.a + this.b;
    },
    
    multiply() {
        return this.a * this.b;
    }
};

calculator.setValues(5, 3);
console.log(calculator.add());      // 8
console.log(calculator.multiply()); // 15
```

## The `this` Keyword

```javascript
let person = {
    name: "Hải",
    age: 22,
    
    greet: function() {
        console.log(`Xin chào, tôi là ${this.name}`);
    },
    
    birthday: function() {
        this.age++;
        console.log(`Bây giờ tôi ${this.age} tuổi`);
    }
};

person.greet();    // "Xin chào, tôi là Hải"
person.birthday(); // "Bây giờ tôi 23 tuổi"

// this trong arrow function - KHÔNG bind!
let obj = {
    name: "Test",
    
    // Regular function - this bind to obj
    regular: function() {
        console.log(this.name); // "Test"
    },
    
    // Arrow function - this bind to outer scope
    arrow: () => {
        console.log(this.name); // undefined (hoặc global)
    }
};
```

## Constructor Functions

```javascript
// Constructor function (convention: PascalCase)
function Person(name, age, major) {
    this.name = name;
    this.age = age;
    this.major = major;
    
    this.introduce = function() {
        return `Tôi là ${this.name}, ${this.age} tuổi`;
    };
}

// Tạo instance với 'new'
let student1 = new Person("Hải", 22, "An ninh mạng");
let student2 = new Person("Nam", 23, "KHMT");

console.log(student1.introduce()); // "Tôi là Hải, 22 tuổi"
console.log(student2.introduce()); // "Tôi là Nam, 23 tuổi"

// Kiểm tra instance
console.log(student1 instanceof Person); // true
```

## Prototypes

### Prototype Chain

```javascript
function Animal(name) {
    this.name = name;
}

// Thêm method vào prototype (memory efficient)
Animal.prototype.eat = function() {
    console.log(`${this.name} đang ăn`);
};

Animal.prototype.sleep = function() {
    console.log(`${this.name} đang ngủ`);
};

let dog = new Animal("Chó");
let cat = new Animal("Mèo");

dog.eat();  // "Chó đang ăn"
cat.sleep(); // "Mèo đang ngủ"

// Tất cả instances share cùng prototype methods
console.log(dog.eat === cat.eat); // true
```

### Prototype Inheritance

```javascript
// Parent constructor
function Animal(name) {
    this.name = name;
}

Animal.prototype.eat = function() {
    console.log(`${this.name} đang ăn`);
};

// Child constructor
function Dog(name, breed) {
    Animal.call(this, name); // Call parent constructor
    this.breed = breed;
}

// Inherit from Animal
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

// Add Dog-specific methods
Dog.prototype.bark = function() {
    console.log("Woof woof!");
};

let myDog = new Dog("Buddy", "Golden Retriever");
myDog.eat();  // "Buddy đang ăn" (inherited)
myDog.bark(); // "Woof woof!" (own method)
```

## Object Methods (Built-in)

### Object.keys(), values(), entries()

```javascript
let student = {
    name: "Hải",
    age: 22,
    major: "An ninh mạng"
};

// Get all keys
let keys = Object.keys(student);
console.log(keys); // ["name", "age", "major"]

// Get all values
let values = Object.values(student);
console.log(values); // ["Hải", 22, "An ninh mạng"]

// Get entries (key-value pairs)
let entries = Object.entries(student);
console.log(entries);
// [["name", "Hải"], ["age", 22], ["major", "An ninh mạng"]]

// Iterate
for (let [key, value] of Object.entries(student)) {
    console.log(`${key}: ${value}`);
}
```

### Object.assign()

```javascript
// Copy object
let original = { a: 1, b: 2 };
let copy = Object.assign({}, original);

// Merge objects
let obj1 = { a: 1, b: 2 };
let obj2 = { c: 3, d: 4 };
let merged = Object.assign({}, obj1, obj2);
console.log(merged); // { a: 1, b: 2, c: 3, d: 4 }

// Add properties
let person = { name: "Hải" };
Object.assign(person, { age: 22, major: "An ninh mạng" });
```

### Object.freeze() và seal()

```javascript
let obj = { name: "Hải" };

// freeze - không thể thay đổi gì
Object.freeze(obj);
obj.name = "Nam";     // Không có effect
obj.age = 22;         // Không thể thêm
delete obj.name;      // Không thể xóa
console.log(obj);     // { name: "Hải" }

// seal - có thể sửa, không thể thêm/xóa
let obj2 = { name: "Hải" };
Object.seal(obj2);
obj2.name = "Nam";    // OK
obj2.age = 22;        // Không thể thêm
delete obj2.name;     // Không thể xóa
```

## Computed Property Names (ES6)

```javascript
let propName = "age";

let person = {
    name: "Hải",
    [propName]: 22,                    // Computed property
    ["favorite" + "Color"]: "blue"     // Expression
};

console.log(person); // { name: "Hải", age: 22, favoriteColor: "blue" }
```

## Property Shorthand (ES6)

```javascript
let name = "Hải";
let age = 22;

// Old way
let person1 = {
    name: name,
    age: age
};

// Shorthand
let person2 = {
    name,
    age
};

console.log(person2); // { name: "Hải", age: 22 }
```

## Object Destructuring (ES6)

```javascript
let student = {
    name: "Hải",
    age: 22,
    major: "An ninh mạng"
};

// Destructuring
let { name, age, major } = student;
console.log(name); // "Hải"

// Rename variables
let { name: studentName, age: studentAge } = student;

// Default values
let { name, gpa = 3.5 } = student;

// Nested destructuring
let user = {
    info: {
        name: "Hải",
        age: 22
    }
};

let { info: { name, age } } = user;
```

## Real-World Examples

### User Management

```javascript
function createUser(name, email) {
    return {
        name,
        email,
        createdAt: new Date(),
        
        updateEmail(newEmail) {
            this.email = newEmail;
        },
        
        getInfo() {
            return `${this.name} (${this.email})`;
        }
    };
}

let user = createUser("Hải", "hai@example.com");
console.log(user.getInfo());
user.updateEmail("newemail@example.com");
```

### Shopping Cart

```javascript
let cart = {
    items: [],
    
    addItem(product, quantity = 1) {
        this.items.push({ product, quantity });
    },
    
    removeItem(productName) {
        this.items = this.items.filter(
            item => item.product.name !== productName
        );
    },
    
    getTotal() {
        return this.items.reduce((sum, item) => {
            return sum + (item.product.price * item.quantity);
        }, 0);
    }
};

cart.addItem({ name: "Laptop", price: 1000 }, 1);
cart.addItem({ name: "Mouse", price: 50 }, 2);
console.log(cart.getTotal()); // 1100
```

## Best Practices

1. **Dùng object literals** cho simple objects
2. **Dùng constructor functions/classes** cho objects cần tạo nhiều instances
3. **Add methods to prototype** thay vì trong constructor (memory efficient)
4. **Use `this` carefully**, especially với arrow functions
5. **Destructure objects** để code cleaner
6. **Validate object properties** trước khi sử dụng

## Kết luận

Objects là core của JavaScript. Hiểu rõ cách làm việc với objects, prototypes, và `this` keyword là nền tảng quan trọng để học OOP trong JavaScript.

Bài tiếp theo: **Classes và Class-Based Approach**!
