The *AAA* (Arrange-Act-Assert) pattern is what is a industry standard in testing. 

# Vitest

We are using [Vitest](https://vitest.dev/) for testing. 

Vitest can be used without Vite.

Vitest provides `chai` assertions by default and also `Jest` compatible assertions build on top of `chai`

## Vitest setup

installation:
`nom install -D vitest` in the project directory (needs sudo)

The flag `-D` is for **development** , meaning that the package is not shipped with the compiled project, it is simply for the development environment.

running the tests:
`npm run vitest`

Tests are placed in a new folder, typically called `__test__`.
Test files are named with the extension `.test.ts` or `.spec.ts`.

>[!INFO] by default, without a configuration file, vitest searches the project directory for any files with the extensions `.test.ts` or `.spec.ts`.
>
# Writing the test files

## importing the test functions

The test file should import the test functions from `vitest` and all the functions that are to be tested. 

```ts
import { it, expect } from "vitest"; // import the test functions from vitest
import { add } from "../src/math"; // import the function add from math.ts to test it
```

## `describe()`

The `describe()` function can be used to wrap several `it()` blocks.
`describe()` has two parameters:
1.  a string that describes the wrapped `it()` blocks
2.  a callback function in whose body the `it()` blocks are defined

 ```ts
describe("this is a new suite of it() blocks",()=>{
/// it() ...
/// it() ...
/// it() ...
});
```

## `it()` / `test()`

The function for testing is `it()`, also available under the alias `test()`.
`it()` has two parameters:
1.  a string that describes the test
2. a callback function that performs the test

```ts
it("should summarize all number values in an array", () => {
const nums = [1, 2, 3];
const result = add(nums);
expect(result).toBe(6);
});
```


## `expect()`

>[!INFO] There can be several `expect()` function calls in an `it()` block.

The `expect()` function accepts a single parameter whose value is to be tested through an assertion.  

`expect()` creates *assertions*. Assertions are method calls that make the `it()` block pass the test or fail it, depending if the assertion throws an error or not.

`expect()` has to be placed inside an `it()` block.

Assertion methods include:

- `toBe()` /  `to.equal()`
- `toEqual()`
- `toBeDefined()`
- `toBeUndefined()`
- `toBeTruthy()`
- `toBeFalsy()`
- `toHaveLength()`
- `toHaveProperty()`
- `toThrowError()` /  `toThrow()`

>[!TIP] `expect()` does not test types, only the values. To test a type, `expectTypeOf()` or `assertType()`.

### `toBe()` /  `to.equal()`

Compares the value of its parameter to the value of parameter from the `expect()` function. Passes the test if the compared values are primitives with the same value or if they are objects  that share the same reference.

```ts
expect(x).toBe(5); // passes the test if the value of x is 5
```

### `toEqual()`

Similiar to `toBe()`, and has the same functionality if the arguments are primitives.
If the arguments are objects, `toEqual()` will compare the structure of the objects, passing the test if their structures match.

### `toThrowError()` /  `toThrow()`


### `not`

`not` negates the assertion chained after it.

```ts
expect(result).not.toBe(6); // passes the test if result is anything except 6
```