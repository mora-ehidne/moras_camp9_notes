# JavaScript Functions

In JavaScript, functions can be treated as complex value types, meaning that they can be assigned to variables. Function calls can then be made by using the variable name followed by parentheses `()`.

# The call operator

The parentheses `()` are called the *call operator*, and the code contained within the curly braces `{}` is called the *function body*.

# Parameters and Arguments

The named variables declared in the parentheses in the function declaration are called ==parameters==. 
The values expressions passed to the function at the function call are called ==arguments==. 

```js
function myFunction(param1, param2){
//function body
} // param1 and param2 are parameters
myFunction(5, "name"); // 5 and "name" are arguments
```

>[!TIP]
>If more arguments are passed than the function has parameters, the **excess arguments** don’t get assigned to any parameters. They can, however, be accessed through the [[JS Functions#Implicitly passed parameters|implicitly passed parameters]]
>
> If less arguments are passed than the function has parameters, the excess parameters are set to a value of `undefined`.

## Implicitly passed parameters

In Javascript, some parameters get implicitly passed, without explicitly passing them during a function call.

### `arguments` 
The `arguments` parameter always gets implicitly passed with each function call. It is an array-like object, with a `length` property, containing all the arguments passed to the function as its items. Its items include the implicitly passed and the excess arguments, but exclude itself, that is, the `arguments` argument.
```js
function myFunction(par1, par2, par3){
  console.log(arguments.length); // Logs the number of all arguments passed
  console.log(arguments[2]); // Logs the 3th argument 
}
```

#### `arguments.length`

The `.length` property of the `arguments` parameter indicates the number of arguments passed in the function call.

### `this`
The `this` parameter always gets implicitly passed with each function call. The `this` parameter refers to the object that called (invoked) the function. It is also known as *function context*.
```js
function myFunc() { 
     return this; // returns the calling object
}
myFunc(); // returns the window object
```

## Rest Parameter

A **rest parameter** is a special parameter that can be declared in the function declaration. It is an `Array` which contains all the **excess arguments**.
It is declared with a special syntax of `...` (an ellipsis) before the parameter name. The rest parameter must also be the last parameter declared in the function declaration.
```js
function myFunction(...restParam){
console.log(restParam.length); // logs the number of arguments passed
console.log(restParam[3]); // logs the 4th argument
}
myFunction(1,2,3,4,5); // function call with excess arguments
// log would first be the number of arguments passed: 
// 5
// then it would log the value of the 4th argument
// 4
```

>[!TIP] The rest parameter contains **only the excess arguments**, while the `arguments` parameter contains **all the arguments**. Also, the rest parameter is a **real array**, while the `arguments` parameter is an array-like object.

## Default parameters

**Default function parameter** is a parameter that is assigned the specified value if no argument for it (or `undefined` or `null`) is passed.

```js
function myFunction(param1, param2="default string", param3){
} // if no second argument is passed, param2 has the value of "default string". The second and third parameters do not have to be passed in a function call.

```

All parameters after the first default parameter do not count towards the `.length` property of the function.

### Logical OR `||` operator as a default value assignment

The logical or `||` operator can be used as a default value assignment. As the logical or tests the the left side operand if it is falsy and then proceeds to the right side, it can be used to assign the right side operand if the left side is a [[Truthy, Falsy, Nullish#Falsy Values|falsy]] value, such as `0`, `false`, `undefined`, `null` etc.

```js
function foo(a, b){
	const c = (a || 0) + (b || 0);
	return c;
} // the parameters a and b now effectively have a default value, as they are first tested for undefined or null and then given the value of zero if that is the case
//or
function foo(a, b){
	this.a = a || 0; // a is tested for falsy, if it is, a is assigned 0
	b = b || 0; // b is tested for falsy, if it is, b is assigned 0
	return a + b; // now we can be sure that the value returned is a number
} 
```

#### Logical OR assignment operator `||=`

The logical OR assignment operator`||=` is a variant of the logical or `||` operator that is used only for assigning values if the left side operand is [[Truthy, Falsy, Nullish#Falsy Values|falsy]].

```js
function foo(a, b){
	a = a || 0; // a receives a default value with logical OR operator
	b ||= 0; // b receives a default value with logical OR assignment operator
	return a + b; // now we can be sure that the value returned is a number
} 
```

### Nullish coalescing operator `??`

An alternative to the logical or `||` operator is the *nullish coalescing operator* `??`.
Its difference to the `||` operator lies in the functionality of only accepting the right-side operand value if the left side operand is equal to `null` or `undefined` ([[Truthy, Falsy, Nullish#Nullish values|nullish]]), not [[Truthy, Falsy, Nullish#Falsy Values|falsy]]. This is useful for situations in which we would like to accept some falsy values such as `0` and empty string `""`; 

```js
function foo(a, b){
	this.a = a ?? 0; // a is tested for nullish, if it is, a is assigned 0
	a = a ?? 0; // alternative syntax 
	b ?? (b = 0); // alternative syntax for the parameter b
	return a + b; // now we can be sure that the value returned is a number
} // if the arguments passed are value of 0, that value gets accepted. Only if null or undefined are passed, the value of 5 is used
```

>[!TIP] The `??` operator can be considered a stricter version of the `||` operator.

#### Nullish coalescing assignment operator`??=`

The **nullish coalescing assignment ** operator, is also known as the **logical nullish assignment** operator. It is a variant of the nullish coalescing operator `??` which can only be used for assigning values if the left side operand is *nullish*.

```js
function foo(a, b){
	a = a ?? 0; // a is tested for nullish, if it is, a is assigned 0
	b ??= 0; // b is tested for nullish, if it is, a is assigned 0
	return a + b; // now we can be sure that the value returned is a number
} // if the arguments passed are value of 0, that value gets accepted. Only if null or undefined are passed, the value of 5 is used
```

# *impure* Functions

An *impure* function is one that is using global variables in a local scope. 
*Pure* functions use only internal values and those that are passed in the parameters.

![|600](JS_pure_and_impure_functions.png)

# Returning Arrays and Objects

A function can return any data type, including complex data types.

## Returning Objects

A function can return an Object.

```js
function myFunction(){
	return {
		firstname: "Mora",
		lastName: "Obradovic",
		age:30
	}
}
const myObject = myFunction(); 
```

### Destructuring Objects:

The **destructuring assignment** syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables.

```js
function myFunction(){
	return {
		firstName: "Mora",
		lastName: "Obradovic",
		age:30
	}
}
const {age, firstName} = myFunction(); // binds the key values from the returned object to the properties with the same name
console.Log(firstName); // logs 'Mora'
```

## Returning Arrays

A function can return an Array.

```js
function myFunction(){
	return [5, 28, "a simple string", false];
	}
const myArray = myFunction();
```

### Destructuring Arrays:

The **destructuring assignment** syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables.

```js
function myFunction(){		
	return [5, 28, "a simple string", false];
	}
const [firstNumber, secondNumber, myString, myBool] = myFunction(); // binds the key values from the returned object to the properties with the same name
console.Log(myBool); // logs 'false'
```

# `Function.length`

The `.length` property of the function object indicates the number of arguments expected by the function. This number excludes the rest parameter and any parameters after the first parameter with a default value.

```js
function func1() {} // func1.length = 0;
function func2(a, b) {} // func1.length = 2;

func2(8, 5, 8); // arguments.length = 3, func1.length = 2;
func2(1); // arguments.length = 1, func1.length = 2;
func2(); // arguments.length = 0, func1.length = 2;
```

>[!TIP] `Function.length` is different than [[JS Functions#`arguments.length|arguments.length]], as it indicates the number of **expected arguments** while `arguments.length` indicates the number of arguments **actually passed **in a function call.

# Alternative function declaration syntax

## Anonymous Functions

An anonymous function is one that is declared without a function name. In order to be able to call the function later in the code, it must be assigned to a variable. 

```js
const squareTwo = function(num){
	return num*num;
	};
squareTwo(5); // returns 25
```

### Immediately Invoked Function Expression (IIFE)

If the function should just be called a single time, it can be called directly after its declaration.
To achieve this, the function must be declared as an *anonymous function*, with the entire declaration placed inside parentheses `()` and the function call parentheses `()` placed immediatly afterwards.
```js
(function() {
	console.log('I get invoked immediately! And cannot be invoked ever again!'); })(); // immediately invoked function with no parameters
(function(name) {
	console.log('I get invoked immediately, ${name}! And cannot be invoked ever again!');})("Mora"); // immediately invoked function with a single parameter
```

An anonymous function can also be immediately invoked after being assigned to a variable. It can then be invoked again through the variable.

```js
const myFunction = (function() {
	console.log('I get invoked immediately! But I can be invoked again through the variable'); })(); // logs immediately
myFunction(); //logs again
```

## Arrow Functions

Arrow functions are always *anonymous*.

```js
const squareTwo = num => {	return num * num;	} // parenthesis around the parameter are unnecesssary when only a single parameter is declared
const multiplyTwo = (num1, num2) => num1 * num2 // the curly braces and the `return` are not necessary if the only line of code in the function body is the return statement	
const squareTwo = num => num * num; // neither parentheses nor curly braces and the return are necessary
const logSomething  = () => console.log("Something"); // the parentheses are necessary if there are no parameters
```


# Callback functions (functions as arguments)

^867672

A function call is treated as an expression with a value equal to the its return value. Because of that, there is a difference between passing a function as an argument that should be called within a function (*callback*) and between passing a function as an argument that is simply a value  that function returns.

Callback functions are therefore always written without the parentheses. 

```js
function add(a, b){
	return a+b;
}
function result(a, b, func){
	return "The result is: " + func(a, b);
}
console.log(add(5,6)); // logs 11, the function is not a callback function, as it is directly invoked and simply its value is passed as an argument
console.log(result(5, 6, add)) // logs "The result is: 11", the add function is passed as a callback function to the results function which is directly invoked and its return value is passed to the console.log method
```

Passing functions as arguments works very good with anonymous functions:
```js
function result(a, b, callback){
	return "The result is: " + callback(a, b);
}
console.log(result(10, 2, function (a, b) {a + b})); // an anonymous function is passed that returns the sum of a+b
```

And even better, with arrow functions.

```js
function result(a, b, callback){
	return "The result is: " + callback(a, b);
}
console.log(result(10, 2, (a, b) => a + b)); // an arrow function is passed that returns the sum of a+b. This syntax is much shorter and clearer than that of a standard anonymous function. 
```

# Returning functions from a function

As a function can return any value, it can also return a function, as functions are a data type. 

A combination of returning a function from a function and an arrow function can be used to effectively pass arguments to a callback function. In this case, we create an anonymous function that simply has in its body a call to the function we initially wanted to callback.

```js
function result(callback) {
return "The result is: " + callback(); 
} // invokes the callback function, which in this case returns a call to the function add with the arguments 5 and 5, which returns 10, with this function finally returning "The result is: 10" 
// same as return "The result is: " + add(5,5); 
function add(a, b) {
return a + b;
}
console.log(result( () => add(5, 5))); // passes a new anonymous arrow function as callback, which calls the add function with the arguments 5 and 5 and returns its value
```