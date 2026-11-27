# 📝 HTML5 Notes

<p align="center">
  <a href="./README.md"><img src="https://img.shields.io/badge/Back%20to%20HTML5-6E7681?style=flat-square" alt="Back to HTML5" /></a>
  <a href="./docs.md"><img src="https://img.shields.io/badge/Docs-2F81F7?style=flat-square" alt="Docs" /></a>
  <a href="./cheat-sheet.md"><img src="https://img.shields.io/badge/Cheat%20Sheet-F38020?style=flat-square" alt="Cheat Sheet" /></a>
</p>

> Short study notes, common mistakes and practice exercises to use alongside the docs.

---

## 🧠 Key Takeaways

- HTML describes the **structure and meaning** of content, not how it looks
- Semantic tags (`<header>`, `<main>`, `<footer>`) improve accessibility and SEO
- Every image needs `alt` text and every input needs a `<label>`
- Use only one `<h1>` per page and keep headings in order
- Use `<button>` for actions and `<a>` for navigation
- Validate your markup to catch mistakes early

---

## ⚠️ Common Mistakes

| Mistake | Fix |
|---|---|
| Using `<div>` for everything | Use semantic tags like `<section>`, `<nav>`, `<article>` |
| Missing `alt` on images | Always add descriptive `alt` text |
| Skipping heading levels (`<h1>` to `<h4>`) | Go in order: `<h1>`, `<h2>`, `<h3>` |
| Inputs without labels | Connect with `<label for="id">` |
| Forgetting `<meta name="viewport">` | Add it so the page works on mobile |
| Using inline `style` everywhere | Move styles to a CSS file |
| Using `<br>` for spacing | Use CSS margin and padding |
| Using a link as a button (or the reverse) | `<a>` for navigation, `<button>` for actions |
| Duplicate `id` values | Each `id` must be unique on the page |
| Forgetting `rel="noopener noreferrer"` on `target="_blank"` links | Always add it for safety |

---

## 💡 Quick Tips

- Write tags in lowercase and indent nested elements
- Use `Ctrl + /` in VS Code to comment and uncomment lines
- Press `!` then `Tab` in VS Code to generate the HTML boilerplate
- Use browser DevTools (`F12`) to inspect any page's HTML
- Name `id` and `class` values clearly, like `main-nav` instead of `box1`

---

## 🧪 Practice Exercises

**🟢 Beginner**
- [ ] Build a simple page with a heading, paragraph and image
- [ ] Create an ordered and an unordered list
- [ ] Build a table of a weekly schedule

**🟡 Intermediate**
- [ ] Build a portfolio page using only semantic tags
- [ ] Build a signup form with validation
- [ ] Add an image gallery with `<figure>` and `<figcaption>`

**🔴 Challenge**
- [ ] Build a multi-section landing page with a working navigation menu
- [ ] Make a page that passes the W3C validator with zero errors
- [ ] Make a form that works with keyboard only

---

## ✅ Self-Check

You are comfortable with HTML5 basics if you can:

- [ ] Write a full HTML5 page from memory
- [ ] Explain the difference between block and inline elements
- [ ] Choose the right semantic tag for a layout
- [ ] Build a form with labels and validation
- [ ] Add images, audio and video correctly
- [ ] Explain why `alt` text and labels matter

---

## ❓ Frequently Asked Questions

**What is the difference between `<div>` and `<section>`?**
`<div>` has no meaning and is only a generic container. `<section>` groups related content, usually under a heading.

**Do I need `<!DOCTYPE html>`?**
Yes. Without it, browsers may switch to quirks mode and render the page inconsistently.

**What is the difference between `id` and `class`?**
An `id` must be unique on a page. A `class` can be reused on many elements.

**Should I use `<b>` or `<strong>`?**
Use `<strong>` for important text. Use `<b>` only for plain bold styling with no extra meaning. For pure styling, CSS is better.

**Where should I put my `<script>` tag?**
Put it in `<head>` with the `defer` attribute, or just before `</body>`, so it doesn't block the page from loading.

**Is HTML a programming language?**
No. HTML is a markup language that structures content. Logic and behavior come from JavaScript.