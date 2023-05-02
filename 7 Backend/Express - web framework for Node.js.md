homepage: https://expressjs.com/

# Setup

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

Inside of `package.json` we createad a script:
`dev: `

>[!TIP] Node.js diverts all console.log output into the terminal.

# Usage

In `main.ts`:
```ts
import express from "express";

const app=express(); // server object binding
app.listen();
```

# The `.env` file

In the `.env` file we can place the number of the server port.
```js
PORT="http://localhost:8080"
```

in `main.ts`:
```ts
import dotenv from 'dotenv';
dotenv.config(); // has to be done once before accessing the .env file
const port = process.env.PORT; // bind the PORT variable from the .env file
```

# Express methods

All Express server methods are accessed as properties of the `app` binding.

## `listen()`

The `listen` method starts the backend server and defines on which port it runs. 

```ts
import express from "express";
import dotenv from 'dotenv';
dotenv.config();

const app=express();
const PORT = process.env.PORT || 8080; // use the port number from the .env file or 8080 if no PORT variable found in the .env file

// manually define the port
app.listen(8080, ()=>{
	console.log('Server started on port 8080');
});
// use the port number from the .env file
app.listen(PORT, ()=>{
	console.log(`Server started on port ${PORT}`);
});
```

## HTTP handler methods

Express HTTP handler methods get called if the HTTP request sent to the server matches the type of the request and the specified URL.
All the Express HTTP handler methods have two parameters:
1.  __a string __- URL of the HTTP request, the method gets called if the URL of the HTTP request matches (optional, if left undefined all URLs will match)
2. __a callback function__ - the request handler function. There can be several callback functions, that would call the next one using the `next` function. The arguments passed to this function are:
	1. `req` - HTTP request object, with the properties:
		- `body` - the data of a `POST`/`PATCH`/`PUT` request
	2. `res` - the response object, with the methods:
		- `send()` - sends the response to the request back to the client
		- `status()` - sends the specified [[HTTP#HTTP response status codes|HTTP response status code]] to the client, eg, (`res.status(201)`)
	1. `next` - function that calls the next matching Express method

>[!TIP] The HTTP methods get executed by order of code. The first method that matches the URL and the HTTP request method gets executed. The next matching method can be called with the `next` function.

### `use()`

The `use()` method triggers on any HTTP request that matches the given URL.
Such functions are also called _middleware_.

```ts
app.use('/', (req, res, next)=>{
	console.log("special use case");
	next(); // calls the next matching method
});
app.use((req, res, next)=>{
	console.log("executes on every HTTP request regardless of the URL");
	next(); // calls the next matching method
});
app.use(express.json({limit:'1mb'})); // parse all HTTP requests as JSON, limit the size of the HTTP request body to a maximum of 1 megabyte
// note that calling the express.json method calls the `next` method on its own
```

### `get()`

The `get()` method handles all incoming `get` HTTP requests.

```ts
app.get('/', (req, res, next)=>{
	res.send("return data"); // send the server answer to the client
});
```

>[!TIP] The `get()` request is triggered automatically by typing the URL of the server in the URL bar of the browser.

### `post()`

The `post()` method handles all incoming `post` HTTP requests.

```ts
app.post('/', (req, res, next)=>{
	console.log(req.body); // logs the body of the POST request
	res.status(201).send("POST method successful"); // send the success message with a 201 response status code
});
```

### `delete()`

The `delete()` method handles all incoming `delete` HTTP requests.

```ts
app.delete('/', (req, res, next)=>{
	console.log(req.body); // logs the body of the DELETE request
	res.send("DELETE method successful"); // send the server answer to the client
});
```

# Routing

Specific URLs can be routed to specific files that handle HTTP requests to those URLs.
inside of the `src` folder, we created a `routes` folder and inside it, a `user.routes.ts` file.

inside `user.routes.ts`:
```ts
import {Router} from 'express';

const router=Router();

//@route POST /api/1.0/user/signup
//@desc Register user
//@access Public

router.post('/signup',(req, res, next)=>{
	res.send("singup"); // sends the string signup to the client
});

export default router;
```

inside `main.ts`:
```ts
import userRouter from '/routes/user.routes';

app.use('/app/1.0/', userRouter)

```

## Controllers

The controllers funcitons that are called by the HTTP requests.

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