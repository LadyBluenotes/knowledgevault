- **Cross-origin resource sharing (CORS)** - HTTP-header based mechanism that allows a server to indicate any origins (domain, scheme, or port) other than its own from which a browser should permit loading resources
- relies on a mechanism that allows browsers to make a "preflight" request to the server hosting the cross-origin resource to check that the server will _permit_ the actual request
  - eg: JS front end using a fetch request on another domain
- browsers restrict cross-origin HTTP requests initiated by scripts _for security reasons_
- CORS supports secure cross-origin requests and data transfers between browsers and servers
  - Used in APIs such as `fetch()` or `XMLHttpRequest` to mitigate risks of cross-origin HTTP requests

## What requests use CORS

- `fetch()` or `XMLHttpRequest`
- **Web fonts** for cross-domain font usage in `@font-face` within CSS
- WebGL textures
- Images/videos drawn to a canvas using `drawImage()`
- CSS Shapes from images

## Functional overview

- adds new HTTP headers that let servers describe which origins are permitted to read that info from a web browser
- with HTTP requests that cause side-effects on server data (eg. `POST`, `GET`) the browsers "preflight" the request with the HTTP `OPTIONS` request method
  - once "approved" by the server, will send the actual request
- can also inform whether "credentials" (eg. cookies, HTTP Authentication) should be sent with requests
- failures result in errors for _security reasons_
  - specifics of error are _not available in JS_ it just knows that an error occurred

## Simple requests

- A simple request is one that meets all of the following:
  - One of: `GET`, `HEAD`, `POST`
  - only the following headers can be manually set:
    - `Accept`
    - `Accept-Language`
    - `Content-Language`
    - `Content-Type`
      - only combos allowed are:
        - `application/x-www-form-urlencoded`
        - `multipart/form-data`
        - `text/plain`
    - `Range`
  - if made using `XMLHttpRequest` object:
    - no event listeners are registered on the object returned by `XMLHttpRequest.upload`
    - no code has called `xhr.upload.addEventListener()` to add an event listener to monitor the upload
  - no `ReadableStream` object is used in the request
- don't trigger a CORS preflight
- `<form>` can submit simple requests to any origin so anyone writing a server must already be protecting against cross-site request forgery (CSRF - an attack that impersonates a trusted user and sends a website unwanted commands)
  - server must opt-in using `Acess-Control-Allow-Origin` to share the response with the script

## Preflight requests
