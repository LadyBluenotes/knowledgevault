---
title: Fetch
date created: Tuesday, April 22nd 2025, 11:02:31 am
date modified: Tuesday, April 22nd 2025, 11:28:48 am
---

# Fetch

- Provides a JS interface for accessing and manipulating parts of the protocol (eg. requests and responses)
- Provides a global `fetch()` method for fetching resources asynchronously across the network
- Is promise-based - provides a better alternative that can easily be used in service workers (Act as a proxy that sits between web applications, the browser, and the network (when available))
- Integrates advanced HTTP concepts such as CORS and other extensions to HTTP

```js
async function logMovies() {
  const response = await fetch("http://example.com/movies.json");
  const movies = await response.json();
  console.log(movies);
}
```

- `fetch()` takes one argument, the path to the resource you want to fetch, and does not _directly_ return the JSON response body
  - returns a promise that resolves with a `Response` object
    - does not directly contain actual JSON response body - sends a _representation_ of the entire HTTP response
    - To extract JSON body content, must use `json()` method which returns a _second promise_ that resolves with the result of parsing the response body text as JSON
- Can optionally accept a second parameter that allows you to control a number of different settings

```js
async function postData(url = "", data = {}) {
  // Default options are marked with *
  const response = await fetch(url, {
    method: "POST", // *GET, POST, PUT, DELETE, etc.
    mode: "cors", // no-cors, *cors, same-origin
    cache: "no-cache", // *default, no-cache, reload, force-cache, only-if-cached
    credentials: "same-origin", // include, *same-origin, omit
    headers: {
      "Content-Type": "application/json",
      // 'Content-Type': 'application/x-www-form-urlencoded',
    },
    redirect: "follow", // manual, *follow, error
    referrerPolicy: "no-referrer", // no-referrer, *no-referrer-when-downgrade, origin, origin-when-cross-origin, same-origin, strict-origin, strict-origin-when-cross-origin, unsafe-url
    body: JSON.stringify(data), // body data type must match "Content-Type" header
  });
  return response.json(); // parses JSON response into native JavaScript objects
}

postData("https://example.com/answer", { answer: 42 }).then((data) => {
  console.log(data); // JSON data parsed by `data.json()` call
});
```

## File uploads

```js
async function upload(formData) {
  try {
    const response = await fetch("https://example.com/profile/avatar", {
      method: "PUT",
      body: formData,
    });
    const result = await response.json();
    console.log("Success:", result);
  } catch (error) {
    console.error("Error:", error);
  }
}

const formData = new FormData();
const fileField = document.querySelector('input[type="file"]');

formData.append("username", "abc123");
formData.append("avatar", fileField.files[0]);

upload(formData);
```

### Multiple Files

```js
async function uploadMultiple(formData) {
  try {
    const response = await fetch("https://example.com/posts", {
      method: "POST",
      body: formData,
    });
    const result = await response.json();
    console.log("Success:", result);
  } catch (error) {
    console.error("Error:", error);
  }
}

const photos = document.querySelector('input[type="file"][multiple]');
const formData = new FormData();

formData.append("title", "My Vegas Vacation");

for (const [i, photo] of Array.from(photos.files).entries()) {
  formData.append(`photos_${i}`, photo);
}

uploadMultiple(formData);
```
