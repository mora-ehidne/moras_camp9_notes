# Prisma Seed

The `seed.ts` file can generate placeholder data for a database.

The `seed.ts` file has to have an instance of PrismaClient in oder to perform CRUD operations on the database.

```ts
import { PrismaClient } from "@prisma/client";

const prisma = new PrismaClient();
```

The async function within the `seed.ts` file performs create actions in the database via the Prisma Client (via the `create()` and `createMany()` methods).

# Faker

In order to randomly generate data, we have used the `faker` package.

```ts
import { faker } from "@faker-js/faker";

await prisma.user.create({
	name:faker.internet.userName(),
	password: faker.internet.password(),
});
```


Generating the data defined in `seed.ts` is executed via the command:

`pnpm prisma db seed`.

>[!WARNING] It is important to disconnect from the database when the mock data is generated, `finally{await prisma.$disconnect();}`