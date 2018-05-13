[![NewBlueFX](img/NewBlueFX_logo.png)](Home.md)

## Titler Live Websocket Connection

```js
var INPUT_NAME = "API Examples: HTML Basic Input Example";

window.onload = function () {
    const socket = new WebSocket(config.wsUrl);
    socket.addEventListener('open', function (event) {
        socket.send('getVars');
    });
    socket.addEventListener('message', function (event) {
        // Do work here...
        console.log('Message from server ', JSON.stringify(event.data));
    });
```
Returned will be a JSON object represented as a string (potentially nested) with variable key / value pairs:

## Set Variables
```js
    // Function to include in control:
    setVariables = function(variables) {
        var message = { "InputName": INPUT_NAME, "Action": "update", "Title": "all", variables };
        socket.send(JSON.stringify(message));
    };

    // Example: 
    var variables = { "Home Score": homeScore, "Visitor Score": visitorScore };
    setVariables(variables};
```
## Send XML Command
```js
    // Function to include in control:
    sendCommand = function(INPUT_NAME, action, title, variables){
        var message = { "InputName": INPUT_NAME, "Action": action, "Title": "", variables };
        socket.send(JSON.stringify(message));
    };

    // Example: 
    var action = "AnimateIn";
    var title = "Scorebug";
    var variables = { "Home Score": homeScore, "Visitor Score": visitorScore };
    sendCommand(action, title, variables};
```

## Clocks
To initialize a clock:
```js
    .initializeClock(INPUT_NAME, Action, Name, Direction, Format, Value);
```

Example Function:
```js
    .initializeClock(INPUT_NAME, "update", "Clock 1", countdownCheck.checked ? "countdown" : "countup", "MM:ss", parseInt(clockBox.value) * 1000);
```