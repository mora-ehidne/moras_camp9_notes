# How the `position` property works


## The `position` property, layout and stacking


| Value | Layout Behaviour | Stacking Context |
| --- | --- | --- |
|  `static` (default) | partakes in layout as expected |  stays in its parent's stacking context |
|  `absolute` | removed from the layout, the space it would have normally taken gets removed from the layout | creates a new stacking context |
| `fixed` |  removed from the layout, the space it would have normally taken gets removed from the layout | creates a new stacking context |
| `sticky` |  removed from the layout, the space it would have normally taken stays in the layout | creates a new stacking context |
| `relative`|  removed from the layout, the space it would have normally taken stays in the layout | creates a new stacking context |

>[!INFO] If an element with `position: absolute` has a parent with a position other than `static`, it is positioned relative to the first parent with a position other than `static`. If such an element has no parents with a position other than `static`, it is positioned relative to the viewport. In this case, the element is positioned as if it had `position: fixed`, but it scrolls normally with the page.

## `top`, `right`, `left` and `bottom` properties

The `top`, `right`, `left` and `bottom` properties have different effects based on the element's `position` property:

| position: | Effect | value expressed in `%` |
| --- | --- | --- |
|  `static` |  no effect |  no effect |
|  `absolute` | positions the element relative to the first parent with a `position` other than `static`. (eg. `top:0` aligns the element's upper edge to the upper edge of the parent). <br><br> If no parent with a `position` other than `static` exists, it behaves like in `position:fixed`. | relates to the height and width of the parent. <br><br> If no parent with a `position` other than `static`exists, it relates to the height and width of the viewport. |
| `fixed` |  positions the element relative to the viewport. (eg. `top:0` aligns the element's upper edge to the upper edge of the viewport)  | relates to the height and width of the viewport |
| `sticky` | no effect until the specified offset position is met by scrolling. After the offset position is met, the element is positioned relative to the viewport, like `position:fixed` | relates to the height and width of the viewport |
| `relative`|  positions the element relative to its initial position | relates to the height and width of the parent |
 