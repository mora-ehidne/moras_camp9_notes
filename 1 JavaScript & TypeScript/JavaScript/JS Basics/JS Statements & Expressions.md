# Statements

A statement is an instruction, an action, a piece of code that can be executed. For example:

```
printf("Start of the program");
```

A variable binding is a statement.

A statement does not resolve to a value.

The semicolon at the end is a **statement terminator**. Statements which cannot contain other statements are _simple_; those which can contain other statements are _compound_.
Simple statements are eg an `exit` statement, a `return` statement  or a `print` statement.
Compound statements are eg. a `for` statement, a `do while` statement or an `if` statement.

A statement that declares a variable, object, class or function is a **declaration**, eg:
```js
let myVariable;
```
and a statement that declares a variable and assigns it a value is a **definition**, eg:
```js
let myVariable = 2;
```

## Expressions

An **expression** is not an instruction, like a statement is, but simply determines a value, eg:
```js
myVariable = 2 + 6;
mySecondVariable = myVariable + 1;
```

