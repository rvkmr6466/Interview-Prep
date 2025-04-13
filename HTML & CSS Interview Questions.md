## HTML & CSS Interview Questions

### 1. UX Design Principles  
- Simplicity  
- Consistency  
- Accessibility
- responsive

---
### 2. HTML5 & CSS  

- **HTML5** → Semantic tags (`<article>`, `<section>`)  
- **CSS** → Flexbox, Grid, Animations  

---
### 3. Block vs Inline vs Inline-Block in CSS
| Property      | Block | Inline | Inline-Block |
|--------------|-------|--------|--------------|
| **Starts on a new line?** | ✅ Yes | ❌ No | ❌ No |
| **Takes full width?** | ✅ Yes (by default) | ❌ No (only as wide as content) | ❌ No (only as wide as content) |
| **Supports width & height?** | ✅ Yes | ❌ No | ✅ Yes |
| **Supports margin & padding?** | ✅ Yes (all sides) | 🚫 No (only horizontal) | ✅ Yes (all sides) |
### **Examples for Better Understanding**  
#### **1️⃣ Block Elements (`display: block`)**  
✅ Takes the full width, starts on a new line  
📌 Examples: `<div>`, `<p>`, `<h1>`, `<section>`
```html
<div style="background: lightblue; width: 300px;">I am a block element</div>
<p style="background: lightcoral;">I also take full width</p>
```
#### **2️⃣ Inline Elements (`display: inline`)**  
Stays in line, only takes up as much space as needed  
Examples: `<span>`, `<a>`, `<strong>`
```html
<span style="background: yellow;">I am inline</span>
<a href="#" style="background: orange;">I am also inline</a>
```
#### **3️⃣ Inline-Block Elements (`display: inline-block`)**  
✅ Stays in line **but** supports width & height  
📌 Examples: `<button>`, `<input>`, custom `<span>` styling  
```html
<span style="display: inline-block; width: 150px; background: lightgreen;">I have width & height</span>
<button style="display: inline-block; width: 100px;">Button</button>
```
### **Visual Representation**
```
[BLOCK]          (Takes full width)
[BLOCK]
[INLINE] [INLINE] [INLINE]   (Stays in line)
[INLINE-BLOCK] [INLINE-BLOCK]   (Stays in line but supports width)
```
### **When to Use?**
- **Use `block`** for sections, divs, and paragraphs.
- **Use `inline`** for text elements that should flow naturally (like links & spans).
- **Use `inline-block`** when you need inline elements but want to set width & height.

---

