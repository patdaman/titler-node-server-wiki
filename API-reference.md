[![NewBlueFX](img/NewBlueFX_logo.png)](Home.md)

<a name="module_titler-node-server"></a>

## titler-node-server
**Emits**: [<code>verbose</code>](#module_titler-node-server--TitlerNodeServer+event_verbose)  
**Example**  
```js
const TitlerNodeServer = require('titler-node-server')
const titlerNodeServer = new TitlerNodeServer()
const server = titlerNodeServer.listen({
  port: 8000,
  https: true,
  directory: 'src',
  spa: 'index.html',
  websocket: 'src/websocket-server.js'
})
// secure, SPA server with listening websocket now ready on port 8050

// Stop listening when/if server is no longer needed
server.close() 
```

* [titler-node-server](#module_titler-node-server)
    * [TitlerNodeServer](#exp_module_titler-node-server--TitlerNodeServer) ⏏
        * [.listen([options])](#module_titler-node-server--TitlerNodeServer+listen) ⇒ <code>Server</code>
        * ["verbose" (key, value)](#module_titler-node-server--TitlerNodeServer+event_verbose)

<a name="exp_module_titler-node-server--TitlerNodeServer"></a>

### TitlerNodeServer ⏏
**Kind**: Exported class  
<a name="module_titler-node-server--TitlerNodeServer+listen"></a>

#### titlerNodeServer.listen([options]) ⇒ <code>Server</code>
Returns a listening HTTP/HTTPS server.

**Kind**: instance method of [<code>TitlerNodeServer</code>](#exp_module_titler-node-server--TitlerNodeServer)  

| Param | Type | Description |
| --- | --- | --- |
| [options] | <code>object</code> | Server options |
| [options.port] | <code>number</code> | Port |
| [options.hostname] | <code>string</code> | The hostname (or IP address) to listen on. Defaults to 0.0.0.0. |
| [options.maxConnections] | <code>number</code> | The maximum number of concurrent connections supported by the server. |
| [options.keepAliveTimeout] | <code>number</code> | The period (in milliseconds) of inactivity a connection will remain open before being destroyed. Set to `0` to keep connections open indefinitely. |
| [options.configFile] | <code>string</code> | Config file path, defaults to 'lws.config.js'. |
| [options.https] | <code>boolean</code> | Enable HTTPS using a built-in key and cert registered to the domain 127.0.0.1. |
| [options.key] | <code>string</code> | SSL key file path. Supply along with --cert to launch a https server. |
| [options.cert] | <code>string</code> | SSL cert file path. Supply along with --key to launch a https server. |
| [options.pfx] | <code>string</code> | Path to an PFX or PKCS12 encoded private key and certificate chain. An alternative to providing --key and --cert. |
| [options.ciphers] | <code>string</code> | Optional cipher suite specification, replacing the default. |
| [options.secureProtocol] | <code>string</code> | Optional SSL method to use, default is "SSLv23_method". |
| [options.stack] | <code>Array.&lt;string&gt;</code> \| <code>Array.&lt;Middlewares&gt;</code> | Array of feature classes, or filenames of modules exporting a feature class. |
| [options.server] | <code>string</code> \| <code>ServerFactory</code> | Custom server factory, e.g. lws-http2. |
| [options.websocket] | <code>string</code> \| <code>Websocket</code> | Path to a websocket module |
| [options.moduleDir] | <code>Array.&lt;string&gt;</code> | One or more directories to search for modules. |

<a name="module_titler-node-server--TitlerNodeServer+event_verbose"></a>

#### "verbose" (key, value)
Highly-verbose debug information event stream.

**Kind**: event emitted by [<code>TitlerNodeServer</code>](#exp_module_titler-node-server--TitlerNodeServer)  

| Param | Type | Description |
| --- | --- | --- |
| key | <code>string</code> | An identifying string, e.g. `server.socket.data`. |
| value | <code>\*</code> | The value, e.g. `{ socketId: 1, bytesRead: '3 Kb' }`. |

