---
title: Combobox
date created: Tuesday, April 22nd 2025, 10:49:51 am
date modified: Tuesday, April 22nd 2025, 11:28:49 am
---

# Combobox

- Input widget that has an _associated popup_
  - Popup enables users to choose a value for the input _from a collection_
    - May be a [listbox](Listbox.md), [grid](Grid.md), [tree](Tree%20View%20Pattern.md), or [dialog](Dialogs.md)
- Some implementations, popup presents values, while in others they present _suggested_ values.
- Many implementations allow a third, optional element – graphical `open` button adjacent to combobox, which indicates availability of the popup
- Supports several optional behaviours
  - One that shapes the most is text input
    - Allow users to type and edit text in the combobox
      - Referred to as **editable**
      - May allow users to either input _any_ arbitrary value or may restrict its value to a discrete set of allowed values
        - Tying input would serve to filter suggestions presented in the popup
    - If not, it is referred to as **select only**
      - Only way users can set a value is by selecting a value in the popup
- Popup is hidden by default (ie. collapsed)
  - Conditions trigger expansion (display) are specific to each implementation. Possible triggers include:
    - Displayed when the `Down arrow` key is pressed or `Open` button is activated
      - If combobox is editable and contains a string that does not match an allowed value, expansion _does not_ occur
    - It is displayed when the combobox receives focus, even if combobox is editable and empty
    - If editable, popup is displayed only if a certain number of characters are typed and those characters match _some portion_ of one of the suggested values
- Combobox widgets are useful for acquiring user input in 2 scenarios:
  - Value must be one of a predefined set of allowed values
  - An arbitrary value is allowed, but it is advantageous to suggest possible values to users
- The nature of possible values present by a popup and the way they are presented is called **autocomplete behaviour**.
  - There are 4 forms:
    - **No autocomplete**: is editable and, when popup is triggered, suggested values it contains are the same regardless of characters typed in the box
    - **List autocomplete with manual selection**: when the popup is triggered, suggested values are present. If editable, suggested values complete or logically correspond to the characters typed.
      - Character string user has typed will become value of combobox unless user selects a value in popup
    - **List autocomplete with automatic selection**: Combobox is editable and, when triggered, presents suggested values that complete or logically correspond to characters typed. _First_ selection is automatically **highlighted as selected**.
      - Automatically selected suggestion becomes value of the combobox when the combobox loses focus unless user chooses a different suggestion or changes the character string
    - **List with inline autocomplete**: Same as list with automatic selection with on additional feature - portion of selected suggestion that has _not_ been typed, a completion string, appears **inline** after input cursor in combobox.
      - Inline completion is **visually highlighted** and has a _selected_ state

Resources:

- https://www.w3.org/WAI/ARIA/apg/patterns/combobox/
