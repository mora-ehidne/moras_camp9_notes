In native JavaScript, all code execution happens synchronously.
Asynchronous code execution is provided through APIs, such as the Web API.

In a JavaScript program, first all synchronous code is performed (even if it takes some time, due to complex loops etc.). After that, the asynchronous function calls are being performed.

Asynchronous functions from the Web API are provided by the `window` object:
* [[#`setTimeout()`]]
* [[#`setInterval()`]]

>[!INFO] All methods and properties of the `window` object can be accessed either by refering to the `window` object or by just refering to the property or method, like `window.setTimeout()` or simply `setTimeout()`

The Promise API provides the `Promise` class, which also functions asynchronously.


# `setTimeout()`

The `setTimeout()` function has two parameters: 
 1. a callback function that will be called after the timeout duration has passed *(function)*
 2. the duration of the timeout in milliseconds *(number)*

`setTimeout()` returns a unique timeout id *(number)*

```js
setTimeout(myFunc, 1000); // calls myFunc() after 1 second
setTimeout(()=>{console.log("5 seconds passed!")}, 5000); // logs 5 seconds passed! after 5 seconds
```

## `clearTimeout()`

In order to discard an initialized timeout from the API, the `clearTimeout()` function is used.

The `clearTimeout()` function has a single parameter:
1. the id of the timeout to be cleared *(number)*

```js
let timeoutID = setTimeout(myFunc, 1000); // calls myFunc() after 1 second, returns the id of the timeout, which is then assigned to the variable timeoutID
clearTimeout(timeoutID); // removes the timeout referenced by the timeoutID from the API, so it will never be called
```

# `setInterval()`

The `setInterval()` function behaves similiarly to the `setTimer()` function, except that instead of calling the callback function once, the callback function is called each time after the interval duration has passed. 
Because of that, `setInterval()` acts as an endless loop that waits a specified duration in between each iteration.

The `setInterval()` function has two parameters: 
 1. a callback function that will be called after the interval duration has passed *(function)*
 2. the duration of the interval in milliseconds *(number)*

`setInterval()` returns a unique interval id *(number)*

```js
setInterval(myFunc, 1000); // calls myFunc() after each 1 second that passes
setInterval(()=>{console.log("5 seconds passed!")}, 5000); // logs 5 seconds passed! after each 5 seconds that pass
```

## `clearInterval()`

In order to stop an interval from iterating, the `clearInterval()` function is used.

The `clearInterval()` function has a single parameter:
1. the id of the interval to be cleared *(number)*

```js
let intervalID = setInterval(myFunc, 1000); // calls myFunc() after each 1 second, returns the id of the interval, which is then assigned to the variable intervalID
clearInterval(intervalID); // stops the interval referenced by the intervalID from iterating ever again
```

# Promise
