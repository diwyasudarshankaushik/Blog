---
title: "Spread vs Rest Operators in JavaScript"
seoTitle: "Spread vs Rest Operators in JavaScript"
seoDescription: "Master the three-dot syntax (...) in JavaScript. Learn the key differences between Spread and Rest operators with clear examples and real-world use ca"
datePublished: 2026-03-25T16:21:40.989Z
cuid: cmn693xmj00822dmmg8m39s9w
slug: spread-vs-rest-operators-in-javascript
cover: https://cdn.hashnode.com/uploads/covers/696e62d612291978e735e98b/4d3cc46a-d984-4de4-bf10-4c7f4610dcd7.png
ogImage: https://cdn.hashnode.com/uploads/og-images/696e62d612291978e735e98b/03edc862-66be-40dc-9c54-669a861bb0b8.png
tags: javascript, frontend, learntocode, devcommunity, programming-tips, learn-javascript, chaicode, chaicohort

---

## **1\. What is the Spread Operator (**`...`**)?**

The **Spread operator** "expands" or "unpacks" an iterable (like an array or object) into individual elements.

### Using Spread with Arrays and Objects

**Arrays:** It’s great for copying or merging arrays without mutating the original.

```javascript
const parts = ['shoulders', 'knees'];
const body = ['head', ...parts, 'toes']; 
// Result: ['head', 'shoulders', 'knees', 'toes']
```

**Objects:** It allows you to shallow-clone objects or update specific properties easily.

```javascript
const user = { name: 'Diwya', role: 'Dev' };
const updatedUser = { ...user, role: 'Senior Dev' }; 
// Result: { name: 'Diwya', role: 'Senior Dev' }
```

## **2\. The Rest Operator (**`...`**)**

The **Rest operator** does the exact opposite: it "collects" multiple individual elements and bunches them into a single array. It is most commonly used in function parameters.

### **Function Arguments**

If you don't know how many arguments a user will pass, "rest" handles it gracefully.

```javascript
function sum(...numbers) {
  return numbers.reduce((acc, curr) => acc + curr, 0);
}
console.log(sum(1, 2, 3, 4)); // Result: 10
```

### **Destructuring**

Pulling one property out of an object and keeping "the rest" together.

```javascript
const [first, ...rest] = [10, 20, 30, 40];

console.log(first); // 10
console.log(rest);  // [20, 30, 40]
```

## **3\. Key Differences: Spread vs. Rest**

<table style="min-width: 75px;"><colgroup><col style="min-width: 25px;"><col style="min-width: 25px;"><col style="min-width: 25px;"></colgroup><tbody><tr><td colspan="1" rowspan="1"><p><strong>Feature</strong></p></td><td colspan="1" rowspan="1"><p><strong>Spread Operator</strong></p></td><td colspan="1" rowspan="1"><p><strong>Rest Operator</strong></p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>Action</strong></p></td><td colspan="1" rowspan="1"><p><strong>Expands</strong> (unpacks) elements.</p></td><td colspan="1" rowspan="1"><p><strong>Collects</strong> (packs) elements.</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>Location</strong></p></td><td colspan="1" rowspan="1"><p>Used in array literals, object literals, or function calls.</p></td><td colspan="1" rowspan="1"><p>Used in function parameters or destructuring patterns.</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>Goal</strong></p></td><td colspan="1" rowspan="1"><p>To distribute values.</p></td><td colspan="1" rowspan="1"><p>To condense multiple values into one variable.</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>Direction</strong></p></td><td colspan="1" rowspan="1"><p>Inside → Outside</p></td><td colspan="1" rowspan="1"><p>Outside → Inside</p></td></tr></tbody></table>

**Simple way to remember:**

*   **Spread = “Break things apart”**
    
*   **Rest = “Gather things together”**
    

## **4\. Expanding vs Collecting (Core Idea)**

### Spread (Expanding)

```javascript
const nums = [1, 2, 3];
console.log(...nums); // 1 2 3
```

### Rest (Collecting)

```javascript
function demo(...args) {
  console.log(args); // [1, 2, 3]
}
demo(1, 2, 3);
```

## **5\. Real-World Use Cases**

### Copying Arrays (Immutable update)

```javascript
const oldList = ["a", "b"];
const newList = [...oldList, "c"];
```

### Merging Objects (React / State updates)

```javascript
const state = { name: "Dev", age: 20 };
const newState = { ...state, age: 21 };
```

### Function Arguments

```javascript
const nums = [5, 10, 15];
Math.max(...nums); // 15
```

### Flexible Functions

```javascript
function logAll(...items) {
  items.forEach(item => console.log(item));
}
```

## **Final Summary**

*   `...` is the same syntax but behaves differently based on **context**
    
*   **Spread → expands values**
    
*   **Rest → collects values**
    
*   Widely used in:
    
    *   React (state updates)
        
    *   APIs (flexible arguments)
        
    *   Clean & modern JS code