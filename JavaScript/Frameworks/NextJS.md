---
title: NextJS
date created: Tuesday, April 22nd 2025, 10:51:59 am
date modified: Tuesday, April 22nd 2025, 11:28:48 am
---

# NextJS

## General

- Provides features for reach such as routing, data fetching, and caching
- uses **file-system routing** - instead of routes, can use folders and files
  - `export default` helps NextJS determine which component to render as the main component
- uses **React server components** - lets you render React on the server
  - do **not** support `useState` → only used within Client components
- `layout.js` created inside `app.js` holds the main layout of the application
  - can use it to add UI elements that are shared across all pages (eg. navigation, footer, etc.)

## Server vs Client Components

- To understand server/client components, it's helpful to know 2 web concepts
  - The **environment** your application code can be executed in (eg. server and client)
  - The **network boundary** that separates sever and client code
  - Server/client components are better suited for one environment over the other

### Network boundary

- Conceptual line that separates different environments and you can chose where you decide to place it within your component tree - Can fetch data and render a user's posts on the server ([server components](#server-components)) then render interactive elements, such as buttons, on the client ([client components](#client-components)) - Can create a nav component that is rendered on the server and shared across pages, but to show active state you would need to render the lists themselves on the clients
  ![](Pasted%20image%2020250306110209.png)
- behind the scenes, are split into two module graphs
  - server module graph (or tree) - contains all **server components** that are rendered on the server
  - client module graph (or tree) - contains all **client components**
- After server is rendered, data format called **React server component payload (RSC)** is sent to client
  - Contains:
    - Rendered result of server components
    - Placeholders (or holes) for Client components that should be rendered / references to JS files
  - This info is used to consolidate Server and Client components and update DOM on the client

### Server Components

- The computer in a data center that stores your application code, receives requests from a client, does some computation, and sends back an appropriate response
- Does **not** support hooks
- Can help reduce the amount of code sent to the client which can improve application's performance
- By default, next uses react server components, which lets you render react on the server
- Do not require additional steps to adopt

### Client components

- Refers to browser on a user's device that sends a request to a server for your application code
  - Turns response into an interface for user to interact with
- Used to update the DOM on the client
- Supports hooks
- Requires `'use client'` directive on top of the file to tell react to render on the client

## Folder structure

- `/app` contains all routes, components, and logic for application
- `/app/lib` contains _functions_ used in application (eg. reusable utility functions and data fetching functions)
- `app/ui` contains all UI elements for application (eg. cards, tables, forms)
- `/public` contains all static assets (eg. images)
- `/app/lib/definitions.ts` - define types in DB
- Config files - `next.config.ts` is at root of application
- Can use `.ts` or `.tsx` to specify TypeScript
  - Prevent the wrong format of data from being passed

## Styling

- CSS Modules scope CSS to a component by creating unique class names
- `clsx` to toggle class names
  - conditionally add styles on an element based on state or another condition

### Cumulative layout shift

- Layout shift can happen when browser initially renders text in a fallout or system font then swaps it for a custom font once loaded
  - Can cause text size, spacing, or layout to change, shifting elements around it
- Next optimizes fonts when using `next/font` module
  - Downloads font files at build time and hosts with static assets
  - Causes no additional network requests for fonts that would impact performance

### Image optimization

- Prevents you from manually having it:
  - Keep track of image responsiveness on different screen sizes
  - Specify images for different devices
  - Prevent layout shifts as images load
  - Lazy load images that are outside user's viewport
- `next/image` to optimize
  - `<Image>` comes with automatic image optimization
    - Prevents layout shift while images load
    - Resize to avoid shipping large images on smaller viewports
    - Lazy load by default (load as they enter viewport)\
    - Serving images in modern formats, when browser supports it

## Routing

- Use file-system routing where folders are used to create nested routes - Each folder represents a route segment that maps to a URL segment
  ![](Pasted%20image%2020250306115505.png)
- The `children` prop can either be a page or another layout
- Using layouts help with navigation
  - Only the page components update while the layout won't re-render
    - Parital re-rendering which preserves client-side state when transitioning between pages
- Root layout is required in every Next application
  - Any UI in the root will be shared across _all_ pages
    - Can be used to modify your `<html>` and `<body>` tags and add metadata

### Link component

- links between pages in an applications
- Allows for client-side navigation with JS
- Automatically code splits application by route segements
  - Avoids the browser loading all application code on initial page load
  - Pages are isolated - if certain pages throw an error, rest of application still works
  - Less code for browser to parse, which makes application faster
- When in viewport, will prefetch code to linked route in background
  - transitions to new pages will be near-instant
- `usePathname` can be used to check path and update UI

## Fetching data

### API layer

- Intermediary layer between application code and database
- Useful when:
  - Using third party services that provide an API
  - If fetching data from client, API layer runs on the server to avoid exposing DB secrets to client
- Can create API endpoints using [route handlers](#route-handlers)

### DB queries

- Needed when:
  - creating API endpoints, need to write logic to interact with DB
  - When using RSC's (fetching data on server), can skip API layer and query DB directly **without risking exposing your db secrets** to the client

### Using server components

- Support JS promises, providing a solution for async tasks like data fetching natively
  - Can use `async/await` without needing `useEffect`, `useState`, or other data fetching libraries
- Run on the server so extensive data fetches and logic are on the server, only sending results to client
- Query DB without additional API layer
  - Saves you from writing and maintaining more code
