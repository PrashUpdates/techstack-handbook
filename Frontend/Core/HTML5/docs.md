# 📘 HTML5 Documentation

[⬅ Back to HTML5](./README.md)

---

## 1. Executive Summary & Use Cases

**HTML5** (HyperText Markup Language, version 5) is the standard language used to describe the structure and content of web pages. It tells the browser what each piece of content *is*: a heading, a paragraph, a link, an image, a form.

**Primary purpose:** structure content so browsers, search engines and assistive technologies can understand it. HTML handles structure, CSS handles style, JavaScript handles behavior.

| Use it when | Example |
|---|---|
| Building any web page or web app | Landing pages, dashboards, portfolios |
| Creating forms and collecting input | Login, signup, search |
| Embedding media | Images, audio, video |
| Improving SEO and accessibility | Semantic tags, `alt` text, labels |
| Writing email templates and documents | Newsletters, static docs |

---

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

---

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

- [ ] Install a code editor (VS Code)
- [ ] Install the **Live Server** extension
- [ ] Create a project folder with `index.html`
- [ ] Add the boilerplate (see section 4)
- [ ] Open with Live Server and check the result

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
- [ ] Load scripts with `defer` at the end of `<head>` or before `</body>`
- [ ] Compress and use modern image formats

**Security**
- [ ] Add `rel="noopener noreferrer"` to links with `target="_blank"`
- [ ] Never insert raw user input into the page without sanitizing it
- [ ] Use `sandbox` on untrusted `<iframe>` content
- [ ] Use HTTPS for all external resources

**Quality**
- [ ] Validate your HTML with the W3C Validator
- [ ] Use consistent indentation and lowercase tag names

---

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
  <title>My First HTML5 Page</title>

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
      <p>This is my first page built with semantic HTML5.</p>
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
    <p>&copy; 2026 My Website</p>
  </footer>
</body>
</html>
```

---

## 5. Official Documentation & Resources

### 📚 Official Documentation

| Resource | Link |
|---|---|
| MDN Web Docs: HTML | [developer.mozilla.org/en-US/docs/Web/HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) |
| HTML Living Standard (WHATWG spec) | [html.spec.whatwg.org](https://html.spec.whatwg.org/) |
| W3C Markup Validator | [validator.w3.org](https://validator.w3.org/) |

### 🎓 Recommended Tutorials

| Resource | Link |
|---|---|
| web.dev: Learn HTML | [web.dev/learn/html](https://web.dev/learn/html) |
| MDN: Learn web development | [developer.mozilla.org/en-US/docs/Learn](https://developer.mozilla.org/en-US/docs/Learn) |

### 🔗 Related Pages

- [⚡ HTML5 Cheat Sheet](./cheat-sheet.md)
- [📝 HTML5 Notes](./notes.md)