- Provides the ability to make HTTP requests
- Is a callback-based API
- Can operate on _any data_, not just "XML" format
- Can be used to upload / download files, track progress, etc.
- `fetch` is the more modern implementation but is used when:
  - Support is needed for existing scripts with `XMLHttpRequest`
  - Support for old browsers
  - Need to do something that `fetch` cannot (eg. track upload progress)

```js
let xhr = new XMLHttpRequest();

xhr.open(method, URL, [async, user, password]);
```

- `xhr.open` - _configures_ the request

  - `method` - HTTP-method (`GET`, `POST`, `PUT`, etc)
  - `URL` - URL to make request to (can be a URL object)
  - `async` - when set to `false`, request will be synchronous
  - `user`, `password` - login and password for basic HTTP auth (if required)

- `xhr.send([body])` - opens the connection and _sends the request_ to the server

```js
xhr.onload = function () {
  alert(`Loaded: ${xhr.status} ${xhr.response}`);
};
```

- `xhr.load` - when request is _complete_, response is fully downloaded
  - Even if HTTP status is `400` or `500`

```js
xhr.onerror = function () {
  // only triggers if the request couldn't be made at all
  alert(`Network Error`);
};
```

- `xhr.error` - when request _cannot be made_ (eg. network down, invalid URL)

```js
xhr.onprogress = function (event) {
  // triggers periodically
  // event.loaded - how many bytes downloaded
  // event.lengthComputable = true if the server sent Content-Length header
  // event.total - total number of bytes (if lengthComputable)
  alert(`Received ${event.loaded} of ${event.total}`);
};
```

- `xhr.progress` - triggers periodically while the response is being downloaded
  - reports _how much has been downloaded_
- `xhr.status` - HTTP status code
- `xhr.statusText` - HTTP status message in the form of a string (eg. `OK`, `Not Found`, `Forbidden`)
- `xhr.response` - server response body
- `xhr.timeout` - if the request does not succeed within a given time, it gets cancelled and `timeout` event triggers
- `xhr.responseType` - property to set the response format
  - `""` (default) - get as string
  - `"text"` - get as string
  - `"arrayBuffer"` - for binary data
  - `"blob"` - get as `Blob`
  - `"document"` - get as XML document or HTML document
  - `"json"` - get as JSON (parsed automatically)
- `xhr.getResponseHeader(name)` - get response header with the given `name` (except `Set-Cookie` and `Set-Cookie2`)
- `getAllResponseHeaders(name)` - get the response headers

```js
xhr.setRequestHeader("Content-Type", "application/json");
```

- `xhr.setRequestHeader` - allows both to send custom headers and read headers from the response
  - sets the request header with the given `name` and `value`

## File upload

```js
function importFile (
	file,
	setProgress,
	token
) {
	return new Promise((resolve, reject) => {
	    const data = new FormData();
	    data.append("file", file);
	    const xhr = new XMLHttpRequest();
	    xhr.upload.onprogress = (e) => {
	      if (e.lengthComputable) {
	        setProgress((e.loaded / e.total) * 100);
	      }
	    };
	    xhr.upload.ontimeout = (e) => resolve(e);
	    xhr.upload.onloadend = (e) => resolve(e);
	    xhr.upload.onerror = (err) => reject(err);
	    xhr.open(
	      "POST",
	      URL,
	      true
	    );
	    xhr.setRequestHeader("Authorization", token);
	    xhr.send(data);
	  });
	}
}
```

```js
function uploadImage(image, setProgress, token) {
  return new Promise((resolve, reject) => {
    const data = new FormData();
    data.append("image", image);

    const xhr = new XMLHttpRequest();
    xhr.open("POST", URL, true);
    xhr.setRequestHeader("Authorization", token);
    xhr.responseType = "json";

    xhr.upload.onprogress = (e) => {
      if (e.lengthComputable) {
        const progressPercent = (e.loaded / e.total) * 100;
        setProgress(progressPercent);
      }
    };

    xhr.onload = () => {
      if (xhr.status >= 200 && xhr.status < 300) {
        resolve(xhr.response);
      } else {
        reject("Error: " + xhr.status);
      }
    };

    xhr.onerror = () => reject("Network error");
    xhr.upload.onerror = (err) => reject(err);
    xhr.upload.ontimeout = () => reject("Timeout error");

    xhr.send(data);
  });
}
```
