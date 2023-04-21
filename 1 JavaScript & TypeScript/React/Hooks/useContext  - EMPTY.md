# useContext hook

The `useContext` hook can be used to access global states.

To use it, first a context must be set up. The context can be set up in its own `.tsx` file. 

```tsx
```

In order for components to access the context, their parent component should be wrapped in the context component. 

in `main.tsx`:
```tsx

```

Finally, in order to access the context, the `useContext` hook can be used in any of the descendent component of the context component wrapper.