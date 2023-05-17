# Storybook

Homepage: https://storybook.js.org/
Youtube channel: https://www.youtube.com/@chromaticui

# Setup

Storybook is installed in the terminal:
````shell
pnpm dlx storybook@latest init
````

Storybook can be run by using the terminal command `pnpm run storybook` and accessing in the browser the localhost URL provided (or allowing Storybook to open in browser).

# Configuration

The Storybook config files are inside the `/.storybook/` folder. There are two files:
1. `main.ts` - addons are installed in this file
2. `preview.ts`

To use Tailwind inside Storybook, the `index.css` file has to be imported into the `preview.ts` file.

inside `/.storybook/preview.ts`:

```ts
import '../src/index.css'
```

# Creating stories

Stories are saved in the `stories` folder in the `src` folder, with a `.stories.ts` extension.

inside `/src/stories/Button.stories.ts`:
```ts
import {Meta, StoryObj} from '@storybook/react';
import Button from "../components/Button"

// the meta object defines the basic information about the story
const meta:Meta<typeof Button> = {
	title: "Button", // name that will be displayed in Storybook
	component: Button, // the react component
	args: {
		children: "Click me!", // the args parameter is an object with all the properties that are defined and editable, when defined in the meta object, it applies to all stories for the component
	},
};

export default meta; // the meta object is the default export

// all other exports are named story exports.
// the const names are also the names that are displayed in the Storybook
// their type is StoryObj with a type parameter which is typeof component
export const Primary: StoryObj<typeof Button> = {
	args: { // when defined in a story object, args are only applied to that specific story, overwriting the properties defined in the meta object if overlapping
		variant: "primary",
	},
};				
export const Secondary: StoryObj<typeof Button>={
	args: {
		variant: "secondary",
		children: "Secondary click",
	},
};
export const Special: StoryObj<typeof Button>={
	args: {
		...Secondary.args, // reusing the args of the Secondary story with the spread argument
	},
};
```