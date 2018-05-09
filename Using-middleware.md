[![NewBlueFX](img/NewBlueFX_logo.png)](Home.md)

Each incoming request passes through the middleware stack configured for your server. If the built-in stack (described in the table below) does not meet your needs you can supply your own using `--stack`.

## Built-in middleware stack

If you do *not* set the `--stack` options the following default stack will be used. It is intended to cover the majority of typical development needs.

| Name               | Description |
| ------------------ | ---- |
| ↓ [Basic Auth]() | Password-protect a server using Basic Authentication |
| ↓ [Body Parser]() | Parses the request body, making `ctx.request.body` available to downstream middleware.|
| ↓ [Request Monitor]() | Feeds traffic information to the `--verbose` output.|
| ↓ [Log]() | Outputs an access log or stats view to the console.|
| ↓ [Cors]() | Support for setting Cross-Origin Resource Sharing (CORS) headers |
| ↓ [Json]() | Pretty-prints JSON responses. |
| ↓ [Rewrite]() | URL Rewriting. Use to re-route requests to local or remote destinations.|
| ↓ [Blacklist]() | Forbid access to sensitive or private resources|
| ↓ [Conditional Get]() | Support for HTTP Conditional requests.|
| ↓ [Mime]() | Customise the mime-type returned with any static resource.|
| ↓ [Compress]() | Compress responses using gzip.|
| ↓ [Mock Response]() | Mock a response for any given request.|
| ↓ [SPA]() | Support for Single Page Applications.|
| ↓ [Static]() | Serves static files.|
| ↓ [Index]() | Serves directory listings.|

## How it works

titler-node-server uses [Koa](https://github.com/koajs/koa/) for its middleware stack. See [here](https://github.com/koajs/koa/blob/master/docs/guide.md) for a guide explaining how Koa middleware works, why middleware order is significant etc. See [here](https://github.com/koajs/koa/blob/master/docs/api/context.md) for the `ctx` object documentation.

## Using a personalised stack

A personalised stack can be created by passing middleware module names to `--stack`. If all you need is to serve static files, the following command is all you need.

```js
  stack: "static",
```
<!-- ```
$ ws --stack lws-static
Serving at http://newbluefx.local:8000, http://127.0.0.1:8000, http://192.168.0.100:8000
``` -->

You may now browse any file in the current folder, e.g. http://127.0.0.1:8000/README.md.

### Third party middleware

If you installed a third-party middleware module into your project you may include it using the same syntax.

```sh
$ npm install another-middleware --save-dev
```
Add to the stack:
```js
  stack: [ ... "another-middleware", ... ],
```
<!-- ```
$ npm install another-middleware --save-dev
$ ws --stack another-middleware
Serving at http://newbluefx.local:8000, http://127.0.0.1:8000, http://192.168.0.100:8000
``` -->

If your project includes the source for a middleware module you may include it by file name.

```js
  stack: [ ... "./src/server/middleware/another-middleware.js", ...]
```
<!-- ```
$ ws --stack ./lib/another-middleware.js
Serving at http://newbluefx.local:8000, http://127.0.0.1:8000, http://192.168.0.100:8000
``` -->

## Middleware order

Middleware order is significant. An incoming request is processed by each middleware in turn, in the order they were supplied to `--stack`. For example, if you are using a middleware which processes the body of a request then it must be placed downstream of the middleware which parses the body of a request (typically `body-parser`). If you are experiencing unexpected issues with your stack, double-check middleware is supplied in the correct order.

## Middleware options

<!-- Each middleware module may define command-line options. For example, the `static` module defines several command-line options - you can view them with this command:

```
$ ws --stack static --help
```

### Using config -->

Your preferred stack can be written to the config file like this.

```js
module.exports = {
  stack: [ 'spa', 'static', 'index' ]
}
```

<!-- ### View built-in middleware list

If you need reminding of the built-in middleware modules names (in order to pass one or more of them to `--stack`), you can print them with this command.

```
$ ws middleware-list
[ 'body-parser',
  'request-monitor',
  'log',
  'cors',
  'json',
  'rewrite',
  'blacklist',
  'conditional-get',
  'mime',
  'compress',
  'mock-response',
  'spa',
  'static',
  'index' ]
``` -->