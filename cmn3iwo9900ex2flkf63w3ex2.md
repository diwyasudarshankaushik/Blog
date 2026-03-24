---
title: "The new Keyword in JavaScript"
seoTitle: "The new Keyword and Constructor Functions in JavaScript"
seoDescription: "Understand the 4-step process behind the new keyword, how prototype linking works, and how to use constructor functions effectively in JS."
datePublished: 2026-03-23T18:32:39.887Z
cuid: cmn3iwo9900ex2flkf63w3ex2
slug: the-new-keyword-in-javascript
cover: https://cdn.hashnode.com/uploads/covers/696e62d612291978e735e98b/a6f742c7-317b-4853-8659-3fdf0293fe8d.png
ogImage: https://cdn.hashnode.com/uploads/og-images/696e62d612291978e735e98b/bfb753ca-a78f-45b8-8a32-5d1ec2c85e07.png
tags: javascript, constructor-functions, chaicode

---

## **1\. What the** `new` **Keyword Actually Does**

In JavaScript, the `new` keyword is used to create an **instance** of a user-defined object type or one of the built-in object types that has a constructor function.

Think of it as a factory command. Without `new`, a constructor is just a regular function. With `new`, it becomes a blueprint for building objects.

👉 It automates multiple steps:

*   Creates a new empty object
    
*   Links it to a prototype
    
*   Calls the constructor function
    
*   Returns the object
    

## **2\. Constructor Functions: The Blueprint**

A constructor function is a regular function, but by convention, we capitalize the first letter (PascalCase) to signal that it should be called with `new`.

```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
}

const user1 = new Person("Diwya", 25);
```

## **3.Object Creation Process (Step-by-Step)**

When you put `new` before a function call, four hidden steps occur behind the scenes:

*   **A Brand New Object is Created:** An empty object `{}` is born.
    
*   **Prototype Linking:** This new object’s internal `[[Prototype]]` (known as `__proto__`) is linked to the constructor function's `.prototype` property.
    
*   **The** `this` **Binding:** The execution context of the function is bound to the new object. Any reference to `this` inside the function now points to our new empty object.
    
*   **The Automatic Return:** The function automatically returns the new object (unless you manually return a different object).
    

```javascript
let obj = {};                  // 1. Create empty object
obj.proto = Person.prototype;  // 2. Link prototype
Person.call(obj, "Diwya", 25); // 3. Call constructor with this
return obj;                    // 4. Return the object
```

## **4\. How** `new` **Links Prototypes**

This is the "secret sauce" of JavaScript inheritance. Every function in JS has a property called `.prototype`.

```javascript
Person.prototype.greet = function () {
  console.log("Hello " + this.name);
};
```

When you create `user1` using `new Person()`, JavaScript ensures that `user1` has access to all methods defined on `Person.prototype`. This keeps your code memory-efficient because the methods aren't copied to every single instance; they are shared via the prototype chain.

```javascript
const user = new Person("Diwya", 25);
user.greet(); // Hello Diwya
```

## **5\. Instances Created from Constructors**

The objects created are called **instances**. You can verify the relationship between an instance and its constructor using the `instanceof` operator.

```javascript
console.log(user1 instanceof Person); // true
```

Each instance:

*   Has its own properties (`name`, `age`)
    
*   Shares prototype methods (`greet`)
    

```typescript
const user1 = new Person("Diwya", 25);
const user2 = new Person("Amit", 30);
```

### **Relationship: Constructor ↔ Object**

```plaintext
Person (Constructor)
     ↓
Person.prototype
     ↓
user (Instance)
```

👉 Key idea:

*   Constructor → creates object
    
*   Prototype → shares methods
    

## Simple Example

```javascript
function Car(brand) {
  this.brand = brand;
}

Car.prototype.show = function () {    // show is method 
  console.log(this.brand);
};

const car1 = new Car("BMW");
car1.show(); // BMW
```

## Comparison: Function vs. Constructor

<table style="min-width: 75px;"><colgroup><col style="min-width: 25px;"><col style="min-width: 25px;"><col style="min-width: 25px;"></colgroup><tbody><tr><td colspan="1" rowspan="1"><p><strong>Feature</strong></p></td><td colspan="1" rowspan="1"><p><strong>Regular Function</strong></p></td><td colspan="1" rowspan="1"><p><strong>Constructor (with new)</strong></p></td></tr><tr><td colspan="1" rowspan="1"><p><code>this</code><strong> value</strong></p></td><td colspan="1" rowspan="1"><p>Global object / undefined</p></td><td colspan="1" rowspan="1"><p>The new instance <code>{}</code></p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>Return Value</strong></p></td><td colspan="1" rowspan="1"><p>Whatever you <code>return</code></p></td><td colspan="1" rowspan="1"><p>The new object (implicit)</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>Purpose</strong></p></td><td colspan="1" rowspan="1"><p>Perform a task</p></td><td colspan="1" rowspan="1"><p>Build an object</p></td></tr></tbody></table>