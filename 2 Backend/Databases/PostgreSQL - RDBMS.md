# PostgreSQL

Docs: https://www.postgresql.org/docs/

PostgreSQL is a RDBMS (Relational Database Managment System). 
All RDBMS work with with the SQL language (Structured Query Language).

Some non-SQL databases are MongoDB (works with Bison - JSON-like format).

PostgreSQL can be used in a cloud solution, provided by the service provider (host service).
PostgreSQL can be used in a terminal, or via a GUI, such as __pgAdmin__ or Prisma Studio.

# Setup

Download: https://www.postgresql.org/download/
During the download, postgreSQL will ask for a master password and a default server port.
The default username is `postgres`.


# PostgreSQL Syntax

in the SQL language, queries consist of __Key Words__ and __Identifiers__.

## Key Words

- written in [[Naming conventions (cases)#Screaming snake case (SCREAMING_SNAKE_CASE)|SCREAMING_SNAKE_CASE]]
- Provided by SQL

### CRUD: Create - Read - Update - Delete

CRUD are the four basic operations of persistent storage in computer programming.
In SQL, CRUD operations are performed by the following keywords:

- Create Data: `INSERT INTO`
- Read Data: `SELECT`
- Update Data: `UPDATE`
- Delete Data: `DELETE`

### `JOIN`

The `JOIN` keyword accesses data from two different tables.

## Identifiers

- written in [[Naming conventions (cases)#Snake case (snake_case)|snake_case]]
- can be written within quotes `""`/`''`
- must start with a letter or an underscore, can contain letters, numbers and underscores

### IDs

Primary Keys are the unique IDs of the individual record (row).
Foreign/secondary IDs reference a record/row in a different table.

# Data types

Different RDBMS can have different data types. 
The most common ones are:
- characters
- numeric
- boolean
- date

>[!NOTE] SQL can only hold primitive data types, not files. Because of that, URLs to files can be stored in a database, and the files themselves can be stored somewhere else, eg. in a cloud service.


