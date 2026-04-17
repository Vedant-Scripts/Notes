1. **Vite**
   - Vite is a frontend build tool + development server.
   - helps in - starting project, running dev server, bundle code for production, reloads changes super fast.
   - It helps in preparing things.
   - *vite.config.ts* defines how all that transformation happens
       <!--    Your React + Tailwind code
                     ↓
               Vite reads config
                     ↓
               react() plugin → handles JSX
               tailwindcss() plugin → generates CSS
                     ↓
               Final JS + CSS sent to browser
      -->
   
2. **React Routing**
   1. **BrowserRouter**
      - BrowserRouter Comp -> React router -> that enables client side routing in react app -> USING Browser's built-in *History API* 
       - *History Api* is js feature in browser that enables 1. change Url without refreshing 2. keep track of naviagtion.
      - enables routing.
      - prevents full page reload.

   2. **Hash Router**
      - In Hash router -> browser + react manages the routing and rendering the server does not have to do anything.
      - Hash router is also the part of react router.
      - *Usefull* => when server can't be configured, so it can work independently ( github pages, static file hosting), Browser router needs cooperation (server).
      - *limitations* => worse for SEO
      ```js
      /*
        const URL = "https://example.com/#/about" 
        BROWSER SENDS = GET /
        SERVER never sees /about
        Server only returns Index.html, then browser + react do magic on it.
      */
      ```
    3. **Memory Router**
       - A router that does NOT use the browser URL at all.
       - stores route in memory.
       - usually works for non-browser environment ( react native, embedded apps etc).
       - All in app functionalities would happen( coz internally routes is changing in memory thats why), but anything that depends on browser URL/history(api) does not.

3. **CSR & SSR**
   - *CSR* - in csr, server sends the code not UI, browser builds the UI.
       - Browser downloads and runs JS bundle, 
       - JS  executes the code. React renders the component in an empty DOM.

   - *SSR* - When req is made, Server runs the react Code, fetches data, builds UI/html. 
       - Fully rendered html is sent to browser, no waiting for JS to build UI.
       - In browser, *Hydration happens*: (Mean: React attaching logic to existing HTML)
                     - Browser downloads the Js bundle (same as CSR)
                     - React attaches this to html to make it interactive (clicks etc stuff)
    
    - CASE 1: IF Frontend is Next and backend is somewhere, then frontend server would do api call to fetch data and build html
    - CASE 2: IF both frontend and backend are on Next. then ta direct db call or a internal api call

4. *PROPS* : -> *read-only* arguments passed to react components
   - In JSX, a prop without = means: **boolean true**
   - ```js
      <UserList
         title
      />
      // The above and below are same
      <UserList
         title={true}
      />

5. *Parent Component* owns state + logic,
   *Child Component* receives via props

6. *Link* : just like <a> tag it acts a hyperlink type thingy
   -> *NavLink*: it is a wrapper around Link, more like a smarter version of Link.
      - it knows the *active route*, which helps in styling the active route automatically.
      for eg 
      ```jsx
         <NavLink 
         to="/users" 
         style={({ isActive }) => ({
            color: isActive ? 'red' : 'black'
         })}
         >
         Users
         </NavLink>
      ```
7. `const Layout = ({ children }: { children: React.ReactNode })` => React.ReactNode = anything React can render
   - “children can be anything React is capable of rendering”
   
8. **CSS**
   1. *flexbox* : turns a container into flex container
         ```css
            <div style={{ display: 'flex'}}>
               <div style={{ width: '200px', borderRight: '1px solid gray' }}>Sidebar</div>
               <div style={{ padding: '20px', flex: 1 }}>MainContent</div>
            </div>
            <!-- Its children become flexible items laid out: [ Sidebar ][ Main Content ] -->
         ```
      - Its children become flexible items laid out:
        - in a row (default)
        - or column (if specified)
      - *flex: 1*: "Take all remaining space available". (sidebar is taking fixed 200, so the other maincontent div will adjust in the remaining space)
        - this only works when the parent has `display="flex"`
    - 

useEFFECT ?
useREF ?