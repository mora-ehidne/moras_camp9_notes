Arrays belong to ==complex data types== in Javascript. They are a subtype of **Objects**,

Arrays in Javascript can contain elements of any type.

Code example:
```js
const myArray = [
	"a string",
	false,
	5
]; // array object declaration

```

Accessing array elements can be done by accessing the index position of an element in an array with square brackets `[]`.
Code example:
```js
myArray[1] = 5; //the elements are changeable even if the array itself has been declared as a constant```
myArray[0]; // The first element of an array is always at the index of 0.
myArray[myArray.length - 1]; // The last element of an array is always at the index of array length - 1.
```

```

If an array contains other arrays, it is defined as such:
```js
const coordinates = [
	["lat", 214356],
	["lng", 835245]
]; //  array object declaration with two more arrays contained within it
console.log(coordinates[1][1]); // logs the first element of the first element, in this case 835245
```

Arrays in Javascript are resizable - their length can be changed even after their declaration.

Arrays have the `length` property which has an initial value of 0.

Some HTML DOM Objects are array-like. An array can be created from such objects by using the static method `Array.from()`.

# Multidimensional Arrays

In Javascript, there are no multidimensional arrays. The functionality of a multidimensional array can be done by nesting arrays (array of arrays). In effect, a two-dimensional array is an array with one level of nesting, a three-dimensional one would be with two levels of nesting etc. As all nested arrays can have different lengths, such an array would be a *jagged array*.

```js
const twoDimensionalArray = [
[0,1,2,3],
[5,6,89,89],
["xoxo", "iiii", 5, 6]
]; /// declaration of a  
```

# Array methods

Arrays have many useful methods, such as:


## `.join()` `.join(joiningString)`
Creates a string from an array. The parameter is used as a string insert between each element. If no parameter is included, a default string insert of `,` is used. Code example:
```js
const fruits = ["Apple", "Banana"];
const fruitsString = fruits.join(", "); // value is "Apple, Banana"
const fruitsString = fruits.join(""); // value is "AppleBanana"
const fruitsString = fruits.join(); // value is "Apple,Banana"
```


## `.indexOf(value)` `.indexOf(value, fromIndex)`
Returns the index of the first element whose value is equal to the value given as the parameter. Code example: 
```js
const fruits = ["Apple", "Banana"];
console.log(fruits.indexOf("Banana")); // logs 1
```
if `.indexOf()` finds no such element, it returns `-1`. Thus, a call of `.indexOf()`  that returns a `-1` is the same as a call of `.includes()` which returns `false`.

`.indexOf()` uses *strict equality* in its search.

##### `fromIndex` parameter

The second, optional, parameter defines at which index to start the search.
* if it is 0, it simply starts from the beginning, as if the parameter were omitted.
* if it is equal to or larger than the length of the array, the method simply returns a -1 and does no search.
* a negative value sets the index counted back from the end of the array and then starts the search normally, front to end, at that index 


## `.includes(value)` `.includes(value, fromIndex)`
Returns `true` if at least one element is equal to the value passed as the parameter. If no such element if found, it returns `false`. Code example: 
```js
const fruits = ["Apple", "Banana"];
fruits.includes("Banana"); // true
fruits.includes("Cherry"); // false
```

`.includes()` uses *strict equality* in its search.

##### `fromIndex` parameter
The second, optional, parameter defines at which index to start the search. Behaves exactly like in the `.indexOf()` method.

## `.sort()`

The array `.sort()` method sorts the array based on the comparison function passed as an argument. If no comparison function is passed, the array elements are sorted as their string values from smallest to largest (alphabetically).

The comparison function is then called on each array item. It has to have two parameters, *a* and *b*.  The *b* parameter refers to the current item, and the *a* parameter to the item before it. The function is expected to return a 0, a positive value or a negative value. A positive value means the current item (*b*) gets sorted to the front of the array, a negative sorts it to the back, and a 0 keeps the number in place.

A common use would be:

```js
let numbers = [9, 3, 4, 5];
function compare(a, b){
	let comparison;
	comparison = a - b; // sort the array from smallest to largest, ascending
	comparison = b - a; // sort the array from largest to smallest, descending
}
numbers.sort(compare);
```

A shortened version would be employing the arrow function:

```js
numbers.sort((a,b) => a - b); // sort the array from smallest to largest
```

## calling array methods on non-array objects

On on-array objects, eg. on a plain object, the `.includes()` method can be called from the `Array.prototype` object. Code example:

```js
const arrayLike = {
  length: 3,
  0: 2,
  1: 3,
  2: 4,
};
console.log(Array.prototype.includes.call(arrayLike, 2));
// true
```

Other array methods can be also used on non-array objects, such as: `.join()`

# [[Destructuring Assignment#Destructuring Arrays:|Destructuring Arrays]]

