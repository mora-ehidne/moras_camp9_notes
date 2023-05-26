# Next 13

Docs: https://nextjs.org/docs

We are using the *App Router*.

# Installation

In the installation, we used all the default Next.js setup settings.

# Next.js Router

Next.js has a built-in router (so we do not have to use the React Router package).
The Next routing system is folder-based: it routes to a folder in the `app` directory corresponding to the given URL. 

A request URL corresponds to a path (nested folder structure).
The `/app` folder corresponds to the root directory `/` when routing.

Example: a URL of `localhost:3000/dashboard/settings` corresponds to the path of `/app/dashboard/settings`.
A home URL (`localhost:3000/`) corresponds to the path of `/app`.

The component that will be served from the corresponding folder depends on the components present in that folder and the status of the GET request sent to the server.

![[Next.js_route-segments-to-path-segments.png]]

## Router Components

There are reserved names for `.tsx` files that get treated specially by the Next.js router.

Depending on the `.tsx` files present in the corresponding folder and the status of the GET request sent to the server, a specific `.tsx` file will get served. 

Some of these are:
- `page.tsx` - gets served when the GET request is successful
- `layout.tsx` - wraps `page.tsx` and can hold additional components. If present, gets served instead of `page.tsx`
- `error.tsx` - gets served when an error is thrown within the folder
- `loading.tsx` - gets served when `page.tsx` is in loading state

>[!TIP] These components get compiled into `.html` files before they get served in the HTTP response. 

### `page.tsx`

A successful HTTP request renders the `page.tsx` in the directory corresponding to the given URL.
Going to a page eg. `localhost:3000/contact` would load a `contact.html` page based on the `page.tsx` component in the`/app/contact` directory. 

>[!NOTE] The home .html page is `page.tsx` in the `/app` directory (instead of index.html).

### `layout.tsx`

`layout.tsx` is a component that wraps a `page.tsx`, making it possible to include headers, footers etc.

`layout.tsx`  is also a good place to define _metadata_ (the same as the HTML metadata from the `<meta>` tag - title, description, author, etc).

Instead of a `main.js` in React, there is the `/app/layout.tsx` in Next.js.
Inside of it, the layout of the app can be defined.

>[!WARNING] Layout routing and nesting:
> `layout.tsx` also gets routed to in order of inheritance - but instead of replacing the inherited ones, they _nest_.
> 
> This means: on `localhost:3000/blog` we will see `/app/blog/page.tsx` rendered within `/app/blog/layout.tsx` rendered within `/app/layout.tsx`.




### `error.tsx`

`error.tsx` is the component that renders when a page within that directory throws an error.
Eg. `/app/about/error.tsx` renders when `/app/about/page.tsx` throws an error.

### `loading.tsx`

`loading.tsx` is the component that renders when a page within that directory is still being loaded.

>[!WARNING] `error.tsx` and `loading.tsx` get routed to in order of inheritance:
> the one that is nearest to the page that is loading/throwing an error will get loading, if it does not exist, the one int the next nearest ancestor directory will be rendered.
> 
>This way, the `error.tsx` and `loading.tsx` in the root app folder (`/app`) will render on error for any page that does not have an `error.tsx` / `loading.tsx` in its own folder.


# Server and Client Components

Docs: https://nextjs.org/docs/getting-started/react-essentials

![[Next.js_Server-Components_vs_Client-Components.png]]

## Server components

Next.js has a server-first approach: most of the components in Next.js are server components.
Server components are used for static components.

Unlike Client Components, Server Components can be *async*.


## Client components

Client Components are used for interactive elements of the UI.
They should generally be components in the `/components` directory, not pages.

Client Components have to be explicitly set by using the `"use client;"` directive at the start of the `.tsx` file of the component.

eg:
```tsx
"use client";

export default function MyButton(){
	return <button>Click me!</button>
}
```
