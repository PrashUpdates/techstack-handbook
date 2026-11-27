# ⚡ HTML5 Cheat Sheet

[⬅ Back to HTML5](./README.md) · [📘 Docs](./docs.md) · [📝 Notes](./notes.md)

---

## 🧱 Document Structure

| Tag | Purpose |
|---|---|
| `<!DOCTYPE html>` | Declares an HTML5 document |
| `<html lang="en">` | Root element with language |
| `<head>` | Metadata container |
| `<meta charset="UTF-8">` | Character encoding |
| `<meta name="viewport" ...>` | Mobile responsiveness |
| `<title>` | Browser tab title |
| `<link>` | Link CSS or icons |
| `<script>` | Add JavaScript |
| `<body>` | Visible content |

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
| `<code>` / `<pre>` | Inline code / preformatted block |
| `<blockquote>` | Long quotation |

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

## 🔗 Links & Media

| Tag | Example |
|---|---|
| Link | `<a href="https://example.com">Text</a>` |
| New tab link | `<a href="..." target="_blank" rel="noopener noreferrer">` |
| Image | `<img src="a.jpg" alt="Description" width="300" height="200">` |
| Audio | `<audio src="a.mp3" controls></audio>` |
| Video | `<video src="a.mp4" controls></video>` |
| Iframe | `<iframe src="..." title="Description"></iframe>` |

## 📋 Lists & Tables

| Element | Tags |
|---|---|
| Unordered list | `<ul><li>Item</li></ul>` |
| Ordered list | `<ol><li>Item</li></ol>` |
| Description list | `<dl><dt>Term</dt><dd>Definition</dd></dl>` |
| Table | `<table>` → `<thead>`, `<tbody>` → `<tr>` → `<th>`, `<td>` |

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

### Input Types

| Type | Use |
|---|---|
| `text` | Plain text |
| `email` | Email address |
| `password` | Hidden text |
| `number` | Numbers |
| `date` | Date picker |
| `checkbox` | Multiple choices |
| `radio` | Single choice |
| `file` | File upload |
| `range` | Slider |
| `color` | Color picker |
| `search` | Search field |
| `tel` / `url` | Phone / website |

### Validation Attributes

`required` · `minlength` · `maxlength` · `min` · `max` · `pattern` · `placeholder` · `disabled` · `readonly` · `autofocus`

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

## 🔣 Common Entities

| Entity | Result |
|---|---|
| `&lt;` | < |
| `&gt;` | > |
| `&amp;` | & |
| `&quot;` | " |
| `&nbsp;` | non-breaking space |
| `&copy;` | © |

## 💡 Quick Reminders

- One `<h1>` per page
- Every `<img>` needs `alt`
- Every input needs a `<label>`
- Use semantic tags before `<div>`
- Validate at [validator.w3.org](https://validator.w3.org/)