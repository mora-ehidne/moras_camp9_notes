TypeScript is a superset of Javascript, which means that it is a kind of additional set of rules for JavaScript.

>[!INFO] A comment of `//@ts-ignore` ignores TypeScript functionality and errors on the next line.

# TypeScript Initialization

To use TypeScript, we will first need to initialize it in the project folder. 
The console is used for all the instructions.

>[!TIP] If the project is initialized using [[Tailwind CSS#^ee8338|Tailwind]], no further TypeScript initialization or compiling is necessary.

`tsc --init` - initializes TypeScript in the current folder

The TypeScript initialization creates a `tsconfig.json` file in the directory. 

To use the TypeScript code, it must be first compiled into JavaScript. The JavaScript file must be connected to the HTML as usual, through the `<script>` tag.

`tsc --build` - compiles the TypeScript into the JavaScript file
`tsc --watch` - compiles the TypeScript into the JavaScript file on each change

# Static Typing

## Type Inference

Type inference is done implicitly, that is to say automatically, by TypeScript. It is a process through which TypeScript guesses the data type expected based on the values assigned to a variable or used by a function.

## Type Annotation

Type annotation is done manually, by the programmer. The syntax for type annotation is a colon `:` after the name of the variable or after the parameters declaration in a function declaration.

A type annotation can also accept several data types, separated with a pipe symbol `|`. This is called a *union type*.

```ts
let myString: string; // annotation to string data type
let mySecondString: string = "a test string."; // annotation to string, binding a value
function myFunction(a:number, b:string="hello"):number{} // annotation of the first parameter to the type Number, second parameter to type String, and the return value to type Number
let myNumberOrBoolean: number | boolean; // annotation to accept either Number type or String type - also called union types
let helloOrBye: "Hello!" | "Goodbye :'("; // annotation to accept either the literal "Hello!" or the literal "Goodbye :'("
let myArray: number[] =[]; // annotation to an array of numbers
let myArray: (number | string)[] =[]; // annotation to an array of either numbers or strings
```

>[!TIP] Literal types can be used as type annotation, making the variable only accept the specified literals.

### Type Annotation in destructuring patterns

The colon `:` syntax cannot be used in a [[Destructuring Assignment|destructuring pattern]] for type annotation, as that syntax already has another functionality ([[Destructuring Assignment#Renaming variables in the destructuring assignment|renaming variables]]).

# [[TS Datatypes|Data Types]]