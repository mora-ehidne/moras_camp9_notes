# Primitive data types / values

All data types in JavaScript are either *primitive* or *complex*. 

Primitive data types are always *deep copied* (creates a new, separate copy), while complex data types get *shallow copied* (only a reference to the value gets created). Because of that, complex values are also called *reference values*.
Primitive data types are *static data*, meaning that they are always stored in a part of memory whose size is fixed at compile time. Such values are stored on the *stack*.

Complex data types get stored on the *heap* and do not get a fixed data size. 

# Primitive data types

Primitive data types / values are:
* null
* undefined
* boolean
* number - floating-point 64-bit (double precision) numbers
* string
* symbol
* BigInt

## Literals

Literals are fixed values in JavaScript. They represent concrete, *literal* values that are stated in the code.
Examples of literals:
```js
// string literals
"a string."; // quotation mark string syntax
'a string'; // apostrophe string syntax
`a string ${expression}`; // template literal / template string syntax\

// object literal
{myCar: "Toyota", carType: "Honda"}; // everything within the curly brackets is an object literal

//array literals
["French Roast", "Colombian", "Kona"]; // everything within the square brackets is an array literal
["French Roast", , "Kona"]; // empty spaces can be left within the commas of an array literal, such elements will be initialized with the value of undefined

// numeric literals
0; // an integer literal, base 10 (decimal)
58484; // an integer literal, base 10 (decimal)
0b11; // an integer literal, base 2 (binary)
0x00111; // an integer literal, base 16 (hexadecimal or hex)
3.1415926 // a floating point literal
.123456789 // a floating point literal

// boolean literals
true;
false;
```

#### Template literals (Template strings)

**Template literals** are literals delimited with backtick (`` ` ``) characters. 
They allow for expressions to be interpolated into strings by using the following syntax: `${}`.
They also allow for multi-line strings.

# Complex data types

## [[JS Objects]]
![[JS Objects]]

## [[JS Arrays]]
![[JS Arrays]]

## [[JS Functions]]
![[JS Functions]]