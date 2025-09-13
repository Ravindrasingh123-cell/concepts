# Core CSS Concepts

**Concepts:**

**Box Model**
- Inline versus Block Elements. Examples.
- Positioning: Relative/Absolute
- Common CSS structural classes
- Common CSS syling classes
- CSS Specificity
- CSS Responsive Queries
- Flexbox/Grid
- Common header meta tags

---

## 1. The CSS Box Model

Every HTML element is essentially a rectangular box. The **Box Model** describes how these boxes are structured and how they affect layout.

- **Content**: The actual text or image.
- **Padding**: Space between the content and the border.
- **Border**: The edge of the element.
- **Margin**: Space outside the border, between the element and others.

```css
.box {
  padding: 10px;
  border: 2px solid black;
  margin: 20px;
}
```
Think of it as layers: Margin → Border → Padding → Content.

## 2. Inline vs Block Elements
HTML elements are either inline or block by default.

Block elements take up the full width and start on a new line.

Examples: ``` <div>, <p>, <h1>, <section> ```

Inline elements flow with text and only take up as much space as needed.

Examples: ```<span>, <a>, <strong>, <img>```

```html

<p>This is <span style="color: red;">inline</span> text inside a block element.</p>
```
You can change display behavior with CSS:

```css

span {
  display: block;
}
```
## 3. CSS Positioning: Relative vs Absolute
CSS positioning allows you to control where elements appear on the page.

- Relative: Moves an element relative to its normal position.

- Absolute: Positions an element relative to the nearest positioned ancestor.

```css

.relative-box {
  position: relative;
  top: 20px;
  left: 10px;
}

.absolute-box {
  position: absolute;
  top: 0;
  right: 0;
}
```
Tip: Use position: relative on a container when using absolute inside it.

## 4. Common CSS Structural Classes
These classes help structure content on the page.

```css

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.row {
  display: flex;
  flex-wrap: wrap;
}

.col {
  flex: 1;
  padding: 10px;
}
```
These mimic common grid systems like Bootstrap and are reusable in layout design.

## 5. Common CSS Styling Classes
Reusable styling classes help maintain consistency.

```css

.text-center {
  text-align: center;
}

.mt-1 {
  margin-top: 1rem;
}

.bg-light {
  background-color: #f9f9f9;
}
```
Use utility classes to simplify styling across pages.

## 6. CSS Specificity
- Specificity determines which CSS rule wins when multiple rules apply.

- Inline styles: style="..." – 1000

- ID selectors: #id – 100

- Class/attribute/pseudo-class: .class, [type], :hover – 10

- Element/pseudo-elements: div, h1, ::before – 1

Tip: Avoid using !important unless absolutely necessary.

## 7. CSS Responsive Media Queries
Media queries make your layout responsive to different screen sizes.

```css

@media (max-width: 768px) {
  .container {
    padding: 10px;
  }
}
```
**Breakpoints:**

- 1200px+: Large screens

- 992px – 1199px: Desktops

- 768px – 991px: Tablets

- Below 768px: Mobile devices

## 8. Flexbox and CSS Grid
**Flexbox**
Best for one-dimensional layouts (row OR column).

```css

.flex-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
```
**Grid**
Best for two-dimensional layouts (rows AND columns).

```css

.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}
```
Use Grid when you want more precise control over both axes.

## 9. Common Header Meta Tags
These go inside <head> and improve performance, accessibility, and responsiveness.

```html

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="description" content="Learn CSS fundamentals with real examples.">
<meta name="author" content="Your Name">
```
- viewport: Crucial for mobile responsiveness.

- charset: Ensures proper text encoding.

- description: Useful for SEO.

## 10.  Other Useful Topics
*a. CSS Variables*
```css

:root {
  --primary-color: #3498db;
}

.button {
  background-color: var(--primary-color);
}
```
*b. Pseudo-classes*
```css

a:hover {
  text-decoration: underline;
}
```
*c. Pseudo-elements*
```css

p::first-letter {
  font-size: 200%;
}
```
## References

MDN Web Docs — CSS: https://developer.mozilla.org/en-US/docs/Web/CSS

W3Schools — CSS Tutorial: https://www.w3schools.com/css/

CSS‑Tricks — A Complete Guide to Flexbox: https://css-tricks.com/snippets/css/a-guide-to-flexbox/

CSS‑Tricks — A Complete Guide to CSS Grid Layout: https://css-tricks.com/snippets/css/complete-guide-grid/
 
