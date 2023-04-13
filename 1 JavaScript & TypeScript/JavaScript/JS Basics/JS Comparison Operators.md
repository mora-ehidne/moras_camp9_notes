Javascript has two different equality and inequality comparison operators:

Equality operators are `==` and `===`.
(the *loose equality operator* and the *strict equality operator*)

Inequality operators are `!=` and `!==`.
(the *loose inequality operator* and the *strict inequality operator*)

The first one of each are called ==loose operators== and the second ones are called ==strict operators==.

Loose operators perform a _type conversion_ of the operands before comparison, while the strict operators do not, they compare the values as well as the data types of the operands.

> In effect, the strict operators behave as default operators in C++, the loose operators are a special Javascript quirk. 

```js
let a = 10;
let b = '10';

a == b; // loose operator, equals: true, as the data types are converted before the comparison
a === b; // strict operator, equals: false, as the data types stay as they are, and a string is not equal to an integer
```

>[!TIP] Comparison operators always return a boolean value, either `true` or `false`.

All comparison is case sensitive, thus "mystring" will never be equal to "MyString".