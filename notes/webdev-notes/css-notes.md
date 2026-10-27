| Problem           | Solution |
| ----------------- | -------- | -------------------------------------- |
| Row/Column layout | flex     | -> aligning stuff inside each card     |
| Grid (like board) | grid     | -> dashboards, galleries, card layouts |
| Center something  | flex     |
| Spacing           | gap      |

_How big is it?_ → width, height
_Does content feel cramped/sticking to edge?_ → padding(cushioning)
_Are elements too close to each other?_ → margin

_PostCSS_: A tool for transforming CSS with JavaScript. It acts as the engine that runs plugins (like Tailwind CSS and Autoprefixer) to process and modify your styles before they reach the browser.
_Tailwind CSS_: A utility-first CSS framework that works as a PostCSS plugin. It processes special directives (e.g., `@tailwind utilities`) and scans your HTML/JS files to generate only the CSS you actually use.
_Autoprefixer_: A PostCSS plugin that parses your CSS and adds vendor prefixes (e.g., -webkit-, -ms-) based on browser support data (from Can I Use). It ensures your CSS works consistently across different browsers.

# Relative & Absolute

```txt
relative parent
    └── absolute child
```

- `relative` → positioning reference
- `absolute` → free positioning inside parent

Example:

```tsx
<div className="relative">
  <div className="absolute bottom-8">
```

---

# bottom-8

```txt
bottom-8 = 32px from bottom
```

Tailwind spacing scale:

- `1 = 4px`
- `8 = 32px`

---

# Horizontal Centering Trick

```txt
left-1/2 -translate-x-1/2
```

Meaning:

1. move left edge to center
2. pull element back by half its width

Used for:

- modals
- floating footers
- overlays

---

# Flexbox

```tsx
flex items-center justify-center gap-2
```

- `flex` → horizontal layout
- `items-center` → vertical alignment
- `justify-center` → horizontal alignment
- `gap-2` → spacing between children

---

# Font Properties

## Font Size

Controls text size

```tsx
text-[18px]
text-3xl
```

---

## Font Weight

Controls text thickness

```tsx
font - normal;
font - semibold;
font - bold;
```

---

## Line Height

```tsx
leading-none
leading-tight
leading-[40px]
```

Important for:

- headings
- multiline text

---
