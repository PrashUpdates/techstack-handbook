# 🎨 CSS3 Documentation

<p align="center">
  <a href="./README.md"><img src="https://img.shields.io/badge/Back%20to%20CSS3-6E7681?style=for-the-badge" alt="Back to CSS3" /></a>
  <a href="./cheat-sheet.md"><img src="https://img.shields.io/badge/Cheat%20Sheet-F38020?style=for-the-badge" alt="Cheat Sheet" /></a>
  <a href="./notes.md"><img src="https://img.shields.io/badge/Notes-3FB950?style=for-the-badge" alt="Notes" /></a>
</p>

> A complete guide to CSS3: what it is, how the browser applies it, the core layout and styling tools, best practices and a ready-to-use starter template.

## 📑 Contents

| # | Section | What's inside |
|---|---|---|
| 1 | [Executive Summary & Use Cases](#summary) | What CSS is and when to use it |
| 2 | [Core Concepts & Architecture](#concepts) | Cascade, selectors, box model, Flexbox, Grid, responsive design |
| 3 | [Standard Checklist & Best Practices](#checklist) | Features, setup steps, performance, accessibility and security tips |
| 4 | [Quick Start & Boilerplate Code](#quickstart) | A minimal, commented starter project |
| 5 | [Official Documentation & Resources](#resources) | Verified docs, tutorials and practice tools |

---

<a id="summary"></a>

## 1. Executive Summary & Use Cases

**CSS** (Cascading Style Sheets) is the language that controls how HTML content looks: colors, fonts, spacing, layout, animations and how a page adapts to different screens. **CSS3** is the name commonly used for modern CSS. It is not a single version: CSS is developed as many independent **modules** (Flexbox, Grid, Selectors, Animations and more), and each module evolves on its own.

**Primary purpose:** separate presentation from structure, so one stylesheet can control the look of an entire website.

| Language | Role |
|---|---|
| **HTML** | Structure and meaning |
| **CSS** | Style and layout |
| **JavaScript** | Behavior and interactivity |

### When to use it

| Use it when | Example |
|---|---|
| Styling any web page | Colors, fonts, spacing, borders |
| Building page layouts | Navigation bars, card grids, sidebars, dashboards |
| Making sites responsive | One design that works on phones, tablets and desktops |
| Adding motion | Hover effects, loaders, page transitions |
| Supporting themes | Dark mode, brand colors using variables |
| Styling for print | Clean printable pages with `@media print` |

---

<a id="concepts"></a>

## 2. Core Concepts & Architecture

### How a browser applies CSS

1. The browser parses the HTML into the **DOM**
2. It downloads and parses the CSS into the **CSSOM** (CSS Object Model)
3. For every element it resolves which rules apply (the **cascade**) and calculates final values
4. It builds the render tree and calculates **layout** (size and position of every box)
5. It **paints** pixels and composites layers on screen

### Anatomy of a CSS Rule

```css
selector {
  property: value;   /* a declaration */
}

/* Example */
.button {
  background-color: royalblue;
  color: white;
}
```

```
.button { background-color: royalblue; }
│         │                │
│         └── property     └── value
└── selector
```

### Three Ways to Add CSS

| Method | Example | When to use |
|---|---|---|
| **External** (recommended) | `<link rel="stylesheet" href="style.css">` | Almost always: reusable and cacheable |
| **Internal** | `<style> ... </style>` in `<head>` | Small demos, single-page experiments |
| **Inline** | `<p style="color: red;">` | Rarely: hard to maintain and overrides most rules |

### Selectors

| Selector | Example | Selects |
|---|---|---|
| Type | `p` | All `<p>` elements |
| Class | `.card` | Elements with `class="card"` |
| ID | `#header` | The element with `id="header"` |
| Universal | `*` | Every element |
| Attribute | `[type="email"]` | Elements with that attribute value |
| Grouping | `h1, h2, h3` | Several selectors at once |

**Combinators**

| Combinator | Example | Meaning |
|---|---|---|
| Descendant | `nav a` | Any `<a>` inside `<nav>` |
| Child | `ul > li` | `<li>` that is a direct child of `<ul>` |
| Adjacent sibling | `h2 + p` | The `<p>` right after an `<h2>` |
| General sibling | `h2 ~ p` | All `<p>` siblings after an `<h2>` |

**Pseudo-classes (state)**

| Pseudo-class | Matches |
|---|---|
| `:hover` | Pointer is over the element |
| `:focus` / `:focus-visible` | Element has keyboard focus (`:focus-visible` only when focus ring is needed) |
| `:active` | Element is being pressed |
| `:first-child` / `:last-child` | First / last child of its parent |
| `:nth-child(2n)` | Every second child |
| `:not(.hidden)` | Elements that do not match the selector |
| `:is(h1, h2)` | Any of the listed selectors |
| `:has(img)` | Parent that contains a matching child |
| `:checked` / `:disabled` / `:required` | Form control states |

**Pseudo-elements (parts)**

| Pseudo-element | Styles |
|---|---|
| `::before` / `::after` | Generated content before or after an element (needs `content`) |
| `::first-line` / `::first-letter` | First line or letter of text |
| `::placeholder` | Placeholder text in inputs |
| `::selection` | Text highlighted by the user |

### The Cascade, Specificity & Inheritance

When several rules target the same element, the browser decides the winner in this order:

1. **Importance**: `!important` declarations beat normal ones
2. **Specificity**: the more specific selector wins
3. **Source order**: if still tied, the rule written last wins

| Selector type | Specificity weight |
|---|---|
| Inline style | 1000 |
| ID (`#id`) | 100 |
| Class, attribute, pseudo-class (`.a`, `[x]`, `:hover`) | 10 |
| Type, pseudo-element (`p`, `::before`) | 1 |

```css
p { color: black; }          /* specificity: 1   */
.note { color: blue; }       /* specificity: 10  */
p.note { color: green; }     /* specificity: 11 → wins */
#intro { color: red; }       /* specificity: 100 → wins over all above */
```

**Inheritance:** some properties (like `color`, `font-family`, `line-height`) pass from parent to child automatically. Others (like `margin`, `border`, `padding`) do not. Use `inherit`, `initial` or `unset` to control this.

**Cascade layers:** `@layer` lets you group styles into ordered layers, so you control priority without fighting specificity.

### The Box Model

Every element is a rectangular box made of four layers:

```
┌──────────────── margin ────────────────┐
│  ┌──────────── border ──────────────┐  │
│  │  ┌──────── padding ──────────┐   │  │
│  │  │                           │   │  │
│  │  │         content           │   │  │
│  │  │                           │   │  │
│  │  └───────────────────────────┘   │  │
│  └──────────────────────────────────┘  │
└────────────────────────────────────────┘
```

| Layer | Property | Purpose |
|---|---|---|
| Content | `width`, `height` | The actual text or media |
| Padding | `padding` | Space inside the border |
| Border | `border` | Line around the padding |
| Margin | `margin` | Space outside the border |

**Always use `box-sizing: border-box`** so `width` includes padding and border, which makes sizing predictable:

```css
*, *::before, *::after {
  box-sizing: border-box;
}
```

### Display & Positioning

| `display` value | Behavior |
|---|---|
| `block` | Starts on a new line, takes full width |
| `inline` | Stays in the text flow, ignores width and height |
| `inline-block` | Inline flow, but accepts width and height |
| `flex` | Flexbox container (one-dimensional layout) |
| `grid` | Grid container (two-dimensional layout) |
| `none` | Removes the element from the page |

| `position` value | Behavior |
|---|---|
| `static` | Default, normal flow |
| `relative` | Normal flow, can be nudged with `top`, `left`... and becomes an anchor for children |
| `absolute` | Removed from flow, positioned against the nearest positioned ancestor |
| `fixed` | Stays fixed relative to the viewport |
| `sticky` | Scrolls normally, then sticks at a set offset |

### Units & Values

| Unit | Type | Notes |
|---|---|---|
| `px` | Absolute | Fixed pixels |
| `rem` | Relative | Relative to the root font size, best for text and spacing |
| `em` | Relative | Relative to the element's own (or parent's) font size |
| `%` | Relative | Relative to the parent |
| `vw` / `vh` | Viewport | 1% of viewport width / height |
| `dvh` | Viewport | Dynamic viewport height, handles mobile browser bars |
| `fr` | Grid | A fraction of available space in a grid |
| `ch` | Relative | Width of the "0" character, useful for text widths |

**Colors:** named (`tomato`), hex (`#2f81f7`), `rgb()`, `hsl()`, and modern formats such as `oklch()`. Add transparency with `rgb(0 0 0 / 50%)`.

**Math functions:** `calc()`, `min()`, `max()` and `clamp(min, preferred, max)` for fluid sizes.

```css
h1 { font-size: clamp(2rem, 5vw, 3.5rem); }
.sidebar { width: calc(100% - 250px); }
```

### Typography

| Property | Purpose |
|---|---|
| `font-family` | Typeface with fallbacks |
| `font-size` | Text size |
| `font-weight` | Thickness (400 normal, 700 bold) |
| `line-height` | Space between lines (1.5 to 1.7 is readable for body text) |
| `letter-spacing` | Space between letters |
| `text-align` | Horizontal alignment |
| `text-decoration` | Underline, line-through |
| `text-transform` | Uppercase, lowercase, capitalize |
| `@font-face` | Load a custom font file |

### Flexbox (one-dimensional layout)

Flexbox arranges items in a row **or** a column.

```css
.container {
  display: flex;
  justify-content: space-between; /* main axis */
  align-items: center;            /* cross axis */
  gap: 1rem;
}
```

| Container property | Purpose |
|---|---|
| `flex-direction` | `row` (default) or `column` |
| `flex-wrap` | Allow items to wrap onto new lines |
| `justify-content` | Align items along the main axis |
| `align-items` | Align items along the cross axis |
| `align-content` | Align wrapped lines |
| `gap` | Space between items |

| Item property | Purpose |
|---|---|
| `flex: 1` | Grow to fill available space |
| `flex-grow` / `flex-shrink` / `flex-basis` | Control growing, shrinking and starting size |
| `align-self` | Override alignment for one item |
| `order` | Change visual order |

### CSS Grid (two-dimensional layout)

Grid arranges items in rows **and** columns at the same time.

```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 1.5rem;
}
```

| Property | Purpose |
|---|---|
| `grid-template-columns` / `grid-template-rows` | Define the tracks |
| `grid-template-areas` | Name areas and lay them out visually |
| `gap` | Space between rows and columns |
| `grid-column` / `grid-row` | Place an item across tracks |
| `place-items` | Align items inside their cells |
| `repeat()`, `minmax()`, `auto-fit` | Build flexible, responsive grids |

| Use | Best choice |
|---|---|
| Navigation bar, button group, centering | Flexbox |
| Full page layout, card galleries, dashboards | Grid |
| Both together | Grid for the page, Flexbox inside components |

### Responsive Design

Responsive design makes one page work on every screen size. It needs `<meta name="viewport" content="width=device-width, initial-scale=1.0">` in the HTML.

```css
/* Mobile-first: base styles are for small screens */
.cards { display: grid; gap: 1rem; }

/* Larger screens */
@media (min-width: 768px) {
  .cards { grid-template-columns: repeat(2, 1fr); }
}

@media (min-width: 1024px) {
  .cards { grid-template-columns: repeat(3, 1fr); }
}
```

| Common breakpoint | Typical target |
|---|---|
| `480px` | Large phones |
| `768px` | Tablets |
| `1024px` | Small laptops |
| `1280px` | Desktops |

**Useful media features:** `min-width`, `max-width`, `orientation`, `prefers-color-scheme` (dark mode), `prefers-reduced-motion`, `print`.

**Container queries** let a component respond to the size of its parent instead of the whole screen (`@container`).

### Custom Properties (CSS Variables)

```css
:root {
  --primary: #0969da;
  --radius: 12px;
}

.button {
  background: var(--primary);
  border-radius: var(--radius);
}
```

Variables make themes, dark mode and consistent design systems easy to maintain.

### Transitions, Transforms & Animations

| Feature | Purpose | Example |
|---|---|---|
| `transition` | Smooth change between two states | `transition: background 0.3s ease;` |
| `transform` | Move, rotate, scale, skew | `transform: translateY(-4px) scale(1.05);` |
| `@keyframes` + `animation` | Multi-step animations | `animation: spin 1s linear infinite;` |

```css
@keyframes fade-in {
  from { opacity: 0; transform: translateY(10px); }
  to   { opacity: 1; transform: translateY(0); }
}

.card { animation: fade-in 0.5s ease both; }
```

### Modern CSS Features

| Feature | What it does |
|---|---|
| **Nesting** | Write child rules inside parent rules, like Sass |
| **`:has()`** | Select a parent based on its children |
| **`aspect-ratio`** | Keep a box at a fixed ratio, such as `16 / 9` |
| **`clamp()`** | Fluid values between a minimum and maximum |
| **Logical properties** | `margin-inline`, `padding-block` adapt to text direction |
| **`@layer`** | Control priority between groups of styles |
| **`@supports`** | Apply styles only if the browser supports a feature |
| **Container queries** | Component-level responsive design |

---

<a id="checklist"></a>

## 3. Standard Checklist & Best Practices

### ✅ Core Features

- [ ] Selectors, combinators, pseudo-classes and pseudo-elements
- [ ] Cascade, specificity and inheritance
- [ ] Box model (`margin`, `border`, `padding`, `box-sizing`)
- [ ] Colors, backgrounds, gradients and shadows
- [ ] Typography and web fonts
- [ ] `display` and `position`
- [ ] Flexbox layouts
- [ ] CSS Grid layouts
- [ ] Media queries and responsive design
- [ ] Custom properties (CSS variables)
- [ ] Transitions, transforms and animations
- [ ] Units (`rem`, `em`, `%`, `vw`, `vh`, `fr`)
- [ ] Modern features (`clamp()`, `:has()`, nesting, `aspect-ratio`)

### 🛠️ Setup Steps

- [ ] Install a code editor such as [VS Code](https://code.visualstudio.com/)
- [ ] Install the **Live Server** extension for instant browser refresh
- [ ] Create a project folder with `index.html` and `style.css`
- [ ] Link the stylesheet in the `<head>` with `<link rel="stylesheet" href="style.css">`
- [ ] Add the boilerplate from section 4
- [ ] Learn the browser **DevTools** (`F12`) to inspect and edit styles live

### 📋 Best Practices

**Organization & Maintainability**
- [ ] Use external stylesheets instead of inline styles
- [ ] Start with a small reset and `box-sizing: border-box`
- [ ] Define colors, spacing and fonts as CSS variables on `:root`
- [ ] Use a consistent naming convention such as **BEM** (`.card__title--large`)
- [ ] Keep selectors short and low in specificity (prefer classes over IDs)
- [ ] Avoid `!important` except for rare utility or override cases
- [ ] Group related rules and add short section comments
- [ ] Remove unused CSS regularly

**Layout & Responsiveness**
- [ ] Design mobile-first and add `min-width` media queries for larger screens
- [ ] Use Flexbox for one-dimensional layouts and Grid for two-dimensional layouts
- [ ] Use relative units (`rem`, `%`, `fr`) instead of fixed pixel widths
- [ ] Never hide horizontal overflow to cover a layout bug: find the cause
- [ ] Test on real devices and with DevTools device mode

**Accessibility**
- [ ] Keep text contrast at least 4.5:1 against its background (3:1 for large text)
- [ ] Never remove focus outlines without a visible replacement (use `:focus-visible`)
- [ ] Do not rely on color alone to communicate meaning
- [ ] Respect `prefers-reduced-motion` and disable heavy animations for those users
- [ ] Use `rem` for font sizes so users can scale text
- [ ] Keep interactive targets large enough to tap (about 44px)

**Performance**
- [ ] Animate `transform` and `opacity` instead of `width`, `height`, `top` or `left`
- [ ] Use `will-change` sparingly and only when needed
- [ ] Minify CSS for production
- [ ] Avoid `@import` in CSS files; use `<link>` tags instead
- [ ] Use `font-display: swap` for custom fonts
- [ ] Avoid overly deep or complex selectors

**Security**
- [ ] Never insert untrusted user input directly into style attributes or stylesheets
- [ ] Load stylesheets only from trusted sources, and use HTTPS
- [ ] Prefer external stylesheets so a Content Security Policy can restrict inline styles
- [ ] Add Subresource Integrity (`integrity` attribute) when using third-party CSS from a CDN

**Compatibility & Quality**
- [ ] Check browser support on [Can I use](https://caniuse.com/)
- [ ] Use `@supports` for newer features and provide a sensible fallback
- [ ] Use a tool like Autoprefixer when you need vendor prefixes
- [ ] Validate your CSS and check the DevTools console for ignored rules
- [ ] Use consistent indentation, lowercase properties and one declaration per line

---

<a id="quickstart"></a>

## 4. Quick Start & Boilerplate Code

Create two files in the same folder: `index.html` and `style.css`.

### `index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <!-- Required for responsive design on mobile -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>CSS3 Starter Page</title>

  <!-- Link the stylesheet -->
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <header class="site-header">
    <h1 class="logo">CSS3 Starter</h1>
    <nav class="nav">
      <a href="#features">Features</a>
      <a href="#contact">Contact</a>
    </nav>
  </header>

  <main>
    <section class="hero">
      <h2>Style the Web</h2>
      <p>Layouts, colors and motion with modern CSS.</p>
      <a class="btn" href="#features">Get Started</a>
    </section>

    <section id="features" class="cards">
      <article class="card">
        <h3>Flexbox</h3>
        <p>Align and distribute items in one dimension.</p>
      </article>
      <article class="card">
        <h3>Grid</h3>
        <p>Build full layouts in rows and columns.</p>
      </article>
      <article class="card">
        <h3>Responsive</h3>
        <p>One design that adapts to every screen.</p>
      </article>
    </section>
  </main>

  <footer id="contact" class="site-footer">
    <p>&copy; 2026 Example Website</p>
  </footer>
</body>
</html>
```

### `style.css`

```css
/* ==========================================================
   1. RESET: predictable sizing and sensible defaults
   ========================================================== */
*,
*::before,
*::after {
  box-sizing: border-box; /* width includes padding and border */
}

body {
  margin: 0;
}

img {
  max-width: 100%;
  display: block; /* removes the small gap under images */
}

/* ==========================================================
   2. DESIGN TOKENS: change the look in one place
   ========================================================== */
:root {
  --color-bg: #ffffff;
  --color-surface: #f6f8fa;
  --color-text: #1f2328;
  --color-primary: #0969da;
  --color-on-primary: #ffffff;
  --radius: 12px;
  --space: 1rem;
  --font-body: system-ui, -apple-system, "Segoe UI", Roboto, sans-serif;
}

/* Automatic dark mode based on the user's system setting */
@media (prefers-color-scheme: dark) {
  :root {
    --color-bg: #0d1117;
    --color-surface: #161b22;
    --color-text: #e6edf3;
    --color-primary: #58a6ff;
    --color-on-primary: #0d1117;
  }
}

/* ==========================================================
   3. BASE STYLES
   ========================================================== */
body {
  font-family: var(--font-body);
  background: var(--color-bg);
  color: var(--color-text);
  line-height: 1.6; /* comfortable reading */
}

/* ==========================================================
   4. LAYOUT WITH FLEXBOX: header and navigation
   ========================================================== */
.site-header {
  display: flex;
  justify-content: space-between; /* logo left, nav right */
  align-items: center;            /* vertical centering */
  padding: var(--space) 2rem;
  background: var(--color-surface);
}

.nav {
  display: flex;
  gap: 1.5rem;
}

.nav a {
  color: inherit;
  text-decoration: none;
}

.nav a:hover,
.nav a:focus-visible {
  color: var(--color-primary);
  text-decoration: underline;
}

/* ==========================================================
   5. HERO SECTION
   ========================================================== */
.hero {
  text-align: center;
  padding: 4rem 1rem;
}

.hero h2 {
  /* fluid size: min 2rem, grows with the screen, max 3.5rem */
  font-size: clamp(2rem, 5vw, 3.5rem);
  margin: 0 0 0.5rem;
}

/* ==========================================================
   6. BUTTON WITH TRANSITION
   ========================================================== */
.btn {
  display: inline-block;
  margin-top: var(--space);
  padding: 0.75rem 1.5rem;
  background: var(--color-primary);
  color: var(--color-on-primary);
  border-radius: var(--radius);
  text-decoration: none;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgb(0 0 0 / 20%);
}

.btn:focus-visible {
  outline: 3px solid var(--color-primary);
  outline-offset: 3px;
}

/* ==========================================================
   7. LAYOUT WITH GRID: responsive card gallery
   ========================================================== */
.cards {
  display: grid;
  /* as many 240px+ columns as fit, each sharing the space equally */
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 1.5rem;
  max-width: 1100px;
  margin-inline: auto; /* centers the grid */
  padding: 2rem 1rem;
}

.card {
  background: var(--color-surface);
  padding: 1.5rem;
  border-radius: var(--radius);
}

.card h3 {
  margin-top: 0;
}

/* ==========================================================
   8. FOOTER
   ========================================================== */
.site-footer {
  text-align: center;
  padding: 2rem 1rem;
  background: var(--color-surface);
}

/* ==========================================================
   9. RESPONSIVE: small screens
   ========================================================== */
@media (max-width: 600px) {
  .site-header {
    flex-direction: column;
    gap: 0.5rem;
  }
}

/* ==========================================================
   10. ACCESSIBILITY: respect reduced-motion preference
   ========================================================== */
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    transition: none !important;
    animation: none !important;
  }
}
```

**What this starter demonstrates:** reset and `box-sizing`, CSS variables, automatic dark mode, a Flexbox header, a Grid card gallery, fluid typography with `clamp()`, a hover transition, visible keyboard focus, responsive media queries and reduced-motion support.

---

<a id="resources"></a>

## 5. Official Documentation & Resources

### 📚 Official Documentation

| Resource | Description | Link |
|---|---|---|
| MDN Web Docs: CSS | The most complete CSS reference and guides | [![MDN](https://img.shields.io/badge/MDN-CSS%20Docs-000000?style=for-the-badge&logo=mdnwebdocs&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS) |
| W3C CSS Specifications | The official standards and modules | [![W3C](https://img.shields.io/badge/W3C-CSS%20Specs-2F81F7?style=for-the-badge&logo=w3c&logoColor=white)](https://www.w3.org/Style/CSS/) |
| W3C CSS Validator | Check your CSS for errors | [![Validator](https://img.shields.io/badge/W3C-CSS%20Validator-3FB950?style=for-the-badge&logo=w3c&logoColor=white)](https://jigsaw.w3.org/css-validator/) |
| Can I use | Browser support tables for CSS features | [![Can I use](https://img.shields.io/badge/Can%20I%20use-Browser%20Support-F38020?style=for-the-badge)](https://caniuse.com/) |

### 🎓 Recommended Tutorials

| Resource | Description | Link |
|---|---|---|
| web.dev: Learn CSS | Free structured CSS course | [![web.dev](https://img.shields.io/badge/web.dev-Learn%20CSS-F38020?style=for-the-badge)](https://web.dev/learn/css) |
| MDN: Learn CSS | Beginner-friendly learning path | [![MDN Learn](https://img.shields.io/badge/MDN-Learn%20CSS-F38020?style=for-the-badge&logo=mdnwebdocs&logoColor=white)](https://developer.mozilla.org/en-US/docs/Learn/CSS) |
| CSS-Tricks: Flexbox Guide | Visual guide to every Flexbox property | [![Flexbox](https://img.shields.io/badge/CSS--Tricks-Flexbox%20Guide-1572B6?style=for-the-badge&logo=css3&logoColor=white)](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) |
| CSS-Tricks: Grid Guide | Visual guide to every Grid property | [![Grid](https://img.shields.io/badge/CSS--Tricks-Grid%20Guide-1572B6?style=for-the-badge&logo=css3&logoColor=white)](https://css-tricks.com/snippets/css/complete-guide-grid/) |

### 🎮 Practice Games

| Resource | Description | Link |
|---|---|---|
| Flexbox Froggy | Learn Flexbox by guiding a frog | [![Flexbox Froggy](https://img.shields.io/badge/Play-Flexbox%20Froggy-3FB950?style=for-the-badge)](https://flexboxfroggy.com/) |
| CSS Grid Garden | Learn Grid by growing a garden | [![Grid Garden](https://img.shields.io/badge/Play-Grid%20Garden-3FB950?style=for-the-badge)](https://cssgridgarden.com/) |

### 🔗 Related Pages

<p align="center">
  <a href="./cheat-sheet.md"><img src="https://img.shields.io/badge/CSS3-Cheat%20Sheet-F38020?style=for-the-badge" alt="CSS3 Cheat Sheet" /></a>
  <a href="./notes.md"><img src="https://img.shields.io/badge/CSS3-Notes-3FB950?style=for-the-badge" alt="CSS3 Notes" /></a>
</p>