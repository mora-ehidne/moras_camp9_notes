# `for of` 

A `for of` loop can be used in Javascript to go through all the items in an array. It can be only used on arrays. Code example:

```js
for (x of myArray){
	console.log(x);
}
```

# `for in`

A `for in` loop can be used in Javascript to go through all the properties of an object. If used on an array, it loops through all the indices of an array. 

```js
// for in loop in an object
for (key in myObject){
console.log(key); // logs keys of an object, eg "firstName"
console.log(myObject[key]); // logs the values stored in properties of an object, eg "Julian"
}
// for in loop in an array
for (index in myArray){
console.log(index); // logs indices of the array, eg 0
console.log(myArray[index]); // logs the values of items in the array, eg "first entry"
}
```