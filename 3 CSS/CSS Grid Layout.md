The grid layout system is similiar to the [[CSS Flexbox layout|flexbox layout system]], but while flexbox is one-directional, grid is explicitly two-dimensional.

In order to use the *grid layout*, the parent element has to have its display property set to `grid`.

# Basic grid terminology

* grid container - the parent element of all the grid items, has `display:grid`
* grid items - the direct children of a grid container
* grid line - horizontal (row grid line) or vertical (column grid line), start at 1, ends at amount of rows/columns +1
* grid cell - the basic unit of the grid, it is the space between two adjecent horizontal and vertical grid lines
* grid track - a single row or column, the space between two adjecent horizontal or vertical grid lines
* grid area - a rectangular space composed of a single or several grid cells

# Grid container properties

## `grid-template`

* `grid-template-columns` is used to define the number of columns and their widths.
* `grid-template-rows` is used to define the number of rows and their heights.
* `grid-template` is the shorthand property, which sets the `grid-template-rows` and `grid-template-columns`, separated by a forward slash `/`.

```css
.grid-parent{
grid-template-columns: 100px 200px; /* defines two columns, first one has the width of 100px, the second one 200px */
grid-template-rows: 300px 150px 200px; /* defines three rows, first one has the height of 300px, the second one 150px, and the third one 200px */
grid-template: 100px 200px / 300px 150px 200px; /* same functionality, just set with the shorthand */
}
```

>[!WARNING] If there are more elements than can fit in the number of grid elements defined by `grid-template-columns` and `grid-template-rows`  , a new row with default height will be created to home the excess elements.

### `repeat(amount, size)`

The `repeat` function can be used as the value of the `grid-template-columns` and `grid-template-rows` properties. It defines how many columns/rows should be defined and what size they are.

```css
.grid-parent{
grid-template-columns: repeat(5, 200px); /* defines 5 columns, of which all have a width of 200px  */
grid-template-rows: repeat(10, 300px); /* defines 10 rows, of which all have a height 300px */
}
```


### The fraction unit `fr`

For the `grid-layout` properties, a special unit can be used: the fraction unit `fr`. It is calculated as a fraction of the parent's available width (for columns) or parent's available height (for rows).

```css
.grid-parent{
grid-template-columns: 1fr 2fr 1fr; /* divides the parent's width in 5 (1+2+1) fractions, then assigns 1 of those fractions to the first column width, 2 to the second, and 1 to the third*/
}
```

## `grid-gap`

The `grid-gap` acts similiarly to the flex `gap` property.

`grid-row-gap` - defines the gap size between rows
`grid-column-gap` - defines the gap size between columns
`grid-gap` - defines both the row and column gap, written with a space in between. If a single value is assigned, it defines both the row and column gaps

```css
.grid-parent{
grid-row-gap: 1px;
grid-column-gap: 9px;
grid-gap: 1px 9px; /* sets row gap to 1px, column gap to 9px */
grid-gap: 9px; /* sets both row and column gap to 9px */
}
```

## `justify-content`

The `justify-content` property aligns or stretches the columns in a grid.
Possible values are:
* `stretch` - stretches the column width  


# Grid item properties

## `grid-column` and `grid-row`

`grid-column-start` - a number defining the starting vertical (column) line of the item
`grid-column-end` - a number defining the ending vertical (column) line of the item
grid
`grid-column` - shorthand for both the `-start` and `-end` value, sperated with a forward slash `/`

`grid-row-start` - a number defining the starting horizontal (row) line of the item
`grid-row-end` - a number defining the ending horizontal (row) line of the item
grid
`grid-row` - shorthand for both the `-start` and `-end` value, sperated with a forward slash `/`

>[!TIP] The `span` keyword can be used instead of specifying the exact starting or ending line, 

*Explicit grid items* are items that have defined starting and ending points in their `grid-column` and `grid-row`.
*Implicit grid items* are the grid items that do not have starting and ending points defined in their `grid-column` and `grid-row`, but instead use a *span* value.

Usually, all grid items will be either set either explicitly or implicitly, with the implicit mode being the primary way of doing grids.
