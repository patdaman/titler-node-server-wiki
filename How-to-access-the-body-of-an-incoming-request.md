If you need to access the request body in middleware, include the module `body-parser` from the [default stack](Using-middleware#built-in-middleware-stack.md) somewhere high up your personal stack. 

Now, if an incoming request contains a body it will be present at `ctx.request.body` or `ctx.request.rawBody`. See [koa-bodyparser](https://github.com/koajs/bodyparser) for more information.