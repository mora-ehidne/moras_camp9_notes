# the `window`element

The root/parent element in the DOM is the `window` element. It represents the entire browser window, including the navigation buttons etc.

# the `document`element

The first direct child of `window` is the `document` element. The `document` element can be referenced on its own, without referencing its parent first. All manipulation of HTML elements in the DOM happen through the `document` element. 

```js
const headingTwo = document.querySelector("h2"); // assigns the first appeared h2 tag from the DOM to the headingTwo constant
const newElement = document.createElement("h3");// creates a new h3 element in the DOM
```

>[!TIP] `document.createElement()` creates an html element, which is not yet part of the DOM. In order to actually have it somewehere in the web page, we must add it as a child of an already existing element, through eg. the `.prepend()` and `.append()` methods of the parent element.