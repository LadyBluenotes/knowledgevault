- Decodes the URI by treating each escape sequences in the form `%xx` as one UTF-8 unit (one byte)
  - By reading the first escape sequence, `decodeURI()` can determine how many more escape sequences to consume
  - If it fails to find the expected number of sequences, or if escape sequences don’t encode a valid UTF-8 character, `URIError` is thrown
- Decodes _all_ escape sequences except if the escape sequences encodes the following: `; \ ? : @ & = + $ , #` because they are part of the URI syntax

```js
decodeURI(encodedURI);
```

`encodedURI` - complete, encoded URI

Returns a new string representing the _unencoded_ version of the given URI

- Throws `URIError` if `encodedURI` contains a `%` not followed by two hexadecimal digits or if the escape sequence does not encode a valid UTF-8 character
