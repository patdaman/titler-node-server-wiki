![NewBlueFX](img/NewBlueFX_logo.png)

To make a `response` asynchronous, use a response function which returns a `Promise` which resolves when complete.

```js
module.exports = MockBase => class MyMockModule extends MockBase {
  mocks (options) {
    return [
      {
        route: '/',
        responses: [
          {
            response: function (ctx) {
              return new Promise((resolve, reject) => {
                setTimeout(() => {
                  ctx.body = '<h1>You waited 2s for this</h1>'
                  resolve()
                }, 2000)
              })
            }
          }
        ]
      }
    ]
  }
}
```