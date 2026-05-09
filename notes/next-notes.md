# Next.js Notes

# What is Next.js?

Next.js is a React framework built by Vercel.

React itself is only a UI library.

Next.js adds:

- Routing
- Server-side rendering
- Backend/API support
- SEO optimization
- Full-stack features
- Better performance tooling
- File-based structure
- Production optimizations

---

# React vs Next.js

| React.js                         | Next.js                      |
| -------------------------------- | ---------------------------- |
| UI Library                       | Full-stack React Framework   |
| Uses React Router                | Built-in Routing             |
| Client-side rendering by default | Supports SSR, SSG, CSR       |
| Manual project setup             | Opinionated structure        |
| No backend support               | API routes + server actions  |
| Separate SEO setup               | SEO-friendly by default      |
| Vite/Webpack commonly used       | Webpack/TurboPack internally |

---

# Key Difference

## React

You build:

- components
- routing manually
- API integration manually
- optimization manually

## Next.js

Framework already provides:

- routing
- rendering strategies
- backend capabilities
- optimization
- deployment support

---

# Project Structure

## React

```bash
src/
  components/
  App.jsx
  main.jsx
```

## Next.js

```bash
app/
  page.js
  layout.js
  about/
    page.js
```

or older:

```bash
pages/
```

---

# Routing Difference

## React Router

```jsx
<Route path="/about" element={<About />} />
```

## Next.js File Routing

```bash
app/about/page.js
```

Automatically becomes:

```bash
/about
```

No React Router needed.

---

# Rendering Types in Next.js

## CSR (Client Side Rendering)

Like normal React.

Browser renders page.

Good for:

- dashboards
- interactive apps

---

## SSR (Server Side Rendering)

Page rendered on server every request.

Good for:

- SEO
- dynamic content

---

## SSG (Static Site Generation)

Page generated at build time.

Very fast.

Good for:

- blogs
- docs
- landing pages

---

# Server Components vs Client Components

## By default in Next.js App Router:

Components are Server Components.

This is VERY important.

---

# Server Component

Runs on server.

Can:

- fetch database data directly
- use async/await
- reduce JS bundle size

Cannot:

- use useState
- useEffect
- browser APIs

Example:

```jsx
export default async function Page() {
  const data = await fetch("...");

  return <div>Hello</div>;
}
```

---

# Client Component

Needed for:

- interactivity
- hooks
- events

Add:

```jsx
"use client";
```

Example:

```jsx
"use client";

import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  return <button>{count}</button>;
}
```

---

# Important Mindset Shift

In React:

- everything runs on client

In Next.js:

- server first
- client only when needed

---

# Data Fetching

## React

Usually:

```jsx
useEffect(() => {
  fetch(...)
}, []);
```

## Next.js

Can directly do:

```jsx
const data = await fetch(...)
```

inside server components.

Cleaner and faster.

---

# API Routes

Next.js can create backend endpoints.

Example:

```bash
app/api/users/route.js
```

Example:

```js
export async function GET() {
  return Response.json({ message: "Hello" });
}
```

Becomes:

```bash
/api/users
```

---

# Special Files in App Router

## page.js

Represents route page.

---

## layout.js

Shared layout.

Example:

- navbar
- sidebar
- footer

---

## loading.js

Loading UI.

---

## error.js

Error boundary UI.

---

## not-found.js

404 page.

---

# Navigation

Use:

```jsx
import Link from "next/link";
```

Example:

```jsx
<Link href="/about">About</Link>
```

NOT:

```jsx
<a href="/about">
```

---

# Image Optimization

Use:

```jsx
import Image from "next/image";
```

Benefits:

- lazy loading
- optimization
- resizing
- better performance

---

# Environment Variables

Use:

```env
NEXT_PUBLIC_API_URL=
```

Client-side variables MUST start with:

```env
NEXT_PUBLIC_
```

---

# Common Commands

## Create Project

```bash
npx create-next-app@latest
```

---

## Start Dev Server

```bash
npm run dev
```

---

## Production Build

```bash
npm run build
```

---

# TurboPack

Next.js now uses TurboPack for faster development builds.

TurboPack:

- written in Rust
- faster than Webpack
- optimized for large apps

---

# Important Things Beginners Forget

## 1. Everything is server component by default

Need hooks?

Add:

```jsx
"use client";
```

---

## 2. File-based routing matters

Folder names become URLs.

---

## 3. Server components reduce bundle size

Do NOT make everything client-side.

---

## 4. Next.js is full-stack

You can:

- build frontend
- backend APIs
- authentication
- database logic

inside one project.

---

# When to Use React Only

Use plain React if:

- simple SPA
- lightweight frontend
- no SSR needed

---

# When to Use Next.js

Use Next.js if:

- SEO matters
- production app
- full-stack app
- authentication
- dashboards
- scalable architecture
- performance matters

---

# Mental Model

```text
React = UI Library

Next.js = React + Framework + Backend + Routing + Rendering + Optimization
```

---

# Final Advice

Do NOT try to memorize everything immediately.

Learn in this order:

1. Routing
2. App Router structure
3. Server vs Client components
4. Data fetching
5. API routes
6. Rendering strategies
7. Deployment

Once Server vs Client Components click, most of Next.js starts making sense.

---

# Next.js App Router Mental Model

## Routing

In Next.js App Router, folders define routes.

Example:

app/
login/
page.tsx

Route:
`/login`

`page.tsx` is mandatory because Next.js uses convention-based routing.

---

# Layouts

`layout.tsx` acts as a shared wrapper for all routes inside that folder.

Example:

app/
(auth)/
layout.tsx
login/
page.tsx
signup/
page.tsx

When visiting `/login`, Next internally builds:

<RootLayout>
  <AuthLayout>
    <LoginPage />
  </AuthLayout>
</RootLayout>

The `children` inside layout are automatically replaced with the current route's page.

---

# Route Groups

Folders inside parentheses are route groups.

Example:

(auth)/

Used only for:

- organization
- shared layouts

They do NOT appear in URL.

So:

(auth)/login/page.tsx

becomes:

`/login`

NOT:

`/auth/login`

---

# Responsibilities

## layout.tsx

Handles:

- shared UI
- structure
- wrappers
- common sections

Example:

- auth background
- split screen
- navbar
- sidebar

---

## page.tsx

Represents actual route.

Should mostly:

- compose components
- stay thin
- avoid massive logic/UI dump

Example:

login/page.tsx
-> renders LoginForm

---

## Components

Actual UI/business pieces.

Example:

components/auth/
LoginForm.tsx
SignupForm.tsx

components/ui/
Button.tsx
Input.tsx

---

# Mental Hierarchy

layout
wraps
page

page
renders
feature components

feature components
use
reusable UI components

---

# Key Idea

Folder hierarchy defines UI hierarchy.

Next.js automatically connects:

- layouts
- routes
- pages

based on file/folder conventions.

# Figma → Frontend

Usually take:

- font size
- font weight
- spacing
- padding
- gap
- colors
- border radius
- alignment

Usually ignore:

- raw X/Y positions
- exact canvas coordinates

Frontend is responsive, not static canvas.

---

# Width & Height

Use explicit sizes when:

- icon/container size matters
- avatar/card/circle/button dimensions matter

Example:

```tsx
w-12 h-12
```

Avoid forcing sizes on:

- paragraphs
- flowing layouts
- text containers

---
