---
title: "Error Handling in JavaScript: Try, Catch, Finally"
seoTitle: "Error Handling in JavaScript: Try, Catch, Finally"
seoDescription: "A beginner's guide to JavaScript error handling. Master try...catch blocks, custom errors, and the finally block for more resilient web applications."
datePublished: 2026-03-25T17:48:49.585Z
cuid: cmn6c801a00bv2dmmah6h9wb1
slug: error-handling-in-javascript-try-catch-finally
cover: https://cdn.hashnode.com/uploads/covers/696e62d612291978e735e98b/7968e253-bad8-4077-a874-3597538597fa.png
ogImage: https://cdn.hashnode.com/uploads/og-images/696e62d612291978e735e98b/bd2fb316-3754-40da-b468-9de94d9f4715.png
tags: javascript, error-handling, webdev, trycatch, chaiaurcode, chaicode

---

## **1.What are Errors in JavaScript?**

Errors are problems that occur during program execution (runtime) and stop your code from working properly.

### Example of a Runtime Error

```javascript
console.log(user.name); // user is not defined
```

This throws a **ReferenceError** and crashes the program.

## **2\. Why Error Handling Matters**

In a **perfect world**, code always works. In **reality**, users enter letters into number fields, servers go down, and APIs return unexpected results.

*   **Graceful Failure:** Instead of the entire application "white-screening" or freezing, error handling allows the app to show a helpful message and keep running.
    
*   **Debugging Benefits:** Proper handling provides clear logs. Instead of seeing a vague `Uncaught TypeError`, you can log a specific message like `Failed to load user profile: Database timeout`.
    

### Runtime Error Example

A runtime error occurs while the code is executing (unlike syntax errors, which prevent the code from even starting).

```javascript
const user = null;
console.log(user.name); // ❌ Uncaught TypeError: Cannot read properties of null
console.log("This will never run"); // The script stops here
```

## **3\. Using Try and Catch Blocks**

The `try...catch` statement consists of a `try` block and a `catch` block.

*   **Try:** Contains the code that might cause an error.
    
*   **Catch:** Contains the code to execute if an error occurs.
    

### Basic Syntax

```javascript
try {
  // risky code
} catch (error) {
  // handle error
}
```

### Example

```javascript
try {
  let data = JSON.parse("invalid json");
} catch (error) {
  console.log("Something went wrong:", error.message);
// The script continues to run safely after this
}
```

## **4\. The Finally Block**

The `finally` block is the "cleanup" crew. It executes **no matter what**, whether an error was thrown or not. This is perfect for closing database connections or hiding loading spinners.

**Execution Order:**

1.  **Try** runs.
    
2.  If error: **Catch** runs.
    
3.  **Finally** runs (always).
    

### Syntax

```javascript
try {
  // code
} catch (error) {
  // handle error
} finally {
  // always runs
}
```

### Example

```javascript
try {
  console.log("Trying...");
} catch (err) {
  console.log("Error occurred");
} finally {
  console.log("Always executed");
}
```

## 5\. Throwing Custom Errors

Sometimes, code is technically "correct" but logically wrong (e.g., a user entering a negative age). You can use the `throw` keyword to create your own errors.

```javascript
function checkAge(age) {
  if (age < 0) {
    throw new Error("Age cannot be negative!"); // Custom error
  }
  return true;
}

try {
  checkAge(-5);
} catch (e) {
  console.log(e.name);    // "Error"
  console.log(e.message); // "Age cannot be negative!"
}
```

## **6\.** Types of Common Errors

Common errors you'll encounter in JavaScript include:

*   **ReferenceError:** Using a variable that hasn't been declared.
    
*   **TypeError:** Performing an operation on the wrong data type (like calling a string as a function).
    
*   **SyntaxError:** Writing code that the engine can't interpret (usually caught before runtime).
    

## 7.Real-World Use Cases

*   API calls (handling failed requests)
    
*   JSON parsing
    
*   Form validation
    
*   File operations
    
*   Payment systems