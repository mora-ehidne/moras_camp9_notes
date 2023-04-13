[[HTML Attributes]] provide additional information about the [[HTML tags]]. THey are used to configure the appearance and behaviour of an HTML element. ^adbf9f

## Common Attributes

Some attributes are tied to a specific HTML tag, while common attributes can be used for all HTML tags.

* [[#The ``class`` Attribute|class]]
* [[#The ``id`` Attribute|id]]
* title
* style
* alt
* src
* href

## Use of HTML Attributes

HTML attributes are always defined inside the opening tag of the HTML element.

```HTML
<img src="images/example.jpg" alt="an image" class="image"/>
```

## The ``class`` Attribute

The ``class`` attribute allows the specification of one or more class names for an HTML element.
Classes can be used to select elements with [[Basics of Web Development (day 8)/CSS/CSS]] in order to apply styles.

```HTML
<p class="highlighted important">Hello everyone</p>
<p class="important">Further information</p>
```

```CSS
.highlighted{
background-color: yellow;
}
.important{
font-weight:700;
}
```

## The ``id`` Attribute

The ``id`` attribute allows to specify a unique id for an HTML element. Id's can be used to select a single element with [[Basics of Web Development (day 8)/CSS/CSS]] in order to apply styles.

```HTML
<p id="header">Hello everyone</p>
<p id="important">Further information</p>
```

```CSS
#header{
font-size:2rem;
}
#important{
font-weight:700;
}
```
>[!Warning] An id should not be used more than a single time!



