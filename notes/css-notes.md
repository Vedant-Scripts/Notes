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
