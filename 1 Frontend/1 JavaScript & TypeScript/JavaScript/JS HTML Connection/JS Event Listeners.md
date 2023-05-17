# The Callback function (the 2nd parameter)

The second parameter of an `addEventListener()` method is a function. 
If it is directly called, (written with parenthesese after the function name) it will be immediately performed. If it is passed as a callback (written without parenthesese after the function name), it will be performed only when the event listener gets triggered.

```js
function myFunction(){
console.log("hi!");
}
btn.addEventListener("click", myFunction); // logs hi! each time the button gets clicked
btn.addEventListener("click", myFunction()); // logs hi! immediately when this code line gets called, and does not do it afterwards

```

[[JS Functions#Callback functions (functions as arguments)|More on callback functions]]

## Event Object

The event object gets impilictly passed to the [[JS Functions#Callback functions (functions as arguments)|callback function]] (the second parameter of the `addEventListener()` method). The event object has some useful properties, such as `target`, that we can use to access the event target, that is, the object that triggered the event listener.

```js
btn.addEventListener("click", myFunction); // myFunction is a callback function, does not have any arguments passed expilictly
myFunction(event){
	console.log(event);
} // myFunction can access the event object as an argument as it got passed implicitly by the event listener
```

or

```js
btn.addEventListener("click", (e) => myFunction(e)); // the callback function is an arrow function that has a paremeter of e. The addEventListener method always  passes the event object to its callback function. In the callback function body, we call myFunction and pass it as an argument the parameter e. 
myFunction(event){
	console.log(event);
} // myFunction can take the e passed by the callback function into its paremeter event
```