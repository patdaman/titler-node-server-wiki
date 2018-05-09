![NewBlueFX](img/NewBlueFX_logo.png)

## Titler Live Websocket Connection

```js
var INPUT_NAME = "API Examples: HTML Basic Input Example";

window.onload = function () {
    const socket = new WebSocket(config.wsUrl);
    socket.addEventListener('open', function (event) {
        socket.send('getVars');
    });
    socket.addEventListener('message', function (event) {
        console.log('Message from server ', JSON.stringify(event.data));
    });
```

Returned will be a JSON object represented as a string (potentially nested) with variable key / value pairs:

