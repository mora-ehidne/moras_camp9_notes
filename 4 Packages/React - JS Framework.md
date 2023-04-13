# React

React code uses JSX syntax - JavaScript XML, which is a combination of JavaScript and HTML.
React code files have the extension `.tsx` instead of `.ts` and `.jsx` instead of `.js`.

Faux-HTML code is used in JSX - notably in the `return` statement of components and within the arguments of the `render` method call in `main.tsx`. 
Within the faux-HTML, all code within curly brackets `{}` is treated as standard JS/TS code.

# Connecting React to index.html

## `index.html`

The entire website created in React gets rendered into the .html file, usually targeting the div element with the id of `root`, which is the first child of the `body` element.

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>React!</title>
	</head>
	<body>
		<div class="" id="root"></div>
		<script type="module" src="/src/main.tsx"></script>
	</body>
</html>
```

>[!WARNING] It is bad practice to render the React app directly into the `body` tag, as it can interfere with functionalities of other web apps.

## `main.tsx`

The `main.tsx` file is responsible for rendering the app in the DOM element with the id of `root`.

```tsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./components/App";
import "./index.css";

ReactDOM.createRoot(document.getElementById("root") as HTMLElement).render(
	<React.StrictMode>
		<App />
	</React.StrictMode>
);
```

>[!INFO] `index.css` is imported into `main.tsx` as the global stylesheet.


# Components

A components is a function in its own `.tsx`/`.jsx` file.
Components are named in [[Naming conventions (cases)#Pascal case (PascalCase)|PascalCase]].
A component returns a single DOM element. If more than a single DOM element schould be returned, elements must be nested in a wrapper element or a fragment (a react-specific html element that gets ignored).

>[!TIP] The component function must be exported in order for its parent components to import it and use it.

```tsx
export function Button() {
return (
<> // opening fragment tag
<button>Hello, this is a button!</button>
<small>button's name: {name}</small>
</> // closing fragment tag
);
}
```

>[!INFO] Note that the `return` statement is a single statement, delimetered by parentheses `()` and ended with a semicolon `;`. WIthin a statement, only expressions are allowed, no other statements. This means that no variable declaration, value assignments, if statements, loops, etc. NOTE: Ternary operator and short-circuiting can still be used as a replacement for conditional statements.


## `App.tsx`

`App.tsx` is the main component of the React project. Within its `return` statement, all the DOM elements for the app are created.

```tsx
import { Button } from "./shared/Button";
import { Navbar } from "./shared/Navbar";

export function App() {
	return (
		<>
			<Navbar/>
			<p>Hi!</p>
			<Button></Button>
		</>
	);
}
```

# Props

All arguments passed to a component are passed to a single parameter, conventionally named `props` (for properties).
`props` is an object containing all the arguments passed, which are stored in the properties of `props`.

In the `MyComp.tsx`:

```tsx
export function MyComp(props: { classes: string; children: string }) {
	return <div className={props.classes}>{props.children}</div>;
}
```

or with `props` destructured:

```tsx
export function MyComp({classes, children}: { classes: string; children: string }) {
	return <div className={classes}>{children}</div>;
}
```

In the `App.tsx`:

```tsx

import { MyComp } from "./shared/MyComp";

function App() {
	return (
		<>
			<MyComp classes="text-xl text-cyan-400">Hi!</MyComp>
		</>
	);
}
```

>[!TIP] Note that all arguments are passed as pseudo-HTML attributes, except the named `children` argument, which is passed as the text content of the pseudo-HTML element.