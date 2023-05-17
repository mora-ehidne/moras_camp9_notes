# Prisma 

ORM stands for **Object-Relational Mapping**.

Docs: https://www.prisma.io/

Prisma can be used with different RDBMS. We will be using it with PostgreSQL.

# Setup

All of the Prisma setup was done in a `backend` folder, independently of the `frontend` or `client` folder.
We have installed prisma as dev dependencies.

`pnpm init` - pnpm initialization (creates the `package.json` file)
`pnpm install -D ts-node` - Node.js installation (TypeScript versionß)
`pnpm install -D typescript` - TypeScript installation
`pnpm install -D @types/node` - Node.js TS types installation 
`pnpm install -D nodemon` - live server installation (node monitor)
`pnpm install doteenv` - .env usage package
`pnpm install -D prisma` - Prisma installation 

initializing Prisma:
`pnpx prisma init --datasource-provider postgresql`

We have also installed the `Prisma` VSCode extension for code highlighting, formatting etc for `.prisma` files.

# Usage

Prisma has its own language that `.prisma` files use.

`pnpx prisma db push` - updates the database with the specified schema

## `schema.prisma`

The main configuration file is `schema.prisma`. This file can define the database to be used and tables in that database.

Online playground with visualisation: https://www.prismabuilder.io/

an example of `schema.prisma`:

```js
datasource db {
	provider = "postgresql"
	url = env("DATABASE_URL")
}

model User{
	id String @id @default(uuid())
	email String @unique
	password String
	createdAt DateTime @default(now())
	modifiedAt DateTime @updatedAt
}
```

### Data source

The data source part of the `schema.prisma` file defines the kind of database that will be used and the URL to that database. 
There can only be a single data source.

```js
datasource db {
	provider = "postgresql"
	url = env("DATABASE_URL")
}
```

### Generator

A schema file can have one or more generators.

## `.env` file

in the `.env` file we have defined a variable of `DATABASE_URL`. That variable is a string including the localhost port, postgresql definition, username and password for the database being accessed.

The default username is `postgres`
DATABASE_URL example: 
`DATABASE_URL=postgresql://postgres:raf6Xmczwg1A8SaCij@localhost:5432/schema`

## Seed

The `seed.ts` file can generate placeholder data for a database.
Generating the data defined in `seed.ts` is executed via the command `pnpm prisma db seed`.
