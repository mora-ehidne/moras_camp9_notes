# Zod

Zod can be used to validate data by comparing it to a given TypeScript schema.
Zod can be used in both Frontend and Backend validation.

homepage: https://zod.dev/

Zod throws as error if 

# Setup

`pnpm install zod`

the file using Zod has to import the `z` object:
```ts
import { z } from "zod";
```

# Usage

## Middleware

We have created a `middleware` folder inside of the `src` folder, and inside of it the `validate.Resource.ts` file.

in `validate.Resource.ts`
```ts
import { AnyZodObject } from 'zod';
import { Request, Response, NextFunction } from 'express';

// validation function, either throws a parsing error or simply calls the next Express function from the one that called it
export const validate = (schema: AnyZodObject) => (
	req: Request,
	res: Response,
	next: NextFunction
) => {
	try {
		schema.parse(req.body); // tries to parse the data as the schema structure
	} catch(err){
		return res.status(422).send(err); // returns status code 422 and the error if the parse method throws an error
	}
	next(); // otherwise go to the next Express function
}
```

We have created a `validate` folder inside of the `src` folder, and inside of it the `userValidation.ts` file.

in `userValidation.ts`:

```ts
import { z } from 'zod';

```

# `z` object methods

The `z` object has methods that define a schema that will be used to validate data.

## `object()`

Returns an object whose structure will be used as a schema for data validation.

```ts
const schema = z.object({
	userName: z.string().min(1).max(25),
	email: z.string().email(),
	password: z.string().min(5).max(50)
});
```

# schema methods

## `parse()`

The `parse()` method compares the structure of the passed argument to the structure of the schema calling it. 

On success, the argument is returned unchanged.
On failure, an error (ZodError type) is thrown.

```ts
try{
	schema.parse(req.body);
}
catch(err){
	console.log(err);
}
```

## `safeParse()`

`safeParse()` does not throw an error on a failed validation. 
It returns an object with two parameters:
1. success - boolean
2. either the data passed as argument or an error: ZodError

```ts
import { z } from "zod";

const mySchema = z.string(); // defines that the passed data must be a string
const result = mySchema.parse(12); // zod will throw an error as 12 is not a string
const result = mySchema.safeParse(12); // zod does not throw an error but returns {success:false, error}
```