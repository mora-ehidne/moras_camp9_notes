# axios - Promise based HTTP client

Github: https://github.com/axios/axios

Axios is used to simplify HTTP requests in JavaScript/TypeScript. It uses XMLHttpRequest API (XHR).

installation: `npm install axios`
Usage: must be imported in the `.ts` or `.js` file: `import axios from "axios";`

The `axios` object has methods that perform HTTP requests in a simplified way, such as:
* `axios.delete()`
* `axios.post()`
* `axios.get()`
* `axios.patch()`

All Axios requests do the [[JSON]] parsing/stringification automatically.

All axios methods return a `promise`.

Example of an axios method call:
```ts
axios
.get("http://localhost:3000/events")
.then((res) => console.log(res.data))
.catch((error) => console.error(error));
```