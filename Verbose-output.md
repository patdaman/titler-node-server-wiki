[![NewBlueFX](img/NewBlueFX_logo.png)](Home.md)

Setting the `--verbose` flag outputs a highly verbose JSON stream containing debug information. It is intended to aid debugging and as a datasource for custom views.

Any custom server, [middleware](Creating-middleware.md), [mock response](How-to-create-a-mock-response.md) or [websocket](How-to-create-a-websocket-module.md) module can send information to the verbose stream with this line (where `key` is a identifying string e.g. `middleware.example.config` and `value` is the information to send). 

```js
this.emit('verbose', key, value)
```

## Verbose stream filtering

You may hand-pick the keys to display in the verbose stream using `--verbose.include` and `--verbose.exclude`. Each option implies `--verbose` and accepts one or more regular expressions.

This command outputs only information regarding the `rewrite` middleware. 

```js
    verboseInclude: "rewrite",
```
<!-- ```
$ ws --verbose.include rewrite
``` -->

Include only `request` and `response` info. 

```js
    verboseInclude: "request response",
```
<!-- ```
ws --verbose.include request response
``` -->

Print everything except `socket` and `middleware` information.

```js
    verboseExclude: "socket middleware",
```
<!-- ```
$ ws --verbose.exclude socket middleware
``` -->

