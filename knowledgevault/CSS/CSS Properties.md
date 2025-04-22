## Display

Sets whether an element is treated as a _block_ or _inline-box_ and the layout used for its children.

| Values   | Description                                                                                                                                                                                 |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `block`  | Generates a _block box_, generating line breaks both before and after the element when in the _normal flow_                                                                                 |
| `inline` | Element generates one or more _inline boxes_ that do not generate line breaks _before or after_ themselves. In normal flow, the next element will be on the _same line_, if there is space. |
| `table`  | Elements that behave like HTML `<table>` elements. Defines a _block level_ box.                                                                                                             |
| `flex`   | Element behaves like a _block level_ element and lays out its contexts according to the _flexbox model_.                                                                                    |
| `grid`   | Element behaves like a _block level_ element and lays out its content according to the _grid model_.                                                                                        |

## Visibility

_Shows_ or _hides_ an element _without_ changing the layout of the document.

| Values                      | Description                                                                                                                                                                                                                                                           |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `visible`                   | Element is _visible_.                                                                                                                                                                                                                                                 |
| `hidden`                    | Element is _invisible_ or _not drawn_, but still _affects layout_ as normal. Descendants _will be visible_ if they have the `visibility` set to `visible`. Will be _removed_ from accessibility tree.                                                                 |
| `collapse` (table)          | For `<table>`, rows, columns, column groups, and row groups, the row(s) and column(s) are hidden and the space they would have occupied is _removed_ (as if `display: none`). Other rows and columns are still calculated as if cells in collapsed are still present. |
| `collapse` (flex)           | Annotations are hidden and the space they would have occupied is _removed_.                                                                                                                                                                                           |
| `collapse` (other elements) | Treated the same as `hidden`.                                                                                                                                                                                                                                         |

## Positioning

Sets how an element is _positioned_ in a document. the `top`, `right`, `bottom`, and `left` properties determine the final location of positioned elements.

| Values   | Description                                                                                                                                                                                                                                                                                                 |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Static   | Positioned according to _normal flow_ of the document. `top`, `right`, `bottom`, `left`, and `z-index` have _no effect_. _Default value._                                                                                                                                                                   |
| Relative | According to normal flow of document then offset _relative_ to itself on the values of `top`, `right`, `bottom`, and `left`. Offset does _not_ affect positioning of other elements.                                                                                                                        |
| Absolute | Element is _removed_ from normal document flow. Positioned relative to closest _positioned_ ancestor or to initial _containing block_. Final position is determined by values of `top`, `right`, `bottom`, and `left`                                                                                       |
| Fixed    | Element is _removed_ from normal document flow. _No space_ is created for the element in the page layout. Element is positioned relative to its _initial containing block_, which is the viewport in the case of visual media. Final position determined by values of `top`, `right`, `bottom`, and `left`. |
| Sticky   | Positioned according to normal document flow, and then offset it to its _nearest scrolling ancestor_ and _containing block_.                                                                                                                                                                                |
