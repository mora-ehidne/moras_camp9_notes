# About

React Router enables "client side routing".

Client side routing allows your app to update the URL from a link click without making another request for another document from the server. Instead, your app can immediately render some new UI and make data requests with `fetch` to update the page with new information.

Homepage: https://reactrouter.com/en/main

# Setup

The package installation command is:
````sh
npm install react-router-dom localforage match-sorter sort-by
````

# Using the React Router

## `BrowserRouter` wrapper component

In order to use to router, the `App` component must be wrapped in a `BrowserRouter` component.

in main.tsx:
```tsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import "./index.css";
import { BrowserRouter } from "react-router-dom";

ReactDOM.createRoot(document.getElementById("root") as HTMLElement).render(
	<React.StrictMode>
		<BrowserRouter>
			<App />
		</BrowserRouter>
	</React.StrictMode>
);
```

## `Routes` and `Route` components

The routing is done by specifying the `Route` tags, wrapped within a `Routes` wrapper. The `Route` tags will generate the page specified in the `element` prop when the page URL is equivalent to the `path` prop. Each page should be a separate component.
The header and the footer can be placed in the `App` component, outside of the pages.

in main.tsx:

```tsx
import { Route, Routes } from "react-router-dom";

function App() {
	return (
		<>
			<header>
			</header>
			<main>
				<Routes>
					<Route path="/" element={<Home />} />
					<Route path="/shop" element={<Shop />} />
					<Route path="/blog" element={<Blog />} />
					<Route path="/blog/:id" element={<BlogPost />} />
					<Route path="/about" element={<About />} />
					<Route path="/*" element={<h1>404 not found!</h1>} />
				</Routes>
			</main>
			<footer>
			</footer>
		</>
	);
}

export default App;
```

## Navigating to a new URL

### `Link` and `NavLink` components

The `Link`/`NavLink`components are provided by the React Router, and are used to redirect to a new URL on click, just like an `<a>` tag. They in fact do render an `<a>` tag with an `href` attribute, but perform client-side routing. 

The `to` prop accepts a string containing the URL to redirect to, just like an `href` attribute of the `<a>` tag.

The `NavLink` component also provides the `active` class for the currently active link, which can be helpful for styling.

in a component that would have some `Link`/`NavLink` components:
```tsx
import { NavLink} from "react-router-dom";

export function SomeNavigationComponent(){

return (
	<nav>
		<NavLink to="/home">Home</NavLink>
		<NavLink to="/blog">Blog</NavLink>
		<NavLink to="/about">About us</NavLink>
	</nav>
	);
}
```

### `useNavigate` hook

The `useNavigate` hook returns a single function. The first parameter of the function is a string containing the new URL (it acts the same as the `to` prop of the `Link`/`NavLink` component). The function call redirects to the new URL, same as the click on a `Link`/`NavLink` component.

in a component that would use the `useNavigate` hook:
```tsx
import { useNavigate } from "react-router-dom";

export function SomeComponent(){
const navigate = useNavigate();

function someFunc(){
	navigate("/home"); // this function call simply redirects to the "/home" url
}

return (<></>);
}
```

## Dynamic Segments

Segments of the URL specified in the `path` prop can be dynamic, meaning that they act as a wildcard that accepts all matching URLs that do not match a more specific `Route` path.
The dynamic segment starts with a colon `:`.

The syntax is:
```tsx
<Route path="projects/:projectId/tasks/:taskId" element={<BlogPost />}/>
```

### `useParams()` hook

The dynamic segments are accessed by an element by using the `useParams()` hook.
`useParams()` returns an object with as many properties as there are dynamic segments. The properties are strings that match the property, without the colon `:`.

In a component using the `useParams()` hook:
```tsx
import { useParams } from "react-router-dom";
function BlogPost(){
const { segmentOne, segmentTwo} = useParams();
return (
	<>
		<p>{segmentOne}</p> // displays "projectId"
	   <p>{segmentTwo}</p> // displays "taskId"
	</>);
}
```
