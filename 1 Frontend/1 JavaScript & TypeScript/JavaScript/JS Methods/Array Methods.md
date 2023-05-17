## `push()`

> changes the array

Adds a new item to the end of the array, increasing it's length by 1. (changes the array)
The method accepts any number of arguments, so it can also be used to add more than a single item to the end of the array.

Accepts all data types. To push all items of a different array into an array, the spread `...` operator is used.

> Returns the new array length.

## `pop()`

> changes the array

Removes the last item of an array.

> Returns the item that got removed.

## `unshift()`

> changes the array

Similiar to `push()`, but adds the elements to the beginning of the array instead.

> Returns the new array length.

## `shift()`
> changes the array

Similiar to `pop()`, but removes the elements from the beginning of the array instead.

> Returns the item that got removed.

## `splice()`
> changes the array

**The first parameter** is the starting index from which all items until the array end get removed. Negative values count backwards from the end of the array.

**The second parameter** is the number of items to be deleted. (optional)

**The third parameter** is the item to be added to the array in place of the removed items. (optional). The third parameter can be repeated as many times as wanted to add several items in place of the removed items.

> Returns the item(s) that got removed.

## `slice()`
> does not change the array, returns a new array

**The first parameter** is the starting index from which items will be returned. 
**The second parameter** is the end position of items until which they will be returned. (optional; if not included, returns items until the end of the array)

## `concat()`
> does not change the array, returns a new array

Returns the array with all the items of the array passed as an argument added to its end.

## `indexOf()`, `lastIndexOf()`
> does not change the array, returns an index

Searches for the first appearance of an item whose value matches the first argument.
**The first parameter** is the value whose appearance we are searching for. 
**The second parameter** is the index at which the search starts. 

`indexOf()` searches *forwards* from the starting index until the end of the array.
`lastIndexOf()` searches *backwards* from the starting index until the beginning of the array.

On failing to find a matching item returns `-1`.

# Methods with callback parameters

## `find()`
> does not change the array, returns an item value

Searches for the first appearance of an item whose iteration makes the callback comparison function returns a truthy value.
The comparison function takes as an argument the array item being compared at the moment.

If no such item is found, returns `undefined`.

```js
const level = [4, 5, 6, 10, 11, 15, 20];
const itemFound = level.find( item => item > 10);
console.log(itemFound); // returns 11, being the first occurance of an item larger than 10
```

## `filter()`
> does not change the array, returns a new array

Searches for all items whose iterations make the callback comparison function returns a truthy value.
The comparison function takes as an argument the array item being compared at the moment.

```js
const levelToFilter = [4, 5, 6, 10, 11, 15, 20];
const itemsFound = levelToFilter.filter( item => item > 10);
console.log(itemsFound); // returns 11, 15, 20
```



## `includes()`
> does not change the array, returns a boolean value

Returns `true` if there is any array item matching the passed argument value, returns `false` if no such item is found.

```js
const level = [4, 5, 6, 10, 11, 15, 20];
const itemFound = level.includes(6); // returns true
const itemFound = level.includes(1); // returns false
```

## `forEach()`
> does not change the array, returns nothing (void)

Calls the callback function as many times as there are items in an array. Passes the current item to the callback function as an argument.

```js
const level = [4, 5, 6];
const level2 = [];
level.forEach(item => level2.push(++item)); // level2 is now [5, 6, 7]
```

>[!TIP] `forEach()` acts similiarly to a `for of` loop.

# `map()`
> does not change the array, returns a new array

Creates a new array with as many items as the caller array, replacing the values of the items with the return value of the callback function.

```js
const level = [4, 5, 6];
const level2 = [];
level2 = level1.map(item => item + 1); // level2 is now [5, 6, 7]
```

>[!TIP] `map()` acts similiarly to a `for of` loop or a `forEach()` method that is used solely to return a new array.









