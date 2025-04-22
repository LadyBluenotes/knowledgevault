## Formatting

### toLocaleDateString(_locales, options_)

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

### toLocaleString(_locales, options_)

Returns a string with a _language-sensitive_ representation of the _number_.

```jsx
const number = 3500;

console.log(number.toLocaleString()); // "3,500" if in `en-us`
```

`locales` and `options` may not be supported for all implementations because support for internationalization API is _optional_ and some _systems may not have the necessary data_. For local systems without internationalization support, `toLocaleString` always uses the _system locale_, which may not be the one you want.

`locales` will let you get the format of the language used in the user interface of application.

[`options`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toLocaleString#using_options) allows for customization - currency - Requires a currency code (e.g. `currency: "CAD"`) - style ("currency", "decimal", "percent")
