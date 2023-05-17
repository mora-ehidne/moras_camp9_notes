# tiny invariant

Homepage: https://www.npmjs.com/package/tiny-invariant

Invariant acts as a type guard. 
It asserts that a binding is not falsy and returns a error string if a given binding is undefined.

# Setup

```bash
npm i tiny-invariant
```

in a `.tsx` component:

```tsx
invariant(data, "Data must not be undefined");
// from here, if data is undefined, the error string will be thrown
// TypeScript considers data as not possibly undefined after this line
```