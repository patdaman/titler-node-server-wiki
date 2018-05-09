[![NewBlueFX](img/NewBlueFX_logo.png)](Home.md)

Some modern techs (HTTP2, ServiceWorker, `MediaDevices.getUserMedia()` etc.) *must* be served from a secure origin (HTTPS). To launch an HTTPS server you must supply one of the following: 

1. the `--https` flag
2. `--key` and `--cert` files
  - or -
3. a `--pfx` file
```js
  https: true,

  key: "Path_to_key_file",
  cert: "Path_to_cert_file",

  pfx: "Path_to_pfx_file",
```

TODO:
The quickest method is to use the `--https` flag, this will use the private key and certificate chain [built into titler-node-server](ssl-certs.md). This example will serve your current project as a secure, static web site.

1. Navigate into to your project

  ```sh
  $ cd example-project
  ```

2. Install titler-node-server 

  ```sh
  $ npm install
  ```

3. Launch the secure webserver.

  ```sh
  $ npm start
  Serving at https://newbluefx.local:8000, https://127.0.0.1:8000, https://192.168.0.100:8000
  ```

4. Navigating to one of the listed URLs will render a directory listing or your `index.html`, if that file exists.
