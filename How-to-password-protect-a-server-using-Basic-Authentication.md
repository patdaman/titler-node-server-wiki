![NewBlueFX](img/NewBlueFX_logo.png)

HTTP Basic Authentication is provided by the `basic-auth` module which is part of the [built-in stack](Using-middleware#built-in-middleware-stack.md).

1. Launch `ws` supplying `--auth.user` and `--auth.pass` values. For added security you could also add the `--https` option. 

    ````js
      authUser: "developer",
      authPass: "development",
    ````
    <!-- ````
    $ ws --auth.user lloyd --auth.pass chimps
    ```` -->

2. Navigate to the server - you will now be prompted to input a username and password. 

To persist options across sessions, add them to the [config](Configuration-Management.md). 

```js
module.exports = {
  authUser: 'lloyd',
  authPass: 'chimps'
}
```
