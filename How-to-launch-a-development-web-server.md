This example will serve your current project as a static web site.

1. Instal titler-node-server to get the `ws` command.

  ```
  $ npm install -g titler-node-server
  ```

2. Navigate into to your project

  ```
  $ cd example-project
  ```

3. Launch the webserver. By default it hosts your project as a static site.

  ```
  $ ws
  Serving at http://newbluefx.local:8000, http://127.0.0.1:8000, http://192.168.0.100:8000
  ```

4. Navigating to one of the listed URLs will render a directory listing or your `index.html`, if that file exists.

    *Tip: iTerm users can cmd+click a server URL to open it in the default browser*

## Other use cases

1. Listen on a single host.

  ```
  $ ws --hostname newbluefx.local
  Serving at http://newbluefx.local:8000
  ```

2. Password-protect your server.

  ```
  $ ws --auth.user lloyd --auth.pass secret
  Serving at http://newbluefx.local:8000, http://127.0.0.1:8000, http://192.168.0.100:8000
  ```

3. [Serve a Single Page Application](How-to-serve-a-Single-Page-Application-(SPA).md)