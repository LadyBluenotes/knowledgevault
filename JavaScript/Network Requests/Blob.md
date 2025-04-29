---
title: Blob
date created: Tuesday, April 22nd 2025, 11:04:35 am
date modified: Tuesday, April 22nd 2025, 11:28:48 am
---

# Blob

- the `Blob` object represents a blob which is a file-like object of immutable, raw data
- can read as text or binary data or can be converted into a `ReadableStream` so its methods can be used for processing the data
- can represent data that isn't necessarily in JS-native format

## Create a blob

```js
const obj = { hello: "world" };
const blob = new Blob([JSON.stringify(obj, null, 2)], {
  type: "application/json",
});
```

## Extracting data from a blob

### FileReader

```js
const reader = new FileReader();
reader.addEventListener("loadend", () => {
  // reader.result contains the contents of blob as a typed array
});
reader.readAsArrayBuffer(blob);
```

### Response

```js
const text = await new Response(blob).text();
```

### `Blob.text()`

```js
const text = await blob.text();
```
