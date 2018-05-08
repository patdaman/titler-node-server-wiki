If your app needs a bi-directional communication channel with the server then WebSockets are the way forward.

**Remember: Websockets are not compatible with HTTP2 therefore will not work with the `--http2` flag.**

## Create a WebSocket module
This is the minimum code required to create a WebSocket server. Only the `websocket` method is required which receives a [`WebSocket.Server`](https://github.com/websockets/ws/blob/master/doc/ws.md#class-websocketserver) instance. This method is not required to return a value. 

```js
module.exports = SocketBase => class Socket extends SocketBase {
  websocket (wss) {}
}
```

To handle incoming WebSocket connections, attach a listener to the `connection` event. Save the following trivial echo server example in a file named `ws-example.js`:

```js
module.exports = SocketBase => class Socket extends SocketBase {
  websocket (wss) {
    wss.on('connection', (ws, req) => {
      ws.on('message', data => {
        ws.send(`message received: ${data.toString()}`)
      })
    })
  }
}
```

## Use a WebSocket module

Save the following client example to a file named `index.html`.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>WebSocket example</title>
  </head>
  <body>
    <script>
      const socket = new WebSocket('ws://127.0.0.1:8000/')
      socket.onopen = function () {
        socket.send('Trivial example')
      }
    </script>
  </body>
</html>
```

Now, launch `ws` with your WebSocket server and navigate to one of the listed URLs. You will be able to see socket communications in the DevTools Network panel.

```
$ ws --websocket ws-example.js
Serving at http://mbp.local:8000, http://127.0.0.1:8000, http://192.168.0.100:8000
```
## Websocket server options

You can set the options the [`Websocket.Server`](https://github.com/websockets/ws/blob/master/doc/ws.md#new-websocketserveroptions-callback) is created with by returning a plain object from the `wsOptions` method. 

In this example, the WebSocket will only accept connections from requests to `/socket`.

```js
module.exports = SocketBase => class Socket extends SocketBase {
  wsOptions () {
    return { path: '/socket' }
  }
  websocket (wss) {
    wss.on('connection', (ws, req) => {
      ws.on('message', data => {
        ws.send(`message received: ${data.toString()}`)
      })
    })
  }
}
```

## Verbose events

To send debug information to the --verbose output, you can emit a `verbose` event from any method within the module passing a key and value.

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
