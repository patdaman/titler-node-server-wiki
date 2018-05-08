Some modern techs (HTTP2, ServiceWorker, `MediaDevices.getUserMedia()` etc.) *must* be served from a secure origin (HTTPS). To launch an HTTPS server you must supply one of the following: 

1. the `--https` flag
2. `--key` and `--cert` files
3. a `--pfx` file

The quickest method is to use the `--https` flag, this will use the private key and certificate chain [built into titler-node-server](ssl-certs.md). This example will serve your current project as a secure, static web site.

1. Install titler-node-server to get the `ws` command

  ```
  $ npm install -g titler-node-server
  ```

2. Navigate into to your project

  ```
  $ cd example-project
  ```

3. Launch the secure webserver.

  ```
  $ ws --https
  Serving at https://newbluefx.local:8000, https://127.0.0.1:8000, https://192.168.0.100:8000
  ```

4. Navigating to one of the listed URLs will render a directory listing or your `index.html`, if that file exists.

Next, read [how to get the "green padlock" using the built-in certificate](How-to-get-the-%22green-padlock%22-using-the-built-in-certificate.md).