# CSS Syntax Guide

## CSS Custom Properties (Variables)

### **`--` (Double Dash)**

Defines **CSS custom properties (variables)**

```css
--vt-c-white: #ffffff; /* Create variable */
color: var(--vt-c-white); /* Use variable */
```

**Benefits:**

- Reusable values throughout your stylesheet
- Easy theme changes in one place
- Dynamic updates possible with JavaScript

---

## Naming Conventions

### **`vt` Prefix**

Just a **naming prefix** (stands for "**V**ue **T**heme")

```css
--vt-c-white: #ffffff; /* Vue Theme Color White */
--vt-c-black: #181818; /* Vue Theme Color Black */
```

**Purpose:**

- Helps avoid naming conflicts with other libraries
- Organizes related variables
- Not a CSS keyword, just a convention

---

## Selectors

### **`:root`**

**Highest-level selector** in CSS (represents `<html>` element)

```css
:root {
  --my-color: blue; /* Available globally everywhere */
}
```

**Characteristics:**

- Variables defined here are **global** to entire website
- Has higher specificity than `html` selector
- Best practice for defining CSS custom properties

### **`*` (Universal Selector)**

Targets **ALL elements** in the document

```css
* {
  margin: 0; /* Remove margin from everything */
  box-sizing: border-box;
}
```

**Common uses:**

- CSS resets
- Applying base styles to all elements

---

## Pseudo-elements

### **`::before` and `::after`**

Creates **virtual elements** before/after element's content

```css
*::before {
  /* Virtual element BEFORE every element's content */
}

*::after {
  /* Virtual element AFTER every element's content */
}
```

**Example:**

```css
.icon::before {
  content: '★';
  color: gold;
}
```

**Uses:**

- Decorative content
- Icons without extra HTML
- Visual effects

---

## Common CSS Patterns in base.css

### **Universal Reset**

```css
*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
  font-weight: normal;
}
```

**What it does:**

- `*` = Targets ALL elements (div, p, button, etc.)
- `*::before` = Targets all virtual elements before content
- `*::after` = Targets all virtual elements after content

**Properties explained:**

- `box-sizing: border-box` - Width includes padding & border (easier sizing math)
- `margin: 0` - Removes default browser margins from everything
- `font-weight: normal` - Resets all text to normal weight

**Visual Example:**

```
WITHOUT box-sizing: border-box:
┌─────────────────────────────┐
│ Width: 200px                │
│ ┌─────────────────────────┐ │  ← Padding adds 20px on each side
│ │                         │ │  ← Total width = 240px (unexpected!)
│ │      Content 200px      │ │
│ │                         │ │
│ └─────────────────────────┘ │
└─────────────────────────────┘

WITH box-sizing: border-box:
┌─────────────────────────────┐  ← Total width stays 200px
│ Width: 200px                │
│ ┌─────────────────────────┐ │  ← Padding included in width
│ │   Content: 160px        │ │  ← Content shrinks to fit
│ └─────────────────────────┘ │
└─────────────────────────────┘
```

**Why use `*` selector?**

```css
/* ❌ Without reset - Different browsers have different defaults */
<p>Hello</p>     /* Chrome: 16px margin-top, Firefox: 14px margin-top */
<h1>Title</h1>   /* Safari: 21px margin, Edge: 20px margin */

/* ✅ With reset - Consistent across all browsers */
* {
  margin: 0;
} /* All elements start with 0 margin */
```

**Real-world impact:**

```html
<div class="card">
  <h2>Title</h2>
  <p>Content</p>
</div>
```

```css
/* Without reset */
.card {
  padding: 20px;
  width: 300px; /* Actual width: 340px (300 + 20 + 20) */
}

/* With box-sizing: border-box */
.card {
  padding: 20px;
  width: 300px; /* Actual width: 300px (padding included!) */
}
```

### **Body Styles**

