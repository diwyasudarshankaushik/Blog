---
title: "Understanding the this Keyword in JavaScript"
seoTitle: "Understanding the this Keyword in JavaScript"
datePublished: 2026-03-26T17:06:44.558Z
cuid: cmn7q5qdp022j2dmmdbh59wiq
slug: understanding-the-this-keyword-in-javascript
cover: https://cdn.hashnode.com/uploads/covers/696e62d612291978e735e98b/8c5b8461-abf5-4c73-878e-4aba1a3fa41a.png
ogImage: https://cdn.hashnode.com/uploads/og-images/696e62d612291978e735e98b/600f041f-4fde-4a98-8dae-c5ede6a5d1b9.png
tags: javascript, this-keyword, chaiaurcode, chaicode, this-call-bind-apply

---

## **1\. What** `this` **Represents**

In plain English, `this` refers to an **object**. Which object? The one that is currently executing the function. It allows you to reuse functions across different objects, making your code more dynamic.  
It does **NOT** depend on *where the function is written*  
It depends on *how the function is called*

## **2\.** `this` **in the Global Context**

When you use `this` outside of any function or object (in the global scope), it refers to the global object.

*   **In a Browser:** `this` refers to the `window` object.
    
*   **In Node.js:** `this` refers to the `global` object.
    

```javascript
console.log(this); // window ,In a browser, this logs the Window object
console.log(this); // {}     ,In a Node.js, this logs the object
```

![](https://cdn.hashnode.com/uploads/covers/696e62d612291978e735e98b/e9a49b37-802a-498f-8e0f-9513c8fb5a22.png align="center")

## **3\.** `this` Inside Objects (Method Context)

When a function is defined as a property of an object, we call it a **method**. When you call that method, `this` refers to the object itself. This is the most common and intuitive use of `this`.

```javascript
const user = {
  name: "Chai",
  greet: function() {
    console.log(`Hello, my name is ${this.name}`);
  }
};

user.greet(); // Output: "Hello, my name is Chai"
// Here, 'user' is the caller, so 'this' = user.
```

## **4\.** `this` **Inside Functions**

The behavior changes depending on how the function is invoked:

*   **Simple Function Call:** If you call a standalone function, `this` defaults to the global object (`window`).
    
*   **Strict Mode:** If `'use strict';` is enabled, `this` will be `undefined` in a regular function call to prevent accidental global changes.
    

```javascript
function show() {
  console.log(this);
}

show(); 
//  In non-strict mode → window
//  In strict mode → undefined
```

## **5\. How Calling Context Changes** `this`

The most important takeaway is that `this` is **dynamic**. The same function can have a different `this` depending on who "touches" it.

Consider this example where a function is shared:

```javascript
function identify() {
  console.log(this.name);
}

const person1 = { name: "Alice", identify: identify };
const person2 = { name: "Bob", identify: identify };

person1.identify(); // "Alice" (person1 is the caller)
person2.identify(); // "Bob"   (person2 is the caller)
```

## Summary Table: Different Contexts of `this`

<table style="min-width: 50px;"><colgroup><col style="min-width: 25px;"><col style="min-width: 25px;"></colgroup><tbody><tr><td colspan="1" rowspan="1"><p><strong>Context</strong></p></td><td colspan="1" rowspan="1"><p><strong>What this refers to</strong></p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>Global Scope</strong></p></td><td colspan="1" rowspan="1"><p>Global Object (<code>window</code> or <code>global</code>)</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>Object Method</strong></p></td><td colspan="1" rowspan="1"><p>The Object before the dot (the caller)</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>Simple Function</strong></p></td><td colspan="1" rowspan="1"><p>Global Object (or <code>undefined</code> in strict mode)</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>Arrow Functions</strong></p></td><td colspan="1" rowspan="1"><p>The <code>this</code> of the surrounding code (lexical)</p></td></tr></tbody></table>