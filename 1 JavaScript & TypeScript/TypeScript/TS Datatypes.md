# Advanced object types - Type Aliases, Interfaces and Classes

Type aliases, interfaces and classes act as  blueprints on which objects can be based. All the *obligatory* (non-[[TS Basics#Optional properties|optional]]) properties and methods defined within a type alias have to be included in an object which is of that type.

>[!TIP] Names of advanced object types are written in [[Naming conventions (cases)#Pascal case (PascalCase)|PascalCase]], unlike variable names, which are written in [[Naming conventions (cases)#Camel case (camelCase)|camelCase]]

## Type Alias

A *type alias* is essentially a blueprint for an object or a variable. 
For **primitive type aliases**, a variable annoted as a the type alias can only hold the values/data types defined in the type alias.
For **object type aliases**, all the properties and methods defined within a type alias have to be included in an object which is annoted as that type, that is, based on that type alias. 

```ts
// primitive type alias, accepts three predefined string values
type Gender = "none" | "other" | "binary";
// object type alias
type Person = {
  name: string;
  age: number;
  gender: Gender; // annotes the property as a primitive type alias Gender 
};
// annotes the object person as the data type Person
let person: Person = {
	name:"Eric J. Cerda",
	age:33,
	gender: "none" // assigns one of the three allowed string values
	};
```

>[!WARNING] Note that the syntax for declaring properties and methods in type aliases and interfaces requires a semicolon `;` after each declaration, instead of the typical comma `,` in objects and arrays.

### Optional properties

All properties and methods defined in interfaces and type aliases are *oblligatory* in objects which are of their type. To declare a property as optional, a question mark `?` has to be added to the end of the property name.

if an optional property does not get defined in an object, it counts as having a value of `undefined`.

```ts
type SquareConfig = {
color: string;
width?: number;
}
const myConfig : SquareConfig{
color: "blue";
}
```

### Read-only properties

Properties can also be read only, meaning that they cannot be directly modified after it has been declared (like a `const` used on a variable). 
They are declared with the word `readonly` before the property name.

```ts
interface SquareConfig {
readonly color: string;
width: number;
}
let myConfig : SquareConfig = {
color: "blue"; 
width: 20;
}
myConfig.width = 100;
myConfig.color = "green"; // throws an error, as color is read-only
```


## Interfaces

An `interface` is very similiar to a type alias, except that it can take methods and properties of other interfaces with the `extends` keyword. 

>[!TIP] Interfaces care based **only** on the `object` data type, unlike type aliases, which can be based on any data type (including primitive ones)

```js
interface Person {
  name: string;
  age: number;  
  sayHello: () => console.log("Hi!");
};
let person: Person = {
	name:"Eric J. Cerda"
	};
```

>[!WARNING] interface definitions do not require the equality operator `=` before the opening curly bracket `{`, unlike type aliases and objects.

## Extending interfaces

An interface or a class can *extend* another interface, meaning it can have all the properties of another interface. It can then have its own, additional properties on top of it.
This is done using the `extends` keyword for interfaces and `implements` for classes.

>[!TIP] An interface or a class can extend any number of interfaces.
 
```ts
interface Animal { 
name: string; 
age: number; 
} 
interface Dog extends Animal { 
breed: string; 
}
let myPuppy:Dog={
name: "Doggo",
age: 12,
breed: "mongrel"
}
```