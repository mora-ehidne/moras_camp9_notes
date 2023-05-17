# Frontend

In the frontend, we are using the Vite live server (run by the `pnpm dev` script) to run our React app. In the browser, we are using the localhost port no. 5173 (`http://localhost:5173`) to access our app.
We are accessing the backend by sending it HTTP requests (via axios) to the localhost port 8000 (`http://localhost:8000`).

# Backend

The backend is in a separate folder from the frontend. All commands are run with the backend as the working directory and all files refer to files within the backend directory.

## Server

We are running a live backend server of our Express framework via nodemon. 

We can specify which port nodemon runs on and which script file it loads. 
- port: can be specified in the nodemon command or in the Express `app.listen()` method call (we used `8000`)
- script: defined in the nodemon command (we used `main.ts`)

We have defined a script in `package.json` for `dev` as:
```json
"dev": "nodemon ./src/main.ts"
```

Thus we can run the nodemon live server with `pnpm run dev`, starting at `./src/main.ts` with the port we specified in the `app.listen()` Express method call in `main.ts`.

All communication with our backend happens through HTTP requests to the server at `http://localhost:8000`.
The Express framework communicates with the database by importing and using the Prisma client.

## Database

We are using a local PostgreSQL database to store our backend data.
The database does not need to be `run`, it is always accessable through its connection url.
Each PostgreSQL database has a username, password and a localhost port to access it.

Our database, the one being created as the default one on PostgreSQL installation, has the connection url of `postgresql://postgres:raf6Xmczwg1A8SaCij@localhost:5432`.

Setting up the database tables happens through the Prisma schema in the `schema.prisma` file.
All communication between our Express framework and the database happens through the Prisma client.

## Prisma

Prisma serves as the in-between between our Express framework and our database.
All prisma code is saved in the prisma directory, mainly in the `schema.prisma` file.

### Prisma schema - accessing and setting up the database

The database is accessed through the data source part of the `schema.prisma`.
```js
datasource db {
	provider = "postgresql"
	url = "postgresql://postgres:raf6Xmczwg1A8SaCij@localhost:5432"
}
```

### Prisma client - connection between Express and the database

The Express framework can access the database through the Prisma client.
The prisma client must be first generated in the `schema.prisma` file:

```js
generator client {
	provider = "prisma-client-js"
}
```

And then imported and used in an Express `.ts` file:

```ts
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();
```