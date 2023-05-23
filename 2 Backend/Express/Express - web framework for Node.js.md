# Express

homepage: https://expressjs.com/

Routes defined by Express constitute an API that allows the frontend to communicate with our backend.

# Setup

All of the backend setup was done in a `backend` folder, independently of the `frontend` or `client` folder.

`pnpm init` - pnpm initialization (creates the `package.json` file)
`pnpm install express` - express server installation
`pnpm install -D ts-node` - Node.js installation (TypeScript versionß)
`pnpm install -D typescript` - TypeScript installation
`pnpm install -D @types/node` - Node.js TS types installation 
`pnpm install -D @types/express` - Express TS types installation 
`pnpm install -D nodemon` - live server installation (node monitor)
`pnpm install doteenv` - .env usage package

We created `tsconfig.json`.
We created a `src` folder and `main.ts` inside of it.

Inside of `package.json` we created a script to be able to run the nodemon live server with the `pnpm dev` command:
`"dev": "nodemon ./src/main.ts"`

Nodemon watches the `./src/main.ts` file for changes and restarts the Node.js server if any changes are present in that file.

>[!TIP] Node.js diverts all console.log output into the terminal.

# Usage

In `main.ts`:
```ts
import express from "express";

const app=express(); // server object binding
```

>[!NOTE] The Express backend server will reject all frontend HTTP requests if no origin is defined in the `app.use` method.

# The `.env` file

In the `.env` file we can place the number of the backend and frontend server port.
```js
BACKEND_SERVER="8000"
FRONTEND_SERVER="http://localhost:5173"
```

in `main.ts`:
```ts
import dotenv from 'dotenv';
dotenv.config(); // has to be done once before accessing the .env file
const port = process.env.BACKEND_SERVER; // bind the BACKEND_SERVER variable from the .env file
app.use(cors({origin:process.env.FRONTEND_SERVER})); // only accepts HTTP requests from the given origin
```

# Routing

Incoming HTTP Requests can be forwarded to other functions using the router object.

Inside of the `src` folder, we created a `routes` folder and inside it, a `user.routes.ts` file. A router function can be passed as the callback function of an HTTP request handler, such as the `use()` method.

inside `user.routes.ts`:
```ts
import {Router} from 'express';

const userRouter=Router();

//@route POST /api/1.0/user/signup
//@desc Register user
//@access Public

userRouter.post('/signup',(req, res, next)=>{
	res.send("singup"); // sends the string signup to the client
});

export default userRouter;
```

inside `main.ts`:
```ts
import userRouter from '/routes/user.routes';

app.use('/app/1.0/user', userRouter); // use the userRouter on all HTTP requests that target the /app/1.0/user path

```

## Controllers

The controller functions handle the logic of HTTP request handlers. They are passed as callback functions to Express HTTP request handlers.

inside of the `src` folder, we created a `controllers` folder and inside it, a `user.contollers.ts` file.

inside `user.contollers.ts`:
```ts
import { Request, Response, NextFunction } from 'express'; // type imports

export const signupController = (
	req:Request,
	res: Response,
	next: NextFunction
) => {
	console.log(req.body);
	res.send("signup successful");
};

export default singupController;
```

inside `user.routes.ts`:
```ts
import {Router} from 'express';
import signupController from '../controllers/user.contollers';

const router=Router();

//@route POST /api/1.0/user/signup
//@desc Register user
//@access Public

router.post('/signup', signupController); // passes the signupController function as the request handler

export default router;
```

## Middleware

Middleware is a term used for functions that parse/validate data coming from a HTTP request.

They pass the data further into the backend via the `next()` function, which calls the following callback function in the Express HTTP request handler that invoked the middleware.