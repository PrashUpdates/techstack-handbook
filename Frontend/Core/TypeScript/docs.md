# 🟦 TypeScript Documentation

<p align="center">
  <a href="https://github.com/PrashUpdates/techstack-handbook/blob/main/README.md#frontend"><img src="https://img.shields.io/badge/Back%20to%20main-6E7681?style=for-the-badge" alt="Back to main" /></a>
  <a href="./cheat-sheet.md"><img src="https://img.shields.io/badge/Cheat%20Sheet-F38020?style=for-the-badge" alt="Cheat Sheet" /></a>
  <a href="./notes.md"><img src="https://img.shields.io/badge/Notes-3FB950?style=for-the-badge" alt="Notes" /></a>
</p>

> A complete guide to TypeScript: what it adds to JavaScript, how the type system works, the core features, best practices and a ready-to-use starter project.

## 📑 Contents

| # | Section | What's inside |
|---|---|---|
| 1 | [Executive Summary & Use Cases](#summary) | What TypeScript is and when to use it |
| 2 | [Core Concepts & Architecture](#concepts) | Compilation, types, interfaces, generics, narrowing, utility types, configuration |
| 3 | [Standard Checklist & Best Practices](#checklist) | Features, setup steps, safety, performance and security tips |
| 4 | [Quick Start & Boilerplate Code](#quickstart) | A minimal, commented starter project |
| 5 | [Official Documentation & Resources](#resources) | Verified docs, tutorials and practice platforms |

---

<a id="summary"></a>

## 1. Executive Summary & Use Cases

**TypeScript** (TS) is a free, open-source programming language built on top of JavaScript. It adds a **static type system**: you describe the shape of your data, and the compiler checks your code for mistakes **before it runs**. TypeScript is a **superset** of JavaScript, so every valid JavaScript program is also valid TypeScript.

Browsers and Node.js cannot run TypeScript directly. The compiler checks the types, then **removes** them and produces plain JavaScript. Types exist only while you write and build your code.

**Primary purpose:** catch bugs early, make code self-documenting, and give editors accurate autocomplete, safe refactoring and instant error messages, especially in medium and large projects.

| | JavaScript | TypeScript |
|---|---|---|
| **Typing** | Dynamic (checked while running) | Static (checked before running) |
| **Errors found** | At runtime, often by users | At build time and in the editor |
| **Runs in browser** | Directly | After compiling to JavaScript |
| **Autocomplete** | Basic, guessed | Precise, based on types |
| **Best for** | Small scripts, quick prototypes | Apps, libraries, teams, long-lived code |

### When to use it

| Use it when | Example |
|---|---|
| Building large or long-lived applications | Dashboards, e-commerce, SaaS products |
| Working in a team | Types act as a shared contract between developers |
| Building with modern frameworks | React, Vue, Angular, Next.js and Node.js all have first-class support |
| Writing libraries and APIs | Typed functions and data shapes help every user of your code |
| Refactoring existing code safely | Rename or reshape code and let the compiler show every place that breaks |
| Working with API data | Describe response shapes and catch mismatches early |

### Where TypeScript runs

| Environment | How |
|---|---|
| **Browser** | Compile to JavaScript first (using `tsc`, Vite or another build tool) |
| **Node.js** | Compile with `tsc`, run with a tool such as `tsx`, or use the type-stripping support in recent Node.js versions (check the Node.js docs for your version) |
| **Frameworks** | Project templates for React, Vue, Next.js, Angular and others include TypeScript out of the box |

---

<a id="concepts"></a>

## 2. Core Concepts & Architecture

### How TypeScript works

1. You write code in `.ts` (or `.tsx` for React) files
2. The **TypeScript compiler** (`tsc`) reads your files and your `tsconfig.json`
3. It builds a model of every type and checks that your code is consistent
4. It reports errors, and **erases the types** to output regular JavaScript
5. The JavaScript runs in the browser or in Node.js

```
app.ts  →  tsc (type check + remove types)  →  app.js  →  runs anywhere JavaScript runs
```

**Important idea: types do not exist at runtime.** `interface`, `type` and annotations disappear after compiling. TypeScript cannot check data that arrives while the program is running (API responses, user input, files), so that data must be validated separately.

### Structural typing

TypeScript compares types by their **shape**, not by their name. If an object has the required properties, it fits the type. This is often called "duck typing".

```ts
interface Point {
  x: number;
  y: number;
}

function print(point: Point) {
  console.log(point.x, point.y);
}

const location = { x: 10, y: 20, label: "Home" };
print(location); // OK: it has x and y (extra properties are fine for variables)
```

### Basic types

| Type | Example | Notes |
|---|---|---|
| `string` | `"hello"` | Text |
| `number` | `42`, `3.14` | All numbers (integers and decimals) |
| `boolean` | `true` | |
| `bigint` | `100n` | Very large integers |
| `symbol` | `Symbol("id")` | Unique identifiers |
| `null` / `undefined` | `null` | Separate types when `strict` is on |
| `any` | anything | Turns type checking **off**: avoid it |
| `unknown` | anything | Safe version of `any`: must be checked before use |
| `never` | no value | A function that never returns, or an impossible case |
| `void` | no return value | Functions that return nothing |
| `object` | `{}` | Any non-primitive value |

```ts
const name: string = "Ada";
const age: number = 36;
const isAdmin: boolean = false;
```

### Type inference

TypeScript works out types for you. You do **not** need to annotate everything.

```ts
let city = "Paris";           // inferred as string
const count = 3;              // inferred as the literal type 3
const prices = [9.99, 4.5];   // inferred as number[]

function double(n: number) {  // return type inferred as number
  return n * 2;
}
```

**Rule of thumb:** annotate function parameters, exported function return types and empty starting values. Let inference handle the rest.

### `any`, `unknown` and `never`

| Type | Meaning | Safe? |
|---|---|---|
| `any` | Opt out of type checking completely | No: errors spread silently |
| `unknown` | A value of a type you do not know yet | Yes: you must check it before using it |
| `never` | A value that can never happen | Yes: useful for exhaustive checks |

```ts
function handle(value: unknown) {
  if (typeof value === "string") {
    return value.toUpperCase(); // OK: narrowed to string
  }
  // value.toUpperCase();       // Error: value is still unknown here
}
```

### Arrays, tuples and objects

```ts
const names: string[] = ["Ada", "Grace"];
const scores: Array<number> = [90, 85];       // same thing, generic syntax
const readonlyList: readonly string[] = ["a"]; // cannot be changed

// Tuple: fixed length, each position has its own type
const entry: [string, number] = ["Ada", 36];

// Object types
const user: { name: string; age: number; email?: string } = {
  name: "Ada",
  age: 36,
};
```

| Modifier | Meaning | Example |
|---|---|---|
| `?` | Optional property | `email?: string` |
| `readonly` | Cannot be reassigned after creation | `readonly id: number` |
| Index signature | Any number of keys of one type | `{ [key: string]: number }` |

### Union and intersection types

A **union** means "one of these types". An **intersection** means "all of these types combined".

```ts
// Union: written with the | symbol
type Id = string | number;
let userId: Id = 42;
userId = "abc-123";

// Intersection: written with the & symbol
type Named = { name: string };
type Aged = { age: number };
type Person = Named & Aged; // must have both name and age
```

### Literal types

A literal type is one exact value. Combined with unions, literals replace most uses of enums.

```ts
type Direction = "up" | "down" | "left" | "right";
type Status = "idle" | "loading" | "success" | "error";

let move: Direction = "up";
// move = "north";   // Error: not one of the allowed values
```

### Type aliases and interfaces

Both describe the shape of data.

```ts
// Type alias
type User = {
  id: number;
  name: string;
};

// Interface
interface Product {
  id: number;
  title: string;
  price: number;
}

// Extending
interface Book extends Product {
  author: string;
}
type Admin = User & { permissions: string[] };
```

| | `interface` | `type` |
|---|---|---|
| Describe object shapes | Yes | Yes |
| Extend | `extends` | Intersection with `&` |
| Merge by declaring twice | Yes (declaration merging) | No |
| Unions, tuples, primitives | No | Yes |
| Mapped and conditional types | No | Yes |
| Good default for | Public object shapes and class contracts | Unions and everything else |

**Rule of thumb:** pick one style for your team and stay consistent. Both work for object shapes.

### Functions

```ts
// Parameter and return types
function add(a: number, b: number): number {
  return a + b;
}

// Arrow function
const greet = (name: string): string => `Hello, ${name}!`;

// Optional, default and rest parameters
function createUser(name: string, age?: number, role = "member") {}
function sum(...numbers: number[]): number {
  return numbers.reduce((total, n) => total + n, 0);
}

// Function type
type Operation = (a: number, b: number) => number;
const subtract: Operation = (a, b) => a - b;

// Function that returns nothing
function log(message: string): void {
  console.log(message);
}

// Overloads: different ways to call one function
function format(value: string): string;
function format(value: number): string;
function format(value: string | number): string {
  return String(value);
}
```

### Generics

Generics let you write one function, type or class that works with **many types** while keeping type safety. Think of them as type variables.

```ts
// A generic function
function firstItem<T>(items: T[]): T | undefined {
  return items[0];
}

const n = firstItem([1, 2, 3]);        // T is number
const s = firstItem(["a", "b"]);       // T is string

// Constraints: T must have a length
function longest<T extends { length: number }>(a: T, b: T): T {
  return a.length >= b.length ? a : b;
}

// A generic interface
interface ApiResponse<T> {
  data: T;
  error?: string;
}

const response: ApiResponse<{ id: number; name: string }> = {
  data: { id: 1, name: "Ada" },
};

// Default type parameter
interface Box<T = string> {
  value: T;
}
```

### Type narrowing

**Narrowing** means TypeScript refines a broad type into a more specific one inside a block of code, based on your checks.

| Technique | Example | Narrows to |
|---|---|---|
| `typeof` | `typeof x === "string"` | A primitive type |
| `instanceof` | `x instanceof Date` | A class type |
| `in` operator | `"swim" in animal` | A type that has that property |
| Equality | `x !== null` | Removes `null` |
| Truthiness | `if (name)` | Removes `null`, `undefined`, `""` |
| `Array.isArray` | `Array.isArray(x)` | An array type |
| Discriminant | `shape.kind === "circle"` | One member of a union |
| Custom guard | `isUser(x)` | Any type you define |

```ts
// Custom type guard
interface Cat { meow: () => void }
interface Dog { bark: () => void }

function isCat(pet: Cat | Dog): pet is Cat {
  return "meow" in pet;
}

function speak(pet: Cat | Dog) {
  if (isCat(pet)) {
    pet.meow();   // narrowed to Cat
  } else {
    pet.bark();   // narrowed to Dog
  }
}
```

### Discriminated unions

A discriminated union gives every member a shared property with a unique literal value (the **discriminant**). It is one of the most useful TypeScript patterns, and it fits states like loading, success and error.

```ts
type RequestState =
  | { status: "loading" }
  | { status: "success"; data: string[] }
  | { status: "error"; message: string };

function render(state: RequestState): string {
  switch (state.status) {
    case "loading":
      return "Loading...";
    case "success":
      return `Loaded ${state.data.length} items`;
    case "error":
      return `Error: ${state.message}`;
    default: {
      // Exhaustive check: if a new status is added later, this line shows an error
      const unreachable: never = state;
      return unreachable;
    }
  }
}
```

### Utility types

Built-in helpers that transform existing types.

| Utility | What it does | Example |
|---|---|---|
| `Partial<T>` | Makes all properties optional | `Partial<User>` |
| `Required<T>` | Makes all properties required | `Required<User>` |
| `Readonly<T>` | Makes all properties read-only | `Readonly<User>` |
| `Pick<T, K>` | Keeps only some properties | `Pick<User, "id" or "name">` as `Pick<User, "id" \| "name">` in code |
| `Omit<T, K>` | Removes some properties | `Omit<User, "password">` |
| `Record<K, V>` | Object with keys K and values V | `Record<string, number>` |
| `Exclude<T, U>` | Removes types from a union | `Exclude<Status, "error">` |
| `Extract<T, U>` | Keeps matching types from a union | `Extract<Status, "idle">` |
| `NonNullable<T>` | Removes `null` and `undefined` | `NonNullable<string or null>` |
| `ReturnType<F>` | The return type of a function | `ReturnType<typeof getUser>` |
| `Parameters<F>` | The parameters of a function as a tuple | `Parameters<typeof add>` |
| `Awaited<T>` | The type a Promise resolves to | `Awaited<Promise<string>>` |

```ts
interface User {
  id: number;
  name: string;
  email: string;
  password: string;
}

type PublicUser = Omit<User, "password">;
type UserUpdate = Partial<Omit<User, "id">>;
type UserMap = Record<number, User>;
```

### `keyof`, `typeof` and indexed access

```ts
const settings = { theme: "dark", fontSize: 14 };

type Settings = typeof settings;          // { theme: string; fontSize: number }
type SettingKey = keyof Settings;         // "theme" with fontSize as a union of keys
type FontSize = Settings["fontSize"];     // number

// A type-safe property getter
function getProp<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

getProp(settings, "theme");   // string
// getProp(settings, "color"); // Error: "color" is not a key
```

### `as const`

`as const` freezes a value into its narrowest literal type and makes it read-only.

```ts
const ROLES = ["admin", "editor", "viewer"] as const;
type Role = (typeof ROLES)[number];   // "admin" with the other two roles as a union

const COLORS = { primary: "#0969da", danger: "#cf222e" } as const;
type ColorName = keyof typeof COLORS; // "primary" with "danger" as a union
```

### Mapped and conditional types

These are advanced tools for building new types from existing ones.

```ts
// Mapped type: transform every property
type Optional<T> = {
  [K in keyof T]?: T[K];
};

type Flags<T> = {
  [K in keyof T]: boolean;
};

// Conditional type: choose a type based on a condition
type IsString<T> = T extends string ? "yes" : "no";

// infer: pull a type out of another type
type ElementType<T> = T extends (infer U)[] ? U : T;
type Item = ElementType<string[]>;   // string

// Template literal types
type EventName = `on${Capitalize<"click" | "hover">}`;   // "onClick" or "onHover"
```

### Type assertions and `satisfies`

```ts
// Assertion: you tell the compiler you know better (it does NOT convert anything)
const input = document.querySelector("#email") as HTMLInputElement;

// Non-null assertion: you promise a value is not null (use sparingly)
const title = document.getElementById("title")!;

// satisfies: check a value against a type while keeping its precise inferred type
type Theme = Record<string, string>;
const theme = {
  primary: "#0969da",
  danger: "#cf222e",
} satisfies Theme;

theme.primary.toUpperCase();   // still known to be a string
```

**Assertions are not runtime checks.** If you assert a wrong type, TypeScript believes you and the bug appears at runtime. Prefer narrowing and type guards.

### Enums versus literal unions

```ts
// Enum: generates real JavaScript code
enum Role {
  Admin = "ADMIN",
  User = "USER",
}

// Literal union: erased at compile time, simple and lightweight (usually preferred)
type RoleName = "admin" | "user";

// Const object pattern: a real object plus a derived type
const Status = { Active: "active", Inactive: "inactive" } as const;
type Status = (typeof Status)[keyof typeof Status];
```

### Classes

```ts
class Account {
  readonly id: number;              // cannot change after the constructor
  private balance = 0;              // only usable inside the class
  protected owner: string;          // usable inside the class and subclasses
  static count = 0;                 // belongs to the class itself

  constructor(id: number, owner: string) {
    this.id = id;
    this.owner = owner;
    Account.count++;
  }

  deposit(amount: number): void {
    this.balance += amount;
  }

  get total(): number {
    return this.balance;
  }
}

// Parameter properties: a shorter way to declare and assign fields
class Person {
  constructor(public name: string, private age: number) {}
}

// Implementing an interface
interface Printable {
  print(): void;
}
class Report implements Printable {
  print() { console.log("Printing..."); }
}

// Abstract class
abstract class Shape {
  abstract area(): number;
}
```

| Modifier | Visible from |
|---|---|
| `public` (default) | Everywhere |
| `protected` | The class and its subclasses |
| `private` | The class only (checked by TypeScript) |
| `#field` | The class only (enforced by JavaScript at runtime) |
| `readonly` | Assigned once, then read-only |

### Modules

TypeScript uses the same `import` and `export` syntax as modern JavaScript, and you can import and export **types** too.

```ts
// types.ts
export interface User {
  id: number;
  name: string;
}
export type Role = "admin" | "user";

// main.ts
import type { User, Role } from "./types";   // type-only import (erased at build time)
import { createUser } from "./users";
```

Use `import type` for imports that are only types. It makes your intent clear and keeps type imports out of the generated JavaScript.

### Declaration files and `@types`

JavaScript libraries have no types of their own. **Declaration files** (`.d.ts`) describe their shapes.

| Case | What to do |
|---|---|
| The library ships its own types | Nothing: types work automatically |
| Types come from DefinitelyTyped | Install them: `npm install --save-dev @types/package-name` |
| No types exist anywhere | Write a small `declare module "name";` in a `.d.ts` file, or write full types yourself |
| Browser or Node.js globals | Install `@types/node` for Node.js, and use `"lib": ["DOM"]` for browser APIs |

### Working with the DOM

```ts
// querySelector returns Element or null, so check it first
const button = document.querySelector("#save");
if (button) {
  button.addEventListener("click", () => console.log("Saved"));
}

// A generic argument sets a more specific element type
const input = document.querySelector<HTMLInputElement>("#email");
if (input) {
  console.log(input.value);
}

// Typed events
function handleInput(event: Event) {
  const target = event.target as HTMLInputElement;
  console.log(target.value);
}

form?.addEventListener("submit", (event: SubmitEvent) => {
  event.preventDefault();
});
```

### Async code

```ts
interface Todo {
  id: number;
  title: string;
  completed: boolean;
}

// An async function always returns a Promise of its result type
async function loadTodo(id: number): Promise<Todo> {
  const response = await fetch(`/api/todos/${id}`);
  if (!response.ok) {
    throw new Error(`HTTP error: ${response.status}`);
  }
  const data: unknown = await response.json();
  if (!isTodo(data)) {
    throw new Error("Unexpected data shape");
  }
  return data;
}

// Check unknown data before trusting it
function isTodo(value: unknown): value is Todo {
  return (
    typeof value === "object" &&
    value !== null &&
    "id" in value &&
    "title" in value
  );
}
```

`response.json()` returns `any`, which silently turns type checking off. Assign it to `unknown` and validate it, or use a runtime validation library.

### Error handling

With `strict` on (and `useUnknownInCatchVariables`), the variable in a `catch` block has the type `unknown`, so check it before use.

```ts
try {
  riskyOperation();
} catch (error) {
  if (error instanceof Error) {
    console.error(error.message);
  } else {
    console.error("Unknown error", error);
  }
}
```

### Configuring TypeScript: `tsconfig.json`

The `tsconfig.json` file controls how the compiler behaves. Create one with `npx tsc --init`.

| Option | Purpose |
|---|---|
| `strict` | Turns on all strict checks. **Always enable it** |
| `target` | Which JavaScript version to output (`ES2022` is a good modern choice) |
| `module` / `moduleResolution` | How imports are handled (`NodeNext` for Node.js, `ESNext` with `Bundler` for apps using Vite or similar) |
| `lib` | Built-in type definitions to include (add `DOM` for browser code) |
| `outDir` / `rootDir` | Where compiled files go and where sources live |
| `include` / `exclude` | Which files belong to the project |
| `noEmit` | Only type check, do not write JavaScript (used with bundlers) |
| `noUncheckedIndexedAccess` | Array and object lookups may be `undefined`: safer |
| `skipLibCheck` | Skip checking `.d.ts` files in dependencies (faster builds) |
| `forceConsistentCasingInFileNames` | Avoids file name case bugs across operating systems |
| `esModuleInterop` | Smoother imports from CommonJS packages |
| `resolveJsonModule` | Allows importing `.json` files |
| `sourceMap` | Debug the original TypeScript in the browser or Node.js |
| `jsx` | How `.tsx` files are compiled (`react-jsx` for React) |
| `verbatimModuleSyntax` | Keeps `import type` and `export type` handling explicit |
| `isolatedModules` | Makes sure each file can be compiled on its own (needed by many bundlers) |
| `declaration` | Generate `.d.ts` files (for libraries) |

### What `strict` turns on

`strict: true` enables a group of checks. The most important ones:

| Check | Effect |
|---|---|
| `strictNullChecks` | `null` and `undefined` are separate types, which prevents "cannot read property of undefined" bugs |
| `noImplicitAny` | Variables and parameters must have a known type |
| `strictFunctionTypes` | Stricter checking of function parameter types |
| `strictPropertyInitialization` | Class properties must be set in the constructor |
| `useUnknownInCatchVariables` | `catch` variables are `unknown` instead of `any` |
| `noImplicitThis` | `this` must have a known type |

### Compiling and running

| Task | Command |
|---|---|
| Create `tsconfig.json` | `npx tsc --init` |
| Compile the project | `npx tsc` |
| Compile and watch for changes | `npx tsc --watch` |
| Type check only | `npx tsc --noEmit` |
| Run a TypeScript file directly during development | `npx tsx src/index.ts` |
| Start a Vite project with TypeScript | `npm create vite@latest my-app -- --template vanilla-ts` |

### Tooling overview

| Tool | Purpose |
|---|---|
| **tsc** | The official compiler and type checker |
| **tsx** | Runs TypeScript files directly in Node.js, great for scripts and development |
| **Vite, esbuild, SWC** | Fast builders that strip types, while `tsc --noEmit` does the type checking |
| **typescript-eslint** | Linting rules that understand types |
| **Prettier** | Automatic formatting |
| **Vitest or Jest** | Testing with TypeScript support |
| **Zod and similar libraries** | Validate data at runtime and infer TypeScript types from the schema |
| **TypeScript Playground** | Try code in the browser and share links |
| **VS Code** | Built-in TypeScript support with hover types, errors and refactoring |

---

<a id="checklist"></a>

## 3. Standard Checklist & Best Practices

### ✅ Core Features

- [ ] Basic types, inference and annotations
- [ ] Arrays, tuples and objects
- [ ] Optional and `readonly` properties
- [ ] Union and intersection types
- [ ] Literal types and `as const`
- [ ] Type aliases and interfaces
- [ ] Functions: parameters, returns and overloads
- [ ] Generics and constraints
- [ ] Type narrowing and type guards
- [ ] Discriminated unions and exhaustive checks
- [ ] Utility types (`Partial`, `Pick`, `Omit`, `Record`)
- [ ] `keyof`, `typeof` and indexed access types
- [ ] Classes and access modifiers
- [ ] Modules and `import type`
- [ ] `unknown`, `any` and `never`
- [ ] Mapped and conditional types
- [ ] Declaration files and `@types` packages
- [ ] `tsconfig.json` options

### 🛠️ Setup Steps

- [ ] Install [Node.js](https://nodejs.org/) (the LTS version)
- [ ] Install a code editor such as [VS Code](https://code.visualstudio.com/)
- [ ] Create a project folder and run `npm init -y`
- [ ] Install TypeScript: `npm install --save-dev typescript`
- [ ] Install Node.js types if you use Node.js APIs: `npm install --save-dev @types/node`
- [ ] Create the config: `npx tsc --init`, then enable `strict`
- [ ] Create `src/index.ts` and add the starter from section 4
- [ ] Compile with `npx tsc` and run the output with `node dist/index.js`
- [ ] Optional: install ESLint with typescript-eslint, and Prettier

### 📋 Best Practices

**Configuration**
- [ ] Always enable `"strict": true`
- [ ] Consider `noUncheckedIndexedAccess` for safer array and object access
- [ ] Use `skipLibCheck` and `forceConsistentCasingInFileNames`
- [ ] Choose `target`, `module` and `lib` that match where your code runs
- [ ] Use `tsc --noEmit` in your scripts or CI to catch type errors

**Types & Safety**
- [ ] Avoid `any`: use `unknown` and narrow it, or use generics
- [ ] Let inference work, and annotate function parameters and exported return types
- [ ] Prefer literal unions or `as const` objects over `enum`
- [ ] Use discriminated unions to model states, and add an exhaustive `never` check
- [ ] Prefer `readonly` and immutable patterns for data that should not change
- [ ] Avoid type assertions (`as`) and non-null assertions (`!`) unless you are sure
- [ ] Use `satisfies` to check a value without losing its precise type
- [ ] Use `// @ts-expect-error` with a reason instead of `// @ts-ignore`
- [ ] Do not use the wrapper types `String`, `Number` or `Boolean`: use `string`, `number` and `boolean`

**Code Organization**
- [ ] Use `PascalCase` for types, interfaces and classes, and `camelCase` for variables and functions
- [ ] Do not prefix interfaces with `I`
- [ ] Keep shared types in clearly named files, such as `types.ts` or beside the feature that uses them
- [ ] Use `import type` for type-only imports
- [ ] Do not repeat yourself: derive types with `Pick`, `Omit`, `typeof` and `ReturnType`
- [ ] Keep generics simple, with short but meaningful names (`T`, `TItem`, `TKey`)

**External Data & Async Code**
- [ ] Treat API responses, form input and file data as `unknown` until validated
- [ ] Validate at runtime with type guards or a schema library such as Zod
- [ ] Check `response.ok` after `fetch`
- [ ] Give async functions explicit `Promise<T>` return types in public code
- [ ] Always handle errors, and narrow `unknown` errors before using them

**Frontend & DOM**
- [ ] Check for `null` after `querySelector` and `getElementById`
- [ ] Use generic arguments such as `querySelector<HTMLInputElement>()` for specific elements
- [ ] Type component props and event handlers in frameworks like React
- [ ] Add `"lib": ["DOM"]` for browser code

**Performance**
- [ ] Use `skipLibCheck` and incremental builds (`incremental: true`) for faster compiles
- [ ] Let a bundler such as Vite or esbuild handle the build, and use `tsc --noEmit` only for checking
- [ ] Split very large projects with project references
- [ ] Avoid extremely deep conditional or recursive types, which slow the compiler
- [ ] Remember that types have no cost at runtime, but `enum` and `namespace` generate real code

**Security**
- [ ] Remember that types vanish at runtime and do not protect against bad data
- [ ] Never trust a type assertion on data from outside your program
- [ ] Never put API keys, passwords or secrets in front-end TypeScript code
- [ ] Install `@types` packages only from the trusted `@types` scope
- [ ] Run `npm audit` and keep dependencies updated
- [ ] Always validate again on the server, since client-side checks can be bypassed

**Quality & Testing**
- [ ] Add ESLint with typescript-eslint and Prettier
- [ ] Write tests for important logic (Vitest or Jest)
- [ ] Run `tsc --noEmit` and your tests in CI
- [ ] Review the strictness of your project regularly, and fix errors instead of silencing them

---

<a id="quickstart"></a>

## 4. Quick Start & Boilerplate Code

This starter creates a small Node.js project that demonstrates interfaces, literal unions, generics, discriminated unions, type guards and async code.

### Step 1: Create the project

```bash
mkdir ts-starter
cd ts-starter
npm init -y
npm install --save-dev typescript @types/node
npx tsc --init
mkdir src
```

### Step 2: `tsconfig.json`

Replace the generated file with this smaller, cleaner version:

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "strict": true,
    "noUncheckedIndexedAccess": true,
    "outDir": "dist",
    "rootDir": "src",
    "sourceMap": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  },
  "include": ["src"]
}
```

For browser code, add `"lib": ["ES2022", "DOM"]`. For a Vite project, use the config that Vite's TypeScript template generates.

### Step 3: `src/index.ts`

```ts
// ---------- 1. Types: describe the shape of your data ----------
type Priority = "low" | "medium" | "high";      // literal union (only these 3 values allowed)

interface Task {
  id: number;
  title: string;
  done: boolean;
  priority: Priority;
  dueDate?: Date;                               // optional property
}

// ---------- 2. State, with an explicit type ----------
const tasks: Task[] = [];
let nextId = 1;

// ---------- 3. Functions with typed parameters and return values ----------
function addTask(title: string, priority: Priority = "medium"): Task {
  const task: Task = { id: nextId++, title, done: false, priority };
  tasks.push(task);
  return task;
}

function toggleTask(id: number): Task | undefined {
  const task = tasks.find((item) => item.id === id);   // find may return undefined
  if (task) {
    task.done = !task.done;                            // narrowed: task is a Task here
  }
  return task;
}

// ---------- 4. Generics: one function that works with any item type ----------
function groupBy<T, K extends string>(
  items: T[],
  getKey: (item: T) => K
): Partial<Record<K, T[]>> {
  const groups: Partial<Record<K, T[]>> = {};
  for (const item of items) {
    const key = getKey(item);
    (groups[key] ??= []).push(item);
  }
  return groups;
}

// ---------- 5. Discriminated union: model success and failure explicitly ----------
type Result<T> =
  | { ok: true; value: T }
  | { ok: false; error: string };

function parsePriority(input: string): Result<Priority> {
  if (input === "low" || input === "medium" || input === "high") {
    return { ok: true, value: input };                 // input is narrowed to Priority
  }
  return { ok: false, error: `"${input}" is not a valid priority` };
}

// ---------- 6. Type guard: check unknown data before trusting it ----------
function isTask(value: unknown): value is Task {
  return (
    typeof value === "object" &&
    value !== null &&
    "id" in value &&
    "title" in value &&
    "done" in value
  );
}

// ---------- 7. Async code with a typed Promise ----------
async function loadTasks(): Promise<Task[]> {
  // Simulates a network request
  await new Promise((resolve) => setTimeout(resolve, 100));
  const raw: unknown = JSON.parse(
    '[{"id": 100, "title": "From server", "done": false, "priority": "low"}]'
  );
  if (!Array.isArray(raw)) {
    throw new Error("Expected an array");
  }
  return raw.filter(isTask);
}

// ---------- 8. Put it all together ----------
async function main(): Promise<void> {
  addTask("Learn TypeScript", "high");
  addTask("Build a project");
  toggleTask(1);

  const parsed = parsePriority("urgent");
  if (parsed.ok) {
    console.log("Valid priority:", parsed.value);
  } else {
    console.log("Error:", parsed.error);                // narrowed: error exists here
  }

  const byPriority = groupBy(tasks, (task) => task.priority);
  console.log(byPriority);

  const remote = await loadTasks();
  console.log(`Loaded ${remote.length} task(s) from the server`);

  // addTask("Oops", "urgent");   // Error: "urgent" is not assignable to type Priority
  // toggleTask("1");              // Error: string is not assignable to number
}

main().catch((error: unknown) => {
  console.error(error instanceof Error ? error.message : error);
});
```

### Step 4: Build and run

```bash
npx tsc
node dist/index.js
```

Add these scripts to `package.json` so you can use `npm run build` and `npm start`:

```json
{
  "scripts": {
    "build": "tsc",
    "start": "node dist/index.js",
    "check": "tsc --noEmit"
  }
}
```

**What this starter demonstrates:** type annotations and inference, optional properties, literal union types, interfaces, typed functions, generics with constraints, utility types (`Partial` and `Record`), discriminated unions with narrowing, a custom type guard, `unknown` handling for external data, typed async code with `Promise<T>`, and the compile errors that TypeScript catches before the program runs.

---

<a id="resources"></a>

## 5. Official Documentation & Resources

### 📚 Official Documentation

| Resource | Description | Link |
|---|---|---|
| TypeScript Documentation | The official documentation home | [![TypeScript Docs](https://img.shields.io/badge/TypeScript-Docs-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/docs/) |
| The TypeScript Handbook | The complete guide to the language | [![Handbook](https://img.shields.io/badge/TypeScript-Handbook-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/docs/handbook/intro.html) |
| TSConfig Reference | Every `tsconfig.json` option explained | [![TSConfig](https://img.shields.io/badge/TSConfig-Reference-2F81F7?style=for-the-badge)](https://www.typescriptlang.org/tsconfig/) |
| TypeScript Playground | Write and share TypeScript in the browser | [![Playground](https://img.shields.io/badge/TypeScript-Playground-F38020?style=for-the-badge)](https://www.typescriptlang.org/play/) |
| DefinitelyTyped | Type definitions for JavaScript libraries (`@types`) | [![DefinitelyTyped](https://img.shields.io/badge/DefinitelyTyped-%40types-3FB950?style=for-the-badge)](https://github.com/DefinitelyTyped/DefinitelyTyped) |
| MDN: TypeScript | Beginner-friendly overview | [![MDN](https://img.shields.io/badge/MDN-TypeScript-000000?style=for-the-badge&logo=mdnwebdocs&logoColor=white)](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Frameworks_libraries/Svelte_TypeScript) |

### 🎓 Recommended Tutorials

| Resource | Description | Link |
|---|---|---|
| TypeScript for JavaScript Programmers | Official quick start for people who know JavaScript | [![TS for JS](https://img.shields.io/badge/TS%20for%20JS-Programmers-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html) |
| Total TypeScript | Free tutorials and exercises by Matt Pocock | [![Total TypeScript](https://img.shields.io/badge/Total%20TypeScript-Tutorials-F38020?style=for-the-badge)](https://www.totaltypescript.com/tutorials) |
| TypeScript Deep Dive | Free online book | [![Deep Dive](https://img.shields.io/badge/Book-TypeScript%20Deep%20Dive-3FB950?style=for-the-badge)](https://basarat.gitbook.io/typescript) |
| React TypeScript Cheatsheet | Typing React components, props and hooks | [![React TS](https://img.shields.io/badge/React-TypeScript%20Cheatsheet-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](https://react-typescript-cheatsheet.netlify.app/) |

### 🎮 Practice Platforms

| Resource | Description | Link |
|---|---|---|
| Type Challenges | Practice questions for the type system, from easy to extreme | [![Type Challenges](https://img.shields.io/badge/Type-Challenges-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://github.com/type-challenges/type-challenges) |
| Exercism: TypeScript track | Coding exercises with mentoring | [![Exercism](https://img.shields.io/badge/Exercism-TypeScript%20Track-009CAB?style=for-the-badge)](https://exercism.org/tracks/typescript) |

### 🔗 Related Pages

<p align="center">
  <a href="./cheat-sheet.md"><img src="https://img.shields.io/badge/TypeScript-Cheat%20Sheet-F38020?style=for-the-badge" alt="TypeScript Cheat Sheet" /></a>
  <a href="./notes.md"><img src="https://img.shields.io/badge/TypeScript-Notes-3FB950?style=for-the-badge" alt="TypeScript Notes" /></a>
</p>