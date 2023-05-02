# Setup

We have used Vitest together with the react testing package. The react testing package extends Vitest.
Additionaly to Vitest, we have installed four packages:

`pnpm add -D @testing-library/react`
`pnpm add -D @testing-library/testing-dom`
`pnpm add -D jsdom`
`pnpm add -D @types/testing-library__jest-dom`

>[!INFO] Note that the `-D` flag marks the packages as solely development dependencies that will not be included in the production. 

We have also edited the configs in the `vite.config.ts` file.
```ts
import defineConfig from "vitest"
export default defineConfig({
	plugins: [react()],
	test:{
		globals: true,
		environment: "jsdom",
		setupFiles: ["./vitest.setup.ts"], // takes the setup from this file
		include: ["**/*test.{ts,tsx}"], // searches for all .test.ts/tsx files and uses them as tests
	},
})
```

We have also created a `vitest.setup.ts` file.

```ts
// jest-dom adds custom jest matchers for asserting on DOM nodes.
// allows you to do things like:
// expect(element).toHaveTextContent(/react/i)
// learn more: https://github.com/testing-library/jest-dom
import "@testing-library/jest-dom";
```

# Test files

The test files are generally either in the same level as the component or in a directory `__tests__`
We have made a testing file `App.test.tsx`.

The standard Vitest syntax of `describe`, `it/test` etc is applicable for writing the test files.

In `App.test.tsx`:
```tsx
import { render, screen } from "@testing-library/react"
import App from "./App";

describe("App", ()=>{
	beforeEach(()=>{ // applies to all the it/test blocks
		render(<App />); // simulated the rendering of the App component, necessary for react testing			
	})

	it("should have a heading",()=>{
		const heading = screen.getByRole("heading", {name: /welcome!/i });
		expect(heading).toBeInTheDocument();
		expect(heading).toBeVisible();
	})
})
```

# Running tests

`pnpm run vitest` runs the tests and outputs the results of the testing.

## `screen`

`getByRole`
`getByText` - returns the element that has the text content that matches the argument. If there are more than one such element, the test fails.
This method has two parameters:
1. a string or a regex - the text content of the element that is to be looked for
2. an object (optional) - additional options, such as `name`, `exact`

examples:
- `screen.getByText("Welcome!")` returns the element that has the exact text context of `Welcome!`
- `screen.getByText(/welcome/i)` returns the element that includes a case-insensitive (`i`) string `welcome`
- `screen.getByText("Welcome!", {exact:false})`