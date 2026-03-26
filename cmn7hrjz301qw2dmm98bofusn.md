---
title: "Async/Await in JavaScript: Writing Cleaner Asynchronous Code"
seoTitle: "Async/Await in JavaScript: Writing Cleaner Asynchronous Code"
datePublished: 2026-03-26T13:11:46.144Z
cuid: cmn7hrjz301qw2dmm98bofusn
slug: async-await-in-javascript-writing-cleaner-asynchronous-code
cover: https://cdn.hashnode.com/uploads/covers/696e62d612291978e735e98b/e3a49cde-1f5a-4a61-8fee-94ca7bbd7bf4.png
ogImage: https://cdn.hashnode.com/uploads/og-images/696e62d612291978e735e98b/7b9b1468-c3c7-4a93-8ba3-a5054030c677.png
tags: javascript, frontend, web-development, tech, async, asyncawait, chaiaurcode, chaicode

---

In the early days of JavaScript, we handled asynchronous operations with **Callbacks**, which led to "Callback Hell." Then came **Promises**, which were better but still felt a bit "clunky" with nested `.then()` blocks.

Enter **Async/Await**: the modern way to write asynchronous code that looks and behaves like synchronous code.

## **1\. Why Async/Await Was Introduced**

The primary goal was **readability and maintainability**. While Promises solved the issue of callback nesting, chaining multiple `.then()` and `.catch()` blocks could still become difficult to follow in complex applications. Async/await provides a cleaner syntax that allows developers to avoid "**Promise chaining hell.**"

## **2\. How Async Functions Work**

An `async` function is a function declared with the `async` keyword.

*   **The Secret:** An async function **always returns a promise**.
    
*   Even if you return a simple string or number, JavaScript automatically wraps it in a resolved Promise.
    

```javascript
async function greet() {
    return "Hello, MasterJi!"; 
}

// This is equivalent to:
// return Promise.resolve("Hello, MasterJi!");
```

## **3\. The** `await` **Keyword Concept**

The `await` keyword can only be used inside an `async` function. It tells JavaScript: *"Pause the execution of this function until the promise is settled (either resolved or rejected)."*

**The "Syntactic Sugar" Aspect:** It’s important to remember that `await` doesn't actually block the main thread of JavaScript. It just makes the code *look* like it's waiting, while the engine goes off to do other tasks.

```javascript
async function getData() {
  let response = await fetch('api/url');
  let data = await response.json();
  console.log(data);
}
```

## **4\. Error Handling: Try/Catch**

One of the biggest wins for `async/await` is that we can use standard `try...catch` blocks, just like we do in synchronous code. This makes catching errors much more intuitive than using `.catch()`.

```javascript
async function getUserData() {
    try {
        const response = await fetch('api/url');
        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.error('Oops! Something went wrong:', error);
    }
}
```

## **5\. Comparison: Promises vs. Async/Await**

While `async/await` is built on top of Promises, the visual difference is striking:

<table style="min-width: 75px;"><colgroup><col style="min-width: 25px;"><col style="min-width: 25px;"><col style="min-width: 25px;"></colgroup><tbody><tr><td colspan="1" rowspan="1"><p><strong>Feature</strong></p></td><td colspan="1" rowspan="1"><p><strong>Promises (.then())</strong></p></td><td colspan="1" rowspan="1"><p><strong>Async/Await</strong></p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>Readability</strong></p></td><td colspan="1" rowspan="1"><p>Can get messy with deep chains</p></td><td colspan="1" rowspan="1"><p>Clean, looks like top-to-bottom code</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>Error Handling</strong></p></td><td colspan="1" rowspan="1"><p>Uses <code>.catch()</code></p></td><td colspan="1" rowspan="1"><p>Uses <code>try...catch</code></p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>Conditionals</strong></p></td><td colspan="1" rowspan="1"><p>Harder to handle logic between steps</p></td><td colspan="1" rowspan="1"><p>Easy to use <code>if/else</code> between awaits</p></td></tr></tbody></table>

### Promise Style

```javascript
fetch("api/url")
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.error(err));
```

### Async/Await Style

```javascript
try {
  const res = await fetch("api/url");
  const data = await res.json();
  console.log(data);
} catch (err) {
  console.error(err);
}
```

### Key Takeaways form Blog:

*   **Syntactic Sugar:** It doesn't change how JS works under the hood; it just makes it easier for humans to read.
    
*   **Sequential vs. Parallel:** Remind your readers that `await` is sequential. If tasks don't depend on each other, they might still want to use `Promise.all()`.
    

### \*\*Thank You

Diwya sudarshan kaushik\*\*