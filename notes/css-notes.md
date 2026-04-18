*Frontend Terminologies*
1. Navbar -> A navbar is just a menu of links that helps users move around your site. (Usually sits at the top)
   - Logo
   - Links (Home, About, Contact)
   - Sometimes buttons (Login, Signup)
2. A sidebar is a vertical navigation menu (Usually on the left side)
3. A header is the top section of a page, not just navigation.
   - Navbar, Title, Hero Section, Call-to-action
   - “The top intro area of a page”
4. A footer is the bottom section.
   - Copyright, Extra links, Contact Info
5. Main Content
   - This is the actual stuff your page is about.
   - Articles, cards, data, UI components
  
LAYOUT VISUAL :
[ Navbar / Header ]
[ Sidebar ] [ Main Content ]
[ Footer ]


| Problem           | Solution |
| ----------------- | -------- |
| Row/Column layout | flex     | -> aligning stuff inside each card
| Grid (like board) | grid     | -> dashboards, galleries, card layouts
| Center something  | flex     |
| Spacing           | gap      |

*How big is it?* → width, height
*Does content feel cramped/sticking to edge?* → padding(cushioning)
*Are elements too close to each other?* → margin

*PostCSS*: A tool for transforming CSS with JavaScript. It acts as the engine that runs plugins (like Tailwind CSS and Autoprefixer) to process and modify your styles before they reach the browser.
*Tailwind CSS*: A utility-first CSS framework that works as a PostCSS plugin. It processes special directives (e.g., `@tailwind utilities`) and scans your HTML/JS files to generate only the CSS you actually use.
*Autoprefixer*: A PostCSS plugin that parses your CSS and adds vendor prefixes (e.g., -webkit-, -ms-) based on browser support data (from Can I Use). It ensures your CSS works consistently across different browsers.