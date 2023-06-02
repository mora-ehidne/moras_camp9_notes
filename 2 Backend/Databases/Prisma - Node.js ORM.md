# ORM - Object-Relational Mapping

ORM frameworks act as a "bridge" between an object-oriented progamming language (OOP) and a relational database.

ORM simplifies database queries and their integration in an OOP language (such as JavaScript).

# Prisma ORM

Docs: https://www.prisma.io/

Prisma can be used with different RDBMS. We will be using it with PostgreSQL.

# Setup

All of the Prisma setup was done in the `backend` folder, independently of the `frontend` or `client` folder. 
All prisma files (seeds and schema) are placed withing the `prisma` folder in the `backend` folder.
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

`pnpx prisma db push` - updates the database with the model defintion
`pnpx prisma db push --force-reset` - clears the database before updating it


## `schema.prisma`

The main configuration file is `schema.prisma`. This file can define the which database will be used (*data source*), create a prisma client (_generator_) and define the data structure of tables in the database (_data model definition)_.

Online playground with visualisation: https://www.prismabuilder.io/

an example of `schema.prisma`:

```js
datasource db {
	provider = "postgresql"
	url = env("DATABASE_URL")
}

generator client {
  provider = "prisma-client-js"
}

model User{
	id String @id @default(uuid()) //generates a uuid value
	email String @unique
	password String
	createdAt DateTime @default(now()) //sets the value of createdAt automatically to the date and time of creation of an entry
	modifiedAt DateTime @updatedAt //sets the value of modifiedAt automatically to the date and time of editing an entry
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

### Data model definition

The structure of each table in the database is created with a _model_ - an object defining fields in a table, including:
- field name (a string)
- data type (String, Int, BigInt, Float, Decimal, DateTime, Boolean etc.)
- type modifiers (`[]` creates an array of given type, `?` makes the field optional)
- attributes (optional, all attributes begin with an `@` or `@@`):
	- `@id` (unique entry identifier)
	- `@unique` (the value can only appear once in the database, eg an e-mail address)
	- `@relation` (relation to other fields/models)
	- `@default` (can be a value or a value generating function, such as now() for DateTime or uuid() or cuid() for an id)
	- `@updatedAt`(auto-updater for DateTime data types)
	- etc.

>[!TIP] Each database entry must be uniquely indentifiable, so each model must have a field with a  `@id`, `@@id`, `@unique` or `@@unique` attribute.

Model names must start with a letter and are written in [[Naming conventions (cases)#Pascal case (PascalCase)|PascalCase]].

Field names must start with a letter and are written in [[Naming conventions (cases)#Camel case (camelCase)|camelCase]].

>[!NOTE] Multi-field (composite) IDs (`@@id`, `@@unique`)
> An ID can consist of more than single field, so the combination of the two fields must be unique. Such an ID is defined with the double-ampersand `@@id` syntax and the fields that are to be composited. Eg:
> ```js
> model User {
  firstName String
  lastName  String
  email     String  @unique
  isAdmin   Boolean @default(false)
  @@id([firstName, lastName])
}


## `.env` file

in the `.env` file we have defined a variable of `DATABASE_URL`. That variable is a string including the localhost port, postgresql definition, username and password for the database being accessed.

DATABASE_URL example: 
`DATABASE_URL=postgresql://postgres:raf6Xmczwg1A8SaCij@localhost:5432/schema`

## Seed

The `seed.ts` file can generate placeholder data for a database.
Generating the data defined in `seed.ts` is executed via the command:

`pnpm prisma db seed`.

# CORS - Cross Origin Resource Sharing

CORS is a security feature that defines which connections are allowed to reach the server. 

It is considered a middleware.

We have used the CORS Node.js package: https://www.npmjs.com/package/cors