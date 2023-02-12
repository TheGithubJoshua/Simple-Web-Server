
# Simple Web Sevrer


### Static web site

Running `ws` without any arguments will host the current directory as a static web site. Navigating to the server will render a directory listing or your `index.html`, if that file exists.

```sh
$ ws
Listening on http://mbp.local:8000, http://127.0.0.1:8000, http://192.168.0.100:8000
```

### Single Page Application

Serving a Single Page Application (an app with client-side routing, e.g. a React or Angular app) is as trivial as specifying the name of your single page:

```sh
$ ws --spa index.html
```

With a static site, requests for typical SPA paths (e.g. `/user/1`, `/login`) would return `404 Not Found` as a file at that location does not exist. However, by marking `index.html` as the SPA you create this rule:

*If a static file is requested (e.g. `/css/style.css`) then serve it, if not (e.g. `/login`) then serve the specified SPA and handle the route client-side.*


### URL rewriting and proxied requests

Another common use case is to forward certain requests to a remote server.

The following command proxies blog post requests from any path beginning with `/posts/` to `https://jsonplaceholder.typicode.com/posts/`. For example, a request for `/posts/1` would be proxied to `https://jsonplaceholder.typicode.com/posts/1`.

```sh
$ ws --rewrite '/posts/(.*) -> https://jsonplaceholder.typicode.com/posts/$1'
```

### HTTPS and HTTP2

For HTTPS or HTTP2, pass the `--https` or `--http2` flags respectively. [See the wiki](https://github.com/lwsjs/local-web-server/wiki) for further configuration options and a guide on how to get the "green padlock" in your browser.

```
$ ws --http2
Listening at https://mba4.local:8000, https://127.0.0.1:8000, https://192.168.0.200:8000
```

