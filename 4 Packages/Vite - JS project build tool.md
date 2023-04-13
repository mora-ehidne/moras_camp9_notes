# Vite

Vite is a build tool for JavaScript and TypeScript projects.

Homepage: https://vitejs.dev/

## Vite project setup

>[!WARNING] Vite needs node.js installed (v14.18+, 16+)

Through the console, we set up a new project directory with the Vite command:

`npm create vite@latest` and following the prompts.

Vite can create a vannilla JS/TS project or a React JS/TS project.

Vite enables us to run a live server (so using the live server extension in VS Code is not necessary) with the command `npm run dev`. Starting the Vite live server will display the localhost port on which the live server is running. Accessing the port in a browser accesses the live server.

`npm run build` will build the project, compiliing TypeScript into JavaScript if necessary and Tailwind into CSS.