titler-node-server uses `Koa` as its middleware engine so first I recommend reading the [Koa guide to writing middleware](https://github.com/koajs/koa/blob/master/docs/guide.md).

## Create a middleware module

This is the minimum code to create a middleware module. A middleware module should export a function which returns a class extending `MiddlewareBase` (a superclass supplied by `ws`). The only required method is `middleware` which is passed the active `ws` configuration and must return a Koa middleware function. 

This example sets the response body to `'Hello'`. Save it to a file named `mw-example.js`.

```js
module.exports = MiddlewareBase => class Example extends MiddlewareBase {
  middleware (options) {
    return (ctx, next) => {
      ctx.response.body = 'Hello'
    }
  }
}
```

## Use a module

Launch your stack with the following command. By setting `--stack` you override the [built-in stack](Using-middleware#built-in-middleware-stack.md) with the middleware supplied. 

```
$ ws --stack mw-example.js
Serving at http://newbluefx.local:8100, http://127.0.0.1:8100, http://192.168.0.100:8100
```

Test you get the expected response.

```
$ curl http://127.0.0.1:8100
Hello
```

## Middleware options

You can parameterise middleware by adding a `optionDefinitions` method which should return one or more `option definitions`. This example defines an option called `message` which will be a string.

```js
module.exports = MiddlewareBase => class Example extends MiddlewareBase {
  optionDefinitions () {
    return [
      { name: 'message', type: String, description: 'A message to print.'}
    ]
  }
  middleware (options) {
    return (ctx, next) => {
      ctx.response.body = 'Hello'
    }
  }
}
```

If you view the `ws` usage guide you will now see your middleware and middleware options listed.

```
$ ws --stack mw-example.js --help
```

```js
module.exports = MiddlewareBase => class Example extends MiddlewareBase {
  optionDefinitions () {
    return [
      { name: 'message', type: String, description: 'A message to print.'}
    ]
  }
  middleware (options) {
    return (ctx, next) => {
      ctx.response.body = options.message
    }
  }
}
```

Now, we can configure our middleware to respond with a different message. 

```
$ ws --stack mw-example.js --message "🦆 🦆 🦆"
Serving at http://newbluefx.local:8100, http://127.0.0.1:8100, http://192.168.0.100:8100
```

Test we receive the correct response.

```
$ curl http://127.0.0.1:8100
🦆 🦆 🦆
```

## Description 

Notice how in the `--help` output your middleware is described as *`<description required>`*. To set a description, define a `description` method which returns a string.

```js
module.exports = MiddlewareBase => class Example extends MiddlewareBase {
  description () {
    return 'Demonstrating how a response can be controlled by config or command line.'
  }
  optionDefinitions () {
    return [
      { name: 'message', type: String, description: 'A message to print.'}
    ]
  }
  middleware (options) {
    return (ctx, next) => {
      ctx.response.body = options.message
    }
  }
}
```

## Verbose events

To send debug information to the `--verbose` output, you can emit a `verbose` event from any method within the module passing a key and value.

Convention within middleware modules is to send a `middleware.*.config` key with the active config.

```js
module.exports = MiddlewareBase => class Example extends MiddlewareBase {
  middleware (options) {
    return (ctx, next) => {
      this.emit('verbose', 'middleware.example.config', { message })
      ctx.response.body = options.message
    }
  }
}
```
