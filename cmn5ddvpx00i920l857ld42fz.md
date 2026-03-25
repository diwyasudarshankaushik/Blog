---
title: "String Polyfills and Common Interview Methods in JavaScript"
seoTitle: "JavaScript String Methods & Polyfills"
seoDescription: "A comprehensive guide to JavaScript string manipulation. Covering everything from basic methods to advanced polyfill implementation and top 20 intervi"
datePublished: 2026-03-25T01:33:37.367Z
cuid: cmn5ddvpx00i920l857ld42fz
slug: string-polyfills-and-common-interview-methods-in-javascript
cover: https://cdn.hashnode.com/uploads/covers/696e62d612291978e735e98b/f837d511-65e7-4857-884b-97166af7a5a8.png
ogImage: https://cdn.hashnode.com/uploads/og-images/696e62d612291978e735e98b/e2d42d9d-15cc-4605-b9d9-cbf7c04b6762.png
tags: javascript, prototype, polyfills, chaicode, javascriptforbeginners

---

## **1\. What are String Methods?**

String methods are built-in functions provided by the `String.prototype` that allow us to inspect, manipulate, or transform text.

**Conceptually:** Think of a string method as a specialized machine. You feed it a string, it performs a specific logic (like searching for a character or slicing a section), and it returns a **new** value because ***strings in JS are immutable***.

Examples:

*   `toUpperCase()` `slice()` `includes()` `Trim()` `replace()`
    

## **2\. Why Developers Write Polyfills**

A **polyfill** is a piece of code used to provide modern functionality on older browsers that do not natively support it.

**Deep Understanding:** In interviews, you aren't asked to write a polyfill because the interviewer thinks `includes()` is missing; they want to see if you understand **prototypal inheritance** and **loop logic**.

💡 Example:  
If `String.prototype.includes` didn’t exist, you can implement it yourself.

## **3\. Implementing Simple String Utilities (Polyfills)**

To write a polyfill, we attach our function to `String.prototype`. Here is how the logic looks for a common method like `includes`.

#### Custom `myIncludes` Polyfill

```javascript
if (!String.prototype.myIncludes) {
  String.prototype.myIncludes = function(searchString, start = 0) {
    // 'this' refers to the string the method is called on
    if (searchString instanceof RegExp) {
      throw TypeError("First argument must not be a RegExp");
    }
    // The core logic: loop through and match substrings
    return this.indexOf(searchString, start) !== -1;
  };
}

// Usage
"hello".myIncludes("ell"); // true
```

## **4\. Common Interview String Problems**

When preparing for interviews, focus on these high-frequency patterns:

<table style="min-width: 50px;"><colgroup><col style="min-width: 25px;"><col style="min-width: 25px;"></colgroup><tbody><tr><td colspan="1" rowspan="1"><p><strong>Problem</strong></p></td><td colspan="1" rowspan="1"><p><strong>Key Logic</strong></p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>Reverse a String</strong></p></td><td colspan="1" rowspan="1"><p>Use a decrementing loop or <code>split('').reverse().join('')</code>.</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>Palindrome Check</strong></p></td><td colspan="1" rowspan="1"><p>Compare the string to its reversed version or use two pointers.<br></p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>First Non-Repeated Char</strong></p></td><td colspan="1" rowspan="1"><p>Use a "Frequency Map" (an object or Map) to count occurrences.<br></p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>Anagram Check</strong></p></td><td colspan="1" rowspan="1"><p>Sort both strings and compare, or compare their character counts.</p></td></tr></tbody></table>

### 1\. Reverse a String

```javascript
function reverse(str) {
  return str.split("").reverse().join("");
}
```

### 2\. Check Palindrome

```javascript
function isPalindrome(str) {
  const reversed = str.split("").reverse().join("");
  return str === reversed;
}
```

3\. Count Characters (Anagram Check)

```javascript
function charCount(str) {
  const map = {};
  for (let char of str) {
    map[char] = (map[char] || 0) + 1;
  }
  return map;
}
```

4\. First Non-Repeating Character

```javascript
function firstUnique(str) {
  const map = {};

  for (let char of str) {
    map[char] = (map[char] || 0) + 1;
  }

  for (let char of str) {
    if (map[char] === 1) return char;
  }

  return null;
}
```

### 5\. Importance of Understanding Built-in Behavior

Why not just use the built-ins and move on?

1.  **Performance:** Using `.split().reverse().join()` creates three new objects in memory. For massive strings, a simple `for` loop is much more memory-efficient.
    
2.  **Edge Cases:** Does `.trim()` remove non-breaking spaces? How does `.slice()` handle negative indices? Knowing these details prevents "phantom bugs" in production.
    

> **Pro-Tip for Interviews:** Always clarify if the string contains special characters or emojis. Emojis use "surrogate pairs," which can break simple `.length` or `.split('')` logic!

*   Always explain logic before coding
    
*   Write clean, readable solutions
    
*   Mention edge cases:
    
    *   Empty string
        
    *   Case sensitivity
        
    *   Special characters
        
*   If possible, **write a polyfill version** of a method
    

### Level 1: Basic String Manipulation

1\. How do you reverse a string without using built-in methods?  
2\. What is the difference between `slice()`, `substring()`, and `substr()`?  
3\. How can you check if a string starts with a specific substring?  
4\. How do you convert a string to an array of characters?  
5\. What does `.trim()` do?

### Level 2: Intermediate Logic & Polyfills

6\. Why are strings called "immutable" in JavaScript?  
7\. Write a polyfill for `String.prototype.includes`.  
8\. Explain the "Two Pointer" technique for checking a Palindrome.  
9\. How do you check if two strings are Anagrams?  
10\. What is the difference between `==` and `===` when comparing strings?

### **Level 3: Advanced Concepts & Performance**

11\. What are "Surrogate Pairs" in JavaScript strings?  
12\. How do you find the first non-repeating character in a string?  
13\. What is String Padding?  
**14\. How does** `localeCompare()` **work?**  
15\. How do you repeat a string ***N*** times without `.repeat()`?

Level 4: Coding Challenges

16\. How do you capitalize the first letter of every word in a sentence?  
17\. How do you find the longest word in a string?  
18\. How do you remove duplicate characters from a string?  
19\. How do you truncate a string and add "..." if it exceeds a certain length?  
20\. What is the time complexity of string concatenation in a loop?

Thank You  
Diwya sudarshan kaushik