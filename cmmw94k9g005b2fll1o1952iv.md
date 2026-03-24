---
title: "Array Flatten in JavaScript"
seoTitle: "How to Flatten Arrays in JS: Interview Questions & Polyfills"
seoDescription: "Preparing for a JS interview? Learn how to flatten nested arrays using modern ES6+ methods and custom recursive logic. Perfect for technical round pre"
datePublished: 2026-03-18T16:24:28.567Z
cuid: cmmw94k9g005b2fll1o1952iv
slug: array-flatten-in-javascript
cover: https://cdn.hashnode.com/uploads/covers/696e62d612291978e735e98b/aed45037-b594-4b2d-83ce-215e7dc274d5.jpg
ogImage: https://cdn.hashnode.com/uploads/og-images/696e62d612291978e735e98b/0b6fa578-a033-4f5d-a726-cbb767391668.jpg
tags: javascript, chaiaurcode, chaicode, chaicohort

---

## 1\. What are Nested Arrays?

A **nested array** (also known as a multi-dimensional array) is simply an array that contains other arrays as its elements. This can go multiple levels deep, creating a tree-like structure.

**Visual Example:**

JavaScript

```typescript
const nested = [1, [2, 3], [4, [5, 6]]];
```

In this example:

*   `1` is at depth 0.
    
*   `[2, 3]` is a nested array at depth 1.
    
*   `[5, 6]` is a deeply nested array at depth 2.
    

## 2\. Why Flattening Arrays is Useful?

**Flattening** is the process of converting a multi-dimensional array into a single-dimensional array, where all elements are at the same level.

### Why is it useful?

*   **Data Normalization:** APIs often return inconsistent nested structures that need to be "cleaned" before being displayed in a UI.
    
*   **Easier Manipulation:** Methods like `.filter()`, `.map()`, and `.find()` are much easier to run on a flat list.
    
*   **Searchability:** It’s simpler to check if a value exists in `[1, 2, 3, 4]` than in `[1, [2, [3]], 4]`.
    

### Step-by-step:

1.  Start with main array
    
2.  Check each element:
    
    *   If number → add to result
        
    *   If array → go inside it
        
3.  Repeat until no nested arrays remain
    

## 3.Different Approaches to Flatten Arrays

### A. The Modern Way: `Array.prototype.flat()`

Introduced in ES2019, this is the most straightforward method. It takes a `depth` argument (default is 1).

JavaScript

```javascript
const arr = [1, [2, [3, 4]]];
// flat(depth)

console.log(arr.flat());       // [1, 2, [3, 4]] (flattens 1 level)
console.log(arr.flat(2));      // [1, 2, 3, 4] (flattens 2 levels)
console.log(arr.flat(Infinity)); // Flattens e
```

### B. The Recursive Approach (Interview Classic)

If you can't use built-in methods, recursion is the standard way to solve this.

**Step-by-Step Logic:**

1.  Initialize an empty result array.
    
2.  Loop through each element of the input array.
    
3.  **If** the element is an array, call the function again (recursion) and spread the result.
    
4.  **Else**, push the element into the result array.
    

JavaScript

```javascript
function flatten(arr) {
  let result = [];

  for (let item of arr) {
    if (Array.isArray(item)) {
      result = result.concat(flatten(item));
    } else {
      result.push(item);
    }
  }

  return result;
}

console.log(flatten([1, [2, [3, 4]], 5]));
```

### C. Using `reduce()` and `concat`

A more functional programming approach:

JavaScript

```javascript
function flatten(arr) {
  return arr.reduce((acc, item) => {
    return acc.concat(
      Array.isArray(item) ? flatten(item) : item
    );
  }, []);
}
```

### D. Using Stack (Iterative Approach)

To flatten any depth without built-in methods, we use recursion. This is a favorite for technical interviews.

**Step-by-Step Thinking:**

1.  Initialize an empty result array.
    
2.  Loop through each element.
    
3.  **If** the element is an array, call the function again (recursion) and spread the result.
    
4.  **Else**, push the element to the result.
    

```javascript
function flatten(arr) {
  const stack = [...arr];
  const result = [];

  while (stack.length) {
    const next = stack.pop();

    if (Array.isArray(next)) {
      stack.push(...next);
    } else {
      result.push(next);
    }
  }

  return result.reverse();
}
```

