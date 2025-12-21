---
title: "JSE2: Module 2 - Classes và Class-Based Approach"
date: 2025-12-12
draft: false
tags: ["JavaScript", "Classes", "OOP", "ES6"]
categories: ["JavaScript Essentials 2"]
description: "Tìm hiểu về Classes trong JavaScript ES6 và lập trình hướng đối tượng"
---

## Giới thiệu

ES6 (ECMAScript 2015) đã giới thiệu cú pháp `class` để làm việc với OOP dễ dàng hơn. Mặc dù bên dưới vẫn sử dụng prototypes, nhưng cú pháp class làm code dễ đọc và gần giống các ngôn ngữ OOP khác.

## Class Declaration

### Cú pháp cơ bản

```javascript
class Person {
    // Constructor - được gọi khi tạo instance mới
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    
    // Method
    introduce() {
        console.log(`Tôi là ${this.name}, ${this.age} tuổi`);
    }
    
    // Method khác
    birthday() {
        this.age++;
        console.log(`Happy birthday! Bây giờ ${this.age} tuổi`);
    }
}

// Tạo instance
let person1 = new Person("Hải", 22);
let person2 = new Person("Nam", 23);

person1.introduce(); // "Tôi là Hải, 22 tuổi"
person2.birthday();  // "Happy birthday! Bây giờ 24 tuổi"
```

### Class Expression

```javascript
// Named class expression
const Person = class PersonClass {
    constructor(name) {
        this.name = name;
    }
    
    greet() {
        console.log(`Hi, I'm ${this.name}`);
    }
};

// Anonymous class expression
const Animal = class {
    constructor(name) {
        this.name = name;
    }
};
```

## Constructor

```javascript
class Student {
    constructor(name, age, major) {
        // Initialize properties
        this.name = name;
        this.age = age;
        this.major = major;
        this.gpa = 0;
        
        // Có thể gọi methods
        this.enrolledCourses = [];
        this.generateStudentId();
    }
    
    generateStudentId() {
        this.studentId = Math.floor(Math.random() * 100000);
    }
    
    getInfo() {
        return `${this.name} - ${this.studentId}`;
    }
}

let student = new Student("Hải", 22, "An ninh mạng");
console.log(student.getInfo());
```

## Class Methods

### Instance Methods

```javascript
class Calculator {
    constructor() {
        this.result = 0;
    }
    
    add(num) {
        this.result += num;
        return this; // Return this để method chaining
    }
    
    subtract(num) {
        this.result -= num;
        return this;
    }
    
    multiply(num) {
        this.result *= num;
        return this;
    }
    
    getResult() {
        return this.result;
    }
}

// Method chaining
let calc = new Calculator();
let result = calc.add(10).multiply(2).subtract(5).getResult();
console.log(result); // 15
```

### Static Methods

Static methods thuộc về class, không thuộc về instance.

```javascript
class MathUtils {
    // Static method
    static add(a, b) {
        return a + b;
    }
    
    static multiply(a, b) {
        return a * b;
    }
    
    static PI = 3.14159; // Static property
}

// Gọi static method từ class
console.log(MathUtils.add(5, 3));      // 8
console.log(MathUtils.multiply(4, 5)); // 20
console.log(MathUtils.PI);             // 3.14159

// KHÔNG thể gọi từ instance
let utils = new MathUtils();
// utils.add(1, 2); // Error!
```

### Getter và Setter

```javascript
class Rectangle {
    constructor(width, height) {
        this._width = width;   // Convention: _ for private
        this._height = height;
    }
    
    // Getter
    get width() {
        return this._width;
    }
    
    get height() {
        return this._height;
    }
    
    get area() {
        return this._width * this._height;
    }
    
    // Setter
    set width(value) {
        if (value <= 0) {
            throw new Error("Width phải > 0");
        }
        this._width = value;
    }
    
    set height(value) {
        if (value <= 0) {
            throw new Error("Height phải > 0");
        }
        this._height = value;
    }
}

let rect = new Rectangle(10, 5);
console.log(rect.area);  // 50 - gọi getter như property

rect.width = 20;         // Gọi setter
console.log(rect.area);  // 100

// rect.width = -5;      // Error: Width phải > 0
```

## Inheritance (Kế thừa)

### extends Keyword

```javascript
// Parent class
class Animal {
    constructor(name) {
        this.name = name;
    }
    
    eat() {
        console.log(`${this.name} đang ăn`);
    }
    
    sleep() {
        console.log(`${this.name} đang ngủ`);
    }
}

// Child class
class Dog extends Animal {
    constructor(name, breed) {
        super(name); // Gọi parent constructor
        this.breed = breed;
    }
    
    bark() {
        console.log("Woof woof!");
    }
    
    // Override parent method
    eat() {
        super.eat(); // Gọi parent method
        console.log(`${this.name} đang gặm xương`);
    }
}

let myDog = new Dog("Buddy", "Golden Retriever");
myDog.eat();   // Inherited + overridden
myDog.sleep(); // Inherited
myDog.bark();  // Own method
```

### super Keyword

```javascript
class Vehicle {
    constructor(brand, model) {
        this.brand = brand;
        this.model = model;
    }
    
    getInfo() {
        return `${this.brand} ${this.model}`;
    }
}

class Car extends Vehicle {
    constructor(brand, model, doors) {
        super(brand, model); // Gọi parent constructor
        this.doors = doors;
    }
    
    getInfo() {
        // Gọi parent method và extend
        return `${super.getInfo()} (${this.doors} cửa)`;
    }
}

