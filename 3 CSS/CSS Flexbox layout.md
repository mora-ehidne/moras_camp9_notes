[[CSS Flexbox layout]] is a new value added to the CSS ``display`` property.
It causes the element that it applies to become a ``flex container`` and sets its ``outer display type`` to ``block``. All the children of the element will become ``flex items``, which participate in the **flex layout model**. ^a6b6f5

Flexbox deals with layout in one dimension at a time — either as a row or as a column.

in the **flexbox layout**, there are two axes: the **Main Axis** and the **Cross Axis**

![Flexbox Axes Illustration|400](flexbox-axes2.jpg)

# Properties for the parent element

### flex-direction

The direction of the Main and Cross Axis changes based on the value of the ``flex-direction`` property.
1.  ``flex-direction: row`` - default value, main axis is left-right, cross axis is top-down
2.  ``flex-direction: row-reverse`` - main axis is right-left, cross axis is top-down
1.  ``flex-direction: column`` - main axis is top-down, cross axis is left-right
2.  ``flex-direction: column-reverse`` - main axis is down-top, cross axis is left-right

The default value of the ``flex-direction`` property is ``row``, meaning that the default direction of the **main axis** is left-right and of the **cross-axis** is top-down

![Flexbox Main Axis with flex-direction: row](flexbox_main-axis_row.png)

![Flexbox Main Axis with flex-direction: column|500](flexbox_main-axis_column.png)

## Flexbox Main Axis

### justify-content

The position of the flex items on the **Main Axis** can be changed by the ``justify-content`` property.
The default value is ``flex-start``.

``justify-content`` can have the following values:

* `flex-start` -  items are at the start edge of the container, empty space is at the end edge of the container
* `flex-end`- items are at the end edge of the container, empty space is at the start edge of the container
* `center`- items are at the center of the container, empty space is equally distributed at the start edge and end edge of the container
*  `space-between` - empty space is distributed only between the items, with no empty space before the first one and after the last one.
* `space-around` - empty space is equally distributed before and after each item. Two empty spaces are placed between two items (similiar to non-collapsing margins)
* `space-evenly`-  empty space is equally distributed before and after each item. A single empty space is placed between two items (similiar to non-collapsing margins)

![|200](css_flexbox_justify-content.png)

## Flexbox Cross Axis

The cross axis runs perpendicular to the main axis, meaning its default direction will be top-down.
The `align-items` and `align-self` properties control alignment of our flex items on the cross axis.

### align-items

``align-items`` can have following values:

*   `stretch` (initial value) - stretches the items along the **cross axis** to fill the container (still respect min-width/max-width)
*   `flex-start` - aligns the items along the start of the flexbox along the **cross axis**
*   `flex-end` - aligns the items along the end of the flexbox along the **cross axis**
*   `center` - aligns the items with their centers at the center of the flexbox along the **cross axis**
*   `baseline` - aligns the items with the baseline of their content (text) aligned along the **cross axis**

![|300](css_flex_align-items.svg)

For more informaton on the Flex Layout Model, refer to the [CSS Tricks Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

``align-content`` is only applicable to multi-line flex containers with active wrap.

## Gap

The ``gap`` property defines the empty spaces **between** the child flex items.

>[!TIP] ``gap`` can be thought of as mininum empty space between the items, as it will not have any effect if the empty space becomes  larger than the ``gap`` value through eg. ``justify-content:space-between``

The ``gap`` property defines the ``row-gap`` and ``column-gap``.

Code example:
```css
.container {
  gap: 10px; /* both gaps are now 10px*/
  gap: 10px 20px; /* row-gap is 10px, column gap is 20px */
  row-gap: 10px; /* row-gap is 10px*/
  column-gap: 20px; /* column-gap is 20px*/
}
```

![|300](css_flex_gap.svg)

### flex-wrap

The ``flex-wrap`` property defines the wrapping of items in a flex container. If there is no more space for an element, `nowrap` makes the element shrink, and `wrap` makes the element wrap into a new line.

``flex-wrap`` can have the following values:
*   `nowrap` (default): all flex items will be on one line, without wrapping
*   `wrap`: flex items will wrap onto multiple lines, from top to bottom.
*  `wrap-reverse`: flex items will wrap onto multiple lines from bottom to top.

![|300](css_flex-wrap.svg)

# Properties for the children elements

### align-self

The `align-self` property overrides the `align-items` property of the parent element. 

`align-self` can have the same values as `align-items`:
*   `stretch` (initial value) - stretches the item along the **cross axis** to fill the container (still respect min-width/max-width)
*   `flex-start` - aligns the item along the start of the flexbox along the **cross axis**
*   `flex-end` - aligns the item along the end of the flexbox along the **cross axis**
*   `center` - aligns the item with its center at the center of the flexbox along the **cross axis**
*   `baseline` - aligns the item with the baseline of its content (text) aligned along the **cross axis**

![|300](css_flex_align-self.svg)
