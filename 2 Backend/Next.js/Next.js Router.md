# Next.js Router

Docs: https://nextjs.org/docs/app/building-your-application/routing

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

## Route Groups `()`

Naming a folder with parenthesis around its name `()` will cause the folder to be a `route group`, meaning that it will be skipped in the URL route structure. It only serves to organize the folder structure, without influencing the routes.

Eg: `app/(auth)/login` structure would correspond to a path of `localhost:3000/login`.

## Dynamic Routes `[]`

A dynamic segment is similiar to the dynamic routes from React Router.
A folder in the app structure whose name is wrapped in square brackets `[]` will correspond to any route segment that does not match with any other folder.

Eg. `app/blog/[id]` will correspond to any leaf of the `localhost:3000/blog/` URL, eg. `localhost:3000/blog/4`, `localhost:3000/blog/something` etc.

### `params` prop

The dynamic route segment (params) can be accessed by a `page` or `layout` through the `params` prop.

The `params` prop has a structure of `{ slug: value}`. That would mean:
- `app/blog/[id]/page.tsx` file routed to by `localhost:3000/blog/4` would have a `params` prop of `{ id: 4 }`
- `app/blog/[id]/page.tsx` file routed to by `localhost:3000/blog/something` would have a `params` prop of `{ id: something }`

### Catch-all segment `[...]`

A dynamic route segment can be a catch-all segment, meaning that any URL segment after that one will be caught by the dynamic route.

Eg: `app/blog/[...id]/page.tsx` will match  `localhost:3000/blog/1` but also `localhost:3000/blog/1/new/`, `localhost:3000/blog/1/new/success` etc. 

The `params` prop for a catch-all segment has a structure of `{ slug: [value1, value2, etc]}`. That would mean:
- `app/blog/[...id]/page.tsx` file routed to by `localhost:3000/blog/4` would have a `{params}` prop of `{ id: [4] }`
- `app/blog/[...id]/page.tsx` file routed to by `localhost:3000/blog/4/new` would have a `{params}` prop of `{ id: [4, 'new'] }`
