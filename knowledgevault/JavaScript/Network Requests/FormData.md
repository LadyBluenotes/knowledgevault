- Provides a way to construct a set of key/value pairs representing form fields and their values
  - Can be sent using `fetch()`, `XMLHttpRequest.send()`

```js
let formData = new FormData([form]);
formData.append(name, value);
```

- `formData.append` - appends a new value onto an existing key inside a `FormData` object, or adds the key if it does not already exist
- `formData.delete` - deletes a key/value pair from a `FormData` object
- `formData.entries` - returns an iterator that iterates through all key/value pairs contained in the `FormData`
- `formData.get` - returns the first value associated with a given key from within a `FormData` object
- `formData.getAll` - returns an array of all values associated with a given key from within a `FormData`
- `formData.has` - returns whether a `FormData` object contains a certain key
- `formData.set` - sets a new value for an existing key inside a `FormData` object, or adds the key/value if it does not already exist
- `formData.values` - returns an iterator that iterates through all values contained in the `FormData`
