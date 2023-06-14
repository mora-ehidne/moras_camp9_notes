# useRef

In order to reference a DOM element in React, `useRef` can be used.

`useRef` saves a DOM element within a binding that can be referenced at any point.

```ts
const myComponent = useRef<HTMLButtonElement>(null); //the reference is always initialized with a null, as the binding will be made after the element has rendered
```

The ref binding is then assigned to the `ref` attribute, which binds the HTML element to the ref binding. 
The `ref` attribute is available on all HTML elements in React.

```tsx
<button ref={myComponent}>Click me!</button> //the button got bound to the stateful binding myComponent
```

Now the DOM element can be referenced via `ref.current` in order to do something with it, eg have it call HTMLElement methods:
```tsx
myComponent.current.focus(); //focuses on the DOM element in the myComponent binding
```

## forwardRef()

In order to bind a DOM element which is not a child to a ref, `forwardRef()` must be used.

This has to be done when there is a custom React component which returns one or several HTML elements, and we want to reference one of those descendent elements. Eg:

```tsx
function ParentComponent() {
	const myRef=useRef<HTMLButtonElement>(null); //this is where we want to bind the button
	return <ChildComponent/> //the button we want to bind is a child of this component
}

function ChildComponent(){
	return <button>Click me!</button> //this is the button we want to bind to myRef
}
```

In this case, the component in between the element that we want to bind and the component in which the ref is has to use `forwardRef()`, in order to be able to accept a ref and pass the ref down to its child and up to its parent.

This in-between component must be wrapped within the `forwardRef()` function.

```tsx
function ParentComponent() {
	const myRef=useRef<HTMLButtonElement>(null);
	return <ChildComponent ref={myRef}/> //as ChildComponent's function is wrapped in forwardRef(), it can now accept a ref
}

const ChildComponent = forwardRef((ref:React.ForwardedRef<HTMLButtonElement>)=>{
	return <button ref={ref}>Click me!</button> //the button is now bound to myRef
	}
)
```

Now the referenced HTML element can be accessed via `myRef.current`:


```tsx
function ParentComponent() {
	const myRef=useRef<HTMLButtonElement>(null);
	useEffect(()=>{myRef.current.focus()}); //focuses the descendent button element
	return <ChildComponent ref={myRef}/> ;
}

const ChildComponent = forwardRef((ref:React.ForwardedRef<HTMLButtonElement>)=>{
	return <button ref={ref}>Click me!</button> ;
	}
)
```

>[!NOTE] The component wrapped in `forwardRef()` must always be saved in a `const` binding and can be written either as a named function or an anonymous (arrow) function.
>eg. `const MyComponent = forwardRef(function MyComponent(ref){//component code})`
>or: `const MyComponent = forwardRef((ref)=>{//component code})`