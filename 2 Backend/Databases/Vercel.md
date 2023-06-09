# Vercel
## Setup

In order to use Vercel cloud databases, a Vercel account has to be created on vercel.com.

A Vercel cloud database can be used in a project regardless if the project is deployed as a Vercel project.

## Vercel Cloud Database

### Creating a new Vercel Database

In the Vercel user dashboard, under the Storage tab, a new database can be created. We have used a PostgreSQL database.

The newly selected database can be optionaly connected to a Vercel project.

### Accessing the database with Prisma

The database can be accessed via Prisma.

#### .env

First, an .env file must be created at the top level of our project.

In the Vercel user dashboard (vercel.com/dashboard/), under the storage tab, with the database selected, there is a tab titled `.env.local`. The contents of this file should be copied inside our .env file at the top level of our project.

In our case, the `.env`  file looked like:
```js
POSTGRES_URL="postgres://default:vMtcDIURL8a7@ep-red-butterfly-258724-pooler.eu-central-1.postgres.vercel-storage.com:5432/verceldb"
POSTGRES_PRISMA_URL="postgres://default:vMtcDIURL8a7@ep-red-butterfly-258724-pooler.eu-central-1.postgres.vercel-storage.com:5432/verceldb?pgbouncer=true&connect_timeout=15"
POSTGRES_URL_NON_POOLING="postgres://default:vMtcDIURL8a7@ep-red-butterfly-258724.eu-central-1.postgres.vercel-storage.com:5432/verceldb"
POSTGRES_USER="default"
POSTGRES_HOST="ep-red-butterfly-258724-pooler.eu-central-1.postgres.vercel-storage.com"
POSTGRES_PASSWORD="vMtcDIURL8a7"
POSTGRES_DATABASE="verceldb"
```

Prisma then got connected with the database by specifying it in the `prisma.schema` file:

```js
generator client {
  provider = "prisma-client-js"
  previewFeatures = ["jsonProtocol"]
}

datasource db {
  provider = "postgresql"
  url = env("POSTGRES_PRISMA_URL") // uses connection pooling
  directUrl = env("POSTGRES_URL_NON_POOLING") // uses a direct connection
  shadowDatabaseUrl = env("POSTGRES_URL_NON_POOLING") // used for migrations
}
```

## New Vercel Project

In order to use a Vercel cloud database, a GitHub repo must be deployed as a new Vercel project.
In the Vercel user dashboard, under the Overview tab, a GitHub repo can be added as a new project via the button `Add New`  and selecting `Project`. In this view, only GitHub repos with enabled permissions for Vercel can be imported. In order to add Vercel permissions for a new GitHub repo, click on `Adjust GitHub App Permissions →`. Here, a repo can be deployed as a Vercel project - meaning it will get deployed online in the Vercel Cloud and get its own URL to access it.

When a GitHub repo gets deployed as a new Vercel project, on each new commit on the `main` branch, Vercel will re-build and re-deploy the project.

>[!TIP] Deployment
>Web deployment refers to the process of uploading and configuring the files and code of a website/web app to a server or hosting service, making it available to be accessed by users on the internet.
