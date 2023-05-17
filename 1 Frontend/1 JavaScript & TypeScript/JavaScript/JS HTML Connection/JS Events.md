examples of HTML events:

-   An HTML web page has finished loading
-   An HTML input field was changed
-   An HTML button was clicked

# Event Handlers

event handlers can be added in html as attributes to the html tags. They can have a javascript code defined as its value.

```html
<element event="JavaScript code"/>
```

 more commonly, event handler attributes tend to call a Javascript function:
 
 ```html
 <button onclick="displayDate()">The time is?</button>
```

For a complete list of HTML DOM Events, refer to this [W3Schools page](https://www.w3schools.com/jsref/dom_obj_event.asp).

# Event Listeners

Instead of adding event handlers as attributes in HTML, we can also add **event listeners** in the javascript file, eg:

```js
element.addEventListener("event", myFunction, useCapture);
```

The first parameter is the type of the event (like "`click`" or "`mousedown`" or any other DOM event),  the second parameter is the function called when the event occurs, the third, optional, parameter is a boolean value specifying whether to use event bubbling or event capturing. 

The `addEventListener()` method attaches an event handler to the specified element. It does not override any existing event handlers, regardless if they are added in the html or javascript code. An unlimited amount of event handlers (even of the same type) can be added to an element, (eg. two "click" events)

You can add event listeners to any DOM object, not onlyto the HTML elements. i.e the window object.


## Passing Parameters to the Function Called by the Event Listener

The second parameter that the `.addEventListener` method accepts is a function. It is not a function call, but a reference to the body of the function. For that reason, no parameters can be passed to the function.
In order to pass parameters to a function passed as the second parameter to the  `.addEventListener` method, an "anonymous function" must be created, which in its body makes a function call that passes the parameters:

```js
element.addEventListener("click", function(){ myFunction(p1, p2); });
```
