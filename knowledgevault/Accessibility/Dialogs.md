## Dialog

### About

- Dialog is a window overlaid on either a _primary window_ or another _dialog window_
- Are inert - user **cannot** interact with content outside an active dialog - Inert content should be _visually obscured_ or _dimmed_ - Make it difficult to discern

  > [!info]
  > Some implementations – attempts to interact with the inert content cause the dialog to close

- Similar to non-modal dialogs:
  - Modal dialogs contain their _tab sequence_ (`Tab` & `Shift + tab`) do not move focus **outside** the dialog
- _Modal_ dialogs **do not** provide means for moving keyboard focus outside the dialog window **without** closing the dialog
- [[#Alert Dialog]] is a special-case dialog designed for dialogs that _divert the users’ attention_ for a brief, important message

### Features

- On small screens, must fill 100% of the screen
- Completely cover background window
  - Hide background movement (can occur on some mobile devices when scrolling content _inside_ the dialog)
- Focus and accessible descriptions set based on the **content** of each dialog
  - Initial **focus** set on _first input_
  - When **closes** as a result of the `Cancel` action, user’s point of regard is maintained by returning focus to button that opened the modal

### Keyboard interaction

- Values greater than 0 are **strongly discouraged**
- When a dialog opens, focus is moved to an element _inside_ the dialog
- `Tab`
  - Moves focus to the _next_ tabbable element inside dialog
  - If on **last** tabbable element, moves focus to the _first_
- `Shift + tab`
  - Moves focus to _previous_ tabbable element in dialog
  - If focus is on **first**, moves focus to the _last_
- `Esc`
  - Closes the dialog

> [!info]
> Focus must move to an element contained within the dialog - should initially be set on the first _focusable_ element - Most appropriate focus depends on nature and size of content: - With semantic structures (eg. lists, tables, multiple paragraphs), that need to be perceived in order to understand (eg. content would be difficult to understand in a single, unbroken string), advisable to use `tabindex='-1'` to a static element to start the content and initially focus that element. - Makes it easier for assistive tech to read content by navigating semantic structures - Advisable to omit `aria-describedby` to dialog container in this scenario - If content is large enough that the first interactive element is _out of view_, advisable to add `tabindex='-1'` to a static element at the _top_ of the dialog (such as title or first paragraph) and initially focus there - If dialog contains final step in process that is **not easily reversible** (eg. deleting data, completing financial transaction), set focus on _least destructive_ action (especially if undoing is difficult or impossible). - [[#Alert Dialog]] is often used in such circumstances - If dialog is limited to interactions that either provide additional info or continue processing, may be advisable to set focus to element most likely to be used _frequently_, such as `Ok` or `Continue` button
>
> When dialog closes, focus returns to the element that _invoked the dialog_ unless: - Invoking element no longer exists - Focus on another element that provides logical work flow - Work flow design includes the following conditions that make focusing a different element a more logical choice: 1. Unlikely user needs to immediately re-invoke dialog 2. Task completed in dialog is directly related to _subsequent step_ in the workflow
>
> Strongly recommended that the tab sequence of all dialogs include a _visible element_ with the role `button` that **closes** the dialog (eg. close icon or cancel button)

### Roles, states, properties

- Element serves as the dialog container has `role="dialog"`
- All elements required to operate dialog are descendants of the element that has the `role="dialog"`
- Dialog container element has `aria-modal` set to `true`
- Dialog has either:
  - Value set by `aria-labelledby` that refers to a _visible_ dialog title
  - Label specified by `aria-label`
- `aria-describedby` is set on the element with the `dialog` role to indicate which element(s) in the dialog contain content that describes the primary purpose or message of the dialog
  - Helps screen readers announce description along with dialog title and initially focused element when dialog opens
    - Helpful only when descriptive content is simple and can be easily understood _without_ structural info
  - Advisable to admit `aria-describedby` if dialog content includes **semantic structures** that need to be perceived in order to easily understand the content

## Modal Dialog

### About

- Marking a modal by setting `aria-model` to `true` can prevent users of some assistive technology from perceiving content _outside_ the dialog.
  - Can negatively impact the experience if marked a modal but _doe snot behave as a modal for other users_

### Criteria

- Mark only when both are true:
  - Application code prevents all users from interacting in any way with content outside of it
  - Visual styles obscures the content outside of it
- `aria-model` _replaces_ `aria-hidden` for informing assistive technologies that content _outside_ a dialog is inert
  - Legacy implementations (where `aria-hidden` is used), it is important that:
    - `aria-hidden` is set to `true` on each element containing a portion of the inert layer
    - The dialog element is _not_ a descendent of any element that has `aria-hidden` set to `true`

## Alert Dialog

### About

- Divert user’s workflow to communicate an important message and acquire a _response_
- Enables assistive technology and browsers to distinguish between alert dialogs and other ones
  - Option of giving alert dialogs special treatment (eg. system alert sound)
- Examples:
  - Action confirmation prompt
  - Error message

### Roles, states, properties

- Contains all the elements of the [standard dialog](#Roles,%20states,%20properties)
  - Includes alert message, any dialog buttons and the role `alertdialog`
- Element with `role='alertdialog'` has either:
  - A value for `aria-labelledby` that refers to the element containing the title of the dialog _if the dialog has a visible label_
  - A value for `aria-label` if the dialog does _not_ have a visible label
- Has a value set for `aria-describedby` that refers to the element containing the alert message

Resources:
https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/examples/dialog/
