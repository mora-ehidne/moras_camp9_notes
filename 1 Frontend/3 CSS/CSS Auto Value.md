# `width: auto`
on the `width` property, the `auto` value makes the element fill its parent horizontally, including the element's margins, border and padding. it is different to `100%`, as `100%`  sets `width` to be  exactly equal to the parent's width.
> **width**: auto = margin-l + border-l + padding-l + width + padding-r + border-r + margin-r
> 
>  but:
> 
> **width**: 100% = parent's width

# `height: auto`

on the `height` property, the `auto` value makes the element's vertical size equal to the height of it's content. In effect, that means:
> **height**: auto = **height**: content-fit

# `margin: auto`

## horizontal centering with ``margin: auto``

When both ``margin-left: auto`` and ``margin-right: auto``, the element gets centered in the parent.

## centering with ``margin: auto`` on `absolute` elements

For elements with `position: absolute`, setting `margin: auto` positions the element horizontally and vertically inside it's parent. For this to work, `width` and `height` have to be set.

## ``margin: auto`` in Flexbox

children of a `display:flex` parent can use `margin: auto` for centering or making the maximum possible distance from other elements or the edge of the parent.
eg. 
> a child with `margin-left: auto` will end up aligned to the right edge of the parent
> a child with `margin-right: auto` will end up aligned to the left edge of the parent
> a child with  `margin-left: auto` and `margin-right: auto` gets centered in the parent (minus any siblings to the left and right)
> a child with `margin-top: auto` will end up aligned to the bottom edge of the parent

## `auto` for positioning `absolute` elements

On absolutely positioned elements, the `auto` value positions the element the way it would have been positioned if it had `position: static`.

Example:
> `left: auto`
> `right: auto`
> `top: auto`
> `bottom: auto`

In the case of `left: auto` the element will be positioned with regard to the parent's padding and any sibling elements, while `left: 0` would align the left edge of the element with the left edge of the parent element.
