# ⚡ CSS3 Cheat Sheet

<p align="center">
  <a href="https://github.com/PrashUpdates/techstack-handbook/blob/main/README.md#frontend"><img src="https://img.shields.io/badge/Back%20to%20main-6E7681?style=for-the-badge" alt="Back to main" /></a>
  <a href="./docs.md"><img src="https://img.shields.io/badge/Docs-2F81F7?style=for-the-badge" alt="Docs" /></a>
  <a href="./notes.md"><img src="https://img.shields.io/badge/Notes-3FB950?style=for-the-badge" alt="Notes" /></a>
</p>

> A quick reference for the most-used CSS selectors, properties, layout tools and ready-to-copy patterns.

**Jump to:**
[Syntax](#syntax) · [Selectors](#selectors) · [Specificity](#specificity) · [Box Model](#box-model) · [Units](#units) · [Colors](#colors) · [Backgrounds](#backgrounds) · [Borders & Shadows](#borders) · [Typography](#typography) · [Display & Position](#display) · [Flexbox](#flexbox) · [Grid](#grid) · [Responsive](#responsive) · [Variables](#variables) · [Animation](#animation) · [Functions](#functions) · [Misc Properties](#misc) · [Snippets](#snippets) · [Accessibility](#a11y) · [Mistakes](#mistakes) · [Debugging](#debugging)

---

<a id="syntax"></a>

## 🧱 Syntax & Adding CSS

```css
selector {
  property: value; /* declaration */
}
```

| Method | Code | Use |
|---|---|---|
| External (best) | `<link rel="stylesheet" href="style.css">` | Almost always |
| Internal | `<style> ... </style>` in `<head>` | Small demos |
| Inline | `<p style="color: red;">` | Avoid when possible |

| Syntax | Example | Purpose |
|---|---|---|
| Comment | `/* note */` | Explain code |
| Import | `@import url("file.css");` | Load another file (slower than `<link>`) |
| Grouping | `h1, h2, h3 { margin: 0; }` | Same rules for several selectors |
| Shorthand | `margin: 10px 20px;` | Several properties in one |
| Important | `color: red !important;` | Force priority (use rarely) |

---

<a id="selectors"></a>

## 🎯 Selectors

### Basic

| Selector | Example | Selects |
|---|---|---|
| Type | `p` | All `<p>` elements |
| Class | `.card` | Elements with `class="card"` |
| ID | `#header` | Element with `id="header"` |
| Universal | `*` | Every element |
| Multiple classes | `.btn.primary` | Elements with both classes |
| Attribute | `[type="email"]` | Elements with that attribute value |
| Attribute starts with | `[href^="https"]` | Value starts with text |
| Attribute ends with | `[href$=".pdf"]` | Value ends with text |
| Attribute contains | `[class*="col-"]` | Value contains text |

### Combinators

| Combinator | Example | Meaning |
|---|---|---|
| Descendant | `nav a` | Any `<a>` inside `<nav>` |
| Child | `ul > li` | Direct child only |
| Adjacent sibling | `h2 + p` | The next sibling right after |
| General sibling | `h2 ~ p` | All following siblings |

### Pseudo-classes

| Pseudo-class | Matches |
|---|---|
| `:hover` | Pointer is over the element |
| `:focus` | Element has focus |
| `:focus-visible` | Focus that should show a ring (keyboard) |
| `:focus-within` | Element or a child has focus |
| `:active` | Element is being pressed |
| `:visited` / `:link` | Visited / unvisited links |
| `:first-child` / `:last-child` | First / last child |
| `:only-child` | Only child of its parent |
| `:nth-child(2n)` | Even children |
| `:nth-child(2n+1)` | Odd children |
| `:nth-of-type(2)` | Second of its tag type |
| `:not(.hidden)` | Does not match the selector |
| `:is(h1, h2, h3)` | Any selector in the list |
| `:where(h1, h2)` | Same as `:is()` with zero specificity |
| `:has(img)` | Parent that contains a matching child |
| `:empty` | Element with no children |
| `:root` | The document root (`<html>`) |
| `:checked` | Checked checkbox or radio |
| `:disabled` / `:enabled` | Form control states |
| `:required` / `:optional` | Required or optional field |
| `:valid` / `:invalid` | Validation state |
| `:placeholder-shown` | Input still showing its placeholder |

### Pseudo-elements

| Pseudo-element | Styles |
|---|---|
| `::before` / `::after` | Generated content (needs `content: ""`) |
| `::first-line` | First line of text |
| `::first-letter` | First letter (drop caps) |
| `::placeholder` | Placeholder text |
| `::selection` | Highlighted text |
| `::marker` | List bullet or number |
| `::backdrop` | Behind a `<dialog>` |

---

<a id="specificity"></a>

## ⚖️ Specificity & Cascade

| Selector type | Weight |
|---|---|
| Inline style | 1000 |
| ID | 100 |
| Class, attribute, pseudo-class | 10 |
| Type, pseudo-element | 1 |
| `*`, combinators, `:where()` | 0 |

**Winner order:** `!important` → higher specificity → later in the file.

```css
p            { color: black; }  /* 1   */
.note        { color: blue; }   /* 10  */
p.note       { color: green; }  /* 11  */
#intro       { color: red; }    /* 100 */
```

| Keyword | Effect |
|---|---|
| `inherit` | Take the parent's value |
| `initial` | Use the property's default value |
| `unset` | `inherit` if inheritable, otherwise `initial` |
| `revert` | Go back to the browser default style |

---

<a id="box-model"></a>

## 📦 Box Model

```
margin → border → padding → content
```

| Property | Example | Notes |
|---|---|---|
| `width` / `height` | `width: 300px;` | Content size (or total with `border-box`) |
| `min-width` / `max-width` | `max-width: 1100px;` | Limits |
| `padding` | `padding: 10px 20px;` | Space inside the border |
| `margin` | `margin: 0 auto;` | Space outside, `auto` centers a block |
| `border` | `border: 1px solid #ccc;` | Width, style, color |
| `box-sizing` | `box-sizing: border-box;` | Include padding and border in the width |
| `overflow` | `overflow: auto;` | `visible`, `hidden`, `scroll`, `auto` |
| `outline` | `outline: 2px solid blue;` | Does not take space |

**Shorthand order**

| Values | Meaning |
|---|---|
| `margin: 10px;` | All four sides |
| `margin: 10px 20px;` | Top and bottom, then left and right |
| `margin: 10px 20px 30px;` | Top, left and right, bottom |
| `margin: 10px 20px 30px 40px;` | Top, right, bottom, left (clockwise) |

```css
/* Recommended reset */
*, *::before, *::after { box-sizing: border-box; }
```

---

<a id="units"></a>

## 📏 Units

| Unit | Type | Notes |
|---|---|---|
| `px` | Absolute | Fixed pixels |
| `rem` | Relative | Based on root font size (best for text and spacing) |
| `em` | Relative | Based on the element's own font size |
| `%` | Relative | Percent of the parent |
| `vw` / `vh` | Viewport | 1% of viewport width / height |
| `dvh` | Viewport | Dynamic height, handles mobile browser bars |
| `vmin` / `vmax` | Viewport | Smaller / larger of `vw` and `vh` |
| `ch` | Relative | Width of the "0" character |
| `fr` | Grid | Fraction of free space |
| `deg` / `turn` | Angle | Used in transforms and gradients |
| `s` / `ms` | Time | Used in transitions and animations |

---

<a id="colors"></a>

## 🎨 Colors

| Format | Example |
|---|---|
| Named | `color: tomato;` |
| Hex | `color: #2f81f7;` |
| Hex with alpha | `color: #2f81f780;` |
| RGB | `color: rgb(47 129 247);` |
| RGB with alpha | `color: rgb(0 0 0 / 50%);` |
| HSL | `color: hsl(215 90% 57%);` |
| `currentColor` | Uses the element's `color` value |
| `transparent` | Fully transparent |

| Property | Purpose |
|---|---|
| `color` | Text color |
| `background-color` | Background color |
| `opacity` | Whole element transparency (0 to 1) |
| `accent-color` | Color of checkboxes, radios and sliders |
| `color-scheme` | Tell the browser about light or dark support |

---

<a id="backgrounds"></a>

## 🖼️ Backgrounds & Gradients

| Property | Example |
|---|---|
| `background-color` | `background-color: #f6f8fa;` |
| `background-image` | `background-image: url("bg.jpg");` |
| `background-repeat` | `no-repeat`, `repeat-x`, `repeat-y` |
| `background-position` | `center`, `top right`, `50% 50%` |
| `background-size` | `cover` (fill) or `contain` (fit) |
| `background-attachment` | `fixed` for a parallax-style effect |
| `background` (shorthand) | `background: #fff url("bg.jpg") center / cover no-repeat;` |

```css
/* Gradients */
background: linear-gradient(to right, #2f81f7, #8957e5);
background: linear-gradient(135deg, #ff7e5f, #feb47b);
background: radial-gradient(circle, #fff, #000);
background: conic-gradient(red, yellow, green, blue, red);
```

---

<a id="borders"></a>

## 🔲 Borders, Radius & Shadows

| Property | Example |
|---|---|
| `border` | `border: 2px solid #d0d7de;` |
| `border-style` | `solid`, `dashed`, `dotted`, `double`, `none` |
| `border-radius` | `border-radius: 12px;` |
| Circle | `border-radius: 50%;` on a square element |
| Pill shape | `border-radius: 999px;` |
| `box-shadow` | `box-shadow: 0 4px 12px rgb(0 0 0 / 15%);` |
| Inset shadow | `box-shadow: inset 0 2px 4px rgb(0 0 0 / 20%);` |
| `text-shadow` | `text-shadow: 1px 1px 2px rgb(0 0 0 / 40%);` |
| `outline-offset` | `outline-offset: 3px;` |

`box-shadow` order: **x-offset, y-offset, blur, spread, color**

---

<a id="typography"></a>

## 🔤 Typography

| Property | Example | Notes |
|---|---|---|
| `font-family` | `font-family: system-ui, sans-serif;` | Always add fallbacks |
| `font-size` | `font-size: 1rem;` | Use `rem` |
| `font-weight` | `font-weight: 700;` | 400 normal, 700 bold |
| `font-style` | `font-style: italic;` | |
| `line-height` | `line-height: 1.6;` | 1.5 to 1.7 for body text |
| `letter-spacing` | `letter-spacing: 0.05em;` | |
| `word-spacing` | `word-spacing: 2px;` | |
| `text-align` | `center`, `left`, `right`, `justify` | |
| `text-decoration` | `underline`, `line-through`, `none` | |
| `text-transform` | `uppercase`, `lowercase`, `capitalize` | |
| `text-indent` | `text-indent: 2em;` | |
| `white-space` | `nowrap`, `pre`, `pre-wrap` | |
| `word-break` | `break-word` | Break long words |
| `overflow-wrap` | `anywhere` | Prevent overflow |
| `text-overflow` | `ellipsis` | Needs `overflow: hidden` and `white-space: nowrap` |
| `vertical-align` | `middle` | For inline and table cells |
| `font` (shorthand) | `font: 700 1rem/1.5 system-ui, sans-serif;` | |

```css
/* Load a custom font */
@font-face {
  font-family: "MyFont";
  src: url("myfont.woff2") format("woff2");
  font-display: swap;
}
```

---

<a id="display"></a>

## 🧭 Display & Position

### Display

| Value | Behavior |
|---|---|
| `block` | New line, full width |
| `inline` | In the text flow, ignores width and height |
| `inline-block` | In the flow, accepts width and height |
| `flex` | Flexbox container |
| `inline-flex` | Inline Flexbox container |
| `grid` | Grid container |
| `none` | Removed from layout |
| `contents` | Element box disappears, children remain |

| Hiding method | Takes space | Seen by screen readers |
|---|---|---|
| `display: none` | No | No |
| `visibility: hidden` | Yes | No |
| `opacity: 0` | Yes | Yes |

### Position

| Value | Behavior |
|---|---|
| `static` | Default, normal flow |
| `relative` | Offset from normal spot, anchors children |
| `absolute` | Removed from flow, placed against nearest positioned ancestor |
| `fixed` | Fixed to the viewport |
| `sticky` | Scrolls, then sticks at an offset |

| Property | Purpose |
|---|---|
| `top`, `right`, `bottom`, `left` | Offsets for positioned elements |
| `inset: 0` | Shorthand for all four offsets |
| `z-index` | Stacking order (needs a positioned element or a flex/grid item) |
| `float` | `left` or `right`, wraps text around (legacy layouts) |
| `clear` | Stop wrapping around floats |

---

<a id="flexbox"></a>

## 📐 Flexbox

```css
.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
}
```

### Container properties

| Property | Values | Purpose |
|---|---|---|
| `flex-direction` | `row`, `row-reverse`, `column`, `column-reverse` | Main axis direction |
| `flex-wrap` | `nowrap`, `wrap`, `wrap-reverse` | Allow wrapping |
| `flex-flow` | `row wrap` | Direction and wrap together |
| `justify-content` | `flex-start`, `center`, `flex-end`, `space-between`, `space-around`, `space-evenly` | Align on the main axis |
| `align-items` | `stretch`, `flex-start`, `center`, `flex-end`, `baseline` | Align on the cross axis |
| `align-content` | same as `justify-content` | Align wrapped lines |
| `gap` | `1rem`, `1rem 2rem` | Space between items |

### Item properties

| Property | Example | Purpose |
|---|---|---|
| `flex` | `flex: 1;` | Grow to fill space |
| `flex-grow` | `flex-grow: 1;` | How much an item grows |
| `flex-shrink` | `flex-shrink: 0;` | Stop an item from shrinking |
| `flex-basis` | `flex-basis: 200px;` | Starting size |
| `align-self` | `align-self: flex-end;` | Override alignment for one item |
| `order` | `order: -1;` | Change visual order |
| `margin-left: auto` | | Push an item to the far end |

**Remember:** `justify-content` follows the main axis, `align-items` follows the cross axis. When `flex-direction` is `column`, they swap directions.

---

<a id="grid"></a>

## 🔳 Grid

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
}
```

### Container properties

| Property | Example | Purpose |
|---|---|---|
| `grid-template-columns` | `200px 1fr 1fr` | Define columns |
| `grid-template-rows` | `auto 1fr auto` | Define rows |
| `grid-template-areas` | `"header header" "side main"` | Name layout areas |
| `gap` | `1rem` | Space between tracks |
| `grid-auto-flow` | `row`, `column`, `dense` | Auto-placement direction |
| `grid-auto-rows` | `minmax(100px, auto)` | Size of implicit rows |
| `justify-items` / `align-items` | `center`, `start`, `end`, `stretch` | Align items in their cells |
| `place-items` | `center` | Shorthand for both |
| `justify-content` / `align-content` | `center`, `space-between` | Align the whole grid |

### Item properties

| Property | Example | Purpose |
|---|---|---|
| `grid-column` | `1 / 3` or `span 2` | Span columns |
| `grid-row` | `1 / 3` or `span 2` | Span rows |
| `grid-area` | `header` | Place into a named area |
| `justify-self` / `align-self` | `center` | Align one item |

### Useful patterns

```css
/* Responsive cards, no media query needed */
grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));

