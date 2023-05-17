Type conversion (also called type casting) can be *implicit* and *explicit*.

# Implicit Type Conversion (Type Coercion)

In JavaScript, implicit (automatic) data type conversions are sometimes performed. These conversions are called *type coercions*. Many built-in operations that expect booleans first coerce their arguments to booleans, such as the condition check in an `if` statement.

Type coercions happen in JavaScript because it is a *weakly typed programming language.

```js
const value1 = "5";
const value2 = 9;
let sum = value1 + value2; // the value of value2 gets coerced from 9 into the string "9", and concatenated the two values, resulting in the string "59"
let sum = value1 - value2; // the value of value1 gets coerced from the string "5" into the number 5, and the value2 is substracted from it, resulting in the number -4
let sum = Number(value1) + value2; // the value of value1 gets explicitly converted into a number, which then gets added to value2, resulting in the number 14
```

# Explicit Type Conversion

Explicit type conversion is a kind of conversion that the programmer explicitly does in the code. There are several data types that can be explicitly type cast in JavaScript:

## Number()

The global method `Number()` returns the passed value converted into a Number data type, that is, a floating-point 64-bit (double precision) number.

Two similiar methods are the global methods `parseInt()` and `parseFloat()`.

>[!TIP] `+` (the unary plus operator) is a shorthand syntax for the `Number()` global method .

#### `parseInt()`

The `parseInt()` global method returns the passed value converted into an integer (whole number). If the passed value has some value after the floating point, it gets truncated, that is to say, the value after the floating point gets discarded (exactly like `Math.trunc()` and similiarly to the `Math.floor()`, `Math.round()` and `Math.ceil()` methods).

#### `parseFloat()`

The `parseFloat()` global method returns the passed value converted into a Number data type, similiarly to the `Number` method.

## String() and .toString()

The global method `String()` returns the passed value converted into a String data type. The `.toString()` method belongs to the Number object and does the same thing.

## Boolean()

The global method `Boolean()`returns the passed value converted into a Boolean data type.

