![NewBlueFX](img/NewBlueFX_logo.png)

By default, the server will accept requests from any origin. To restrict access to a specific origin use `--cors.origin`.

This example will only accept XHR/fetch requests from `http://127.0.0.1:8200`.

```js
    corsOrigin: "http://127.0.0.1:8200"
```

<!-- ```
$ ws --cors.origin http://127.0.0.1:8200
``` -->