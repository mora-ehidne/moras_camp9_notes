# textContents / innerText / innerHtml

`textContents` refers only to the text within the element and only that of the children that are for styling purposes (bold, strong, em etc.)
`innerText` refers to the text within the element and all of its children
`innerHtml` refers to the entire html code within the element and all of its children, including tags etc.

# .className / .classList 

## `.className`

`element.className` is a property refering to the `class` attribute of the html element. Its value expressed as a string. It can contain a single or multiple class names, separated by a white-space. It can be set (not read-only).

```js
console.log(element.className); // logs the names of all the classes applied to the element. In essence, it is the value of the 'class' attribute of the HTML tag
element.className = "dark-mode"; // overwrites all the classes of the element with the single class called 'dark-mode', in essence, it overwrites the value of the 'class' attribute of the HTML tag with a new string
element.className = "light-mode blue-bg"; // overwrites the 'dark-mode' class with the classes 'light-mode' and 'blue-bg'
```

## `.classList`

`element.classList` is a read-only property that returns an array-like DOMTokenList of the `class` attributes of the element. 
It has the `add()`, `remove()`, `replace()` and `toggle()` methods, which can be used to modify it.

```js
console.log(element.classList); // logs all the names of all the classes applied to the element
console.log(element.classList[0]); // logs the first class of the element, accessing the item at the index of zero of the array-like classList object 
element.classList[0]="my-class"; // doesn't work! 
```