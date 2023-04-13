Each part of the website, including text, images and other elements. These can be described by [[HTML tags]]. ^6d55dc

## Opening and closing tags

An HTML tag consists of an opening tag and a closing tag. The opening tag is written as follows:

```HTML
<tagname>
```

>[!TIP] It is possible to write HTML attributes in the opening tag


The closing tag is written as follows:

```html
</tagname>
```

The element described by the tag is located between the opening and closing tags.

## Self-Closing Tags

Some HTML tags have no text content and do not need to be closed. These are called self-closing tags and are written as follows:

```HTML
<tagname/>
```

## Nesting HTML Tags

[[HTML tags]] can be nested to create more complex structures. An example is:

```HTML
<body>
	<h1>Heading</h1>
	<p>Paragraph 1</p>
</body>
```

## HTML nesting relations

In HTML, elements can be in a parent-child or a sibling-sibling relationship. In the above example, ``<body>`` is the parent to ``<h1>`` and ``<p>``, while ``<h1>`` and ``<p>`` are children to ``<body>``. ``<h1>`` and ``<p>`` are siblings to each other.

## HTML Block and Inline elements

[[HTML Block Elements]] take up the full width available to them and are displayed on a new line.

![[HTML Block Elements]]

[[HTML Inline Elements]] take up only the width of its content and do not start on a new line. HTML Inline elements cannot have its margin and padding set.

![[HTML Inline Elements]]

[a detailed list of all HTML tags and their default display values](https://www.w3schools.com/html/html_blocks.asp)

>[!TIP] the ``display`` value can be changed by CSS