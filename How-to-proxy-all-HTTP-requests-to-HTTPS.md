If you have an HTTPS server running at `https://127.0.0.1:8000` then any HTTP requests to `http://127.0.0.1:8000` will fail (as HTTP is a different protocol).

HTTP and HTTPS are two separate services. To respond to both HTTP and HTTPS requests both HTTP and HTTPS servers should be launched.

1. Launch an HTTPS server. For example,

```js
    https: true,
    port: 8000,
```
<!-- 
```
$ ws --https --port 8000
``` -->

2. Launch a separate HTTP server, hosting the same directory, on a different port of your choice. Configure a blanket rewrite rule to redirect all HTTP traffic to the HTTPS server. 

```js
    port: 7000,
    rewrite: '/* -> https://127.0.0.1:8000/$1',
```
<!-- 
```
$ ws --port 7000 --rewrite '/* -> https://127.0.0.1:8000/$1'
``` -->

### Standard ports

If your system permits it, you could launch the above servers on the standard ports of 80 (HTTP) and 443 (HTTPS).