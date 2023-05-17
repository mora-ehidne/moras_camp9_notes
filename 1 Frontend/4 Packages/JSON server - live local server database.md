The JSON server offers a fake live local server database, used for prototyping and mocking.
Github: https://github.com/typicode/json-server

# JSON server setup

## JSON server installation

JSON server is simply installed in a directory by using:

`npm install -g json-server`

The server is run by using:

`json-server --watch db.json`

If we do not have a `db.json` file, the `--watch` command will create a db.json file with some default data. The `--watch` command will give a local port on which the sever is run, which can then be used as the URL for all HTTP requests. 
The default port is `http://localhost:3000`, but can be changed by adding the `--port` flag to the `--watch` command:

`json-server --watch db.json --port 3001`

## Custom script for simplifying the `--watch` command

The `--watch` command call can be simplified by making a new entry in the `scripts` property of the `package.json` file of  the [[Vite - JS project build tool]] project directory. 

```json
"scripts": {
// some other scripts
"db": "json-server --watch db.json"
},
```

This would make simply running `npm run db` run the `json-server --watch db.json` command.