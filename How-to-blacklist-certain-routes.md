[![NewBlueFX](img/NewBlueFX_logo.png)](Home.md)

By default, access to all files is allowed (including dot files). If you prefer to forbid certain routes, pass [express-style](https://expressjs.com/en/guide/routing.html) route expressions to `--blacklist`:

```js
    blacklist: [ '*.json', '*.php']
```
<!-- 
```sh
$ ws --blacklist '*.json' '*.php'
Serving at http://mbp.local:8000, http://127.0.0.1:8000, http://192.168.0.100:8000
``` -->

Test in a separate terminal:

```sh
$ curl -I http://127.0.0.1:8000/something.php 
HTTP/1.1 403 Forbidden
Vary: Origin
Date: Wed, 21 Jun 2017 12:25:16 GMT
Connection: keep-alive
```
