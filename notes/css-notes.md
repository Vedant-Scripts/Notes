| Problem           | Solution |
| ----------------- | -------- |
| Row/Column layout | flex     |
| Grid (like board) | grid     |
| Center something  | flex     |
| Spacing           | gap      |


*PostCSS*: A tool for transforming CSS with JavaScript. It acts as the engine that runs plugins (like Tailwind CSS and Autoprefixer) to process and modify your styles before they reach the browser.
*Tailwind CSS*: A utility-first CSS framework that works as a PostCSS plugin. It processes special directives (e.g., `@tailwind utilities`) and scans your HTML/JS files to generate only the CSS you actually use.
*Autoprefixer*: A PostCSS plugin that parses your CSS and adds vendor prefixes (e.g., -webkit-, -ms-) based on browser support data (from Can I Use). It ensures your CSS works consistently across different browsers.