Tailwind (https://tailwindcss.com)  is a CSS framework which enables the usage of Tailwind utility classes.

>[!TIP] Tailwind automatically removes all default HTML styles, as if using *a reset.css*.

Tailwind has a just-in-time compiler, meaning that tailwind ships just the utility classes you have used in your project with your website, not the entire Tailwind library.

# Setting up Tailwind

## Vite setup

To set up Tailwind, we have used the build tool Vite to create a new project in its own new directory. 

![[Vite - JS project build tool]]

## Tailwind setup

![[Tailwind - CSS Framework]]

# Directives

Directives are Tailwind instructions whose name starts with an `@`.

## `@apply` 

the `@apply` keyword can be used in the .css file to use Tailwind classes as vanilla css.

```css
.my-custom-class{
@apply bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded;
}

```

## `@layer`

The `@layer` directive is used to target a specific Tailwind layer to place custom CSS inside that layer. All CSS code written inside the layers gets *treeshaked*.

The three Tailwind layers are:

* `base` - used for styles affecting HTML elements (tags) - lowest specificity
* `components` - used for custom classes - medium specificity
* `utilities` - used for custom utility classes - highest specificity

These three layers have their own specificity, with the `utilities` being the most specific, the `components` layer being less specific, and the `base` layer being the least specific.


```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base{
	p{	}
	html{	}
}
@layer


```

# Modifiers

Modifiers are used as prefixes for Tailwind classes in order to handle pseudoclasses, dark mode, media queries etc.

```HTML
<div class="md:p-4 hover:bg-cyan400"> <!--  -->
</div>
```

# Shortcuts

`command + i` - bring up the drop-down menu

# A tailwind online playground

(https://play.tailwindcss.com/)