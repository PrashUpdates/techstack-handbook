# 🟨 JavaScript (ES6+) Documentation

<p align="center">
  <a href="https://github.com/PrashUpdates/techstack-handbook/blob/main/README.md#frontend"><img src="https://img.shields.io/badge/Back%20to%20main-6E7681?style=for-the-badge" alt="Back to main" /></a>
  <a href="./cheat-sheet.md"><img src="https://img.shields.io/badge/Cheat%20Sheet-F38020?style=for-the-badge" alt="Cheat Sheet" /></a>
  <a href="./notes.md"><img src="https://img.shields.io/badge/Notes-3FB950?style=for-the-badge" alt="Notes" /></a>
</p>

> A complete guide to modern JavaScript: how it runs, the core language, asynchronous code, the DOM, best practices and a ready-to-use starter project.

## 📑 Contents

| # | Section | What's inside |
|---|---|---|
| 1 | [Executive Summary & Use Cases](#summary) | What JavaScript is and when to use it |
| 2 | [Core Concepts & Architecture](#concepts) | Engine, types, functions, objects, async code, the DOM, modules |
| 3 | [Standard Checklist & Best Practices](#checklist) | Features, setup steps, performance, accessibility and security tips |
| 4 | [Quick Start & Boilerplate Code](#quickstart) | A minimal, commented starter project |
| 5 | [Official Documentation & Resources](#resources) | Verified docs, tutorials and practice platforms |

---

<a id="summary"></a>

## 1. Executive Summary & Use Cases

**JavaScript** (JS) is a high-level, multi-paradigm programming language that makes web pages interactive. It is the only programming language that runs natively in every web browser, and with runtimes like Node.js it also runs on servers, command-line tools and more.

JavaScript is standardized as **ECMAScript (ES)**. The term **ES6+** means ES2015 and every later version, which added modern features such as `let` and `const`, arrow functions, classes, modules, promises and `async`/`await`.

**Primary purpose:** add behavior and logic to web pages: respond to user actions, update content without reloading, talk to servers and build full applications.

| Language | Role |
|---|---|
| **HTML** | Structure and meaning |
| **CSS** | Style and layout |
| **JavaScript** | Behavior and interactivity |

### Where JavaScript runs

| Environment | Used for |
|---|---|
| **Browser** | Interactive pages and web apps (uses the DOM and Web APIs) |
| **Node.js, Deno, Bun** | Servers, APIs, scripts and tooling |
| **Frameworks and runtimes** | Mobile and desktop apps (React Native, Electron and others) |

### When to use it

| Use it when | Example |
|---|---|
| Making pages interactive | Menus, modals, tabs, sliders |
| Validating and handling forms | Live validation, submit without reload |
| Loading data from servers | Fetching from an API and rendering results |
| Building single-page apps | Dashboards, web apps with React, Vue or Angular |
| Building back-end services | REST APIs with Node.js |
| Drawing and animation | Canvas, games, data visualization |
| Automating tasks | Build scripts, command-line tools |

---

<a id="concepts"></a>

## 2. Core Concepts & Architecture

### How JavaScript runs

1. The browser downloads the script
2. The **engine** (V8 in Chrome and Edge, SpiderMonkey in Firefox, JavaScriptCore in Safari) parses and compiles the code
3. The code runs on a **single thread**, one task at a time, using the **call stack**
4. Long or waiting tasks (timers, network requests, events) are handled by the browser, and their callbacks are queued by the **event loop** (see the async section)

### Adding JavaScript to HTML

| Method | Example | When to use |
|---|---|---|
| **External with `defer`** (recommended) | `<script src="script.js" defer></script>` | Almost always: runs after the HTML is parsed |
| **ES module** | `<script type="module" src="main.js"></script>` | Modern projects with `import` and `export` (deferred by default) |
| **Internal** | `<script> ... </script>` | Tiny demos |
| **Inline handler** | `<button onclick="go()">` | Avoid: mixes logic into HTML |

### Syntax Basics

```js
// Single-line comment
/* Multi-line
   comment */

console.log("Hello, World!"); // prints to the browser console
```

- JavaScript is **case-sensitive** (`name` and `Name` are different)
- Statements end with `;` (optional in many cases, but be consistent)
- Use `camelCase` for variables and functions, `PascalCase` for classes, `UPPER_SNAKE_CASE` for constants

### Variables

| Keyword | Scope | Reassign | Redeclare | Notes |
|---|---|---|---|---|
| `const` | Block | No | No | **Default choice** |
| `let` | Block | Yes | No | Use when the value must change |
| `var` | Function | Yes | Yes | Legacy: avoid in new code |

```js
const name = "Ada";   // cannot be reassigned
let score = 0;        // can be reassigned
score = score + 1;

const user = { name: "Ada" };
user.name = "Grace";  // allowed: const protects the binding, not the contents
```

**Temporal Dead Zone (TDZ):** `let` and `const` exist from the start of their block but cannot be used before their line runs. Using them early throws a `ReferenceError`.

### Data Types

| Type | Example | Notes |
|---|---|---|
| `string` | `"hello"`, `'hi'`, `` `hi` `` | Text |
| `number` | `42`, `3.14`, `NaN`, `Infinity` | All numbers are 64-bit floats |
| `bigint` | `9007199254740993n` | Very large integers |
| `boolean` | `true`, `false` | |
| `undefined` | `undefined` | A variable with no value yet |
| `null` | `null` | Intentional "no value" |
| `symbol` | `Symbol("id")` | Unique identifiers |
| `object` | `{}`, `[]`, functions, dates | Everything else |

```js
typeof "text";      // "string"
typeof 42;          // "number"
typeof undefined;   // "undefined"
typeof null;        // "object"  (a historic quirk of the language)
typeof [];          // "object"  (use Array.isArray([]) to check arrays)
typeof function(){} // "function"
```

**Primitives** are copied by value. **Objects** (including arrays and functions) are copied by reference, so two variables can point to the same object.

### Type Coercion, Equality & Truthiness

| Operator | Name | Behavior |
|---|---|---|
| `===` | Strict equality | Compares value and type (**use this**) |
| `==` | Loose equality | Converts types first, with surprising results |
| `Object.is(a, b)` | Same-value equality | Like `===`, but treats `NaN` as equal to `NaN` |

```js
0 == "0";    // true   (surprising)
0 === "0";   // false  (predictable)
```

**Falsy values** (everything else is truthy): `false`, `0`, `-0`, `0n`, `""`, `null`, `undefined`, `NaN`. Note that `"0"`, `[]` and `{}` are truthy.

### Operators

```js
// Arithmetic:   +  -  *  /  %  **  ++  --
// Comparison:   ===  !==  >  <  >=  <=
// Logical:      &&  (and)    ||  (or)    !  (not)
// Nullish:      ??   returns the right side only if the left is null or undefined
// Optional:     ?.   stops safely if something is null or undefined
// Assignment:   =  +=  -=  *=  /=  ??=  (and the logical versions &&= and ||=)

const city = user?.address?.city ?? "Unknown";
```

### Control Flow

| Structure | Example |
|---|---|
| `if / else if / else` | `if (age >= 18) { ... } else { ... }` |
| Ternary | `const label = isOn ? "On" : "Off";` |
| `switch` | `switch (day) { case 1: ... break; default: ... }` |
| `for` | `for (let i = 0; i < 5; i++) { ... }` |
| `for...of` | `for (const item of array) { ... }` (values of any iterable) |
| `for...in` | `for (const key in object) { ... }` (keys of an object) |
| `while` / `do...while` | `while (condition) { ... }` |
| `break` / `continue` | Exit a loop / skip to the next round |

### Functions

```js
// Declaration (hoisted: can be called before it appears)
function add(a, b) {
  return a + b;
}

// Expression
const multiply = function (a, b) { return a * b; };

// Arrow function (short syntax, does not have its own `this`)
const square = (n) => n * n;

// Default, rest and spread
function greet(name = "friend") { return `Hello, ${name}!`; }
function sum(...numbers) { return numbers.reduce((total, n) => total + n, 0); }
const maxValue = Math.max(...[3, 9, 4]);
```

| Concept | Meaning |
|---|---|
| **Parameter vs argument** | Parameters are in the definition, arguments are the values passed in |
| **Return** | A function with no `return` gives back `undefined` |
| **First-class functions** | Functions are values: store them, pass them, return them |
| **Higher-order function** | A function that takes or returns another function (`map`, `filter`) |
| **Callback** | A function passed to another function to run later |
| **IIFE** | `(() => { ... })();` runs immediately, creates a private scope |

### Scope, Hoisting & Closures

- **Scope** decides where a variable can be used: global, function or block (`{ }`)
- Inner scopes can read outer variables, never the other way around
- **Hoisting:** declarations are processed before the code runs. Function declarations are fully usable early, `var` is `undefined` until assigned, and `let` and `const` stay in the TDZ

A **closure** is a function that remembers the variables from where it was created, even after the outer function has finished.

```js
function createCounter() {
  let count = 0;                 // private variable
  return () => ++count;          // the inner function keeps access to `count`
}

const next = createCounter();
next(); // 1
next(); // 2
```

### The `this` Keyword

| How the function is called | Value of `this` |
|---|---|
| Method call: `obj.method()` | `obj` |
| Plain function call | `undefined` in strict mode and modules, otherwise the global object |
| Arrow function | Inherited from the surrounding scope |
| `new Foo()` | The newly created object |
| `fn.call(x)`, `fn.apply(x)`, `fn.bind(x)` | `x` (set explicitly) |
| Regular function as a DOM event handler | The element the handler is attached to |

**Rule of thumb:** use arrow functions for callbacks, and regular methods on objects and classes.

### Objects

```js
const user = {
  name: "Ada",
  age: 36,
  greet() { return `Hi, I am ${this.name}`; },
};

user.name;            // dot access
user["age"];          // bracket access (for dynamic keys)
user.email = "a@b.c"; // add a property
delete user.age;      // remove a property

// Destructuring, spread and shorthand
const { name, email = "none" } = user;
const copy = { ...user, role: "admin" };   // shallow copy with an extra field
const point = { x: 1, y: 2 };
const key = "z";
const point3d = { ...point, [key]: 3 };    // computed property name
```

| Useful `Object` method | Purpose |
|---|---|
| `Object.keys(obj)` / `Object.values(obj)` | Arrays of keys / values |
| `Object.entries(obj)` | Array of `[key, value]` pairs |
| `Object.fromEntries(pairs)` | Build an object from pairs |
| `Object.assign(target, src)` | Copy properties |
| `Object.freeze(obj)` | Prevent changes (shallow) |
| `Object.hasOwn(obj, key)` | Check for an own property |
| `structuredClone(obj)` | Deep copy |

### Prototypes & Classes

Every object has a hidden link to a **prototype**, and property lookups follow this **prototype chain**. Classes are a cleaner syntax built on top of it.

```js
class Animal {
  #energy = 10;                   // private field (only usable inside the class)
  static kingdom = "Animalia";    // belongs to the class itself

  constructor(name) {
    this.name = name;
  }

  speak() {
    return `${this.name} makes a sound.`;
  }

  get energy() { return this.#energy; }   // getter
}

class Dog extends Animal {
  speak() {
    return `${super.speak()} Woof!`;       // call the parent method
  }
}

const dog = new Dog("Rex");
dog.speak(); // "Rex makes a sound. Woof!"
```

### Arrays

```js
const nums = [1, 2, 3, 4, 5];

nums.map((n) => n * 2);            // [2, 4, 6, 8, 10]   transform each item
nums.filter((n) => n % 2 === 0);   // [2, 4]             keep matches
nums.reduce((sum, n) => sum + n, 0); // 15               combine into one value
nums.find((n) => n > 3);           // 4                  first match
nums.some((n) => n > 4);           // true               any match?
nums.every((n) => n > 0);          // true               all match?
nums.includes(3);                  // true
```

| Changes the original array | Returns a new value (original untouched) |
|---|---|
| `push`, `pop`, `shift`, `unshift` | `map`, `filter`, `reduce`, `slice`, `concat` |
| `splice`, `sort`, `reverse`, `fill` | `find`, `findIndex`, `some`, `every`, `includes`, `indexOf` |
| | `flat`, `flatMap`, `join`, `at` |
| | `toSorted`, `toReversed`, `toSpliced`, `with` (newer browsers) |

```js
const [first, second, ...rest] = nums;   // array destructuring
const merged = [...nums, 6, 7];          // spread into a new array
```

### Strings, Numbers, JSON & Dates

```js
// Template literals
const message = `Hello, ${name}! 2 + 2 = ${2 + 2}`;

// Useful string methods
"  hi  ".trim();            // "hi"
"a-b-c".split("-");         // ["a", "b", "c"]
"hello".includes("ell");    // true
"hello".replaceAll("l", "L");
"abc".padStart(5, "0");     // "00abc"

// Numbers and Math
Number("42");               // 42
parseInt("42px", 10);       // 42
(3.14159).toFixed(2);       // "3.14"
Math.round(2.5);            // 3
Math.random();              // 0 to just under 1
Number.isNaN(NaN);          // true

// JSON: convert between objects and text
const text = JSON.stringify({ a: 1 });   // '{"a":1}'
const data = JSON.parse(text);           // { a: 1 }

// Dates
const now = new Date();
now.toISOString();                       // "2026-01-01T10:00:00.000Z"
new Intl.DateTimeFormat("en-US").format(now);
```

### Collections & Iteration

| Structure | Purpose |
|---|---|
| `Array` | Ordered list |
| `Set` | Unique values only |
| `Map` | Key-value pairs where keys can be any type |
| `WeakMap` / `WeakSet` | Hold objects without preventing garbage collection |

```js
const unique = [...new Set([1, 2, 2, 3])];        // [1, 2, 3]
const scores = new Map([["Ada", 10]]);
scores.set("Grace", 12);
scores.get("Ada");                                // 10
```

**Iterables and generators:** `for...of` works on arrays, strings, maps and sets. A **generator** (`function*` with `yield`) produces values one at a time.

### Modules

Modules split code into files with their own scope.

```js
// math.js
export const PI = 3.14159;
export function area(r) { return PI * r * r; }
export default function greet() { return "Hello"; }

// main.js
import greet, { PI, area } from "./math.js";
```

```html
<script type="module" src="main.js"></script>
```

- Module code runs in **strict mode** and has its own scope (no accidental globals)
- Use a local server (such as Live Server) when testing modules, because `file://` pages block them
- **Dynamic import:** `const mod = await import("./heavy.js");` loads code only when needed

### Error Handling

```js
try {
  const data = JSON.parse(userInput);
} catch (error) {
  console.error("Invalid JSON:", error.message);
} finally {
  console.log("Runs either way");
}

// Throwing your own error
function divide(a, b) {
  if (b === 0) throw new RangeError("Cannot divide by zero");
  return a / b;
}
```

| Common error | Meaning |
|---|---|
| `ReferenceError` | A variable does not exist or is in the TDZ |
| `TypeError` | Wrong type, such as calling `undefined` as a function |
| `SyntaxError` | Invalid code or invalid JSON |
| `RangeError` | A value outside its allowed range |

### Asynchronous JavaScript

JavaScript runs one thing at a time, so slow operations (network, timers, files) are handled asynchronously, which keeps the page responsive.

**The event loop**

```
Call stack  →  runs the current code
Microtask queue  →  promise callbacks (run as soon as the stack is empty)
Macrotask queue  →  timers, DOM events, network callbacks (one per loop turn)
```

```js
console.log("1: synchronous");
setTimeout(() => console.log("4: macrotask (timer)"), 0);
Promise.resolve().then(() => console.log("3: microtask (promise)"));
console.log("2: synchronous");
// Output order: 1, 2, 3, 4
```

**Three styles of async code**

| Style | Example | Notes |
|---|---|---|
| **Callbacks** | `setTimeout(done, 1000)` | Original style: nesting leads to "callback hell" |
| **Promises** | `fetch(url).then(r => r.json())` | Chainable, with `.catch()` for errors |
| **`async` / `await`** | `const data = await getData();` | Reads like normal code (**preferred**) |

A **Promise** has three states: **pending**, **fulfilled** and **rejected**.

```js
// A reusable fetch helper with proper error handling
async function getJSON(url) {
  try {
    const response = await fetch(url);

    // fetch only rejects on network failure, so check the HTTP status yourself
    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }

    return await response.json();
  } catch (error) {
    console.error("Request failed:", error.message);
    throw error; // let the caller decide what to do
  }
}

const data = await getJSON("https://api.example.com/items"); // inside a module or async function
```

| Promise helper | Behavior |
|---|---|
| `Promise.all([...])` | Waits for all; rejects if any fails |
| `Promise.allSettled([...])` | Waits for all; reports each result |
| `Promise.race([...])` | Settles with the first one to finish |
| `Promise.any([...])` | Fulfills with the first one that succeeds |

```js
// Run independent requests in parallel instead of one after another
const [users, posts] = await Promise.all([
  getJSON("/api/users"),
  getJSON("/api/posts"),
]);
```

**Timers:** `setTimeout(fn, ms)` runs once, `setInterval(fn, ms)` repeats, and `clearTimeout` / `clearInterval` cancel them. Use `requestAnimationFrame(fn)` for smooth animations.

### The DOM (Document Object Model)

The browser turns your HTML into a tree of objects. JavaScript reads and changes that tree to update the page.

**Selecting elements**

```js
document.getElementById("title");
document.querySelector(".card");        // first match
document.querySelectorAll("li");        // all matches (NodeList)
element.closest(".card");               // nearest ancestor that matches
```

**Changing elements**

| Task | Code |
|---|---|
| Set text (safe) | `el.textContent = "Hello";` |
| Set HTML (risky with user input) | `el.innerHTML = "<b>Hi</b>";` |
| Attributes | `el.setAttribute("href", "#")`, `el.getAttribute("href")` |
| Classes | `el.classList.add("active")`, `.remove()`, `.toggle()`, `.contains()` |
| Inline style | `el.style.color = "tomato";` (prefer toggling classes) |
| Data attributes | `el.dataset.id` for `data-id="5"` |
| Create | `const li = document.createElement("li");` |
| Insert | `parent.append(li)`, `parent.prepend(li)`, `el.before(x)`, `el.after(x)` |
| Remove | `el.remove()` |

**Events**

```js
button.addEventListener("click", (event) => {
  event.preventDefault();       // stop the default action (such as a form submit)
  console.log(event.target);    // the element that was clicked
});
```

| Common events | |
|---|---|
| Mouse | `click`, `dblclick`, `mouseover`, `mouseout` |
| Keyboard | `keydown`, `keyup` |
| Forms | `submit`, `input`, `change`, `focus`, `blur` |
| Page | `DOMContentLoaded`, `load`, `scroll`, `resize` |
| Touch and pointer | `pointerdown`, `pointermove`, `touchstart` |

**Bubbling and event delegation:** events travel up from the clicked element to its ancestors. Instead of adding a listener to every item, add one to the parent and check `event.target`. This is faster and also works for items added later.

```js
list.addEventListener("click", (event) => {
  const item = event.target.closest("li");
  if (!item) return;
  console.log("Clicked:", item.textContent);
});
```

### Browser APIs

| API | Purpose | Example |
|---|---|---|
| **Fetch** | HTTP requests | `fetch(url)` |
| **Web Storage** | Small key-value storage in the browser | `localStorage.setItem("k", "v")` |
| **URL / URLSearchParams** | Build and read URLs | `new URL(location.href)` |
| **History** | Change the URL without reloading | `history.pushState(...)` |
| **Intersection Observer** | Detect when an element enters the screen | Lazy loading, scroll animations |
| **Clipboard** | Copy and paste | `navigator.clipboard.writeText(text)` |
| **Geolocation** | User location (needs permission) | `navigator.geolocation` |
| **Canvas** | Draw graphics | `canvas.getContext("2d")` |
| **Web Workers** | Run heavy code off the main thread | `new Worker("worker.js")` |

`localStorage` keeps data across sessions, `sessionStorage` keeps it until the tab closes. Both store **text only** (use `JSON.stringify` for objects) and are readable by any script on the page, so **never store passwords, tokens or other secrets there**.

### Modern ES6+ Features at a Glance

| Version | Highlights |
|---|---|
| **ES2015 (ES6)** | `let` / `const`, arrow functions, classes, template literals, destructuring, spread and rest, modules, promises, `Map` / `Set`, generators |
| **ES2016-2017** | `**` operator, `Array.includes`, `async` / `await`, `Object.entries` / `values` |
| **ES2018-2019** | Object spread, `Promise.finally`, `flat` / `flatMap`, `Object.fromEntries` |
| **ES2020** | Optional chaining `?.`, nullish coalescing `??`, `BigInt`, `Promise.allSettled`, `globalThis`, dynamic `import()` |
| **ES2021** | `replaceAll`, logical assignment operators, `Promise.any`, numeric separators (`1_000`) |
| **ES2022** | Class fields and private `#fields`, top-level `await`, `.at()`, `Object.hasOwn` |
| **ES2023 and later** | `toSorted` / `toReversed`, `findLast`, `Object.groupBy`, `Promise.withResolvers` (check browser support) |

### Tooling Overview

| Tool | Purpose |
|---|---|
| **Node.js and npm** | Run JavaScript outside the browser and install packages |
| **Vite** | Fast dev server and bundler for modern projects |
| **ESLint** | Finds bugs and style problems in your code |
| **Prettier** | Automatic code formatting |
| **TypeScript** | Adds static types on top of JavaScript |
| **Browser DevTools** | Console, debugger, network and performance panels |

---

<a id="checklist"></a>

## 3. Standard Checklist & Best Practices

### ✅ Core Features

- [ ] Variables: `const`, `let` and scope
- [ ] Data types, coercion and equality
- [ ] Operators and control flow
- [ ] Functions: declarations, arrows, parameters, closures
- [ ] Objects, destructuring and spread
- [ ] Arrays and array methods (`map`, `filter`, `reduce`)
- [ ] Strings, template literals, numbers and `Math`
- [ ] Classes, prototypes and `this`
- [ ] Modules (`import` and `export`)
- [ ] Error handling (`try`, `catch`, `throw`)
- [ ] Promises and `async` / `await`
- [ ] `fetch` and JSON
- [ ] DOM selection, manipulation and events
- [ ] Event delegation
- [ ] Web Storage
- [ ] Modern syntax (`?.`, `??`, destructuring)

### 🛠️ Setup Steps

- [ ] Install a code editor such as [VS Code](https://code.visualstudio.com/)
- [ ] Install the **Live Server** extension for instant browser refresh
- [ ] Create a project folder with `index.html` and `script.js`
- [ ] Link the script with `<script src="script.js" defer></script>`
- [ ] Open the browser **Console** (`F12`) to see output and errors
- [ ] Optional: install [Node.js](https://nodejs.org/) to run JavaScript files from the terminal (`node file.js`)
- [ ] Optional: add ESLint and Prettier for cleaner code

### 📋 Best Practices

**Code Quality**
- [ ] Use `const` by default, `let` when needed, and never `var`
- [ ] Always use `===` and `!==`
- [ ] Use clear names: `userList`, `isLoggedIn`, `getTotal()`
- [ ] Keep functions small and focused on one job
- [ ] Avoid global variables, and use modules and block scope
- [ ] Use `"use strict"` (modules are already strict)
- [ ] Prefer array methods and `for...of` over manual index loops where it is clearer
- [ ] Avoid mutating shared data: copy with spread or `structuredClone`
- [ ] Remove unused code and leftover `console.log` calls before shipping
- [ ] Format with Prettier and lint with ESLint

**Async Code**
- [ ] Prefer `async` / `await` over long promise chains
- [ ] Always handle errors with `try` / `catch` or `.catch()`
- [ ] Check `response.ok` after `fetch`
- [ ] Run independent requests in parallel with `Promise.all`
- [ ] Never leave a promise unhandled
- [ ] Show loading and error states in the UI

**DOM & Events**
- [ ] Load scripts with `defer` (or `type="module"`)
- [ ] Select an element once and reuse the reference
- [ ] Use event delegation for lists of items
- [ ] Toggle CSS classes instead of writing inline styles
- [ ] Batch DOM updates (build elements first, then insert once)
- [ ] Remove event listeners you no longer need

**Performance**
- [ ] Debounce or throttle handlers for `scroll`, `resize` and `input`
- [ ] Use `requestAnimationFrame` for animations
- [ ] Avoid reading and writing layout properties repeatedly in a loop
- [ ] Lazy-load heavy code with dynamic `import()`
- [ ] Use Web Workers for heavy calculations
- [ ] Minify and bundle code for production
- [ ] Avoid large dependencies for small tasks

**Accessibility**
- [ ] Use real `<button>` and `<a>` elements instead of clickable `<div>` elements
- [ ] Make sure every interaction works with the keyboard
- [ ] Move focus sensibly after opening or closing dialogs and menus
- [ ] Announce dynamic updates with `aria-live` regions
- [ ] Update `aria-expanded`, `aria-pressed` and similar states when the UI changes
- [ ] Respect `prefers-reduced-motion` in animations

**Security**
- [ ] Never insert untrusted input with `innerHTML`: use `textContent` or sanitize the HTML
- [ ] Never use `eval()` or `new Function()` with dynamic input
- [ ] Never put API keys, passwords or secrets in front-end code
- [ ] Do not store tokens or sensitive data in `localStorage`
- [ ] Always validate data again on the server, since client-side checks can be bypassed
- [ ] Serve everything over HTTPS
- [ ] Use a Content Security Policy (CSP) to limit which scripts can run
- [ ] Add Subresource Integrity (`integrity`) to third-party scripts from a CDN
- [ ] Run `npm audit` and keep dependencies updated

**Quality & Testing**
- [ ] Handle edge cases: empty input, `null`, network failure
- [ ] Write tests for important logic (Vitest or Jest)
- [ ] Check browser support on [Can I use](https://caniuse.com/)
- [ ] Debug with breakpoints in DevTools, not only `console.log`

---

<a id="quickstart"></a>

## 4. Quick Start & Boilerplate Code

Create two files in the same folder: `index.html` and `script.js`. This small to-do app demonstrates DOM handling, events, safe rendering and `localStorage`.

### `index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>JavaScript Starter: To-Do List</title>
  <style>
    body { font-family: system-ui, sans-serif; max-width: 480px; margin: 2rem auto; padding: 0 1rem; }
    li { display: flex; justify-content: space-between; align-items: center; padding: 0.4rem 0; }
    li.done span { text-decoration: line-through; opacity: 0.6; }
  </style>
</head>
<body>
  <main>
    <h1>To-Do List</h1>

    <form id="todo-form">
      <label for="todo-input">New task</label>
      <input id="todo-input" type="text" autocomplete="off" required />
      <button type="submit">Add</button>
    </form>

    <ul id="todo-list"></ul>

    <!-- aria-live announces changes to screen readers -->
    <p id="status" aria-live="polite"></p>
  </main>

  <!-- defer: the script runs after the HTML has been parsed -->
  <script src="script.js" defer></script>
</body>
</html>
```

### `script.js`

```js
"use strict";

// ---------- 1. Select the elements once ----------
const form = document.querySelector("#todo-form");
const input = document.querySelector("#todo-input");
const list = document.querySelector("#todo-list");
const status = document.querySelector("#status");

const STORAGE_KEY = "todos";

// ---------- 2. State ----------
let todos = loadTodos();

// ---------- 3. Storage helpers (wrapped in try/catch: storage can fail) ----------
function loadTodos() {
  try {
    // JSON.parse(null) returns null, so ?? gives an empty array as a fallback
    return JSON.parse(localStorage.getItem(STORAGE_KEY)) ?? [];
  } catch {
    return [];
  }
}

function saveTodos() {
  try {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(todos));
  } catch {
    // Storage can be unavailable or full; the app keeps working without it
  }
}

// ---------- 4. Render the list from the state ----------
function render() {
  list.replaceChildren(); // clear the old items

  for (const todo of todos) {
    const item = document.createElement("li");
    item.dataset.id = todo.id;
    item.classList.toggle("done", todo.done);

    const label = document.createElement("label");

    const checkbox = document.createElement("input");
    checkbox.type = "checkbox";
    checkbox.checked = todo.done;

    const text = document.createElement("span");
    text.textContent = todo.text; // textContent is safe: no HTML is ever parsed

    label.append(checkbox, text);

    const remove = document.createElement("button");
    remove.type = "button";
    remove.className = "remove";
    remove.textContent = "Delete";
    remove.setAttribute("aria-label", `Delete task: ${todo.text}`);

    item.append(label, remove);
    list.append(item);
  }

  const remaining = todos.filter((todo) => !todo.done).length;
  status.textContent = `${remaining} task(s) left`;
}

// ---------- 5. Events ----------
// Add a task
form.addEventListener("submit", (event) => {
  event.preventDefault(); // stop the page from reloading

  const text = input.value.trim();
  if (!text) return;

  todos.push({ id: Date.now(), text, done: false });
  saveTodos();
  render();

  input.value = "";
  input.focus();
});

// Delete a task (event delegation: one listener for the whole list)
list.addEventListener("click", (event) => {
  const button = event.target.closest(".remove");
  if (!button) return;

  const id = Number(button.closest("li").dataset.id);
  todos = todos.filter((todo) => todo.id !== id);
  saveTodos();
  render();
});

// Mark a task as done or not done
list.addEventListener("change", (event) => {
  if (!event.target.matches('input[type="checkbox"]')) return;

  const id = Number(event.target.closest("li").dataset.id);
  todos = todos.map((todo) =>
    todo.id === id ? { ...todo, done: event.target.checked } : todo
  );
  saveTodos();
  render();
});

// ---------- 6. First render ----------
render();
```

**What this starter demonstrates:** `const` and `let`, functions, arrays and array methods (`filter`, `map`), objects with spread, template literals, `try` / `catch`, DOM creation and safe rendering with `textContent`, event delegation, `localStorage` with `JSON`, the nullish operator `??`, and accessible labels and live regions.

---

<a id="resources"></a>

## 5. Official Documentation & Resources

### 📚 Official Documentation

| Resource | Description | Link |
|---|---|---|
| MDN Web Docs: JavaScript | The most complete JavaScript reference and guides | [![MDN](https://img.shields.io/badge/MDN-JavaScript%20Docs-000000?style=for-the-badge&logo=mdnwebdocs&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/JavaScript) |
| ECMAScript Specification | The official language standard | [![ECMAScript](https://img.shields.io/badge/ECMAScript-Spec-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://tc39.es/ecma262/) |
| TC39 Proposals | Upcoming language features | [![TC39](https://img.shields.io/badge/TC39-Proposals-2F81F7?style=for-the-badge)](https://github.com/tc39/proposals) |
| Can I use | Browser support tables | [![Can I use](https://img.shields.io/badge/Can%20I%20use-Browser%20Support-F38020?style=for-the-badge)](https://caniuse.com/) |

### 🎓 Recommended Tutorials

| Resource | Description | Link |
|---|---|---|
| The Modern JavaScript Tutorial | Free, in-depth guide from basics to advanced | [![javascript.info](https://img.shields.io/badge/javascript.info-Tutorial-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://javascript.info/) |
| MDN: Learn JavaScript | Beginner-friendly learning path | [![MDN Learn](https://img.shields.io/badge/MDN-Learn%20JavaScript-F38020?style=for-the-badge&logo=mdnwebdocs&logoColor=white)](https://developer.mozilla.org/en-US/docs/Learn/JavaScript) |
| Eloquent JavaScript | Free online book | [![Eloquent JavaScript](https://img.shields.io/badge/Book-Eloquent%20JavaScript-3FB950?style=for-the-badge)](https://eloquentjavascript.net/) |
| You Don't Know JS Yet | Deep-dive book series on the language | [![YDKJS](https://img.shields.io/badge/Book-You%20Don't%20Know%20JS-3FB950?style=for-the-badge)](https://github.com/getify/You-Dont-Know-JS) |

### 🎮 Practice Platforms

| Resource | Description | Link |
|---|---|---|
| freeCodeCamp | Free interactive JavaScript curriculum | [![freeCodeCamp](https://img.shields.io/badge/freeCodeCamp-Practice-0A0A23?style=for-the-badge&logo=freecodecamp&logoColor=white)](https://www.freecodecamp.org/) |
| Exercism: JavaScript track | Coding exercises with mentoring | [![Exercism](https://img.shields.io/badge/Exercism-JavaScript%20Track-009CAB?style=for-the-badge)](https://exercism.org/tracks/javascript) |
| JavaScript30 | 30 projects in 30 days with vanilla JavaScript | [![JavaScript30](https://img.shields.io/badge/JavaScript30-Projects-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://javascript30.com/) |

### 🔗 Related Pages

<p align="center">
  <a href="./cheat-sheet.md"><img src="https://img.shields.io/badge/JavaScript-Cheat%20Sheet-F38020?style=for-the-badge" alt="JavaScript Cheat Sheet" /></a>
  <a href="./notes.md"><img src="https://img.shields.io/badge/JavaScript-Notes-3FB950?style=for-the-badge" alt="JavaScript Notes" /></a>
</p>