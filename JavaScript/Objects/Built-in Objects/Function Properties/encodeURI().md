> Does not encode `-.!~*'()` as they are “unreserved marks”, which do not have a reserved purpose but are allowed in a URI “as is”

- encodes a URI by replacing each instance of certain characters by one, two, three, or four escape sequences representing the UTF-8 encoding of the character
  - will only be four escape sequences for characters composed of two surrogate characters
- compared to [[encodedURIComponent()]], this function encodes fewer characters, preserving those that are part of the URI syntax
- escapes by characters by UTF-8 code units, with each octet encoded in the format `%xx`, left-padded with 0 if necessary
  - lone surrogates in UTF-16 do not encode any valid Unicode character, they cause `encodeURI()` to throw a `URI`

```js
encodeURI(uri);
```

`uri` - a string to be encoded as a URI

Returns a new string representing the provided string encoded as a URI

- Throws a `URIError` if `uri` contains a lone surrogate
  - escapes all characters **except** for reserved characters (characters with special meaning)

```text
A–Z a–z 0–9 - _ . ! ~ * ' ( )

; / ? : @ & = + $ , #  <- Only escaped by encodeURIComponent()
```
