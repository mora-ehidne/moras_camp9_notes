>[!INFO] This page details only the setup steps for Tailwind, for tips on how to use Tailwind, see [[Tailwind CSS]]

# Tailwind setup

We have installed Tailwind as a postCSS plugin. We have installed it via (https://tailwindcss.com/docs/installation/using-postcss).

Inside our [[Vite - JS project build tool]] project directory, we entered the commands through the terminal to install and setup Tailwind.

`npm install -D tailwindcss postcss autoprefixer` - installs tailwind
`npx tailwindcss init -p` - initializes Tailwind and adds the postCSS filexs

In the `tailwind.config.js` file we have to add all the files that will be using tailwind classes to the content property:

>[!INFO] Files referenced in the `content` property will be searched for any strings that match tailwind class names. Only the tailwind classes whose names are mentioned in the `content` files will be compiled to the final project.

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{js,ts}", "index.html"],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

>[!WARNING] The main .css file has to be connected to the index.html either through the `link` tag or through the `script` tag connecting to the typescript file that imports the .css file.