```css
body {
  min-height: 100vh;
  color: var(--color-text);
  background: var(--color-background);
  transition:
    color 0.5s,
    background-color 0.5s;
  line-height: 1.6;
  font-family:
    Inter,
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    Oxygen,
    Ubuntu,
    Cantarell,
    'Fira Sans',
    'Droid Sans',
    'Helvetica Neue',
    sans-serif;
  font-size: 15px;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

**Property breakdown:**

| Property                  | Value                               | What it does                                         |
| ------------------------- | ----------------------------------- | ---------------------------------------------------- |
| `min-height`              | `100vh`                             | Minimum height = 100% of viewport (full screen)      |
| `color`                   | `var(--color-text)`                 | Text color from CSS variable                         |
| `background`              | `var(--color-background)`           | Background color from CSS variable                   |
| `transition`              | `color 0.5s, background-color 0.5s` | Smooth color changes over 0.5 seconds                |
| `line-height`             | `1.6`                               | Space between lines (1.6× font size for readability) |
| `font-family`             | Font stack                          | List of fonts (tries in order)                       |
| `font-size`               | `15px`                              | Base text size for entire site                       |
| `text-rendering`          | `optimizeLegibility`                | Better text rendering quality                        |
| `-webkit-font-smoothing`  | `antialiased`                       | Smoother fonts on Mac/iOS                            |
| `-moz-osx-font-smoothing` | `grayscale`                         | Smoother fonts on Firefox Mac                        |

**Font Family Stack Explained:**

```css
font-family:
  Inter,
  /* 1st choice: Inter font (if loaded) */ -apple-system,
  /* 2nd: macOS system font (San Francisco) */ BlinkMacSystemFont,
  /* 3rd: macOS Chrome font */ 'Segoe UI',
  /* 4th: Windows system font */ Roboto,
  /* 5th: Android system font */ Oxygen,
  /* 6th: Linux KDE font */ Ubuntu,
  /* 7th: Linux Ubuntu font */ Cantarell,
  /* 8th: Linux GNOME font */ 'Fira Sans',
  /* 9th: Mozilla font */ 'Droid Sans',
  /* 10th: Older Android font */ 'Helvetica Neue',
  /* 11th: Apple fallback */ sans-serif; /* Final fallback: browser default */
```

**How to change font:**

1. Replace the entire `font-family` line with your choice:

```css
/* Option 1: Simple modern font */
font-family: 'Roboto', sans-serif;

/* Option 2: System fonts only (no web font needed) */
font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;

/* Option 3: Custom Google Font (add link in index.html first) */
font-family: 'Poppins', sans-serif;
```

2. If using Google Fonts, add to `index.html`:

```html
<link href="https://fonts.googleapis.com/css2?family=Poppins&display=swap" rel="stylesheet" />
```

---

## Media Queries

### **`@media (prefers-color-scheme: dark)`**

**Media query** that detects user's OS theme preference

```css
@media (prefers-color-scheme: dark) {
  :root {
    --color-background: var(--vt-c-black);
    /* CSS only applies when OS is in dark mode */
  }
}
```

**Values:**

- `light` - User prefers light theme
- `dark` - User prefers dark theme
- `no-preference` - No preference detected

---

## CSS Functions

### **`var(--variable-name)`**

Function to **use CSS variables**

```css
/* Define variable */
:root {
  --color-background: #ffffff;
}

/* Use variable */
body {
  background: var(--color-background);
}

/* With fallback value */
color: var(--color-text, black); /* Use black if --color-text not defined */
```

**Syntax:**

```css
var(--variable-name, fallback-value)
```

---

## Quick Reference

| Syntax        | Purpose                        | Example                           |
| ------------- | ------------------------------ | --------------------------------- |
| `--name`      | Create CSS variable            | `--color: blue;`                  |
| `var(--name)` | Use CSS variable               | `color: var(--color);`            |
| `:root`       | Global scope selector          | `:root { --x: 10px; }`            |
| `*`           | Select all elements            | `* { margin: 0; }`                |
| `::before`    | Virtual element before content | `.icon::before { content: "→"; }` |
| `::after`     | Virtual element after content  | `.label::after { content: "*"; }` |
| `@media`      | Conditional CSS rules          | `@media (max-width: 768px) { }`   |

---

## Example from base.css

```css
/* 1. Define variables globally */
:root {
  --vt-c-white: #ffffff;
  --color-background: var(--vt-c-white);
}

/* 2. Override for dark mode */
@media (prefers-color-scheme: dark) {
  :root {
    --color-background: var(--vt-c-black);
  }
}

/* 3. Reset all elements */
* {
  box-sizing: border-box;
  margin: 0;
}

/* 4. Use variables */
body {
  background: var(--color-background);
}
```

This creates a **theme system** where:

- Variables are defined once in `:root`
- Dark mode automatically swaps colors
- Variables are used throughout with `var()`
- All elements get consistent base styles with `*`
