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