Here is a custom **Polyfill** for `Array.prototype.flat()`. This is a classic "Senior Engineer" interview question because it requires you to understand prototypes, recursion, and how to handle the `depth` parameter.

### E. Using Stack (Iterative Approach)

Interviewers don't just want the code; they want to see your **problem-solving logic**.

*   **"Write a polyfill for Array.flat":** They want to see if you understand recursion and how to attach methods to the prototype.
    
*   **"Flatten up to a specific depth":** The recursion stops when `depth` is no longer greater than 0 or the item is not an array.
    
*   **Performance Constraints:** For massive arrays, recursion might cause a "Stack Overflow." In such cases, you might discuss an **iterative stack-based approach**.
    
*   **Context (**`this`**)**: Explain that `this` refers to the array instance (e.g., `nestedArr`).
    
*   **Spread Operator**: Mention that `...item.myFlat()` is used to "unpack" the returned array from the recursive call so we don't end up with nested results.
    
*   **Handling "Holes"**: Real `Array.prototype.flat()` removes empty slots in arrays. You can mention that `forEach` naturally skips empty slots, which makes this implementation quite accurate.
    

> **Pro Tip:** Always ask the interviewer, "Should I handle any depth, or just one level?" and "Should I handle empty slots in the array?" (The built-in `.flat()` automatically removes empty slots).

### The Polyfill Implementation

```javascript
if (!Array.prototype.myFlat) {
  Array.prototype.myFlat = function (depth = 1) {
    // 'this' refers to the array the method is called on
    let result = [];

    this.forEach((item) => {
      if (Array.isArray(item) && depth > 0) {
        // Recursively flatten and decrement depth
        // We use spread to push individual elements into result
        result.push(...item.myFlat(depth - 1));
      } else {
        // If not an array or depth reached, push the item as-is
        result.push(item);
      }
    });

    return result;
  };
}

// Testing the polyfill
const nestedArr = [1, [2, [3, [4]]], 5];

console.log(nestedArr.myFlat(1)); // [1, 2, [3, [4]], 5]
console.log(nestedArr.myFlat(2)); // [1, 2, 3, [4], 5]
console.log(nestedArr.myFlat(Infinity)); // [1
```

### Common Mistakes (and how to avoid them) Even seasoned developers can trip up when flattening arrays. Here are the most common pitfalls to watch out for:

1.  Forgetting that flat() is Non-Mutating A common mistake is assuming that .flat() changes the original array. In JavaScript, most array methods return a new array.
    

The Bug: Calling myArr.flat() and expecting myArr to be flattened.

The Fix: Always assign the result to a new variable.

JavaScript const nested = \[1, \[2\]\]; const flat = nested.flat(); // Correct! 2. Underestimating the Depth The default depth for .flat() is 1. If you have an array nested three levels deep, a standard call won't finish the job.

The Bug: \[1, \[2, \[3\]\]\].flat() results in \[1, 2, \[3\]\].

**The Fix:** If you don't know the depth, use Infinity as the argument: arr.flat(Infinity).

1\. Mutating the Input (In Custom Functions) When writing a custom recursive function, it's tempting to use .push() on the input array or modify it directly. This can lead to side effects that are hard to debug.

**The Fix:** Always treat the input as read-only and build a new result array to return.

2\. Ignoring "Holes" in Arrays If you have a sparse array (e.g., \[1, , \[3\]\]), some manual flattening methods (like using a standard for loop) might preserve that "empty" slot or turn it into undefined.

**The Fix:** Use Array.prototype.flat() or functional methods like .filter() or .forEach(), which naturally skip empty slots.

3\. Recursion Limits (The "Stack Overflow") For extremely deep arrays (e.g., thousands of levels deep), a recursive function will hit the call stack limit and crash your application.

**The Fix:** For massive data structures, use an iterative approach with a stack (FIFO) instead of recursion.

## Final Summary

*   Nested arrays = arrays inside arrays
    
*   Flattening = converting to single level
    
*   Best methods:
    
    *   `flat()` → easy
        
    *   Recursion → interview favorite
        
    *   `reduce()` → functional style
        
    *   Stack → iterative solution