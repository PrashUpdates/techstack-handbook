# ⚡ HTML5 Cheat Sheet

<p align="center">
  <a href="./README.md"><img src="https://img.shields.io/badge/Back%20to%20HTML5-6E7681?style=for-the-badge" alt="Back to HTML5" /></a>
  <a href="./docs.md"><img src="https://img.shields.io/badge/Docs-2F81F7?style=for-the-badge" alt="Docs" /></a>
  <a href="./notes.md"><img src="https://img.shields.io/badge/Notes-3FB950?style=for-the-badge" alt="Notes" /></a>
</p>

> A quick reference for the most-used HTML5 tags, attributes and patterns.

**Jump to:** [Structure](#structure) · [Head & Meta](#head-meta) · [Text](#text) · [Semantic Layout](#semantic) · [Links & Media](#media) · [Lists & Tables](#lists) · [Forms](#forms) · [Interactive](#interactive) · [Attributes](#attributes) · [Accessibility](#a11y) · [Entities](#entities) · [Deprecated](#deprecated)

---

<a id="structure"></a>

## 🧱 Document Structure

| Tag | Purpose |
|---|---|
| `<!DOCTYPE html>` | Declares an HTML5 document |
| `<html lang="en">` | Root element with page language |
| `<head>` | Metadata container (not visible) |
| `<body>` | Visible page content |

<a id="head-meta"></a>

## 🧠 Head & Meta

| Tag | Purpose |
|---|---|
| `<meta charset="UTF-8">` | Character encoding |
| `<meta name="viewport" content="width=device-width, initial-scale=1.0">` | Mobile responsiveness |
| `<meta name="description" content="...">` | Search result description |
| `<title>` | Browser tab title |
| `<link rel="stylesheet" href="style.css">` | Attach a CSS file |
| `<link rel="icon" href="favicon.ico">` | Tab icon |
| `<script src="main.js" defer></script>` | Load JavaScript without blocking the page |

---

<a id="text"></a>

## ✍️ Text

| Tag | Purpose |
|---|---|
| `<h1>` to `<h6>` | Headings |
| `<p>` | Paragraph |
| `<br>` | Line break |
| `<hr>` | Horizontal rule |
| `<strong>` | Important text (bold) |
| `<em>` | Emphasized text (italic) |
| `<mark>` | Highlighted text |
| `<small>` | Side comments, fine print |
| `<sub>` / `<sup>` | Subscript / superscript |
| `<code>` / `<pre>` | Inline code / preformatted block |
| `<blockquote>` / `<q>` | Long quote / short quote |
| `<abbr title="...">` | Abbreviation with tooltip |
| `<time datetime="2026-01-01">` | Machine-readable date or time |

<a id="semantic"></a>

## 🏛️ Semantic Layout

| Tag | Purpose |
|---|---|
| `<header>` | Intro or top area |
| `<nav>` | Navigation links |
| `<main>` | Main content (one per page) |
| `<section>` | Themed content group |
| `<article>` | Self-contained content |
| `<aside>` | Side content |
| `<footer>` | Bottom area |
| `<figure>` + `<figcaption>` | Media with caption |

---

<a id="media"></a>

## 🔗 Links & Media

| Element | Example |
|---|---|
| Link | `<a href="https://example.com">Text</a>` |
| New tab link | `<a href="..." target="_blank" rel="noopener noreferrer">` |
| Page anchor | `<a href="#section-id">Jump</a>` |
| Email / phone | `<a href="mailto:me@site.com">` · `<a href="tel:+123456789">` |
| Image | `<img src="a.jpg" alt="Description" width="300" height="200">` |
| Lazy image | `<img src="a.jpg" alt="..." loading="lazy">` |
| Audio | `<audio src="a.mp3" controls></audio>` |
| Video | `<video src="a.mp4" controls></video>` |
| Iframe | `<iframe src="..." title="Description"></iframe>` |

### 🖼️ Responsive Images

```html
<!-- Different image per screen size -->
<picture>
  <source media="(min-width: 800px)" srcset="large.jpg" />
  <img src="small.jpg" alt="Description" />
</picture>
```

---

<a id="lists"></a>

## 📋 Lists & Tables

| Element | Tags |
|---|---|
| Unordered list | `<ul><li>Item</li></ul>` |
| Ordered list | `<ol><li>Item</li></ol>` |
| Description list | `<dl><dt>Term</dt><dd>Definition</dd></dl>` |
| Table | `<table>` → `<thead>`, `<tbody>` → `<tr>` → `<th>`, `<td>` |
| Merge cells | `colspan="2"` · `rowspan="2"` |

---

<a id="forms"></a>

## 📝 Forms

| Tag | Purpose |
|---|---|
| `<form action="" method="">` | Form container |
| `<label for="id">` | Label linked to an input |
| `<input>` | Input field (type decides behavior) |
| `<textarea>` | Multi-line text |
| `<select>` + `<option>` | Dropdown |
| `<button type="submit">` | Submit button |
| `<fieldset>` + `<legend>` | Group related inputs |
| `<datalist>` | Suggestions for an input |

### Input Types

| Type | Use |
|---|---|
| `text` | Plain text |
| `email` | Email address |
| `password` | Hidden text |
| `number` | Numbers |
| `date` / `time` | Date / time picker |
| `checkbox` | Multiple choices |
| `radio` | Single choice |
| `file` | File upload |
| `range` | Slider |
| `color` | Color picker |
| `search` | Search field |
| `tel` / `url` | Phone / website |
| `hidden` | Value not shown to the user |

### Validation Attributes

`required` · `minlength` · `maxlength` · `min` · `max` · `pattern` · `placeholder` · `disabled` · `readonly` · `autofocus` · `autocomplete`

---

<a id="interactive"></a>

## 🎛️ Interactive Elements

| Tag | Purpose |
|---|---|
| `<details>` + `<summary>` | Collapsible section, no JavaScript needed |
| `<dialog>` | Modal or popup window |
| `<progress value="50" max="100">` | Progress bar |
| `<meter value="0.6">` | Value within a known range |

```html
<details>
  <summary>Click to expand</summary>
  <p>Hidden content appears here.</p>
</details>
```

---

<a id="attributes"></a>

## 🏷️ Global Attributes

| Attribute | Purpose |
|---|---|
| `id` | Unique identifier |
| `class` | Group for CSS / JS |
| `style` | Inline CSS (avoid when possible) |
| `title` | Tooltip text |
| `hidden` | Hides the element |
| `data-*` | Custom data |
| `lang` | Language of the element |
| `tabindex` | Keyboard focus order |
| `contenteditable` | Makes content editable |

---

<a id="a11y"></a>

## ♿ Accessibility Quick Reference

| Attribute | Purpose |
|---|---|
| `alt` | Text alternative for images |
| `aria-label` | Accessible name when no visible text exists |
| `aria-hidden="true"` | Hides decorative content from screen readers |
| `role` | Defines an element's purpose (use only if no native tag fits) |
| `aria-live` | Announces dynamic content changes |

**Rule of thumb:** use the correct native HTML element first, and add ARIA only when needed.

---

<a id="entities"></a>

## 🔣 Common Entities

| Entity | Result |
|---|---|
| `&lt;` | `<` |
| `&gt;` | `>` |
| `&amp;` | `&` |
| `&quot;` | `"` |
| `&nbsp;` | non-breaking space |
| `&copy;` | © symbol |

---

<a id="deprecated"></a>

## 🚫 Deprecated Tags (Don't Use)

| Old tag | Use instead |
|---|---|
| `<center>` | CSS `text-align: center` |
| `<font>` | CSS `font-family`, `color`, `font-size` |
| `<b>` / `<i>` for emphasis | `<strong>` / `<em>` |
| `<marquee>` | CSS animations |
| `<frame>` / `<frameset>` | `<iframe>` or CSS layout |

---

## 🚀 Mini Boilerplate

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Page Title</title>
</head>
<body>
  <h1>Hello, World!</h1>
</body>
</html>
```

---

## 💡 Quick Reminders

- One `<h1>` per page
- Every `<img>` needs `alt`
- Every input needs a `<label>`
- Use semantic tags before `<div>`
- Validate your markup at [validator.w3.org](https://validator.w3.org/)