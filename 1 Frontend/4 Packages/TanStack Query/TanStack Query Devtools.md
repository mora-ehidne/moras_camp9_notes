# TanStack Query React Devtools

Docs: https://tanstack.com/query/v4/docs/react/devtools

The TanStack Query React Devtools provides an additional development console for the TanStack Query.

## Setup

```bash
npm i @tanstack/react-query-devtools
# or
pnpm add @tanstack/react-query-devtools
```

The TanStack Query React Devtools must be imported in the main component of the react app, eg. `main.tsx` or `App.tsx` and included as a component in the `QueryClientProvider` wrapper component.

in `main.tsx`
```tsx
import { ReactQueryDevtools } from '@tanstack/react-query-devtools';

<QueryClientProvider>
		<App />
      <ReactQueryDevtools />
</QueryClientProvider>
```
