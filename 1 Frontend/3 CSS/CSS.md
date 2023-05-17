[[Moras Web Dev Notes/3 CSS/CSS]] (Cascading Style Sheets) is a stylesheet language that is used to style and format [[Moras Web Dev Notes/2 HTML/HTML]] pages. CSS is used to control the layout, colors, fonts, and other visual aspects of the website, and provides a way to separate the content of the website from its presentation. ^071011

## CSS properties and values

A CSS command is divided into two parts:
1. the property
2. the value

Example:
```css
.exampleclass{
/*property: value;*/
margin: 12px;
}
```

### CSS `position` property

![[CSS Position Property]]

### CSS `auto` Value

![[CSS Auto Value]]

## How does CSS work?

CSS rules are defines in a separate, .css file, or within the ``<head>`` section of the .html file.
These rules are applied to the HTML elements selected by the CSS Selectors.

Example:
```css
h1{
font-size:1.5rem;
color:blue;
}
```

## Measurement Units in CSS

In CSS, different measurement units can be made use of:
1. **px (pixel)** - a px unit is equal to a CSS pixel
2. **rem** - relative to the font-size defined in the root element, default is 1 rem = 16 px
3. **em** - relative to the font-size defined in the parent element, default is 1 rem = 16 px
4. **% (percentage)** - the size in percent of the parent element, if used for font, 100% = 1em
5.  **vw (viewport width)** - the width of the viewport of the device, 100vw = total width of the viewport
5.  **vh (viewport height)** - the height of the viewport of the device, 100vh = total height of the viewport

Example of using the ``rem`` unit:
```css
html{
font-size:22px;
}
h1{
font-size:2rem; /*font-size is now 2*22px/
}
```


Example of using the ``em`` unit:
```html
<div class="parent">
	<h1 class="heading">Heading</h1>
</div>
```

```css
.parent{
	font-size:25px;
}
.heading{
	font-size:2em; /* font-size is now 2*25px */
}
```

## CSS Box Model

The ![[CSS Box Model#^4b2ab8]]

## The Display Property

The **display** property changes the layout behaviour of HTML elements. It sets an element's **inner** and **outer** _display types_.

* **outer display type** defines how the element behaves in the **flow layout**.
* **inner display type** sets the layout of children, which can be **flow**, **flex** or **grid**

### Outer Display Type

The **Outer Display Type** can have following values:

* **block** - starts on a line break, takes up the entire width available to it, vertical padding and margin properties can be set. Vertical margins between ``block`` elements collapse.
* **inline-block** - same as ``block`` but does not start on a line break
* **inline** - does not start on a line break, size is defined by its contents, vertical padding and margin properties cannot be set

For a list of default outer display values refer to [[HTML Block Elements]] and [[HTML Inline Elements]]

For more information on the **block** and **inline** elements in the **flow layout** refer to [MDN Block and inline layout in normal flow](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flow_Layout/Block_and_Inline_Layout_in_Normal_Flow)

### Inner Display Type

The Inner Display Type defines the type of formatting context that its contents (children) are laid out in.
It can have the following values:
 * flow (default on all HTML elements)
 * flex
 * grid

``Flow`` lays out its contents using **flow layout** (block-and-inline layout), also called *default flow layout*. 

``Flex`` lays out its contents using the **flexbox model**. The element's **outer display type** becomes ``block``

``Grid`` lays out its contents using the **grid model**. The element's **outer display type** becomes ``block``


Code example:
```css
display:block; /*block element*/
display:inline; /*inline element*/
display: inline-block; /*inline element*/
display: flex; /*enables flexbox behaviour as a parent*/
```

## CSS Flexbox layout

![[CSS Flexbox layout#^a6b6f5]]

