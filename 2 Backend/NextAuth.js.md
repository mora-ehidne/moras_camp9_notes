# NextAuth.js

Docs: https://next-auth.js.org/getting-started/introduction

## Setup

Package installation command:
`pnpm add next-auth`

### Folder structure

`app/api/auth/[...slug]` contains a file `routes.ts`.

`app/libs/auth.ts` - NextAuth configuration

#### `auth.ts` - NextAuth config file

```js
import GithubProvider from "next-auth/providers/github"

export const authOptions : AuthOptions = {
	providers: [  
		GitHubProvider({  
			clientId: process.env.GITHUB_ID,  
			clientSecret: process.env.GITHUB_SECRET  
		})  
	], // defines all authorization provides to be used in the app
	
}
```

## Client-side

### GitHub provider

Docs: https://next-auth.js.org/providers/github

In order to do authorization via GitHub, we need to register a new app in the GitHub menu Settings/Developer settings/OAuth Apps (https://github.com/settings/developers). 
To register an app, following fields must be defined:
- app name
- URL from which the authentication will be called
- URL to return to after the authentication

When an app is registered, following is generated:
- Client ID
- Client Secret (similiar to an API key)

After connecting the app, the user authentication can be reset for all already authenticated users (all generated tokens get invalidated).

The Client ID and Client Secret must be included in the `.env` file (or any other secret manager) and referenced in the `libs/auth.ts` config file:

```js
import GitHubProvider from "next-auth/providers/github";  
...  
export const authOptions : AuthOptions = {
	providers: [  
		GitHubProvider({  
			clientId: process.env.GITHUB_ID,  
			clientSecret: process.env.GITHUB_SECRET  
		})  
	],
	session: {
		strategy: "jwt", // method of saving the session token
	},
	secret: process.env.SECRET!, // secret to use for the jwt token
}
```

#### `signIn()`

Docs: https://next-auth.js.org/getting-started/client#signin

In the client component, eg. `login.tsx`, the `signIn()` function can be imported and used to redirect to a sign in provider:

```tsx
import { signIn } from "next-auth/react";

function Login() {
	return (
	<button onClick={()=>signIn("github")}>Log in with GitHub</button>
	);
}
export default Login;
```

>[!NOTE] `signIn("github")` function redirects to a GitHub page, on which the user can log in. On successful GitHub login, an authentication token will be saved in a cookie.



### Client API - `useSession()`, `<SessionProvider>`

Docs: https://next-auth.js.org/getting-started/client#sessionprovider

In order to access the session object token returned by the GitHub sign in, the `useSession()` hook can be used. In order to use `useSession()`, a `<SessionProvider>` must be set up first.

An example session object structure:
```js{
  user: {
    name: string
    email: string
    image: string
  },
  expires: Date // This is the expiry of the session
}
```

>[!WARNING] Both the  `useSession()` hook and the `<SessionProvider>` component can only be used in Client-Side Components.


#### `<SessionProvider>`

In order to enable a component to use the `useSession()` hook, the `<SessionProvider>` component must wrap the component (or its ancestor).

`<SessionProvider>` uses React Context under the hood.

In `layout.tsx`:



#### `useSession()`

```tsx
"use client";
import { useSession } from "next-auth/react";

function Dashboard(){
	const data = useSession();
	console.log(data);
	return <></>
}
```

# Server-side

## Prisma adapter

in `app/libs/db.ts`:
```ts

```


in `app/libs/auth.ts`:
```ts
import { AuthOptions } from "next-auth";
import GitHubProvider from "next-auth/providers/github";  
import { prismaAdapter } from "@next-auth/prisma-adapter";  
import { db } from "./db";

	export const authOptions : AuthOptions = {
	adapter: PrismaAdapter(db),
	providers: [  
		GitHubProvider({  
			clientId: process.env.GITHUB_ID,  
			clientSecret: process.env.GITHUB_SECRET  
		})  
	]
}
```


