# Destructuring Arrays:

^e64f95

The **destructuring assignment** syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables.
It is a kind of shorthand for dealing with array items.
The syntax for array destructuring looks like declaring a nameless array with variable names instead of item values. ^7bc780
```js
// example of not using destructuring
const foo = ["one", "two", "three"]; // creating a three-item array

const red = foo[0]; // bind the first item of the array to the variable
const yellow = foo[1]; // bind the second item of the array to the variable
const green = foo[2]; // bind the third item of the array to the variable

console.log(red); // "one"
console.log(yellow); // "two"
console.log(green); // "three"

// example of using destructuring
const foo = ["one", "two", "three"]; // creating a three-item array

const [red, yellow, green] = foo; // bind the first item of the array to the variable red, bind the second item of the array to the variable yellow, bind the third item of the array to the variable green
// note that the array cannot be called, it has no name. 

console.log(red); // "one"
console.log(yellow); // "two"
console.log(green); // "three"
```

Item values are assigned to variables in the order of their indices. 
An array item can be skipped during destructuring by simply writing a comma. 

```js
const foo = ["one", "two", "three"]; // creating a three-item array
const [, second, third] = foo; // binds the value of "two" to second and "three" to third. The first item is skipped.
```

Array destructuring allows to directly store some or all values of items of an array to one or several variables.

Array destructuring can be used inside a for loop:

```js
const entries = [
	['name', 'Alice'],
	['name', 'Mora']
];
for([key, name] of entries){
	console.log(key, name); // logs the values of the first two elements of the nested array for each item of the entries array
}
```

### Rest Operator in Array Destructuring

A rest operator `...` can be used to assign all the remaining items of an array that did not get assigned to the variables. The rest operator makes the variable into an array.

```js
const [a, b, ...c] = [1, 2, 3, 4, 5, 6]; // 1 is assigned to a, 2 is assigned to b, c is an array containing 3 , 4, 5 and 6
```

### Spread Operator in Array Destructuring

The spread operator has the same syntax as the rest operator `...`.
It is used to "unpack" or expand the items of an array into individual items.

```js
const array1 = [1, 2, 3]; // declare a new three-item array
const array2 = [...array1]; // declare a new array with as many items as array1 has and the corresponding values. (deep copy)
const array3 = array1; //creates a pointer to the array array1 (shallow copy)
```

# Destructuring Objects:

^91a7b7

The **destructuring assignment** syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables. The variable names have to match the keys of the properties. The order of the properties makes no difference. 

```js
function myFunction(){
	return {
		firstName: "Mora",
		lastName: "Obradovic",
		age:30
	};
}
const {age, firstName} = myFunction(); // binds the property values from the returned object to the variables with the same name
console.Log(firstName); // logs 'Mora'
```

## Renaming variables in the destructuring assignment

Variable names can be given new names instead of the key names with the colon `:` syntax.

```js
const myObject = {
	age: 30,
	firstName: Mora
};
const {age: myAge, firstName: myName} = myObject;
```

## Destructuring on nested objects

Object destructuring can also be done on nested objects. Note that retrieving the values of properties of nested objects has a different syntax but also simply  gets assigned to a variable.

```js
const person={
	name: "Alice",
	address:{
		street: "123 Main str",
		city: "Sometown"
	}
};
const {name, address:{city}} = person; // assigns the value of "Alice" to the variable name and the value "Sometown" to the variable city

```