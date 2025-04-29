---
title: Events
date created: Tuesday, April 22nd 2025, 10:54:02 am
date modified: Tuesday, April 22nd 2025, 11:28:49 am
---

# Events

## Methods

| Event                 | Description                                                                                                                                         |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| `e.preventDefault()`  | When invoked, prevents the _default action_ associated with the event. (eg. bringing up context menu with right click while using `onContextMenu`). |
| `e.stopPropagation()` | _Stops_ the event from bubbling down (or up) the DOM hiearchy, preventing any other event listeners on parent elements from being triggered.        |

## DOM event properties

| Event                      | Description                                                                                                                               |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `e.target`                 | _Element_ that _triggered_ the event.                                                                                                     |
| `e.type`                   | _Type_ of event.                                                                                                                          |
| `e.clientX` or `e.clientY` | The horizontal or vertical _coordinates_ of the _mouse pointer_ when the _event occurred_, relative to the _viewport_.                    |
| `e.pageX` or `e.pageY`     | The horizontal or vertical _coordinates_ of the _mouse pointer_ when the event occurred, relative to the _document_ (includes scrolling). |
| `e.button`                 | Indicates which _mouse buttons_ are pressed when the event fired (0: main button, 1: auxillary, 2: secondary).                            |
| `e.relatedTarget`          | For `mouseOver` or `mouseOut` events, refers to the _element_ the mouse is coming from (`mouseOver`) or going to (`mouseOut`).            |

## Mouse events

| Event           | Description                                                                                             |
| --------------- | ------------------------------------------------------------------------------------------------------- |
| `oMouseEnter`   | Fires when the _pointer_ moves _onto_ the element but will not trigger (bubble) for child elements.     |
| `onMouseOver`   | Fires when the _pointer_ moves _onto_ the element.                                                      |
| `onMouseDown`   | Fires when a _mouse button_ is _pressed_ on the element.                                                |
| `onMouseUp`     | Fires when a _mouse button_ is _released_ on the element.                                               |
| `onMouseOut`    | Fires when the _pointer_ is moved _out_ of the element.                                                 |
| `onMouseLeave`  | Fires when the _pointer_ is moved _out_ of an element but does not trigger (bubble) for child elements. |
| `onClick`       | Fires when a mouse _clicks on_ the element.                                                             |
| `onContextMenu` | Fires when the _context menu_ is triggered (usually right click).                                       |