let myCar = new Car("Toyota", "Camry", 4);
console.log(myCar.getInfo()); // "Toyota Camry (4 cửa)"
```

## Private Fields (ES2022)

```javascript
class BankAccount {
    #balance = 0; // Private field (bắt đầu với #)
    
    constructor(owner, initialBalance) {
        this.owner = owner;
        this.#balance = initialBalance;
    }
    
    // Private method
    #validateAmount(amount) {
        return amount > 0 && amount <= 10000;
    }
    
    deposit(amount) {
        if (this.#validateAmount(amount)) {
            this.#balance += amount;
            return true;
        }
        return false;
    }
    
    withdraw(amount) {
        if (this.#validateAmount(amount) && amount <= this.#balance) {
            this.#balance -= amount;
            return true;
        }
        return false;
    }
    
    getBalance() {
        return this.#balance;
    }
}

let account = new BankAccount("Hải", 1000);
account.deposit(500);
console.log(account.getBalance()); // 1500

// console.log(account.#balance); // Error! Private field
```

## Class Composition

Thay vì inheritance sâu, composition thường tốt hơn.

```javascript
// Mixin pattern
const CanEat = {
    eat() {
        console.log(`${this.name} đang ăn`);
    }
};

const CanSwim = {
    swim() {
        console.log(`${this.name} đang bơi`);
    }
};

const CanFly = {
    fly() {
        console.log(`${this.name} đang bay`);
    }
};

class Duck {
    constructor(name) {
        this.name = name;
        // Compose behaviors
        Object.assign(this, CanEat, CanSwim, CanFly);
    }
}

let duck = new Duck("Donald");
duck.eat();  // "Donald đang ăn"
duck.swim(); // "Donald đang bơi"
duck.fly();  // "Donald đang bay"
```

## instanceof Operator

```javascript
class Animal {}
class Dog extends Animal {}
class Cat extends Animal {}

let myDog = new Dog();
let myCat = new Cat();

console.log(myDog instanceof Dog);    // true
console.log(myDog instanceof Animal); // true
console.log(myDog instanceof Cat);    // false

console.log(myCat instanceof Cat);    // true
console.log(myCat instanceof Animal); // true
console.log(myCat instanceof Dog);    // false
```

## Real-World Examples

### User Management System

```javascript
class User {
    #password; // Private
    
    constructor(username, email, password) {
        this.username = username;
        this.email = email;
        this.#password = this.#hashPassword(password);
        this.createdAt = new Date();
    }
    
    #hashPassword(password) {
        // Simplified hash
        return `hashed_${password}`;
    }
    
    verifyPassword(password) {
        return this.#hashPassword(password) === this.#password;
    }
    
    getInfo() {
        return {
            username: this.username,
            email: this.email,
            createdAt: this.createdAt
        };
    }
}

class Admin extends User {
    constructor(username, email, password) {
        super(username, email, password);
        this.role = "admin";
        this.permissions = ["read", "write", "delete"];
    }
    
    hasPermission(perm) {
        return this.permissions.includes(perm);
    }
}

let admin = new Admin("admin", "admin@example.com", "secret123");
console.log(admin.hasPermission("delete")); // true
console.log(admin.verifyPassword("secret123")); // true
```

### Todo List Application

```javascript
class Todo {
    static #idCounter = 0; // Static private field
    
    constructor(title, description) {
        this.id = ++Todo.#idCounter;
        this.title = title;
        this.description = description;
        this.completed = false;
        this.createdAt = new Date();
    }
    
    complete() {
        this.completed = true;
        this.completedAt = new Date();
    }
    
    uncomplete() {
        this.completed = false;
        delete this.completedAt;
    }
}

class TodoList {
    constructor(name) {
        this.name = name;
        this.todos = [];
    }
    
    addTodo(title, description) {
        const todo = new Todo(title, description);
        this.todos.push(todo);
        return todo;
    }
    
    removeTodo(id) {
        this.todos = this.todos.filter(todo => todo.id !== id);
    }
    
    getTodo(id) {
        return this.todos.find(todo => todo.id === id);
    }
    
    getCompleted() {
        return this.todos.filter(todo => todo.completed);
    }
    
    getPending() {
        return this.todos.filter(todo => !todo.completed);
    }
}

let myList = new TodoList("Work Tasks");
myList.addTodo("Học JavaScript", "Hoàn thành JSE2");
myList.addTodo("Làm project", "Build blog với Hugo");

let todo = myList.getTodo(1);
todo.complete();

console.log(myList.getCompleted().length); // 1
console.log(myList.getPending().length);   // 1
```

## Best Practices

1. **Dùng PascalCase** cho tên class: `MyClass`, không `myClass`
2. **Một class một trách nhiệm** (Single Responsibility)
3. **Favor composition over inheritance** - không kế thừa quá sâu
4. **Sử dụng private fields** (#) cho internal state
5. **Validate trong constructor và setters**
6. **Document với JSDoc** cho public methods
7. **Return `this`** trong methods để method chaining

```javascript
/**
 * Represents a user account
 */
class Account {
    /**
     * @param {string} username - The username
     * @param {string} email - User's email
     */
    constructor(username, email) {
        this.username = username;
        this.email = email;
    }
}
```

## Kết luận

Classes trong ES6+ làm cho OOP trong JavaScript dễ dàng và trực quan hơn. Hiểu rõ về classes, inheritance, encapsulation (private fields), và composition sẽ giúp bạn xây dựng các ứng dụng có cấu trúc tốt.

Bài tiếp theo: **Built-In Objects trong JavaScript**!
