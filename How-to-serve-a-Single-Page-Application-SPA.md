[![NewBlueFX](img/NewBlueFX_logo.png)](Home.md)


### Serving a Single Page Application (an app with client-side routing, e.g. a React or Angular app) is as trivial as specifying the name of your single page:

```js
    directory: "src/controls/",  <-- not required if located in root dir
    spa: "index.html",
```
<!-- ```sh
$ ws --spa index.html
Serving at http://newbluefx.local:8000, http://127.0.0.1:8000, http://192.168.0.100:8000
``` -->

By default, requests for typical SPA paths (e.g. `/user/1`, `/login`) return `404 Not Found` as a file at that location does not exist. By marking `index.html` as the SPA you create this rule:

*If a static file is requested (e.g. `/css/style.css`) then serve it, if not (e.g. `/login`) then serve the specified SPA file and handle the route client-side.*

### Custom static file test

By default, any path containing a `.` (full stop) is considered a static file. To change this, pass a regular expression to `--spa.asset-test`.

For example, this command will treat only files ending with `.json` as a static resource, otherwise the SPA will be returned.

```js
    directory: "src/controls/",
    spa: "index.html",
    spaAssetTest: "\.json$"
```
<!-- or
```sh
    $ ws --spa index.html
``` -->