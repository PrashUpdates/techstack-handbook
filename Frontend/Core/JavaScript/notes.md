# 📝 JavaScript (ES6+) Notes

<p align="center">
  <a href="https://github.com/PrashUpdates/techstack-handbook/blob/main/README.md#frontend"><img src="https://img.shields.io/badge/Back%20to%20main-6E7681?style=for-the-badge" alt="Back to main" /></a>
  <a href="./docs.md"><img src="https://img.shields.io/badge/Docs-2F81F7?style=for-the-badge" alt="Docs" /></a>
  <a href="./cheat-sheet.md"><img src="https://img.shields.io/badge/Cheat%20Sheet-F38020?style=for-the-badge" alt="Cheat Sheet" /></a>
</p>

> Study notes, mental models, common mistakes, practice exercises and mini projects to use alongside the JavaScript docs.

**Jump to:**
[Key Takeaways](#takeaways) · [Mental Models](#models) · [Common Mistakes](#mistakes) · [Quick Tips](#tips) · [Roadmap](#roadmap) · [Exercises](#exercises) · [Mini Projects](#projects) · [Self-Check](#selfcheck) · [Glossary](#glossary) · [FAQ](#faq)

---

<a id="takeaways"></a>

## 🧠 Key Takeaways

- JavaScript adds **behavior** to a page: it reacts to users, changes content and talks to servers
- Use `const` by default, `let` when a value must change, and avoid `var`
- Always compare with `===` instead of `==`
- Functions are **values**: you can store them, pass them and return them
- **Primitives** are copied by value, **objects and arrays** are copied by reference
- A **closure** lets a function remember the variables from where it was created
- The value of `this` depends on **how a function is called**, and arrow functions take it from the surrounding scope
- JavaScript runs on **one thread**, and the **event loop** handles waiting tasks such as timers and network requests
- Prefer **`async` / `await`** for asynchronous code, and always handle errors
- `fetch` does not reject on a 404 or 500, so check `response.ok`
- Use `textContent` for user-provided text, never `innerHTML`
- Use **event delegation** for lists of items
- Copy objects and arrays instead of changing the original
- Never put secrets or passwords in front-end code or `localStorage`
- Use **DevTools** (`F12`) and the Console to read errors and debug

---

<a id="models"></a>

## 🧭 Mental Models

### 1. One thread, one task at a time

JavaScript has a single call stack, so it runs one piece of code at a time. Slow tasks (network, timers) are handed to the browser, and their results come back through queues, so the page does not freeze.

Think of a **restaurant with one chef**. The chef cooks one dish at a time, while the kitchen timer and the delivery driver work in the background. When they finish, they wait in line until the chef is free.

```js
console.log("1: synchronous");
setTimeout(() => console.log("4: timer (macrotask)"), 0);
Promise.resolve().then(() => console.log("3: promise (microtask)"));
console.log("2: synchronous");
// Order: 1, 2, 3, 4
```

| Queue | What goes in | When it runs |
|---|---|---|
| Call stack | The code running now | Immediately |
| Microtask queue | Promise callbacks | As soon as the stack is empty |
| Macrotask queue | Timers, events, network callbacks | One per turn of the loop, after microtasks |

### 2. Values versus references

```js
// Primitives: copied by value
let a = 5;
let b = a;
b = 10;
console.log(a); // 5

// Objects and arrays: copied by reference
const user1 = { name: "Ada" };
const user2 = user1;       // both names point to the same object
user2.name = "Grace";
console.log(user1.name);   // "Grace"

// Make a real copy
const shallow = { ...user1 };
const deep = structuredClone(user1);
```

### 3. A closure is a backpack

When a function is created, it packs the variables around it into a "backpack" and carries them wherever it goes, even after the outer function has finished.

```js
function makeCounter() {
  let count = 0;
  return () => ++count;   // carries `count` in its backpack
}
const counter = makeCounter();
counter(); // 1
counter(); // 2
```

### 4. `this` depends on the call, not the definition

| How the function is called | `this` is |
|---|---|
| `object.method()` | `object` |
| Plain function call | `undefined` in strict mode and modules |
| Arrow function | The `this` of the surrounding scope |
| `new Thing()` | The new object |
| `fn.call(x)` / `fn.bind(x)` | `x` |

**Rule of thumb:** regular methods on objects and classes, arrow functions for callbacks.

### 5. A Promise is a receipt

A Promise is like a receipt for a value you will get later. It is **pending** at first, then either **fulfilled** (you got the value) or **rejected** (something went wrong). `await` simply pauses your function until the receipt is settled.

```js
async function loadUser() {
  try {
    const response = await fetch("/api/user");
    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    return await response.json();
  } catch (error) {
    console.error(error.message);
  }
}
```

### 6. The DOM is a tree you edit

The browser reads your HTML and builds a **tree of objects**. JavaScript edits that tree, and the browser redraws the page. Your HTML file itself never changes. Refresh the page and the changes are gone, unless you saved them somewhere (such as `localStorage` or a server).

### 7. State in, page out

A clean way to build interactive pages:

```
state (data)  →  render()  →  what the user sees
     ↑                              │
     └──────── event handler ←──────┘  (user clicks, types, submits)
```

1. Keep your data in a variable (the **state**)
2. Write a `render()` function that draws the page from that state
3. When something happens, update the state, then call `render()` again

This is the idea behind frameworks like React, and it keeps vanilla JavaScript organized too.

### 8. Pick the right array method with a question

```
Do I want a new array with every item changed?   → map
Do I want only some of the items?                → filter
Do I want one single result from all items?      → reduce
Do I want the first match?                       → find
Do I just want to do something for each item?    → for...of or forEach
Do I want to know if any/all items match?        → some / every
```

---

<a id="mistakes"></a>

## ⚠️ Common Mistakes

| Mistake | Fix |
|---|---|
| Using `==` and getting surprising results | Use `===` |
| Using `var` | Use `const` or `let` |
| Forgetting `await` | Without it you get a pending Promise, not the data |
| `fetch` seems to succeed on a 404 | Check `response.ok` yourself |
| `JSON.parse` crashes on bad input | Wrap it in `try` / `catch` |
| `[10, 2, 1].sort()` gives the wrong order | Pass a compare function: `sort((a, b) => a - b)` |
| `0.1 + 0.2` is not `0.3` | Round before showing, or work in whole units such as cents |
| `typeof null` returns `"object"` | Check with `value === null` |
| `NaN === NaN` is `false` | Use `Number.isNaN(value)` |
| `parseInt` without a radix | Write `parseInt(value, 10)` |
| `forEach` with `await` does not wait | Use `for...of`, or `Promise.all` with `map` |
| The script runs before the HTML is ready | Add `defer` to the script tag |
| `document.querySelector` returns `null` | The element does not exist yet, or the selector is wrong |
| `this` is `undefined` inside a callback | Use an arrow function or `.bind(this)` |
| Arrow function used as an object method | Use a regular method so `this` points to the object |
| Changing an object or array that is shared | Copy it with spread or `structuredClone` |
| Spread copy still shares nested objects | Use `structuredClone` for a deep copy |
| Returning an object literal from an arrow gives `undefined` | Wrap it in parentheses: `() => ({ a: 1 })` |
| Adding a listener to every item in a loop | Use event delegation on the parent |
| Using `innerHTML` with user input | Use `textContent`, or sanitize the HTML |
| Using `eval()` | Avoid it: parse data with `JSON.parse` instead |
| Date month is off by one | Months start at `0` (January is `0`) |
| Mutating state and not re-rendering | Update the state, then call `render()` |
| Infinite loop or recursion with no base case | Make sure every loop and recursive call can finish |
| Storing passwords or tokens in `localStorage` | Never do this: any script on the page can read it |
| Ignoring console errors | Read the first error message and line number carefully |

---

<a id="tips"></a>

## 💡 Quick Tips

- Read the **error type** first: `ReferenceError`, `TypeError` and `SyntaxError` point to different causes
- Use `console.table()` to inspect arrays of objects
- Use `debugger;` or DevTools breakpoints instead of many `console.log` lines
- Use `?.` and `??` to handle missing data safely: `user?.address?.city ?? "Unknown"`
- Use destructuring to keep code short: `const { name, age } = user;`
- Use template literals instead of joining strings with `+`
- Use `Array.from({ length: 5 }, (_, i) => i)` to create a range of numbers
- Use `[...new Set(array)]` to remove duplicates
- Use `Object.entries()` with `for...of` to loop over an object
- Use `structuredClone()` for a deep copy
- Use `array.at(-1)` to get the last item
- Name booleans like questions: `isLoggedIn`, `hasError`, `canEdit`
- Keep functions short and give each one a single job
- Write a small test in the Console before adding code to your project
- Debounce `input` and `scroll` handlers so they do not run too often
- Run a formatter (Prettier) and a linter (ESLint) to catch problems early

---

<a id="roadmap"></a>

## 🗺️ Learning Roadmap

Work through the stages in order. Each stage builds on the one before it.

**Stage 1: Foundations**
- [ ] Add JavaScript to a page (`<script defer>`) and use the Console
- [ ] Variables: `const`, `let` and naming
- [ ] Data types, `typeof` and type conversion
- [ ] Operators, `===` and truthy and falsy values
- [ ] Conditions: `if`, `else`, ternary, `switch`
- [ ] Loops: `for`, `while`, `for...of`

**Stage 2: Core Language**
- [ ] Functions: declarations, arrows, parameters, return values
- [ ] Scope, hoisting and closures
- [ ] Objects, destructuring and spread
- [ ] Arrays and the main array methods
- [ ] Strings, numbers, `Math` and dates
- [ ] Error handling with `try`, `catch` and `throw`

**Stage 3: The Browser**
- [ ] Selecting and changing DOM elements
- [ ] Events, event delegation and forms
- [ ] `localStorage` and `sessionStorage`
- [ ] Browser APIs: timers, URL, clipboard, Intersection Observer

**Stage 4: Asynchronous JavaScript**
- [ ] The event loop, callbacks and timers
- [ ] Promises and `async` / `await`
- [ ] `fetch`, JSON and working with APIs
- [ ] Loading, error and empty states in the interface

**Stage 5: Modern and Professional**
- [ ] Modules with `import` and `export`
- [ ] Classes, `this` and prototypes
- [ ] Tooling: Node.js, npm, Vite, ESLint and Prettier
- [ ] Testing basics with Vitest or Jest
- [ ] Security, performance and accessibility habits
- [ ] Next step: TypeScript and a framework such as React

---

<a id="exercises"></a>

## 🧪 Practice Exercises

**🟢 Beginner**
- [ ] Print your name and age with a template literal
- [ ] Write a function that returns the larger of two numbers
- [ ] Loop from 1 to 20 and print "Fizz" for multiples of 3, "Buzz" for multiples of 5
- [ ] Reverse a string and check if a word is a palindrome
- [ ] Find the largest number in an array without using `Math.max`
- [ ] Change the text and color of a heading when a button is clicked

**🟡 Intermediate**
- [ ] Use `map`, `filter` and `reduce` to total the prices of in-stock products
- [ ] Count how many times each word appears in a sentence
- [ ] Remove duplicates from an array in two different ways
- [ ] Build a character counter for a textarea that updates as you type
- [ ] Validate a signup form and show error messages next to each field
- [ ] Fetch a list from a public API and show it as cards
- [ ] Save a theme choice (light or dark) in `localStorage`

**🔴 Challenge**
- [ ] Write your own `debounce` function and use it in a search box
- [ ] Build a function that flattens a deeply nested array without `flat`
- [ ] Write `Promise.all` from scratch using `new Promise`
- [ ] Create a simple event emitter class with `on`, `off` and `emit`
- [ ] Build a tiny state manager: `getState`, `setState`, `subscribe`
- [ ] Implement an infinite scroll list with Intersection Observer

---

<a id="projects"></a>

## 🛠️ Mini Projects

| Project | Skills practiced | Level |
|---|---|---|
| Counter and color changer | Variables, events, DOM | 🟢 Beginner |
| Tip calculator | Numbers, forms, functions | 🟢 Beginner |
| Digital clock | Dates, `setInterval` | 🟢 Beginner |
| To-do list | Arrays, DOM, events, `localStorage` | 🟡 Intermediate |
| Quiz app | Objects, arrays, state, score logic | 🟡 Intermediate |
| Weather app | `fetch`, `async` / `await`, error states | 🟡 Intermediate |
| Expense tracker | Array methods, forms, storage | 🟡 Intermediate |
| Image gallery with modal | Events, delegation, accessibility | 🟡 Intermediate |
| Memory card game | State, timers, game logic | 🔴 Challenge |
| Kanban board | Drag and drop, state, storage | 🔴 Challenge |
| Markdown previewer | Strings, regular expressions, DOM | 🔴 Challenge |

**How to approach each project**

1. Write down what the app must do in plain sentences
2. Sketch the layout and write the HTML structure first
3. Decide what the **state** is (the data that changes)
4. Write a `render()` function that draws the page from the state
5. Add event handlers that update the state and call `render()`
6. Handle edge cases: empty input, network failure, no results
7. Save data with `localStorage` if it should survive a refresh
8. Test with the keyboard only, and check the Console for errors

---

<a id="selfcheck"></a>

## ✅ Self-Check

You are comfortable with JavaScript basics if you can:

- [ ] Explain the difference between `const`, `let` and `var`
- [ ] Explain why `===` is safer than `==`
- [ ] List the falsy values from memory
- [ ] Explain the difference between copying a value and copying a reference
- [ ] Write a closure and explain what it remembers
- [ ] Predict the value of `this` in a method, an arrow function and a callback
- [ ] Choose between `map`, `filter`, `reduce` and `find` for a task
- [ ] Use destructuring, spread and rest in real code
- [ ] Explain the order of synchronous code, promises and `setTimeout`
- [ ] Fetch data with `async` / `await`, check `response.ok` and handle errors
- [ ] Select, create, change and remove DOM elements
- [ ] Use event delegation on a list
- [ ] Store and read an object with `localStorage` and `JSON`
- [ ] Explain why `innerHTML` with user input is dangerous
- [ ] Read an error message in the Console and find the line that caused it

---

<a id="glossary"></a>

## 📖 Glossary

| Term | Meaning |
|---|---|
| **ECMAScript (ES)** | The official standard that JavaScript follows |
| **ES6 / ES2015** | The big 2015 update that added `let`, `const`, classes, modules and promises |
| **Engine** | The program that runs JavaScript, such as V8 |
| **Runtime** | The environment around the engine: a browser or Node.js |
| **Call stack** | Where the engine keeps track of the function currently running |
| **Event loop** | The mechanism that moves finished async tasks back onto the call stack |
| **Callback** | A function passed to another function to be called later |
| **Promise** | An object that represents a value you will get in the future |
| **`async` / `await`** | Syntax that makes promise-based code read like normal code |
| **Scope** | The area where a variable can be used |
| **Hoisting** | Declarations being processed before the code runs |
| **Closure** | A function together with the variables it remembers |
| **Higher-order function** | A function that takes or returns another function |
| **Pure function** | A function with no side effects that always gives the same output for the same input |
| **Mutation** | Changing an existing object or array instead of creating a new one |
| **Immutable** | Not changed after creation; you make a new copy instead |
| **Destructuring** | Pulling values out of arrays or objects into variables |
| **Spread / rest** | The `...` syntax for expanding or collecting values |
| **Prototype** | The object that another object inherits properties from |
| **Module** | A file with its own scope that uses `import` and `export` |
| **DOM** | The tree of objects the browser builds from your HTML |
| **Event bubbling** | An event traveling up from the clicked element to its ancestors |
| **Event delegation** | Listening on a parent element to handle events from its children |
| **Debounce** | Waiting until activity stops before running a function |
| **Throttle** | Limiting a function to run at most once per time interval |
| **JSON** | A text format for sending and storing data |
| **API** | A set of rules for talking to another program or server |
| **Transpiler / bundler** | Tools that convert and combine code for browsers (Babel, Vite, Webpack) |
| **Linter** | A tool that finds bugs and style problems, such as ESLint |
| **Polyfill** | Code that adds a missing feature to an older browser |

---

<a id="faq"></a>

## ❓ Frequently Asked Questions

**Is JavaScript the same as Java?**
No. They are completely different languages. The names are similar only for historical marketing reasons.

**What does ES6+ mean?**
ES6 (also called ES2015) was a major update that added `let`, `const`, arrow functions, classes, modules, promises and more. ES6+ means ES6 and every yearly version after it. When people say "modern JavaScript", this is what they mean.

**What is the difference between `var`, `let` and `const`?**
`const` cannot be reassigned, `let` can, and both are block-scoped. `var` is function-scoped, can be redeclared and behaves in surprising ways, so avoid it. Start with `const` and switch to `let` only when a value must change.

**Does `const` make a value unchangeable?**
No. It stops the variable from being reassigned, but an object or array stored in a `const` can still be changed. Use `Object.freeze()` if you need a read-only object.

**What is the difference between `==` and `===`?**
`==` converts types before comparing, which gives surprising results such as `0 == "0"`. `===` compares value and type, so it is predictable. Always use `===`.

**What is the difference between `null` and `undefined`?**
`undefined` means a variable has no value yet. `null` means "no value" on purpose. Check them together with `value == null`, or use `??` and `?.` to handle both safely.

**What is a closure?**
A closure is a function that keeps access to the variables from the scope where it was created, even after that scope has finished. It is used for private data, counters and callbacks.

**What is hoisting?**
JavaScript processes declarations before it runs the code. Function declarations can be used before they appear, `var` variables exist but are `undefined`, and `let` and `const` cannot be used before their line (the temporal dead zone).

**What is the difference between `map` and `forEach`?**
`map` returns a **new array** with a changed value for every item. `forEach` returns nothing and is only for side effects, such as logging. Use `map` when you need the result.

**What is the difference between a callback, a promise and `async` / `await`?**
They are three ways to handle code that finishes later. Callbacks are the original style and become hard to read when nested. Promises are chainable with `.then()` and `.catch()`. `async` / `await` is built on promises and reads like normal top-to-bottom code, so it is the preferred style.

**Why does `0.1 + 0.2` not equal `0.3`?**
JavaScript uses binary floating point numbers, which cannot store some decimals exactly. Round the result for display (`toFixed(2)`), or work in whole units such as cents.

**Why is my code in the `<head>` not finding elements?**
The script runs before the HTML below it has been created. Add `defer` to the script tag (or use `type="module"`), or place the script just before `</body>`.

**Why does `fetch` not throw an error for a 404?**
`fetch` only rejects when the network request itself fails. A 404 or 500 is still a completed response, so check `response.ok` and throw your own error.

**Why does my loop with `await` inside `forEach` not wait?**
`forEach` does not wait for async callbacks. Use `for...of` for one-after-another work, or `await Promise.all(array.map(...))` to run everything in parallel.

**What is the difference between `localStorage` and `sessionStorage`?**
`localStorage` keeps data until it is cleared, even after the browser closes. `sessionStorage` is cleared when the tab closes. Both store only text, and both can be read by any script on the page, so never store secrets in them.

**What does `use strict` do?**
It turns on stricter rules that turn some silent mistakes into errors, such as using an undeclared variable. Modules and classes are strict by default.

**Do I need a framework like React to build real apps?**
No. Learn plain JavaScript first, because frameworks are built on it. After that, a framework helps manage larger interfaces and shared state.

**What is the difference between JavaScript in the browser and Node.js?**
The language is the same. The browser provides the DOM, `window` and `fetch` for working with pages. Node.js provides files, the network and the operating system, but no DOM.

**Should I learn TypeScript?**
Yes, after you are comfortable with JavaScript. TypeScript is JavaScript with types, and it catches many bugs before your code runs.

**How do I find out why my code is not working?**
Open the Console (`F12`) and read the first error message with its line number. Then check the types and values with `console.log` or `console.table`, set a breakpoint in the Sources tab, and test small pieces separately. Also check for typos, missing brackets and a wrong file path.