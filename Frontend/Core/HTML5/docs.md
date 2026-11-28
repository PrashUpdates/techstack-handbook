# 📘 HTML5 Documentation

<p align="center">
    <a href="https://github.com/PrashUpdates/techstack-handbook/blob/main/README.md"><img src="https://img.shields.io/badge/Back%20to%20main-6E7681?style=for-the-badge" alt="Back to main" /></a>
  <a href="./cheat-sheet.md"><img src="https://img.shields.io/badge/Cheat%20Sheet-F38020?style=for-the-badge" alt="Cheat Sheet" /></a>
  <a href="./notes.md"><img src="https://img.shields.io/badge/Notes-3FB950?style=for-the-badge" alt="Notes" /></a>
</p>

> A complete guide to HTML5: what it is, how it works, best practices and a ready-to-use starter template.

## 📑 Contents

| # | Section | What's inside |
|---|---|---|
| 1 | [Executive Summary & Use Cases](#summary) | What HTML5 is and when to use it |
| 2 | [Core Concepts & Architecture](#concepts) | How browsers use HTML, terminology, semantic tags |
| 3 | [Standard Checklist & Best Practices](#checklist) | Features, setup steps, security and performance tips |
| 4 | [Quick Start & Boilerplate Code](#quickstart) | A minimal, commented starter page |
| 5 | [Official Documentation & Resources](#resources) | Verified docs and tutorials |

---

<a id="summary"></a>

## 1. Executive Summary & Use Cases

**HTML5** (HyperText Markup Language, version 5) is the standard language used to describe the structure and content of web pages. It tells the browser what each piece of content *is*: a heading, a paragraph, a link, an image, a form.

**Primary purpose:** structure content so browsers, search engines and assistive technologies can understand it.

| Language | Role |
|---|---|
| **HTML** | Structure and meaning |
| **CSS** | Style and layout |
| **JavaScript** | Behavior and interactivity |

### When to use it

| Use it when | Example |
|---|---|
| Building any web page or web app | Landing pages, dashboards, portfolios |
| Creating forms and collecting input | Login, signup, search |
| Embedding media | Images, audio, video |
| Improving SEO and accessibility | Semantic tags, `alt` text, labels |
| Writing email templates and documents | Newsletters, static docs |

---

<a id="concepts"></a>

## 2. Core Concepts & Architecture

### How a browser uses HTML

1. The browser downloads the HTML file
2. It parses the HTML into a tree called the **DOM** (Document Object Model)
3. It combines the DOM with CSS to build the render tree
4. It paints the page; JavaScript can modify the DOM at any time

### Key Terminology

| Term | Meaning |
|---|---|
| **Element** | A full unit: opening tag + content + closing tag, e.g. `<p>Hello</p>` |
| **Tag** | The markup that defines an element, e.g. `<p>` and `</p>` |
| **Attribute** | Extra information inside a tag, e.g. `href`, `src`, `alt`, `class` |
| **Void element** | An element with no closing tag, e.g. `<img>`, `<br>`, `<input>` |
| **Block vs inline** | Block elements start on a new line (`<div>`, `<p>`); inline elements stay in the flow (`<span>`, `<a>`) |
| **Semantic element** | A tag whose name describes its meaning, e.g. `<header>`, `<nav>`, `<article>` |
| **DOM** | The tree representation of the page that JavaScript can read and change |
| **Doctype** | `<!DOCTYPE html>` tells the browser to use standards mode |

### Anatomy of an Element

```html
<a href="https://example.com" target="_blank">Visit site</a>
│   │                         │                │
│   └── attribute: name="value"                └── content
└── opening tag                                   closing tag: </a>
```

### Basic Page Anatomy

```
<!DOCTYPE html>
└── <html lang="en">
    ├── <head>      → metadata (title, charset, viewport, links to CSS)
    └── <body>      → visible content
        ├── <header>
        ├── <nav>
        ├── <main>
        │   ├── <section> / <article>
        │   └── <aside>
        └── <footer>
```

### Semantic Elements

| Element | Use for |
|---|---|
| `<header>` | Intro content or navigation area of a page or section |
| `<nav>` | Main navigation links |
| `<main>` | The primary content (only one per page) |
| `<section>` | A themed group of content, usually with a heading |
| `<article>` | Self-contained content (blog post, news item) |
| `<aside>` | Related side content (sidebar, tips) |
| `<footer>` | Footer of a page or section |
| `<figure>` / `<figcaption>` | An image or diagram with a caption |

### Common Attributes

| Attribute | Used on | Purpose |
|---|---|---|
| `href` | `<a>`, `<link>` | Destination URL |
| `src` | `<img>`, `<script>`, `<video>` | Source file |
| `alt` | `<img>` | Text alternative for the image |
| `id` | Any element | Unique identifier |
| `class` | Any element | Group elements for CSS and JavaScript |
| `type` | `<input>`, `<button>` | Kind of input or button |
| `name` | Form controls | Key used when the form is submitted |
| `required` | Form controls | Field must be filled before submitting |

---

<a id="checklist"></a>

## 3. Standard Checklist & Best Practices

### ✅ Core Features

- [ ] Document structure (`<!DOCTYPE>`, `<html>`, `<head>`, `<body>`)
- [ ] Headings (`<h1>` to `<h6>`) and paragraphs
- [ ] Links and navigation (`<a>`, `<nav>`)
- [ ] Images with `alt` text (`<img>`, `<picture>`)
- [ ] Lists (ordered, unordered, description)
- [ ] Tables (`<table>`, `<thead>`, `<tbody>`, `<th>`, `<td>`)
- [ ] Forms and input types (`<form>`, `<input>`, `<select>`, `<textarea>`, `<button>`)
- [ ] Form validation attributes (`required`, `pattern`, `min`, `max`)
- [ ] Audio and video (`<audio>`, `<video>`)
- [ ] Semantic layout elements
- [ ] Global attributes (`id`, `class`, `data-*`, `hidden`)

### 🛠️ Setup Steps

- [ ] Install a code editor such as [VS Code](https://code.visualstudio.com/)
- [ ] Install the **Live Server** extension for instant browser refresh
- [ ] Create a project folder with an `index.html` file
- [ ] Add the boilerplate from section 4
- [ ] Right-click the file and choose **Open with Live Server**

### 📋 Best Practices

**Structure & Semantics**
- [ ] Always start with `<!DOCTYPE html>`
- [ ] Set the language: `<html lang="en">`
- [ ] Use only one `<h1>` per page and do not skip heading levels
- [ ] Use semantic tags instead of generic `<div>` wherever possible
- [ ] Keep HTML for structure; put styling in CSS and behavior in JavaScript

**Accessibility**
- [ ] Add meaningful `alt` text to every informative image (use `alt=""` for decorative ones)
- [ ] Connect every input to a `<label>` using `for` and `id`
- [ ] Use `<button>` for actions and `<a>` for navigation
- [ ] Make sure the page works with keyboard only

**SEO**
- [ ] Write a unique `<title>` and `<meta name="description">` for each page
- [ ] Use descriptive link text (avoid "click here")

**Performance**
- [ ] Add `width` and `height` on images to prevent layout shift
- [ ] Use `loading="lazy"` for images below the fold
- [ ] Load scripts with `defer` in the `<head>`, or place them just before `</body>`
- [ ] Compress images and use modern formats

**Security**
- [ ] Add `rel="noopener noreferrer"` to links with `target="_blank"`
- [ ] Never insert raw user input into the page without sanitizing it
- [ ] Use `sandbox` on untrusted `<iframe>` content
- [ ] Use HTTPS for all external resources

**Quality**
- [ ] Validate your HTML with the W3C Validator
- [ ] Use consistent indentation and lowercase tag names

---

<a id="quickstart"></a>

## 4. Quick Start & Boilerplate Code

Save this as `index.html` and open it in a browser:

```html
<!DOCTYPE html>
<!-- Tells the browser this is an HTML5 document -->
<html lang="en">
<head>
  <!-- Character encoding: supports all languages and emojis -->
  <meta charset="UTF-8" />

  <!-- Makes the page responsive on mobile devices -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <!-- SEO: description shown in search results -->
  <meta name="description" content="A short description of this page." />

  <!-- Title shown in the browser tab -->
  <title>HTML5 Starter Page</title>

  <!-- Link your stylesheet and script here -->
  <!-- <link rel="stylesheet" href="style.css" /> -->
  <!-- <script src="main.js" defer></script> -->
</head>
<body>
  <header>
    <h1>Hello, World!</h1>
    <nav>
      <a href="#about">About</a>
      <a href="#contact">Contact</a>
    </nav>
  </header>

  <main>
    <section id="about">
      <h2>About</h2>
      <p>This page is built with semantic HTML5.</p>
      <img src="photo.jpg" alt="Describe the image here" width="300" height="200" loading="lazy" />
    </section>

    <section id="contact">
      <h2>Contact</h2>
      <form>
        <label for="email">Email</label>
        <input type="email" id="email" name="email" required />
        <button type="submit">Send</button>
      </form>
    </section>
  </main>

  <footer>
    <p>&copy; 2026 Example Website</p>
  </footer>
</body>
</html>
```

**What this page demonstrates:** document structure, mobile-friendly viewport, SEO metadata, semantic layout, an accessible image, and a validated form with a label.

---

<a id="resources"></a>

## 5. Official Documentation & Resources

### 📚 Official Documentation

| Resource | Description | Link |
|---|---|---|
| MDN Web Docs: HTML | The most complete HTML reference | [![MDN](https://img.shields.io/badge/MDN-Docs-000000?style=for-the-badge&logo=mdnwebdocs&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML) |
| HTML Living Standard | The official specification | [![WHATWG](https://img.shields.io/badge/WHATWG-Spec-2F81F7?style=for-the-badge)](https://html.spec.whatwg.org/) |
| W3C Markup Validator | Check your HTML for errors | [![W3C](https://img.shields.io/badge/W3C-Validator-3FB950?style=for-the-badge&logo=w3c&logoColor=white)](https://validator.w3.org/) |

### 🎓 Recommended Tutorials

| Resource | Description | Link |
|---|---|---|
| web.dev: Learn HTML | Free structured HTML course | [![web.dev](https://img.shields.io/badge/web.dev-Learn%20HTML-F38020?style=for-the-badge)](https://web.dev/learn/html) |
| MDN: Learn web development | Beginner-friendly learning path | [![MDN Learn](https://img.shields.io/badge/MDN-Learn-F38020?style=for-the-badge&logo=mdnwebdocs&logoColor=white)](https://developer.mozilla.org/en-US/docs/Learn) |

### 🔗 Related Pages

<p align="center">
  <a href="./cheat-sheet.md"><img src="https://img.shields.io/badge/HTML5-Cheat%20Sheet-F38020?style=for-the-badge" alt="HTML5 Cheat Sheet" /></a>
  <a href="./notes.md"><img src="https://img.shields.io/badge/HTML5-Notes-3FB950?style=for-the-badge" alt="HTML5 Notes" /></a>
</p>