- Uses the same decoding algorithm as described in [[decodeURI()]]
- Decodes _all_ escape sequences, including those that are not created by [[encodedURIComponent()]] (`- . ! ~ * ' ( )`)

```js
decodeURIComponent(encodedURI);
```

`encodedURI` - encoded component of a URI

Returns a new string representing the decoded version of the given URI component

- Throws `URIError` if `encodedURI` contains a `%` not followed by two hexadecimal digits, or if the escape sequence does not encode a valid UTF-8 character
