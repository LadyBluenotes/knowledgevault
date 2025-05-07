> Encodes all characters except: `A–Z a–z 0–9 - _ . ! ~ * ' ( )`

- Uses the same encoding method as [[encodeURI()]], but escapes a larger set of characters
- Good to be used on user-entered fields from forms sent _to_ the server
  - Will encode `&` symbols that may inadvertently be generated during data entry for character references or other characters that require encoding/decoding

```js
encodeURIComponent(uriComponent);
```

`uriComponent` - String to be encoded by URI component (a path, query string, fragement, etc)

- other values are converted to strings

Returns a new string representing the provided `uriComponent` encoded as a URI component

- Throws a `URIError` if `uriComponent` contains a lone surrogate
