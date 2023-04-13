In JavaScript, **Truthy** values are values that are considered `true` when coerced/converted into a `boolean` data type.  **falsy** values are the opposite,they are values that are considered `false` when coerced/converted into a `boolean` data type. 

Operators that test expressions for being `true` or `false` are:
* [[JS Comparison Operators]]
* [[JS Logical Operators#Conditional (ternary) operator ` ? : `|Conditional (ternary) operator ? : ]]
* [[JS Logical Operators#Logical OR <code> </code> operator|Logical OR operator ||]]
* [[JS Logical Operators#Logical OR assignment operator <code> =</code>|Logical OR assignment operator ||=]]

# Falsy Values

The only values that are *falsy* are 
* `false`
* `0`
* `-0`
* `0n`
* `""`
* `null`
* `undefined`
* `NaN`

# Truthy values

All other values are considered *truthy*.

# Nullish values

Nullish values are a subset of *falsy* values. Only `undefined` and `null` are considered *nullish values*.

Operators that test expressions for being *nullish*  are:
* [[JS Logical Operators#optional chaining `?.` operator|Optional chaining operator `?.` ]]
* [[JS Logical Operators#Nullish coalescing operator `??`|Nullish coalescing operator `??`]]
* [[JS Logical Operators#Nullish coalescing assignment operator`??=`|Nullish coalescing assignment operator`??=`]]