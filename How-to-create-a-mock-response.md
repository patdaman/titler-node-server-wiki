If you need a server-side resource or service which doesn't yet exist or is out of reach, the goal of mocks is to enable you to quickly create one.

## Consuming mock modules

If you have `mock-response` present in your stack (included by default) you will have the option to pass one or more mock module paths to `--mocks`. 

```
$ ws --mocks my-mocks-module.js
```

## Creating a mock module

This is the minimum code required for a mock module, you can use it as a boilerplate template. Replace `MyMockModule` with a more useful name. The `options` argument will contain the currently active `ws` config.

```js
module.exports = MockBase => class MyMockModule extends MockBase {
  mocks (options) {
    return []
  }
}
```

### `route` and `responses`

The `mocks` method must return one or more objects, each with two properties - `route` and `responses`. The route value can use any Express-style routing syntax, described [here](https://expressjs.com/en/guide/routing.html) in the "Route paths" and "Route parameters" sections.

```js
module.exports = MockBase => class MyMockModule extends MockBase {
  mocks (options) {
    return [
      {
        route: '/pizzas/:id',
        responses: []
      }
    ]
  }
}
```

### `response`

The `responses` property must contain one or more objects, each with a `response` property. The `response` property value will be written directly to the Koa `ctx` object, meaning on this object you can set any of the standard [`ctx` response values](https://github.com/koajs/koa/blob/master/docs/api/context.md#response-aliases). The properties you will set must commonly are `body`, `status` and `type`.

This example will respond with `200` (the default statusCode) and the body `Margerita` to any request for `/pizzas/:id`, e.g. `/pizzas/1`.

```js
module.exports = MockBase => class MyMockModule extends MockBase {
  mocks (options) {
    return [
      {
        route: '/pizzas/:id',
        responses: [
          {
            response: {
              body: 'Margerita'
            }
          }
        ]
      }
    ]
  }
}
```

### response `type`

We can convert our response to return JSON.

```js
module.exports = MockBase => class MyMockModule extends MockBase {
  mocks (options) {
    return [
      {
        route: '/pizzas/:id',
        responses: [
          {
            response: {
              type: 'json',
              body: '{ "name": "Margerita" }'
            }
          }
        ]
      }
    ]
  }
}
```

### `request`

Each response object can optionally include a `request` property. The `request` property limits which type of request should receive this mock response. The value should be an object with three possible properties: `method`, `is` and `accepts` (all correlating to properties of the same name on the [Koa Response object](https://github.com/koajs/koa/blob/master/docs/api/request.md)).

#### `accepts`

With this mock example...

```js
module.exports = MockBase => class MyMockModule extends MockBase {
  mocks (options) {
    return [
      {
        route: '/pizzas/:id',
        responses: [
          {
            request: {
              method: 'GET',
              accepts: 'json'
            },
            response: {
              type: 'json',
              body: '{ "name": "Margerita" }'
            }
          }
        ]
      }
    ]
  }
}
```

...this request would receive a `404 Not Found` (as `accept` is not `json`):

```
$ curl http://127.0.0.1:8000/pizzas/1 --header 'accept: application/xml'
```

However, if we `accept` JSON will we receive a `200`:

```
$ curl http://127.0.0.1:8000/pizzas/1 --header 'accept: application/json'
```

#### `is`

With this example...

```js
module.exports = MockBase => class MyMockModule extends MockBase {
  mocks (options) {
    return [
      {
        route: '/pizzas/:id',
        responses: [
          {
            request: {
              method: 'PUT',
              is: 'json'
            },
            response: {
              type: 'json',
              body: '{ "status": "updated" }'
            }
          }
        ]
      }
    ]
  }
}
```

...this request would receive a `404 Not Found` (as `content-type` is not `json`):

```
$ curl http://127.0.0.1:8000/pizzas/1 --header 'content-type: application/xml'
```

However, if we set `content-type` to JSON will we receive a `200`:

```
$ curl http://127.0.0.1:8000/pizzas/1 --header 'content-type: application/json'
```

### `response` function 

If you need to craft a more complex response and know what you're doing with the [Koa ctx object](https://github.com/koajs/koa/blob/master/docs/api/context.md), you can define `response` as a function and handle setting the `ctx` values yourself. Note that the `response` function also receives any route parameter values. Therefore, if the `route` is `/pizzas/:id` and you received a request for `/pizzas/5` then `id` will equal `5`.

```js
module.exports = MockBase => class MyMockModule extends MockBase {
  mocks (options) {
    return [
      {
        route: '/pizzas/:id',
        responses: [
          {
            request: {
              method: 'GET',
              is: 'json'
            },
            response: function (ctx, id) {
              ctx.json = 'json'
              ctx.body = `{ "name": "Margerita", "id": ${id} }`
            }
          }
        ]
      }
    ]
  }
}
```

### verbose events 

Finally, if you want to send any debug information to the `--verbose` output, you can do so by emitting the `verbose` event anywhere within the `mocks` method. 

```js
module.exports = MockBase => class MyMockModule extends MockBase {
  mocks (options) {
    this.emit('verbose', 'mock.MyMockModule', 'some debug information')
    return []
  }
}
```

## See also

* [How to create an asynchronous mock response](How-to-create-an-asynchronous-mock-response.md)
* [How to mock a RESTful API](How-to-prototype-a-REST-API-using-Mock-Responses.md)
* [How to mock a Server-Sent Events service](How-to-mock-a-Server-Sent-Events-(SSE)-service.md)