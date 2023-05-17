# axios - Promise based HTTP client

Simplifies HTTP requests. Github: https://github.com/axios/axios

installation: `npm install axios`
Usage: must be imported in the `.ts` or `.js` file: `import axios from "axios";`

The `axios` object has methods that perform HTTP requests in a simplified way, such as:
* `axios.delete()`
* `axios.post()`
* `axios.get()`
* `axios.patch()`

All axios methods return a `promise`.

```ts
axios
.get("http://localhost:3000/events")
.then((res) => console.log(res.data))
.catch((error) => console.error(error));
```