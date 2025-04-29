---
title: aria-labelledby
date created: Tuesday, April 22nd 2025, 10:48:01 am
date modified: Tuesday, April 22nd 2025, 11:28:49 am
---

# aria-labelledby

Identifies the _element(s)_ that _label_ the element it is applied to.

- Has the _highest precedence_ when browsers calculate accessible names. It will _override_ other methods naming the element, including `aria-label` or even the element's contents.
- Takes a value as a _space separated id reference list_, which means you can combine more than one element into a _single accessible name_.
- Property order matters. When more than one is references, content from each is combined _in the order _
- Can include content from elements that _are not even visible_.
- Incorporates value of _input elements_
- Cannot be chained\*.
