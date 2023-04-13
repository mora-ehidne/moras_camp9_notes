# i18n

homepage: https://www.i18next.com/

i18n also does caching of the active language in the local storage, so the page will be loaded with the last active language next time. 

# i18next Setup

## installation and download

We have installed several packages via `npm install` in the Vite React project:

`i18next`
`react-i18next`
`i18next-browser-languagedetector`
`i18next-http-backend`

## initial configuration

We have then created an i18next config file: `i18n.ts`

In `i18n.ts`:

```ts
import i18next from "i18next";
import {initReactI18next} from "react-i18next";
import LanguageDetector from "i18next-browser-languagedetector";

i18next.use(initReacti18next)use(LanguageDetector).init( // sets the initial configs, init() accepts an object with all configurations as key-value pairs
	{
		debug: true, // console.logs important i18next behaviour
		lng: "de-DE", // sets the default language of the app, overwrites the language of the browser
		fallbackLng: "de-DE", // language that gets loaded if the language of the browser does not get found in the resources
		resources:{
			de:{
				pastry:{ // namespace: a set of values for a specific page or a component
						title: "Kuchen"
					}
				}
			},
			en:{
				pastry:{
						title: "cake"
					}
				}
			}
	}
)
```

The config file has to be imported into the main React file `main.tsx`:

```tsx
// some other imports
import "./utils/i18n";
```

>[!TIP] The language information of the browser is found in the  `window.location.Navigator.language` and `window.location.Navigator.languages` properties.

# Usage

We have used the `useTranslation()` hook from the `react-i18next` package.

`useTranslation()` hook accepts a single parameter:
 1. an array of strings which match the names of the namespaces to be used

`useTranslation()` returns an object. The first property of that object is a function that has a single parameter: a string that matches the name of a property in the namespace. It returns a string whose value matches the value of that property.

in `App.tsx`:

```tsx
import {useTranslation} from "react-i18next"

function App(){
	const{t, i18n}=useTranslation(["pastry"]); // useTranslation hook returns an object, from which the first property is a function that translates the strings passed to it
	return(
		<h1>{t("title")}</h1> // the t() function returns a string based on the value of the title key in the pastry namespace of the active language
	)
}
```

# Backend

https://github.com/i18next/i18next-http-backend

Instead of placing the text content into the *resources* property of the object passed to the `i18next.init()` function call in the `i18n.ts`, the text content can be saved in `.json` files.

The individual namespaces are saved as individual `.json` files.

>[!INFO] By default, the i18n backend looks for `.json` files in directories named as languages being used (eg *en*, *de*, *fr*), inside the directory *locales*. By default, it includes the namespace named `translations`. The default namespaces are overwritten when specifying the namespaces in the `ns` key of the configs object.

This can be changed in the configuration object passed to the `i18next.init()` call.

Example of `pastry.json` file in the `en` directory:

```json
{
	"title": "cake",
	"description": "an amazing cake"
}
```

Example of `pastry.json` file in the `de` directory:

```json
{
	"title": "Kuchen",
	"description": "ein richtig guter Kuchen"
}
```

In `i18n.ts`:

```ts
import i18next from "i18next";
import { initReactI18next } from "react-i18next";
import LanguageDetector from "i18next-browser-languagedetector";
import Backend from "i18next-http-backend"; // import the backend

// use the backend
i18next.use(initReactI18next).use(LanguageDetector).use(Backend).init({
  debug: true,
  fallbackLng: "en",
  ns: ["pastry"], // defines the namespaces
  backend: { loadPath: "/locales/{{lng}}/{{ns}}.json" } // defines the path for the backend files
});
```



# `Trans` component

