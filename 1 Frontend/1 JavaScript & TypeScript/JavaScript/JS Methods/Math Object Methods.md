# Math.round()

The `Math.round()` static method returns the value of a number rounded to the nearest integer.

```js
Math.round(5.44); // returns 5
Math.round(5.67); // returns 6
Math.round(5.50); // returns 6
```

# Math.floor()

The `Math.floor()` static method returns the value of a number rounded *down* to the nearest integer.

# Math.ceil()

The `Math.ceil()` static method returns the value of a number rounded *up* to the nearest integer.

# Math.trunc()

The `Math.trunc()` static method returns the value of a number truncated to a whole number (integer). The value after the floating point gets discarded. This method function essentially the same as the `parseInt()` global method.

>[!TIP] `~~` (double tilde or double bitwise not operator) is a shorthand for `Math.trunc()`.

# Math.random()

The `Math.random()` static method returns a floating-point, pseudo-random number that's greater than or equal to 0 and less than 1. 
For more information, visit the [MDN Web docs Math.random() reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/random)