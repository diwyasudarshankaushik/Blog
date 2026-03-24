---
title: "Node.js Internals and Architecture"
seoTitle: "Node.js Internals and Architecture"
datePublished: 2026-03-15T14:58:20.308Z
cuid: cmmrvq8eq00m22ehddk4u62aw
slug: node-js-internals-and-architecture
cover: https://cdn.hashnode.com/uploads/covers/696e62d612291978e735e98b/15444e0d-4ee3-4e68-9e1b-578ef3de90f2.png
ogImage: https://cdn.hashnode.com/uploads/og-images/696e62d612291978e735e98b/3b83ed97-43d0-45d1-81df-c2cde3808b02.png
tags: nodejs, v8, libuv, chaicode

---

## Basic

1.Javascript is single thread.  
2.Every Browsers have java script engine.  
3.JS work different in both environment Node.js and Browser

## What is Node.JS?

**Node.js** is a **runtime environment** that allows JavaScript to run outside the browser. It is built on **Chrome’s V8 JavaScript engine** and uses an **event-driven, non-blocking I/O architecture** which makes it highly efficient for scalable applications.

> `'V8' + 'C++' + 'LIBUV' is Node.js`

![](https://cdn.hashnode.com/uploads/covers/696e62d612291978e735e98b/c1031211-2c9e-4171-90f0-41bd4dbc8fa3.png align="center")

## 1️⃣ V8 Engine (JavaScript Engine)

The **V8 engine** executes JavaScript code.

### Key Functions

1.Converts **JavaScript → Machine Code**  
2.Executes the code very fast using **Just-In-Time (JIT) compilation**  
3.Handles **memory management and garbage collection**

### 2️⃣ Node.js Bindings (C/C++ Layer)

Node.js bindings act as a **bridge between JavaScript and C/C++ libraries**.

### Why they exist

JavaScript alone cannot directly access system-level features like:

1.File system  
2.Network  
3.OS operations

### What bindings do

They connect JavaScript APIs to **native C/C++ implementations**.

Example:

```plaintext
fs.readFile()
```

Flow:

```plaintext
JavaScript → Node.js API → C++ Bindings → libuv / OS
```

###   
3️⃣ Libuv (Core Asynchronous Engine)

**libuv** is a C library that handles **asynchronous operations**.

### Responsibilities

1.Event Loop  
2.Thread Pool  
3.File system operations  
4.Network I/O  
5.DNS operations  
6.Child processes

libuv allows Node.js to perform **non-blocking I/O operations**.

Example:

```plaintext
Reading files
Database calls
API requests
```

> Instead of blocking the thread, these operations run **in background threads**.

### 4️⃣ Event Loop

The **Event Loop** manages asynchronous tasks.

It continuously checks:

*   Is there any callback waiting?
    
*   Is any operation completed?
    

![](https://cdn.hashnode.com/uploads/covers/696e62d612291978e735e98b/eac358b0-9641-4f23-a987-a89868a281c6.png align="center")

**Event Loop Phases**

1.Exipred Callback()  
2\. IO Polling()  
3\. SetImmediate()  
4\. Close Callback()

```plaintext
while true{
  1.expriedcallback()->set timeout(()=>{},2)
  2.IO Polling->file reading Operation callback
  3.setimmediate()->only available in node.js
  4.close callbacks()
  5.check if anything pending? 
  No=exit 
  yes=continue
}
```

### 5️⃣ Thread Pool

Node.js uses a **thread pool (4 threads by default)** for operations like:

*   File system operations
    
*   DNS lookup
    
*   Compression
    
*   Cryptography
    

Example:

```plaintext
fs.readFile()
crypto.pbkdf2()
```

These run in the **libuv thread pool** instead of blocking the main thread.

### 6️⃣ Execution Flow in Node.js

### Example code:

```javascript
import fs from 'fs';
import crypto from 'crypto';

const start = Date.now();

process.env.UV_THREADPOOL_SIZE = 4;

setTimeout(() => console.log('Hello from Timer'), 0);
setImmediate(() => console.log('Hello from Immediate'), 0);

fs.readFile('sample.txt', 'utf-8', function (err, data) {
  console.log(`File Reading Complete...`);

  setTimeout(() => console.log('Time 2'), 0);
  setTimeout(() => console.log('Time 3'), 0);
  setImmediate(() => console.log('Immediate 2'), 0);

  crypto.pbkdf2('password', 'salt', 300000, 1024, 'sha256', () => {
    console.log('Password 1 has been hashed', Date.now() - start);
  });

  crypto.pbkdf2('password', 'salt', 300000, 1024, 'sha256', () => {
    console.log('Password 2 has been hashed', Date.now() - start);
  });

  crypto.pbkdf2('password', 'salt', 300000, 1024, 'sha256', () => {
    console.log('Password 3 has been hashed', Date.now() - start);
  });

  crypto.pbkdf2('password', 'salt', 300000, 1024, 'sha256', () => {
    console.log('Password 4 has been hashed', Date.now() - start);
  });

  crypto.pbkdf2('password', 'salt', 300000, 1024, 'sha256', () => {
    console.log('Password 5 has been hashed', Date.now() - start);
  });
});

console.log('Hello from Top Level Code');
```

### Execution order

```plaintext
Hello from Top Level Code
Hello from Timer
File Reading Complete...
Hello from Immediate
Immediate 2
Time 2
Time 3
Password 2 has been hashed 8047
Password 3 has been hashed 8047
Password 1 has been hashed 8156
Password 4 has been hashed 8436
Password 5 has been hashed 9959
```