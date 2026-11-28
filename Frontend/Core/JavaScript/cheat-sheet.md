# ⚡ JavaScript (ES6+) Cheat Sheet

<p align="center">
  <a href="https://github.com/PrashUpdates/techstack-handbook/blob/main/README.md#frontend"><img src="https://img.shields.io/badge/Back%20to%20main-6E7681?style=for-the-badge" alt="Back to main" /></a>
  <a href="./docs.md"><img src="https://img.shields.io/badge/Docs-2F81F7?style=for-the-badge" alt="Docs" /></a>
  <a href="./notes.md"><img src="https://img.shields.io/badge/Notes-3FB950?style=for-the-badge" alt="Notes" /></a>
</p>

> A quick reference for modern JavaScript: syntax, data structures, functions, async code, the DOM, browser APIs and ready-to-copy patterns.

**Jump to:**
[Basics](#basics) · [Variables](#variables) · [Types](#types) · [Operators](#operators) · [Conversion](#conversion) · [Control Flow](#control) · [Functions](#functions) · [Scope & this](#scope) · [Objects](#objects) · [Classes](#classes) · [Arrays](#arrays) · [Strings](#strings) · [Numbers & Math](#numbers) · [Set & Map](#collections) · [Dates](#dates) · [JSON](#json) · [Destructuring](#destructuring) · [Modules](#modules) · [Errors](#errors) · [Async](#async) · [DOM](#dom) · [Events](#events) · [Browser APIs](#apis) · [Regex](#regex) · [Console](#console) · [Snippets](#snippets) · [Mistakes](#mistakes) · [Debugging](#debugging)

---

<a id="basics"></a>

## 🧱 Basics & Syntax

```js
// Single-line comment
/* Multi-line comment */

console.log("Hello, World!");
```

| Rule | Detail |
|---|---|
| Case-sensitive | `name` and `Name` are different |
| Statements | End with `;` (be consistent) |
| Naming | `camelCase` variables and functions, `PascalCase` classes, `UPPER_SNAKE_CASE` constants |
| Strict mode | `"use strict";` at the top (modules are strict automatically) |

| Add JavaScript to HTML | Code |
|---|---|
| External (best) | `<script src="script.js" defer></script>` |
| ES module | `<script type="module" src="main.js"></script>` |
| Internal | `<script> ... </script>` |

---

<a id="variables"></a>

## 📦 Variables

| Keyword | Scope | Reassign | Redeclare | Use |
|---|---|---|---|---|
| `const` | Block | No | No | **Default** |
| `let` | Block | Yes | No | When the value changes |
| `var` | Function | Yes | Yes | Avoid |

```js
const PI = 3.14159;
let count = 0;
count += 1;

const user = { name: "Ada" };
user.name = "Grace";   // allowed: const protects the binding, not the contents
```

---

<a id="types"></a>

## 🔤 Data Types

| Type | Example |
|---|---|
| `string` | `"text"`, `'text'`, `` `text` `` |
| `number` | `42`, `3.14`, `NaN`, `Infinity` |
| `bigint` | `123n` |
| `boolean` | `true`, `false` |
| `undefined` | Variable with no value |
| `null` | Intentional empty value |
| `symbol` | `Symbol("id")` |
| `object` | `{}`, `[]`, functions, dates |

```js
typeof "a";            // "string"
typeof 1;              // "number"
typeof undefined;      // "undefined"
typeof null;           // "object"   (historic quirk)
typeof [];             // "object"
Array.isArray([]);     // true
typeof (() => {});     // "function"
```

**Falsy values:** `false`, `0`, `-0`, `0n`, `""`, `null`, `undefined`, `NaN`. Everything else is truthy (including `"0"`, `[]`, `{}`).

---

<a id="operators"></a>

## ➕ Operators

| Group | Operators |
|---|---|
| Arithmetic | `+` `-` `*` `/` `%` `**` `++` `--` |
| Comparison | `===` `!==` `>` `<` `>=` `<=` |
| Assignment | `=` `+=` `-=` `*=` `/=` `%=` `**=` |
| Logical assignment | `&&=` `??=` and the OR version |
| Nullish | `??` returns the right side only for `null` or `undefined` |
| Optional chaining | `?.` stops safely on `null` or `undefined` |
| Ternary | `condition ? a : b` |
| Spread / rest | `...` |
| Type check | `typeof`, `instanceof` |

```js
// Logical operators
a && b      // AND: returns b if a is truthy, otherwise a
a || b      // OR:  returns a if a is truthy, otherwise b
!a          // NOT

// Nullish vs OR
0 || 10     // 10   (0 is falsy)
0 ?? 10     // 0    (0 is not null or undefined)

// Optional chaining
const city = user?.address?.city ?? "Unknown";
const first = list?.[0];
const result = obj.method?.();
```

| Equality | Behavior |
|---|---|
| `===` | Value and type must match (**use this**) |
| `==` | Converts types first (avoid) |
| `Object.is(a, b)` | Like `===`, but `NaN` equals `NaN` |

---

<a id="conversion"></a>

## 🔄 Type Conversion

| To | Code | Notes |
|---|---|---|
| Number | `Number("42")` | `Number("abc")` is `NaN` |
| Number (parse) | `parseInt("42px", 10)` / `parseFloat("3.5")` | Reads until a non-digit |
| Number (shortcut) | `+"42"` | |
| String | `String(42)` / `(42).toString()` / `` `${42}` `` | |
| Boolean | `Boolean(value)` / `!!value` | |
| Array | `Array.from("abc")` / `[..."abc"]` | |
| Array from object | `Object.entries(obj)` | |

```js
Number.isNaN(NaN);        // true  (reliable check)
Number.isInteger(5);      // true
Number.isFinite(10);      // true
```

---

<a id="control"></a>

## 🔀 Control Flow

```js
// if / else
if (score >= 90) {
  grade = "A";
} else if (score >= 80) {
  grade = "B";
} else {
  grade = "C";
}

// Ternary
const label = isOn ? "On" : "Off";

// switch
switch (day) {
  case 1:
    name = "Mon";
    break;
  case 2:
    name = "Tue";
    break;
  default:
    name = "Other";
}
```

| Loop | Example |
|---|---|
| `for` | `for (let i = 0; i < 5; i++) { ... }` |
| `for...of` | `for (const item of array) { ... }` (values of any iterable) |
| `for...in` | `for (const key in object) { ... }` (keys of an object) |
| `while` | `while (condition) { ... }` |
| `do...while` | `do { ... } while (condition);` |
| `forEach` | `array.forEach((item, index) => { ... });` |
| `break` / `continue` | Exit the loop / skip to the next round |

```js
for (const [key, value] of Object.entries(obj)) {
  console.log(key, value);
}

for (const [index, item] of array.entries()) {
  console.log(index, item);
}
```

---

<a id="functions"></a>

## 🧩 Functions

```js
// Declaration (hoisted)
function add(a, b) {
  return a + b;
}

// Expression
const multiply = function (a, b) { return a * b; };

// Arrow function
const square = (n) => n * n;
const greet = (name) => `Hello, ${name}!`;
const getUser = () => ({ name: "Ada" });   // return an object literal: wrap it in ()

// Default, rest and spread
function hello(name = "friend") { return `Hi, ${name}`; }
function sum(...numbers) { return numbers.reduce((t, n) => t + n, 0); }
Math.max(...[3, 9, 4]);

// Immediately invoked function expression (IIFE)
(() => { /* private scope */ })();
```

| Concept | Meaning |
|---|---|
| Parameter vs argument | Parameters are in the definition, arguments are the passed values |
| Return value | No `return` gives back `undefined` |
| Callback | A function passed to another function to run later |
| Higher-order function | Takes or returns a function (`map`, `filter`) |
| Pure function | Same input gives the same output, with no side effects |
| Recursion | A function that calls itself (needs a base case) |

---

<a id="scope"></a>

## 🎯 Scope, Closures & `this`

| Concept | Rule |
|---|---|
| Block scope | `let` and `const` live inside `{ }` |
| Function scope | `var` lives inside the whole function |
| Global scope | Avoid adding globals |
| Hoisting | Function declarations are usable early, `var` is `undefined` early, `let` and `const` are in the temporal dead zone |

```js
// Closure: the inner function remembers the outer variable
function createCounter() {
  let count = 0;
  return () => ++count;
}
const next = createCounter();
next(); // 1
next(); // 2
```

| How the function is called | `this` is |
|---|---|
| `obj.method()` | `obj` |
| Plain function call | `undefined` in strict mode, otherwise the global object |
| Arrow function | Taken from the surrounding scope |
| `new Foo()` | The new object |
| `fn.call(x, a)` / `fn.apply(x, [a])` / `fn.bind(x)` | `x` |

---

<a id="objects"></a>

## 🗂️ Objects

```js
const user = {
  name: "Ada",
  age: 36,
  greet() { return `Hi, I am ${this.name}`; },
};

user.name;              // dot access
user["age"];            // bracket access
user.email = "a@b.c";   // add
delete user.age;        // remove
"name" in user;         // true
```

| Method | Purpose |
|---|---|
| `Object.keys(obj)` | Array of keys |
| `Object.values(obj)` | Array of values |
| `Object.entries(obj)` | Array of `[key, value]` |
| `Object.fromEntries(pairs)` | Build an object from pairs |
| `Object.assign(target, src)` | Copy properties |
| `Object.freeze(obj)` | Make it read-only (shallow) |
| `Object.hasOwn(obj, key)` | Has its own property? |
| `structuredClone(obj)` | Deep copy |

```js
const copy = { ...user, role: "admin" };       // shallow copy with a new field
const key = "color";
const item = { [key]: "red" };                 // computed key
const x = 1, y = 2;
const point = { x, y };                        // shorthand: { x: 1, y: 2 }
```

---

<a id="classes"></a>

## 🏛️ Classes

```js
class Animal {
  #energy = 10;                    // private field
  static kingdom = "Animalia";     // belongs to the class

  constructor(name) {
    this.name = name;
  }

  speak() {
    return `${this.name} makes a sound.`;
  }

  get energy() { return this.#energy; }
  set energy(value) { this.#energy = value; }

  static create(name) { return new Animal(name); }
}

class Dog extends Animal {
  speak() {
    return `${super.speak()} Woof!`;
  }
}

const dog = new Dog("Rex");
dog instanceof Animal;   // true
```

---

<a id="arrays"></a>

## 📚 Arrays

```js
const nums = [1, 2, 3, 4, 5];

nums.map((n) => n * 2);               // [2, 4, 6, 8, 10]
nums.filter((n) => n % 2 === 0);      // [2, 4]
nums.reduce((sum, n) => sum + n, 0);  // 15
nums.find((n) => n > 3);              // 4
nums.findIndex((n) => n > 3);         // 3
nums.some((n) => n > 4);              // true
nums.every((n) => n > 0);             // true
nums.includes(3);                     // true
```

| Task | Method |
|---|---|
| Add to end / remove from end | `push(x)` / `pop()` |
| Add to start / remove from start | `unshift(x)` / `shift()` |
| Insert or remove in the middle | `splice(start, deleteCount, ...items)` |
| Copy a part | `slice(start, end)` |
| Join arrays | `concat(b)` or `[...a, ...b]` |
| Join into text | `join(", ")` |
| Find position | `indexOf(x)` / `lastIndexOf(x)` |
| Last item | `arr.at(-1)` |
| Flatten | `flat(depth)` / `flatMap(fn)` |
| Sort | `sort((a, b) => a - b)` |
| Reverse | `reverse()` |
| Fill | `fill(value)` |
| Create | `Array.from({ length: 5 }, (_, i) => i)` |
| Check | `Array.isArray(x)` |

| Changes the original | Returns a new array |
|---|---|
| `push`, `pop`, `shift`, `unshift` | `map`, `filter`, `slice`, `concat` |
| `splice`, `sort`, `reverse`, `fill` | `flat`, `flatMap`, spread |
| | `toSorted`, `toReversed`, `toSpliced`, `with` (newer browsers) |

```js
// Sort
[10, 2, 33].sort();                       // [10, 2, 33]  (sorts as text!)
[10, 2, 33].sort((a, b) => a - b);        // [2, 10, 33]
people.sort((a, b) => a.name.localeCompare(b.name));

// Remove duplicates
const unique = [...new Set(array)];

// Group and count
const counts = array.reduce((acc, x) => {
  acc[x] = (acc[x] ?? 0) + 1;
  return acc;
}, {});
```

---

<a id="strings"></a>

## 📝 Strings

```js
const name = "Ada";
const message = `Hello, ${name}! 2 + 2 = ${2 + 2}`;   // template literal
```

| Method | Example | Result |
|---|---|---|
| `length` | `"hello".length` | `5` |
| `toUpperCase()` / `toLowerCase()` | `"Hi".toUpperCase()` | `"HI"` |
| `trim()` | `"  hi  ".trim()` | `"hi"` |
| `includes()` | `"hello".includes("ell")` | `true` |
| `startsWith()` / `endsWith()` | `"hello".startsWith("he")` | `true` |
| `indexOf()` | `"hello".indexOf("l")` | `2` |
| `slice(start, end)` | `"hello".slice(1, 3)` | `"el"` |
| `split()` | `"a-b-c".split("-")` | `["a", "b", "c"]` |
| `replace()` / `replaceAll()` | `"aaa".replaceAll("a", "b")` | `"bbb"` |
| `repeat()` | `"ab".repeat(2)` | `"abab"` |
| `padStart()` / `padEnd()` | `"5".padStart(3, "0")` | `"005"` |
| `at()` | `"hello".at(-1)` | `"o"` |
| `charAt()` | `"hello".charAt(0)` | `"h"` |
| `localeCompare()` | `"a".localeCompare("b")` | `-1` |

Strings are **immutable**: methods return a new string and never change the original.

---

<a id="numbers"></a>

## 🔢 Numbers & Math

| Task | Code |
|---|---|
| Round | `Math.round(2.5)` gives `3` |
| Round down / up | `Math.floor(2.9)` / `Math.ceil(2.1)` |
| Remove decimals | `Math.trunc(2.9)` gives `2` |
| Fixed decimals | `(3.14159).toFixed(2)` gives `"3.14"` |
| Minimum / maximum | `Math.min(1, 5)` / `Math.max(...array)` |
| Absolute value | `Math.abs(-5)` |
| Power / root | `2 ** 3` or `Math.pow(2, 3)` / `Math.sqrt(9)` |
| Random 0 to 1 | `Math.random()` |
| Random integer 1 to 10 | `Math.floor(Math.random() * 10) + 1` |
| Format | `(1234567.89).toLocaleString("en-US")` gives `"1,234,567.89"` |
| Currency | `new Intl.NumberFormat("en-US", { style: "currency", currency: "USD" }).format(9.5)` |
| Constants | `Math.PI`, `Number.MAX_SAFE_INTEGER` |

Floating point math is not exact: `0.1 + 0.2` gives `0.30000000000000004`. Round before displaying, or work in whole units (such as cents).

---

<a id="collections"></a>

## 🧺 Set & Map

```js
// Set: unique values
const set = new Set([1, 2, 2, 3]);
set.add(4);
set.has(2);       // true
set.delete(1);
set.size;         // 3
[...set];         // back to an array

// Map: key-value pairs with any key type
const map = new Map();
map.set("name", "Ada");
map.get("name");      // "Ada"
map.has("name");      // true
map.delete("name");
map.size;

for (const [key, value] of map) { /* ... */ }
```

| Choose | When |
|---|---|
| Array | Ordered list with duplicates |
| Set | Unique values, fast lookup |
| Object | Fixed, known keys (records) |
| Map | Dynamic keys, any key type, frequent add and remove |

---

<a id="dates"></a>

## 📅 Dates

```js
const now = new Date();
const specific = new Date("2026-01-15T10:30:00");
const ts = Date.now();                 // milliseconds since 1970
```

| Task | Code |
|---|---|
| Year / month / day | `d.getFullYear()`, `d.getMonth()`, `d.getDate()` |
| Day of week (0 is Sunday) | `d.getDay()` |
| Hours / minutes / seconds | `d.getHours()`, `d.getMinutes()`, `d.getSeconds()` |
| ISO text | `d.toISOString()` |
| Readable | `d.toLocaleDateString("en-US", { dateStyle: "medium" })` |
| Difference in days | `(date2 - date1) / (1000 * 60 * 60 * 24)` |

**Months are zero-based:** January is `0` and December is `11`.

---

<a id="json"></a>

## 📄 JSON

```js
const text = JSON.stringify({ a: 1, b: [2, 3] });   // '{"a":1,"b":[2,3]}'
const pretty = JSON.stringify(obj, null, 2);        // indented
const data = JSON.parse(text);                      // back to an object

// Safe parse
try {
  const parsed = JSON.parse(input);
} catch {
  console.error("Invalid JSON");
}
```

JSON cannot hold functions, `undefined`, or `Date` objects (dates become text).

---

<a id="destructuring"></a>

## 🎁 Destructuring, Spread & Rest

```js
// Arrays
const [first, second, ...others] = [1, 2, 3, 4];
const [a, , c] = [1, 2, 3];          // skip an item
[a, b] = [b, a];                      // swap values

// Objects
const { name, age = 18 } = user;      // with a default
const { name: userName } = user;      // rename
const { address: { city } } = user;   // nested

// In function parameters
function show({ name, role = "guest" }) { return `${name} (${role})`; }

// Spread
const merged = [...arr1, ...arr2];
const updated = { ...user, age: 37 };
Math.max(...numbers);

// Rest
const [head, ...tail] = items;
const { id, ...rest } = record;
```

---

<a id="modules"></a>

## 📦 Modules

```js
// math.js
export const PI = 3.14159;
export function area(r) { return PI * r * r; }
export default function greet() { return "Hello"; }

// main.js
import greet, { PI, area } from "./math.js";
import * as math from "./math.js";
import { area as circleArea } from "./math.js";   // rename

// Dynamic import (loads on demand)
const module = await import("./heavy.js");
```

| Rule | Detail |
|---|---|
| HTML | `<script type="module" src="main.js"></script>` |
| File paths | Include the extension: `./math.js` |
| Scope | Each module has its own scope |
| Local testing | Use a local server such as Live Server (`file://` blocks modules) |

---

<a id="errors"></a>

## 🚨 Error Handling

```js
try {
  riskyCode();
} catch (error) {
  console.error(error.name, error.message);
} finally {
  cleanUp();   // always runs
}

function divide(a, b) {
  if (b === 0) throw new RangeError("Cannot divide by zero");
  return a / b;
}
```

| Error | Meaning |
|---|---|
| `ReferenceError` | Variable does not exist |
| `TypeError` | Wrong type, such as calling `undefined` |
| `SyntaxError` | Invalid code or JSON |
| `RangeError` | Value out of range |

---

<a id="async"></a>

## ⏳ Async JavaScript

```js
// Promise
fetch(url)
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error(error));

// async / await (preferred)
async function getData(url) {
  try {
    const response = await fetch(url);
    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    return await response.json();
  } catch (error) {
    console.error("Request failed:", error.message);
    throw error;
  }
}
```

| Promise helper | Behavior |
|---|---|
| `Promise.all([...])` | Waits for all; rejects if any fails |
| `Promise.allSettled([...])` | Waits for all; reports every result |
| `Promise.race([...])` | First one to finish wins |
| `Promise.any([...])` | First one to succeed wins |
| `Promise.resolve(x)` / `Promise.reject(e)` | Create a settled promise |

```js
// Run in parallel
const [users, posts] = await Promise.all([getData("/users"), getData("/posts")]);

// Create your own promise
const wait = (ms) => new Promise((resolve) => setTimeout(resolve, ms));
await wait(1000);

// Send data with fetch
const response = await fetch("/api/items", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ name: "Book" }),
});
```

| Timer | Code |
|---|---|
| Run once after a delay | `const id = setTimeout(fn, 1000); clearTimeout(id);` |
| Repeat | `const id = setInterval(fn, 1000); clearInterval(id);` |
| Next frame | `requestAnimationFrame(fn)` |

**Order of execution:** synchronous code first, then microtasks (promises), then macrotasks (timers, events).

---

<a id="dom"></a>

## 🌳 DOM

### Select

```js
document.getElementById("title");
document.querySelector(".card");          // first match
document.querySelectorAll("li");          // all matches
element.closest(".card");                 // nearest matching ancestor
element.matches(".active");               // does it match this selector?
```

### Modify

| Task | Code |
|---|---|
| Text (safe) | `el.textContent = "Hello";` |
| HTML (risky with user input) | `el.innerHTML = "<b>Hi</b>";` |
| Attribute | `el.setAttribute("href", "#")` / `el.getAttribute("href")` / `el.removeAttribute("href")` |
| Classes | `el.classList.add("a")` / `.remove("a")` / `.toggle("a")` / `.contains("a")` |
| Style | `el.style.color = "tomato";` |
| Data attribute | `el.dataset.id` for `data-id="5"` |
| Create | `document.createElement("li")` |
| Add inside | `parent.append(child)` / `parent.prepend(child)` |
| Add beside | `el.before(x)` / `el.after(x)` |
| Replace | `el.replaceWith(x)` |
| Remove | `el.remove()` |
| Clear children | `el.replaceChildren()` |
| Clone | `el.cloneNode(true)` |

### Navigate

| Property | Meaning |
|---|---|
| `el.parentElement` | Parent |
| `el.children` | Child elements |
| `el.firstElementChild` / `el.lastElementChild` | First / last child |
| `el.nextElementSibling` / `el.previousElementSibling` | Neighbors |

### Size & scroll

```js
el.getBoundingClientRect();           // position and size on screen
el.scrollIntoView({ behavior: "smooth" });
window.scrollTo({ top: 0, behavior: "smooth" });
window.innerWidth;                    // viewport width
```

---

<a id="events"></a>

## 🖱️ Events

```js
button.addEventListener("click", (event) => {
  event.preventDefault();      // stop the default action
  event.stopPropagation();     // stop bubbling
  console.log(event.target);   // the element that was clicked
});

button.removeEventListener("click", handler);

// Run once
button.addEventListener("click", handler, { once: true });
```

| Group | Events |
|---|---|
| Mouse | `click`, `dblclick`, `mouseenter`, `mouseleave`, `contextmenu` |
| Keyboard | `keydown`, `keyup` (check `event.key`, such as `"Enter"` or `"Escape"`) |
| Form | `submit`, `input`, `change`, `focus`, `blur` |
| Page | `DOMContentLoaded`, `load`, `scroll`, `resize` |
| Pointer and touch | `pointerdown`, `pointermove`, `pointerup`, `touchstart` |
| Drag | `dragstart`, `dragover`, `drop` |

```js
// Event delegation: one listener for many items
list.addEventListener("click", (event) => {
  const item = event.target.closest("li");
  if (!item) return;
  console.log(item.textContent);
});

// Form data
form.addEventListener("submit", (event) => {
  event.preventDefault();
  const data = Object.fromEntries(new FormData(form));
  console.log(data);
});
```

---

<a id="apis"></a>

## 🌐 Browser APIs

| API | Example |
|---|---|
| **localStorage** (persists) | `localStorage.setItem("k", "v")` / `.getItem("k")` / `.removeItem("k")` / `.clear()` |
| **sessionStorage** (per tab) | Same methods as `localStorage` |
| **Store objects** | `localStorage.setItem("user", JSON.stringify(user))` then `JSON.parse(localStorage.getItem("user"))` |
| **URL** | `const url = new URL(location.href); url.searchParams.get("id");` |
| **Query string** | `new URLSearchParams({ q: "js" }).toString()` |
| **Location** | `location.href`, `location.search`, `location.reload()` |
| **History** | `history.pushState({}, "", "/page")`, `history.back()` |
| **Clipboard** | `await navigator.clipboard.writeText("text")` |
| **Geolocation** | `navigator.geolocation.getCurrentPosition(onSuccess, onError)` |
| **Media query** | `window.matchMedia("(prefers-color-scheme: dark)").matches` |
| **Intersection Observer** | `new IntersectionObserver(callback).observe(el)` |
| **Resize Observer** | `new ResizeObserver(callback).observe(el)` |
| **Web Worker** | `new Worker("worker.js")` |
| **Notifications** | `Notification.requestPermission()` |

Storage holds **text only** and can be read by any script on the page. Never store passwords, tokens or other secrets in it.

---

<a id="regex"></a>

## 🔍 Regular Expressions

```js
const pattern = /\d+/g;                 // literal
const same = new RegExp("\\d+", "g");   // from a string

pattern.test("abc 123");                // true
"abc 123 def 45".match(/\d+/g);         // ["123", "45"]
"a1b2".replace(/\d/g, "#");             // "a#b#"
[..."a1b22".matchAll(/\d+/g)];          // all matches with details
```

| Pattern | Meaning |
|---|---|
| `.` | Any character |
| `\d` / `\D` | Digit / not a digit |
| `\w` / `\W` | Word character / not a word character |
| `\s` / `\S` | Whitespace / not whitespace |
| `^` / `$` | Start / end of text |
| `*` / `+` / `?` | 0 or more / 1 or more / 0 or 1 |
| `{3}` / `{2,5}` | Exact count / range |
| `[abc]` / `[^abc]` | Any of / none of |
| `(abc)` | Capture group |
| `\b` | Word boundary |

| Flag | Meaning |
|---|---|
| `g` | Find all matches |
| `i` | Ignore case |
| `m` | Multi-line |
| `u` | Unicode support |

```js
// Alternation (this OR that), shown in code to keep it readable
/cat|dog/.test("hotdog");   // true

// Simple email check (not perfect: still validate on the server)
/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
```

---

<a id="console"></a>

## 🖥️ Console & Debugging Methods

| Method | Purpose |
|---|---|
| `console.log(x)` | Print a value |
| `console.error(x)` / `console.warn(x)` | Error / warning |
| `console.table(array)` | Show data as a table |
| `console.dir(obj)` | Inspect an object |
| `console.group("name")` / `console.groupEnd()` | Group related logs |
| `console.time("t")` / `console.timeEnd("t")` | Measure time |
| `console.assert(cond, "msg")` | Log only if the condition is false |
| `debugger;` | Pause here when DevTools is open |

---

<a id="snippets"></a>

## 🧪 Ready-to-Copy Snippets

### Debounce (wait until the user stops typing)

```js
function debounce(fn, delay = 300) {
  let timer;
  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => fn(...args), delay);
  };
}

input.addEventListener("input", debounce((e) => search(e.target.value), 300));
```

### Throttle (run at most once per interval)

```js
function throttle(fn, limit = 200) {
  let waiting = false;
  return (...args) => {
    if (waiting) return;
    fn(...args);
    waiting = true;
    setTimeout(() => (waiting = false), limit);
  };
}
```

### Toggle dark mode and remember it

```js
const root = document.documentElement;
const saved = localStorage.getItem("theme");
if (saved) root.dataset.theme = saved;

toggle.addEventListener("click", () => {
  const next = root.dataset.theme === "dark" ? "light" : "dark";
  root.dataset.theme = next;
  localStorage.setItem("theme", next);
});
```

### Copy text to the clipboard

```js
async function copyText(text) {
  try {
    await navigator.clipboard.writeText(text);
    return true;
  } catch {
    return false;
  }
}
```

### Fetch with a timeout

```js
async function fetchWithTimeout(url, ms = 8000) {
  const controller = new AbortController();
  const timer = setTimeout(() => controller.abort(), ms);
  try {
    const response = await fetch(url, { signal: controller.signal });
    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    return await response.json();
  } finally {
    clearTimeout(timer);
  }
}
```

### Lazy-load on scroll

```js
const observer = new IntersectionObserver((entries) => {
  for (const entry of entries) {
    if (entry.isIntersecting) {
      entry.target.classList.add("visible");
      observer.unobserve(entry.target);
    }
  }
});
document.querySelectorAll(".reveal").forEach((el) => observer.observe(el));
```

### Group an array by a key

```js
const groupBy = (array, key) =>
  array.reduce((groups, item) => {
    (groups[item[key]] ??= []).push(item);
    return groups;
  }, {});
```

### Shuffle an array

```js
const shuffle = (array) => {
  const copy = [...array];
  for (let i = copy.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [copy[i], copy[j]] = [copy[j], copy[i]];
  }
  return copy;
};
```

### Capitalize and slugify

```js
const capitalize = (s) => s.charAt(0).toUpperCase() + s.slice(1);
const slugify = (s) => s.toLowerCase().trim().replace(/\s+/g, "-").replace(/[^\w-]/g, "");
```

### Wait (sleep)

```js
const sleep = (ms) => new Promise((resolve) => setTimeout(resolve, ms));
await sleep(500);
```

---

<a id="mistakes"></a>

## ⚠️ Common Mistakes

| Mistake | Fix |
|---|---|
| Using `==` | Use `===` |
| Using `var` | Use `const` or `let` |
| `typeof null` is `"object"` | Check with `value === null` |
| `[10, 2, 1].sort()` gives wrong order | Pass a compare function: `sort((a, b) => a - b)` |
| `0.1 + 0.2 !== 0.3` | Round the result, or use whole units like cents |
| `parseInt("08")` confusion | Always pass the radix: `parseInt(value, 10)` |
| Forgetting `await` | The result is a pending Promise, not the data |
| `fetch` does not reject on 404 or 500 | Check `response.ok` |
| `forEach` with `await` does not wait | Use `for...of`, or `Promise.all` with `map` |
| Script runs before the HTML exists | Add `defer` to the script tag |
| Arrow function as an object method uses the wrong `this` | Use a regular method |
| `this` is lost in a callback | Use an arrow function or `.bind(this)` |
| Mutating shared arrays or objects | Copy with spread or `structuredClone` |
| `innerHTML` with user input | Use `textContent` or sanitize the HTML |
| Adding a listener inside a loop for many items | Use event delegation |
| `NaN === NaN` is `false` | Use `Number.isNaN(value)` |
| Object copy still shares nested objects | Use `structuredClone` for a deep copy |
| Returning an object literal from an arrow gives `undefined` | Wrap it: `() => ({ a: 1 })` |
| Date month off by one | Months start at `0` |
| Storing secrets in `localStorage` | Never do this |

---

<a id="debugging"></a>

## 🐞 Debugging Tips

- Open DevTools with `F12`, and read the **Console** for errors and line numbers
- Use the **Sources** tab to set breakpoints and step through code
- Use `debugger;` to pause at an exact line
- Use `console.table()` for arrays and objects
- Use the **Network** tab to check requests, status codes and responses
- Read the error type first: `ReferenceError`, `TypeError` and `SyntaxError` each point to a different cause
- Log the **type** and the **value** when something behaves strangely
- Test small pieces in the Console before putting them in your code
- Use ESLint to catch problems while you type
- Check feature support on [Can I use](https://caniuse.com/)

---

## 💡 Quick Reminders

- `const` by default, `let` when needed, never `var`
- Always use `===`
- Prefer `async` / `await`, and handle every error
- Check `response.ok` after `fetch`
- Use `textContent` for user text, never `innerHTML`
- Use event delegation for lists
- Copy objects and arrays instead of changing the original
- Use `defer` on your script tags
- Never put secrets in front-end code or `localStorage`