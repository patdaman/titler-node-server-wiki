[![NewBlueFX](img/NewBlueFX_logo.png)](Home.md)

## Proxy client directly to Titler Live

Proxy rules can be set to route multiple hosts based on the url.

**The proxy supports SSL for both https and wss.**

*Websockets sent to the same host as http must have slightly different url.*
*Recommend appending '/ws' to the end*

config.js
```js
    useProxy: true,
    proxyRules: {
        rules: {
            "/posts/([0-9]+)/comments/([0-9]+)": "http://localhost:8080/p/$1/c/$2",
            "/author/([0-9]+)/posts/([0-9]+)/": "http://localhost:8080/a/$1/p/$2/",
            "https://*": "http://" + targetHttpUrl + ":" + JSON.stringify(targetHttpPort),
            "http://*": "http://192.168.2.179:8022",
            "http://*": "http://127.0.0.1:8022",
            "ws://*": "ws://" + targetWebsocketUrl + ":" + JSON.stringify(targetWebsocketPort),
            "wss://*": "ws://" + targetWebsocketUrl + ":" + JSON.stringify(targetWebsocketPort),
            ".*/ws": "ws://127.0.0.1:57546"
        },
        default: "http://127.0.0.1:8022"
    },
```
