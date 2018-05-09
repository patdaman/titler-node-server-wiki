![NewBlueFX](img/NewBlueFX_logo.png)

Creating an [SSE](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events) service with a mock response is straight forward.

This example responds to any request for `/sse` with a persistent SSE stream. The body of the response (`ctx.body`) is set to a stream which is fed a random number every ten seconds. If the client disconnects, the `interval` is cleared and the SSE stream ended.

```js
module.exports = MockBase => class SSE extends MockBase {
  mocks () {
    let i = 0
    return   [
      {
        route: '/sse',
        responses: [
          {
            response: async function (ctx) {
              ctx.body = new require('stream').PassThrough()
              ctx.type = 'text/event-stream'
              ctx.set('Cache-Control', 'no-cache')
              ctx.set('Connection', 'keep-alive')

              const interval = setInterval(() => {
                const randomNumber = parseInt(Math.random() * 10)
                ctx.body.write(`event: number\n`)
                ctx.body.write(`data: ${randomNumber}\n\n`)
              }, 1000)

              function finished () {
                clearInterval(interval)
                ctx.body.end()
              }

              ctx.req.on('close', finished);
              ctx.req.on('finish', finished);
              ctx.req.on('error', finished);
            }
          }
        ]
      }
    ]
  }
}
```

Save the above mock module as `sse-mock.js` then launch a server.

```js
  mocks: "sse-mock.js",
```

<!-- ```
$ ws --mocks sse-mock.js
``` -->

Try this simple client example.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>SSE Client Example</title>
  </head>
  <body>
    <h1>SSE Client Example</h1>

    <script>
      const eventSource = new EventSource('sse')
      eventSource.addEventListener('number', function (e) {
        console.log('number event:', e.data)
      })
    </script>
  </body>
</html>
```

