[![NewBlueFX](img/NewBlueFX_logo.png)](Home.md)

If you need to access the request body in middleware, include the module `body-parser` (Using-middleware#built-in-middleware-stack.md) somewhere high up your personal stack (stack: [...] in the config). 

Now, if an incoming request contains a body it will be present at `ctx.request.body` or `ctx.request.rawBody`. See [koa-bodyparser](https://github.com/koajs/bodyparser) for more information.