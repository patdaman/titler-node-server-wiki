![NewBlueFX](img/NewBlueFX_logo.png)

<!-- ## Local targets

Your application requested `/css/style.css` but you'd like to serve `/css/new-theme.css`. The syntax is:

```
$ ws --rewrite '<source route> -> <destination route>'
```

Routes are specified using [Express routing syntax](https://expressjs.com/en/guide/routing.html). For example.

```sh
$ ws --rewrite '/css/style.css -> /css/new-theme.css'
```

Re-route any stylesheet under `/css/` to `/build/css/`.

```sh
$ ws --rewrite '/css/:stylesheet -> /build/css/:stylesheet'
```

Re-route the entire directory structure under `/css/` to `/build/css/` (this rewrites `/css/a` as `/build/css/a`, `/css/a/b/c` as `/build/css/a/b/c` etc.)

```sh
$ ws --rewrite '/css/* -> /build/css/$1'
```

### Proxied requests

If the `to` URL contains a remote host, local-web-server will act as a proxy - fetching and responding with the remote resource.

Mount the npm registry locally:
```sh
$ ws --rewrite '/npm/* -> http://registry.npmjs.org/$1'
```

Map local requests for repo data to the Github API:
```sh
$ ws --rewrite '/:user/repos/:name -> https://api.github.com/repos/:user/:name'
``` -->

## Config

Rewrite rules are stored in config as an array of `{ from: string, to: string }` objects.

```js
module.exports = {
  rewrite: [
    { from: "/css/*", "to": "/build/styles/$1" },
    { from: "/npm/*", "to": "http://registry.npmjs.org/$1" },
    { from: "/broken/*", "to": "http://localhost:9999" },
    { from: "/:user/repos/:name", "to": "https://api.github.com/repos/:user/:name" }
  ]
}
```