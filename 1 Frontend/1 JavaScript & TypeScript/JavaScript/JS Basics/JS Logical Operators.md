# Operators that test for [[Truthy, Falsy, Nullish|truthiness]]

## Conditional (ternary) operator ` ? : `

The **conditional (ternary) operator** is the only JavaScript operator that takes three operands.
Its syntax is as follows: `condition ? doIfTrue : doIfFalse`. 
>[!TIP] A ternary operator is essentially a shorter alternative to a `if...else` statement.

```js
if(a==true){
	return "sucess!";
}
else {
return "fail!";
}
a==true ? return "sucess!" : return "fail!"; // exact same functionality as the if..else statement
```

The ternary operator can be "chained", mimicing the functionality of an  `if … else if … else if … else` chain:

```js
if(a==true){
	return "A sucess!";
}
else if (b==true){
	return "B sucess!";
}
else if (c==true){
	return "C sucess!";
}
else {
	return "fail!";
}
// exact same functionality with a ternary operator:
a == true ? return "A sucess!"
: b==true ? return "B sucess!"
: c==true ? return "C sucess!"
: return "fail!";
```

## Logical OR <code>||</code> operator

The logical OR (logical disjunction) operator tests the the left side operand for truthiness. 
If the left side operand converts to `false`, it discards it and proceeds to the right side operand.
If the left side operand converts to `true`, the right side operand never gets evaluated.

>[!TIP] In an `if` statement, the logical OR operator makes the condition true if **either of the operators are truthy**.

```js
if(a===b || a===c){
	// the left side operand is first evaluated. 
	// If it is true, the if condition is true and the right side operator does not get evaluated.
	// If it is not true, it gets discarded and the right side operator is evaluated. If the right side operator is true, the if condition is true, otherwise it is false.
}
```

### Short-circuit evaluation

The logical OR operator can be used for short-circuiting.

The logical OR operator can be used as a shorthand for an `if not do` statement. 

```js
if(a!=="myString"){
 a+=" and myString";
}
//is the same as
a===="myString" || a+=" and myString" ;
```

One such use case would be a default value assignment.  As the left hand operand is discarded if it is `falsy`, the right hand operand can hold a default value if that case occurs.

```js
function foo(a, b){
	const c = (a || 5) + (b || 5);
	return c;
} // the parameters a and b now effectively have a default value, as they are first tested for falsiness and then given the value of zero if that is the case
//or
function foo(a, b){
	this.a = a || 0; // a is tested for falsy, if it is, a is assigned 10
	b = b || 0; // b is tested for falsy, if it is, b is assigned 10
	return a + b; // now we can be sure that the value returned is a number
} 
```

### Logical OR assignment operator <code>||=</code>

The logical OR assignment operator`||=` is a variant of the logical or `||` operator that is used only for assigning values if the left side operand is [[Truthy, Falsy, Nullish##Falsy Values|falsy]].

```js
function foo(a, b){
	a = a || 5; // a receives a default value with logical OR operator
	b ||= 5; // b receives a default value with logical OR assignment operator
	return a + b; // now we can be sure that the value returned is a number
} 
```


## Logical AND <code>&&</code> operator

The logical AND (logical conjunction) operator tests the the left side operand for truthiness. 
If the left side operand converts to `true`, it proceeds to the right side operand.
If the left side operand converts to `false`, the right side operand never gets evaluated.

>[!TIP] In an `if` statement, the logical AND operator makes the condition true only if **both of the operators are truthy**.

```js
if(a===b && a===c){
	// the left side operand is first evaluated. 
	// If it is not true, the entire if condition is false
	// If it is true, the right side operator gets evaluated. If the right side operator is true, the entire if condition is true. If the right side operator is false, the entire if condition is false.
}
```

>[!TIP] The AND operator has a higher precedence than the OR operator, meaning the `&&` operator is executed before the `||` operator.

### Short-circuit evaluation

The logical AND operator can be also used for short-circuiting.

The logical AND operator can be used as a shorthand for an `if do` statement. Such a use is like a shortened version of a [[JS Logical Operators#Conditional (ternary) operator ` ? : `| ternary operator ? :]], in which there is no need for an `else` (`:`) statement.

```js
if(a=="myString"){
 a+="!";
}
// is the same as
a===="myString" && a+="!" ;

// is the same as
a===="myString" ? a+="!" : null ;
```

# Operators that test for [[Truthy, Falsy, Nullish#Nullish values|nullish]]

## optional chaining `?.` operator

The questionmark-dot syntax `?.` can be used instead of the dot syntax `.` to access an object property.  It first tests if the object is [[Truthy, Falsy, Nullish##Nullish values|nullish]], and if it is not, it attempts to access the property. If the object is nullish, the property access is not attempted (it gets short-circuited).

## Nullish coalescing operator `??`

An alternative to the logical or `||` operator is the *nullish coalescing operator* `??`.
Its difference to the `||` operator lies in the functionality of only accepting the right-side operand value if the left side operand is equal to `null` or `undefined` ([[Truthy, Falsy, Nullish##Nullish values|nullish]]), not [[Truthy, Falsy, Nullish##Falsy Values|falsy]]. This is useful for situations in which we would like to accept some falsy values such as `0` and empty string `""`; 

```js
function foo(a, b){
	this.a = a ?? 0; // a is tested for nullish, if it is, a is assigned 0
	a = a ?? 0; // alternative syntax 
	b ?? (b = 0); // alternative syntax for the parameter b
	return a + b; // now we can be sure that the value returned is a number
} // if the arguments passed are value of 0, that value gets accepted. Only if null or undefined are passed, the value of 5 is used
```

>[!TIP] The `??` operator can be considered a stricter version of the `||` operator.

## Nullish coalescing assignment operator`??=`

The **nullish coalescing assignment ** operator, is also known as the **logical nullish assignment** operator. It is a variant of the nullish coalescing operator `??` which can only be used for assigning values if the left side operand is *nullish*.

```js
function foo(a, b){
	a = a ?? 0; // a is tested for nullish, if it is, a is assigned 0
	b ??= 0; // b is tested for nullish, if it is, a is assigned 0
	return a + b; // now we can be sure that the value returned is a number
} // if the arguments passed are value of 0, that value gets accepted. Only if null or undefined are passed, the value of 5 is used
