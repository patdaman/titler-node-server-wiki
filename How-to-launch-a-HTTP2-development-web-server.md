![NewBlueFX](img/NewBlueFX_logo.png)

***This feature requires node version 8.4.0 or above and does NOT support Websockets***

As a HTTP2 connection must always be secure (modern browsers demand it), launching an HTTP2 server is identical to [launching an HTTPS server](How-to-launch-a-secure-titler-node-server-HTTPS.md) with one exception - you set the `--http2` flag instead of `--https`.

So, typical usage looks the same. Launch HTTP2 using the built-in SSL certificate:

```js
    http2: true,
```

<!-- ```
$ ws --http2
``` -->

Launch using your own private key and certificate:

```js
    http2: true,
    key: "my-key.pem",
    cert: "my-cert.pem",
```

<!-- ```
$ ws --http2 --key my-key.pem --cert my-cert.pem
``` -->
