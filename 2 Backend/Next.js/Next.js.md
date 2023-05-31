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

What will be served from the corresponding folder depends on the `.tsx` files present in that folder and the status of the GET request.

![[Next.js_route-segments-to-path-segments.png]]

## Router Components

There are reserved names for `.tsx` files that get treated specially by the Next.js router.
One of these files will be served in response to a GET request depending on which one of the files is present in the corresponding folder and the status of the GET request.

- `page.tsx` - gets served when the GET request is successful
- `layout.tsx` - wraps `page.tsx` and can hold additional components. If present, gets served instead of `page.tsx`
- `error.tsx` - gets served when an error is thrown within the folder
- `loading.tsx` - gets served when `page.tsx` is in loading state

>[!TIP] These components get compiled into `.html` files before they get served in the HTTP response. 

### `page.tsx`

A successful HTTP request renders the `page.tsx` in the directory corresponding to the given URL.
Going to a page eg. `localhost:3000/contact` would load a `contact.html` page based on the `page.tsx` component in the`/app/contact` directory. 

>[!NOTE] In Next.js there is no `main.js` or `index.html`. The `/app/page.tsx` /  `/app/layout.tsx` can be seen as the home page of the entire app.

### `layout.tsx`

`layout.tsx` is a component that wraps a `page.tsx`, making it possible to include headers, footers etc.

`layout.tsx`  is also a good place to define _metadata_ (the same as the HTML metadata from the `<meta>` tag - title, description, author, etc).

Instead of a `main.js` in React, there is the `/app/layout.tsx` in Next.js.
Inside of it, the layout of the app can be defined.

>[!WARNING] Layout routing and nesting:
> `layout.tsx` gets routed to in order of inheritance - the children `layout.tsx` files get nested within their parent `layout.tsx` files.
> 
> This means: on `localhost:3000/blog` we will get `/app/blog/page.tsx` nested within `/app/blog/layout.tsx` nested within `/app/layout.tsx`.

### `error.tsx`

`error.tsx` is the component that renders when a page within that directory throws an error.
Eg. `/app/about/error.tsx` renders when `/app/about/page.tsx` throws an error.

### `loading.tsx`

`loading.tsx` is the component that renders when a page within that directory is still being loaded.

>[!WARNING] `error.tsx` and `loading.tsx` get routed to in order of inheritance:
> The one that is nearest in the nesting structure to the page that is loading/throwing an error will get served.
> 
> For example, for an error thrown by `/app/blog/posts/page.tsx`, `/app/blog/posts/error.tsx` will be served. If no `error.tsx` exits within the `/app/blog/posts` folder, the one in the parent directory (`/app/blog`) will be served. If no `error.tsx` exits within that folder, than the one from the parent folder will be served etc. all the way up the nesting structure until finally, `/app/error.tsx` is reached.

# Server and Client Components

Some Next.js components are only available to Server Components and other only to Client Components.

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
