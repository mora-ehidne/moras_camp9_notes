Objects are a kind of complex data types in Javascript. It is a collection of ==properties==, which can be of various data types, including complex ones such as other objects or arrays, but also functions. Functions declared within objects are called ==methods==. ^a72551

Objects created with initializers are called _plain objects_, because they are instances of `Object`, but not any other object type, such as [[JS Arrays]].


```js
const user = {
	firstName: "Julian",
	lastName: "Vogel",
	age: 31
}; // Object initializer aka object literal

const obj = {
  property1: value1, // property name may be an identifier
  2: value2, // or a number
  "property n": value3, // or a string
};

console.log(user.firstName);
```
the name of the property inside an object is called a ==key==.
each line of declaration is called a ==key:value pair==

the **key:value** pairs are called ==properties==.

New properties can be added even after the object declaration. Code Example:
```js
const user = {
firstName: "Julian",
lastName: "Vogel"
}; // object initializer
user.hobbies = ["sports", "board games"]; // the property hobbies is created for the object user and assigned an array
```

Objects can be one-of-a-kind, an instance of an object type or an instance of a class.

# Property accessors

**Property accessors** provide access to an object's properties. 
There are two different notations: the *dot notation* and the *bracket notation*.

Dot notation is: `object.propertyName`.
Bracket notation is: `object[propertyName]`.

Both notations can also be used to call methods:
```js
document.createElement("id"); // dot notation
document[createElement]("id"); // bracket notation
```

# Pointers/References

If an object is assigned to a variable, not the entire object is assigned as a value but a ==pointer== towards that object is bound to the variable. Code example:
```js
let myObject = {
	a = 5,
	b = "a string."
}; // declaration of an object
let a = myObject; // a pointer to the object myObject is assigned to the variable a
a.b = "a different string."; // the property b is changed for the object myObject, in effect a.b and myObject.b refer to the same thing
```

The properties of an object, as long as they are primitive data types, are not assigned pointers to, their value is simply bound to the new variable. Code example:
```js
let myObject = {
	a = 5,
	b = "a string."
}; // declaration of an object
let a = myObject.a; // variable a now holds the value of 5
a = 20; // the property a is not changed for the object myObject, the variable a simply has its value changed to 20
```

# Methods

A method is a property of an object that is a function. Methods are defined the way normal functions are defined, except that they have to be assigned as the property of an object. Code example:

```js
const myObj = {
  myMethod: function (params) {
    // function body
  }, //one way of claring a method
  myOtherMethod(params) {
    // function body
  }, //second way of claring a method
};
myObj.myMethod(params); // method call
```

## Getters and setters

# Comparing objects

In JavaScript, objects are a **reference type**. Two distinct objects are never equal, even if they have the same properties. Only comparing the same object reference with itself returns true.
Code example:
```js
// Two variables, two distinct objects with the same properties
const fruit = { name: "apple" };
const fruitbear = { name: "apple" };

fruit == fruitbear; // return false
fruit === fruitbear; // return false
fruit == fruit; // return true
```

# [[Destructuring Assignment#Destructuring Objects:|Destructuring Objects]]