/* Classic page layout */
.layout {
  display: grid;
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
  grid-template-columns: 250px 1fr;
}
.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main    { grid-area: main; }
.footer  { grid-area: footer; }
```

| Function | Meaning |
|---|---|
| `repeat(3, 1fr)` | Three equal columns |
| `minmax(200px, 1fr)` | At least 200px, at most one fraction |
| `auto-fit` | Fit as many columns as possible, stretch to fill |
| `auto-fill` | Fit as many columns as possible, keep empty tracks |

| Choose | When |
|---|---|
| Flexbox | One direction: navbars, button rows, centering |
| Grid | Two directions: page layouts, galleries, dashboards |

---

<a id="responsive"></a>

## 📱 Responsive Design

**Required in HTML:** `<meta name="viewport" content="width=device-width, initial-scale=1.0">`

```css
/* Mobile-first: base styles for small screens */
.cards { display: grid; gap: 1rem; }

@media (min-width: 768px) {
  .cards { grid-template-columns: repeat(2, 1fr); }
}
```

| Breakpoint | Typical target |
|---|---|
| `480px` | Large phones |
| `768px` | Tablets |
| `1024px` | Small laptops |
| `1280px` | Desktops |

| Media query | Purpose |
|---|---|
| `(min-width: 768px)` | Screens at least this wide |
| `(max-width: 600px)` | Screens at most this wide |
| `(orientation: landscape)` | Landscape screens |
| `(prefers-color-scheme: dark)` | User prefers dark mode |
| `(prefers-reduced-motion: reduce)` | User wants less animation |
| `(hover: hover)` | Device supports real hover |
| `print` | Printing |

```css
/* Container query: respond to the parent, not the screen */
.wrapper { container-type: inline-size; }

