# Prisma Client

Prisma client is installed separately from the prisma schema.
The prisma client can do CRUD operations on the database defined in the Prisma schema.

# Setup

`pnpm install @prisma/client`

When the Prisma schema gets updated, the Prisma client must be generated again.
`pnpx prisma generate`

# Usage

The Prisma client can be imported into a `.js/.ts` file.
It has to be initialized and then it can be used to access tables and their methods.

The Prisma client services can be placed in a folder called `services`, inside a file such as `user.service.ts`:

```ts
import { PrismaClient} from "@prisma/client";

const prisma = new PrismaClient(); // initialized the prisma client

async function createUser(request){
// access the user table and create a new record in it (async)
	return await prisma.user.create({
		data: {
			email: request.body.email,
			password: request.body.password,
			firstName: request.body.firstName,
			lastName: request.body.lastName,
		}
	});
} 
async function doesUserExist(userEmail){
// access the user table and attempt to find a user with a unique property matching the given value
	const newUser = await prisma.user.findUnique({
		where: {
			email: userEmail,
		}
	});
	return !!newUser;
} 
```