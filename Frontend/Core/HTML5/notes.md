# 📝 HTML5 Notes

[⬅ Back to HTML5](./README.md) · [📘 Docs](./docs.md) · [⚡ Cheat Sheet](./cheat-sheet.md)

> Short study notes, common mistakes and practice ideas to go with the docs.

---

## 🧠 Key Takeaways

- HTML describes the structure and meaning of content, not how it looks
- Semantic tags (`<header>`, `<main>`, `<footer>`) improve accessibility and SEO
- Every image needs `alt` text and every input needs a `<label>`
- Use only one `<h1>` per page
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

---

## 🧪 Practice Exercises

- [ ] Build a personal portfolio page using only semantic tags
- [ ] Build a signup form with validation
- [ ] Build a table of a weekly schedule
- [ ] Add an image gallery with `<figure>` and `<figcaption>`
- [ ] Make a page that passes the W3C validator with zero errors

---

## 📊 Topic Progress

- [ ] Document structure
- [ ] Text and headings
- [ ] Links and images
- [ ] Lists and tables
- [ ] Forms and validation
- [ ] Semantic elements
- [ ] Audio and video
- [ ] Accessibility basics
- [ ] SEO basics

---

## ❓ Frequently Asked Questions

**What is the difference between `<div>` and `<section>`?**
`<div>` has no meaning and is only a generic container. `<section>` groups related content under a heading.

**Do I need `<!DOCTYPE html>`?**
Yes. Without it, browsers may switch to quirks mode and render the page inconsistently.

**What is the difference between `id` and `class`?**
An `id` must be unique on a page. A `class` can be reused on many elements.