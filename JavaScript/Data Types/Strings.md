---
title: Strings
date created: Tuesday, April 22nd 2025, 11:02:12 am
date modified: Tuesday, April 22nd 2025, 11:28:48 am
---

# Strings

- How text-data is stored.
- International format is always `UTF-16`
- Are immutable

## Special characters

- All special characters start with a backslash character `\` (“escape character”)
  - Escaped quotes are needed when inserting a quote into a same-quoted string

```javascript
alert("I'm the Walrus!"); // I'm the Walrus!
```

| Character            | Description                                                                                                                                                                                              |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `\n`                 | New line                                                                                                                                                                                                 |
| `\r`                 | In Windows text files a combination of two characters `\r\n` represents a new break, while on non-Windows OS it’s just `\n`. That’s for historical reasons, most Windows software also understands `\n`. |
| `\'`, `\"`, `` \` `` | Quotes                                                                                                                                                                                                   |
| `\\`                 | Backslash                                                                                                                                                                                                |
| `\t`                 | Tab                                                                                                                                                                                                      |
| `\b`, `\f`, `\v`     | Backspace, Form Feed, Vertical Tab – mentioned for completeness, coming from old times, not used nowadays (you can forget them right now).                                                               |

## Length

- A property therefore it is just `str.length` and **not** `str.length()`

## Accessing characters

### Square brackets

- Using square brackets `[pos]` will give you a character at a certain position
- Square brackets return `undefined` for negative indexes

```javascript
let str = `Hello`;

// first character
str[0]; // H

// last character
str[str.length - 1]; // 0
```

## `.at(pos)`

- `.at(-1)` accesses last character
- `.at(-2)` accesses one before it

```javascript
let str = `Hello`;

// first character
str.at(0); // H

// last character
str.at(-1); // 0
```

## Changing case

### `.toLowerCase()`

```js
"Interface".toLowerCase(); // interface
```

### `.toUpperCase()`

```js
"Interface".toUpperCase(); // INTERFACE
```

## Searching for a substring

### `.indexOf(substr, pos)`

- Looks for the `substr` in a string
  - Can look starting at a given position `pos`
- Search is case sensitive

```js
let str = "Widget with id";

str.indexOf("Widget"); // 0, since at beginning
str.indexOf("widget"); // -1, not found since case sensitive

str.indexOf("id"); // 1, "id" first found at position 1 within "Widget"

str.indexOf("id", 2); // 12, since it is now looking for "id" after the first
```

### `.lastIndexOf(substr, pos)`

- Searches from the end of a string to its beginning, therefore lists all occurrences in reverse order

```js
"Widget with id".lastIndexOf("id"); // 12
```

### `.includes(substr, pos)`

- Returns `true` or `false` depending on whether a string contains the `substr`

```js
"Widget with id".includes("Widget"); // true

"Hello".includes("Bye"); // false
```

### `.startsWith(substr, pos)`

- Determines whether the string begins with characters of a specified string, returning `true` or `false` as appropriate

```js
"Saturday night plans".startsWith("Sat"); // true

"Saturday night plans".startsWith("Sat", 3); // false
```

### `.endsWith(substr, pos)`

- Determines whether the string begins with characters of a specified string, returning `true` or `false` as appropriate

```js
"Saturday night plans".endsWith("plans"); // true

"Saturday night plans".endsWith("night"); // false
```

## Getting a substring

### `.slice(start [, end])`

- Returns the part of the string from `start` to (but not including) `end`
- Negative values mean position is counted from the string end

```js
let str = "stringify";

str.slice(0, 5); // 'strin', the substring 0 to 5 (not including 5)
str.slice(0, 1); // 's', from 0 to 1, but not including 1

str.slice(2); // 'ringify', from 2nd position to end
str.slice(-4, -1); // 'gif'
```

### `.substr(start [, end])`

- Returns part of string **between** start and end (not including end)
  - Similar to `.slice()` but `start` can be greater than `end`
  - Negative numbers are treated as `0`
- May not be supported by non-browser environments

```js
let str = "stringify";

str.substring(2, 6); // "ring"
str.substring(6, 2); // "ring"
```

## Compare strings

- Strings are compared character-by-character in alphabetical order
  - Lowercase is always greater than uppercase
  - Letters with diacritical marks are “out of order” which can lead to strange results

```js
"a" > "Z"; // true

"Österreich" > "Zealand"; // true
```

### `str.localeCompare(str2)`

- Returns an integer indicating whether `str` is less, equal, or greater than str2 based on the language rules:
  - Negative number if `str` < `str2`
  - Positive number if `str` > `str2`
  - `0` if equivalent

```js
"Österreich".localeCompare("Zealand"); // -1
```

## String codes

- Strings are encoded using UTF-16
  - Each character has a corresponding numeric code
  - Different cased letters have different codes
    - Capital before lower cased

### `.codePointAt(pos)`

- Returns a decimal number representing the code for the character at position `pos`

```js
"Z".codePointAt(0); // 90
"z".codePointAt(0); // 122
```

### `.fromCodePoint(code)`

Creates a character by its numeric `code`

```js
String.fromCodePoint(90); // Z
```

- Can loop through codes starting at 65 to get the latin alphabet and some of the following characters by making a string of them

```js
let str = "";

for (let i = 65; i <= 220; i++) {
  str += String.fromCodePoint(i);
}
alert(str);
// Output:
// ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefghijklmnopqrstuvwxyz{|}~
// ¡¢£¤¥¦§¨©ª«¬­®¯°±²³´µ¶·¸¹º»¼½¾¿ÀÁÂÃÄÅÆÇÈÉÊËÌÍÎÏÐÑÒÓÔÕÖ×ØÙÚÛÜ
```

## Formatting

#### `.toLocaleDateString(_locales, options_)`

Returns a string with a _language-sensitive_ representation of the date portion of the _specified date_ in the user agent's time zone.

```js
const event = new Date();
const options = {
  // these can all change
  weekday: "long",
  year: "numeric",
  month: "long",
  day: "numeric",
};
console.log(event.toLocaleDateString(`en-US`, options)); // the `en-us` can vary
// Logged: Wednesday, October 25, 2023
```

Optional [locales](https://www.w3schools.com/jsref/jsref_tolocalestring_number.asp#:~:text=Description-,locales,-Try%20it).

#### `.toLocaleString(_locales, options_)`

Returns a string with a _language-sensitive_ representation of the _number_.

```jsx
const number = 3500;

console.log(number.toLocaleString()); // "3,500" if in `en-us`
```

`locales` and `options` may not be supported for all implementations because support for internationalization API is _optional_ and some _systems may not have the necessary data_. For local systems without internationalization support, `toLocaleString` always uses the _system locale_, which may not be the one you want.

`locales` will let you get the format of the language used in the user interface of application.

[`options`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toLocaleString#using_options) allows for customization - currency - Requires a currency code (e.g. `currency: "CAD"`) - style ("currency", "decimal", "percent")
