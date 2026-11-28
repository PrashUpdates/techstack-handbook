# 📝 CSS3 Notes

<p align="center">
  <a href="https://github.com/PrashUpdates/techstack-handbook/blob/main/README.md#frontend"><img src="https://img.shields.io/badge/Back%20to%20main-6E7681?style=for-the-badge" alt="Back to main" /></a>
  <a href="./docs.md"><img src="https://img.shields.io/badge/Docs-2F81F7?style=for-the-badge" alt="Docs" /></a>
  <a href="./cheat-sheet.md"><img src="https://img.shields.io/badge/Cheat%20Sheet-F38020?style=for-the-badge" alt="Cheat Sheet" /></a>
</p>

> Study notes, mental models, common mistakes, practice exercises and mini projects to use alongside the CSS3 docs.

**Jump to:**
[Key Takeaways](#takeaways) · [Mental Models](#models) · [Common Mistakes](#mistakes) · [Quick Tips](#tips) · [Roadmap](#roadmap) · [Exercises](#exercises) · [Mini Projects](#projects) · [Self-Check](#selfcheck) · [Glossary](#glossary) · [FAQ](#faq)

---

<a id="takeaways"></a>

## 🧠 Key Takeaways

- CSS controls **presentation**: color, spacing, layout, motion and responsiveness
- Every element is a **box**, and layout is mostly about sizing and arranging boxes
- Start every project with `box-sizing: border-box`
- The **cascade** decides conflicts: importance, then specificity, then source order
- Use **Flexbox** for one direction and **Grid** for two directions
- Design **mobile-first** and add `min-width` media queries for larger screens
- Use **CSS variables** for colors, spacing and fonts so a theme can change in one place
- Prefer **classes** over IDs, and avoid `!important`
- Use `rem` for text and spacing so users can scale text in their browser
- Animate `transform` and `opacity` for smooth performance
- Always keep a visible **focus style** for keyboard users
- Use **DevTools** (`F12`) to inspect, test and debug any style live

---

<a id="models"></a>

## 🧭 Mental Models

### 1. Everything is a box

Every element, even a circle or a line of text, sits inside a rectangular box: content, padding, border and margin. When a layout looks wrong, inspect the boxes first.

### 2. Block flows down, inline flows across

| Type | Behavior | Examples |
|---|---|---|
| Block | Starts on a new line and fills the width | `div`, `p`, `h1`, `section` |
| Inline | Sits inside a line of text | `span`, `a`, `strong` |
| Inline-block | Sits in a line but accepts width and height | buttons, badges |

### 3. Flexbox has two axes

```
flex-direction: row      → main axis: left to right, cross axis: top to bottom
flex-direction: column   → main axis: top to bottom, cross axis: left to right
```

| Property | Works on |
|---|---|
| `justify-content` | The main axis |
| `align-items` | The cross axis |

### 4. Grid is rows and columns together

Define the tracks on the **parent** (`grid-template-columns`), and the children fall into the cells automatically.

### 5. Specificity is a scoreboard

| Selector | Score |
|---|---|
| Inline style | 1000 |
| ID | 100 |
| Class, attribute, pseudo-class | 10 |
| Element, pseudo-element | 1 |

A selector with a higher score wins. If scores tie, the rule written last wins.

### 6. Pick the layout tool with a question

```
Do I need to line things up in one direction?   → Flexbox
Do I need rows AND columns?                     → Grid
Do I just need to center a block horizontally?  → margin-inline: auto
Do I need to place something over another?      → position
```

### 7. Mobile-first thinking

Write the small-screen layout as the default. Then add `@media (min-width: ...)` blocks that enhance the design for larger screens. This usually means less code and fewer overrides.

---

<a id="mistakes"></a>

## ⚠️ Common Mistakes

| Mistake | Fix |
|---|---|
| Width plus padding makes the box too wide | Use `box-sizing: border-box` |
| `margin: auto` does not center the element | Give it a width, and use it on a block, flex or grid item |
| `z-index` has no effect | The element needs `position` other than `static` (or be a flex or grid item) |
| Styles do not apply at all | Check the file link, spelling, a missing `;` or `}` and specificity |
| `height: 100%` does nothing | The parent needs a defined height, or use `min-height: 100dvh` |
| `100vh` is cut off on phones | Use `100dvh` |
| A horizontal scrollbar appears | Find the wide element, and avoid fixed widths and `100vw` plus padding |
| Vertical margins between blocks merge | Use `gap`, padding, or a Flexbox or Grid layout |
| Using `!important` to win fights | Reduce specificity or reorder the rules instead |
| Selecting by ID everywhere | Use classes, which are easier to reuse and override |
| Removing the focus outline | Replace it with a clear `:focus-visible` style |
| Using `px` for all font sizes | Use `rem` so text respects user settings |
| Stretched images | Use `max-width: 100%` with `height: auto`, or `object-fit: cover` |
| Animating `width`, `height` or `top` | Animate `transform` and `opacity` instead |
| Using `float` for page layouts | Use Flexbox or Grid |
| Hiding content with `opacity: 0` and expecting no clicks | Use `display: none` or `visibility: hidden` |
| Forgetting the viewport meta tag | Add it to the HTML `<head>` so responsive CSS works on phones |
| Overusing absolute positioning | Use it only for overlays, badges and decoration |

---

<a id="tips"></a>

## 💡 Quick Tips

- Use `display: grid; place-items: center;` for the shortest way to center something
- Use `gap` instead of margins between flex and grid children
- Use `margin-inline: auto` to center a block with a `max-width`
- Use `inset: 0` as a shorthand for `top`, `right`, `bottom` and `left`
- Use `aspect-ratio: 16 / 9` instead of padding hacks
- Use `clamp()` for fluid typography: `font-size: clamp(1rem, 2.5vw, 2rem);`
- Use `:is()` and `:where()` to shorten long selector lists
- Use `scroll-behavior: smooth` for animated anchor links
- Use `scroll-margin-top` so anchored headings do not hide under a sticky header
- Add a temporary `outline: 1px solid red;` to see an element's box
- Keep one design-token block (`:root`) at the top of the file
- Write properties in a consistent order, for example: layout, box, typography, color, effects
- Use `Ctrl + /` in VS Code to comment or uncomment lines
- Use the **Computed** tab in DevTools to see the final value of any property

---

<a id="roadmap"></a>

## 🗺️ Learning Roadmap

Work through the stages in order. Each stage builds on the previous one.

**Stage 1: Foundations**
- [ ] Add CSS to HTML (external, internal, inline)
- [ ] Selectors: type, class, ID, attribute, grouping
- [ ] Colors, units (`px`, `rem`, `%`) and fonts
- [ ] The box model and `box-sizing`

**Stage 2: Core Styling**
- [ ] Backgrounds, gradients, borders and shadows
- [ ] Typography: line height, spacing, alignment, web fonts
- [ ] Pseudo-classes and pseudo-elements
- [ ] Specificity, inheritance and the cascade

**Stage 3: Layout**
- [ ] `display` and `position`
- [ ] Flexbox
- [ ] CSS Grid
- [ ] Responsive design with media queries

**Stage 4: Polish**
- [ ] CSS variables
- [ ] Transitions and transforms
- [ ] Keyframe animations
- [ ] Dark mode with `prefers-color-scheme`

**Stage 5: Modern and Professional**
- [ ] `clamp()`, `min()`, `max()` and `calc()`
- [ ] Container queries and `:has()`
- [ ] Accessibility: contrast, focus styles, reduced motion
- [ ] Code organization: naming (BEM), structure and performance

---

<a id="exercises"></a>

## 🧪 Practice Exercises

**🟢 Beginner**
- [ ] Style a page with custom fonts, colors and spacing
- [ ] Make a button with a hover and a focus style
- [ ] Build a profile card using the box model (padding, border, radius, shadow)
- [ ] Style a list as a horizontal navigation bar
- [ ] Create a gradient background and a text shadow

**🟡 Intermediate**
- [ ] Build a responsive navbar with Flexbox
- [ ] Create a three-column card layout with Grid that becomes one column on phones
- [ ] Build a pricing table with a highlighted plan
- [ ] Make an image gallery with `object-fit` and hover zoom
- [ ] Add a dark theme using CSS variables and `prefers-color-scheme`

**🔴 Challenge**
- [ ] Recreate the layout of a website you admire using only Flexbox and Grid
- [ ] Build a CSS-only accordion using `<details>` and `<summary>`
- [ ] Create a loading spinner and a skeleton loader with `@keyframes`
- [ ] Build a responsive dashboard layout with `grid-template-areas`
- [ ] Design a component that adapts using a container query

---

<a id="projects"></a>

## 🛠️ Mini Projects

| Project | Skills practiced | Level |
|---|---|---|
| Profile card | Box model, typography, shadows | 🟢 Beginner |
| Responsive navbar | Flexbox, media queries, hover states | 🟢 Beginner |
| Pricing cards | Grid, pseudo-elements, transitions | 🟡 Intermediate |
| Photo gallery | Grid, `object-fit`, `aspect-ratio` | 🟡 Intermediate |
| Landing page | Full layout, variables, responsive design | 🟡 Intermediate |
| Dark mode theme | Variables, `prefers-color-scheme` | 🟡 Intermediate |
| Animated loader pack | `@keyframes`, transforms | 🔴 Challenge |
| Dashboard layout | `grid-template-areas`, sticky sidebar | 🔴 Challenge |

**How to approach each project**

1. Sketch the layout on paper
2. Write the HTML structure first, with semantic tags
3. Add the reset and variables
4. Style mobile first
5. Add larger-screen styles with `min-width` media queries
6. Add hover, focus and motion last
7. Test with DevTools device mode and with the keyboard only

---

<a id="selfcheck"></a>

## ✅ Self-Check

You are comfortable with CSS3 basics if you can:

- [ ] Explain the box model and draw it from memory
- [ ] Explain why `box-sizing: border-box` is useful
- [ ] Predict which of two rules wins using specificity
- [ ] Center an element horizontally and vertically in three different ways
- [ ] Choose between Flexbox and Grid and explain why
- [ ] Build a responsive card grid without writing a media query
- [ ] Use CSS variables to switch between a light and a dark theme
- [ ] Write a transition and a keyframe animation
- [ ] Explain the difference between `relative`, `absolute`, `fixed` and `sticky`
- [ ] Use DevTools to find out why a style is not applying
- [ ] Make a page usable with keyboard only, with visible focus styles

---

<a id="glossary"></a>

## 📖 Glossary

| Term | Meaning |
|---|---|
| **Selector** | The part of a rule that chooses which elements to style |
| **Declaration** | A property and value pair, such as `color: red;` |
| **Cascade** | The process that decides which rule wins when several apply |
| **Specificity** | A score that ranks how strongly a selector targets an element |
| **Inheritance** | Passing certain property values from parent to child |
| **Box model** | Content, padding, border and margin around every element |
| **Viewport** | The visible area of the page in the browser |
| **Flex container** | An element with `display: flex` |
| **Grid track** | A single row or column in a grid |
| **`fr` unit** | A fraction of the free space in a grid |
| **Breakpoint** | The screen width where the layout changes |
| **Custom property** | A CSS variable, defined with `--name` |
| **Pseudo-class** | A selector for an element state, such as `:hover` |
| **Pseudo-element** | A selector for part of an element, such as `::before` |
| **Stacking context** | A group of layers that `z-index` is compared within |
| **Reflow** | The browser recalculating layout after a change |
| **Vendor prefix** | A browser-specific prefix such as `-webkit-` |
| **Reset** | A small stylesheet that removes inconsistent browser defaults |

---

<a id="faq"></a>

## ❓ Frequently Asked Questions

**Is CSS a programming language?**
No. CSS is a style sheet language that describes how HTML looks. It has some logic tools, such as variables, `calc()` and media queries, but it does not have loops or functions like JavaScript.

**What is the difference between CSS and CSS3?**
CSS3 is the common name for modern CSS. CSS is now split into independent modules (Flexbox, Grid, Selectors, Animations and more) that evolve separately, so there is no official "CSS4".

**Flexbox or Grid: which one should I learn first?**
Learn Flexbox first, because it is simpler and solves everyday alignment tasks. Then learn Grid for full page layouts. In real projects you will use both together.

**What is the difference between `px`, `em` and `rem`?**
`px` is a fixed size. `em` is relative to the element's own font size. `rem` is relative to the root font size, which makes it the most predictable choice for text and spacing.

**What is the difference between `margin` and `padding`?**
Padding is space inside the element, between the content and the border. Margin is space outside the border, between the element and its neighbors.

**What is the difference between `id` and `class` in CSS?**
An ID is unique on a page and has high specificity. A class can be reused on many elements and is easier to override, so classes are preferred for styling.

**What is the difference between `relative` and `absolute` positioning?**
`relative` keeps the element in the normal flow and offsets it from its own position. `absolute` removes it from the flow and places it relative to the nearest positioned ancestor.

**Why is my CSS not working?**
Check these in order: the stylesheet is linked correctly, the selector matches the element, there are no typos or missing `;` and `}`, another rule is not overriding it (check specificity in DevTools), and the browser is not showing a cached file (hard refresh with `Ctrl + Shift + R`).

**What does `!important` do, and should I use it?**
It forces a declaration to win over normal rules. Avoid it in regular code, because it makes styles hard to override and debug. Use it only for rare utility classes or to override third-party CSS.

**What is the difference between a transition and an animation?**
A transition smoothly changes between two states when something triggers it, such as `:hover`. An animation uses `@keyframes` to run multi-step motion that can start on its own and repeat.

**What does mobile-first mean?**
You write the base styles for small screens and use `min-width` media queries to add enhancements for bigger screens. It keeps the code simpler and the mobile experience fast.

**Do I need Sass or Tailwind to write good CSS?**
No. Modern CSS has variables, nesting, `clamp()` and `:has()`, which cover most needs. Sass and Tailwind are optional tools that can speed up larger projects.

**What is BEM?**
BEM (Block, Element, Modifier) is a naming convention such as `.card`, `.card__title` and `.card--featured`. It keeps class names clear and avoids conflicts in larger projects.

**Why does `margin-top` on a child push the parent down?**
This is margin collapsing: vertical margins of a parent and its first child can merge. Add padding or a border to the parent, use `display: flow-root`, or use Flexbox or Grid with `gap`.

**How do I make a site work in dark mode?**
Define colors as CSS variables on `:root`, then redefine them inside `@media (prefers-color-scheme: dark)`. The site follows the user's system setting automatically.