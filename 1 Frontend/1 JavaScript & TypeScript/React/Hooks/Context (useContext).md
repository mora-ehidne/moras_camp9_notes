# Context

Docs: https://react.dev/learn/passing-data-deeply-with-context

The `useState` React hook is only accessable in a React component and its descendents, to which the state can be passed down via `props`. This can become cumbersome when the props have to be passed several components down (_prop drilling_).

In order to avoid prop drilling, Context can be used to create and access global states.

Context has a `Provider` and a `Consumer`.

## `createContext()`

docs: https://react.dev/reference/react/createContext

To use context, first a context must be set up. The context can be set up in its own `.tsx` file, using the `createContext()` function. 

```tsx
const myContext = createContext();
```

The `Provider` defines which parts of the context can be used by a `Consumer`. 

In the `MyContextProvider.tsx`
```tsx
return
```

In order for a `Consumer` component to access the context, it (or one of its ancestors) must be wrapped in the context Provider component.

in `main.tsx`:
```tsx

```

## `useContext()`

docs: https://react.dev/reference/react/useContext

Finally, in order to access the context, the `useContext` hook can be used by any component that is wrapped or has any ancestors that are wrapped in the Context Provider component.

The `useContext()` hook must be passed the name of the context to be used (which is the name of the binding of the `createContext` hook).
`useContext()` returns the `value` object of the Context Provider (defined as an attribute of the Provider).

In a component:
```tsx
import { useContext } from 'react';  

function MyComponent() {  
const myContextValue = useContext(MyContext);  
// ...eg. myContextValue.changeColor(); etc
}
```