@container (min-width: 400px) {
  .card { display: flex; }
}
```

```css
/* Fluid typography and sizes */
h1 { font-size: clamp(2rem, 5vw, 3.5rem); }
img { max-width: 100%; height: auto; }
```

---

<a id="variables"></a>

## 🧩 Variables (Custom Properties)

```css
:root {
  --primary: #0969da;
  --space: 1rem;
  --radius: 12px;
}

.button {
  background: var(--primary);
  padding: var(--space);
  border-radius: var(--radius);
  color: var(--text, white); /* fallback value */
}
```

| Syntax | Meaning |
|---|---|
| `--name: value;` | Define a variable |
| `var(--name)` | Use a variable |
| `var(--name, fallback)` | Use with a fallback |
| `:root` | Global scope |

```css
/* Dark mode with variables */
@media (prefers-color-scheme: dark) {
  :root { --bg: #0d1117; --text: #e6edf3; }
}
```

---

<a id="animation"></a>

## 🎬 Transitions, Transforms & Animations

### Transitions

```css
.btn {
  transition: background 0.3s ease, transform 0.2s ease;
}
.btn:hover { transform: translateY(-2px); }
```

| Property | Example |
|---|---|
| `transition-property` | `background, transform` |
| `transition-duration` | `0.3s` |
| `transition-timing-function` | `ease`, `linear`, `ease-in`, `ease-out`, `ease-in-out` |
| `transition-delay` | `0.1s` |

### Transforms

| Function | Effect |
|---|---|
| `translate(x, y)` / `translateX()` / `translateY()` | Move |
| `scale(1.1)` | Resize |
| `rotate(45deg)` | Rotate |
| `skew(10deg)` | Slant |
| `transform-origin` | Set the pivot point |
| Combine | `transform: translateY(-4px) scale(1.05);` |

### Keyframe animations

```css
@keyframes fade-in {
  from { opacity: 0; transform: translateY(10px); }
  to   { opacity: 1; transform: translateY(0); }
}

.card {
  animation: fade-in 0.5s ease both;
}
```

| Property | Example |
|---|---|
| `animation-name` | `fade-in` |
| `animation-duration` | `0.5s` |
| `animation-timing-function` | `ease`, `linear`, `steps(4)` |
| `animation-delay` | `0.2s` |
| `animation-iteration-count` | `3` or `infinite` |
| `animation-direction` | `normal`, `reverse`, `alternate` |
| `animation-fill-mode` | `forwards`, `both` |
| `animation-play-state` | `paused`, `running` |

**Performance tip:** animate `transform` and `opacity`. Avoid animating `width`, `height`, `top` or `left`.

---

<a id="functions"></a>

## 🧮 Functions

| Function | Example | Purpose |
|---|---|---|
| `calc()` | `width: calc(100% - 250px);` | Math with mixed units |
| `min()` | `width: min(90%, 600px);` | Smaller of the values |
| `max()` | `width: max(50%, 300px);` | Larger of the values |
| `clamp()` | `font-size: clamp(1rem, 2.5vw, 2rem);` | Value between a minimum and maximum |
| `var()` | `color: var(--primary);` | Use a variable |
| `url()` | `background: url("a.png");` | Load a file |
| `rgb()` / `hsl()` | `rgb(0 0 0 / 50%)` | Colors |
| `linear-gradient()` | `linear-gradient(to right, red, blue)` | Gradients |
| `repeat()` / `minmax()` | Grid helpers | Grid track sizing |
| `attr()` | `content: attr(data-label);` | Read an HTML attribute |
| `translate()` / `scale()` / `rotate()` | Transform helpers | Move, resize, rotate |
| `blur()` / `brightness()` | `filter: blur(4px);` | Visual filters |

---

<a id="misc"></a>

## 🧰 Other Useful Properties

| Property | Example | Purpose |
|---|---|---|
| `cursor` | `cursor: pointer;` | Mouse cursor style |
| `pointer-events` | `none` | Make an element ignore clicks |
| `user-select` | `none` | Prevent text selection |
| `object-fit` | `cover`, `contain` | How images and video fill their box |
| `object-position` | `center top` | Position inside the box |
| `aspect-ratio` | `16 / 9` | Fixed shape |
| `filter` | `grayscale(100%)` | Visual effects on an element |
| `backdrop-filter` | `blur(8px)` | Blur what is behind (glass effect) |
| `mix-blend-mode` | `multiply` | Blend with what is below |
| `clip-path` | `circle(50%)` | Cut an element into a shape |
| `scroll-behavior` | `smooth` | Smooth anchor scrolling |
| `scroll-margin-top` | `80px` | Offset anchors under a sticky header |
| `scroll-snap-type` | `x mandatory` | Snap scrolling |
| `position: sticky` | with `top: 0` | Sticky header |
| `resize` | `vertical` | Allow resizing a box |
| `list-style` | `none` | Remove bullets |
| `content` | `"→"` | Text for `::before` and `::after` |
| `will-change` | `transform` | Hint for upcoming animation (use sparingly) |
| `visibility` | `hidden` | Hide but keep space |
| `isolation` | `isolate` | Create a new stacking context |

---

<a id="snippets"></a>

## 🧪 Ready-to-Copy Snippets

### Center anything

```css
/* Flexbox */
.center { display: flex; justify-content: center; align-items: center; }

/* Grid (shortest) */
.center { display: grid; place-items: center; }

/* Center a block horizontally */
.box { width: 600px; max-width: 100%; margin-inline: auto; }
```

### Full-height page

```css
.page { min-height: 100dvh; }
```

### Sticky footer

```css
body { min-height: 100dvh; display: flex; flex-direction: column; }
main { flex: 1; }
```

### Truncate text with ellipsis

```css
/* One line */
.truncate { white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }

/* Three lines */
.clamp-3 {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
```

### Responsive image

```css
img { max-width: 100%; height: auto; display: block; }
.cover { width: 100%; aspect-ratio: 16 / 9; object-fit: cover; }
```

### Responsive card grid

```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 1.5rem;
}
```

### Sticky header

```css
.header { position: sticky; top: 0; z-index: 100; background: var(--bg); }
```

### Smooth scrolling

```css
html { scroll-behavior: smooth; }
```

### Hover lift effect

```css
.card { transition: transform 0.2s ease, box-shadow 0.2s ease; }
.card:hover { transform: translateY(-4px); box-shadow: 0 8px 20px rgb(0 0 0 / 15%); }
```

### Accessible focus ring

```css
:focus-visible { outline: 3px solid #2f81f7; outline-offset: 3px; }
```

### Visually hidden (still readable by screen readers)

```css
.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  overflow: hidden;
  clip-path: inset(50%);
  white-space: nowrap;
}
```

### Glass effect

```css
.glass {
  background: rgb(255 255 255 / 15%);
  backdrop-filter: blur(10px);
  border: 1px solid rgb(255 255 255 / 25%);
  border-radius: 16px;
}
```

### Loading spinner

```css
.spinner {
  width: 40px;
  height: 40px;
  border: 4px solid #d0d7de;
  border-top-color: #2f81f7;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}
@keyframes spin { to { transform: rotate(360deg); } }
```

### Respect reduced motion

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after { animation: none !important; transition: none !important; }
}
```

---

<a id="a11y"></a>

## ♿ Accessibility Quick Reference

| Do | Avoid |
|---|---|
| Keep contrast at least 4.5:1 for body text | Light gray text on a white background |
| Use `:focus-visible` for a clear focus ring | `outline: none` with no replacement |
| Use `rem` for font sizes | Fixed `px` text that ignores user settings |
| Respect `prefers-reduced-motion` | Large, constant motion for everyone |
| Make tap targets about 44px | Tiny buttons on mobile |
| Add more than color to show state | Using only red or green to show meaning |

---

<a id="mistakes"></a>

## ⚠️ Common Mistakes

| Mistake | Fix |
|---|---|
| Width plus padding makes the box too big | Use `box-sizing: border-box` |
| `margin: auto` does not center | The element needs a width, and must be a block or flex/grid item |
| `z-index` has no effect | The element needs `position` (other than `static`) |
| Text will not center vertically | Use Flexbox: `display: flex; align-items: center;` |
| Style does not apply | Check specificity, spelling, and that the file is linked |
| `height: 100%` does nothing | Parent needs a defined height, or use `min-height: 100dvh` |
| `100vh` is cut off on mobile | Use `100dvh` |
| Horizontal scrollbar appears | Find the wide element, avoid fixed widths and `100vw` with padding |
| Margins between elements collapse | Use `gap`, `padding`, or Flexbox/Grid |
| Using `!important` everywhere | Lower specificity instead |
| Images stretch | Use `object-fit: cover` or `height: auto` |

---

<a id="debugging"></a>

## 🐞 Debugging Tips

- Press `F12` and use **Inspect** to see which rules apply to an element
- Crossed-out styles in DevTools are overridden by a more specific rule
- Use the DevTools **device toolbar** to test mobile sizes
- Add a temporary `outline: 1px solid red;` to see an element's box
- Check the **Computed** tab for the final value of every property
- Use the **Flexbox** and **Grid** overlays in DevTools to see the layout
- Validate your CSS at the [W3C CSS Validator](https://jigsaw.w3.org/css-validator/)
- Check feature support on [Can I use](https://caniuse.com/)

---

## 💡 Quick Reminders

- Start with `box-sizing: border-box`
- Design mobile-first and use `min-width` media queries
- Use Flexbox for one direction and Grid for two
- Prefer classes over IDs, and avoid `!important`
- Use variables for colors and spacing
- Animate `transform` and `opacity` only
- Always keep a visible focus style