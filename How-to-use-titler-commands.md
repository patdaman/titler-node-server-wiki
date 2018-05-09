[![NewBlueFX](img/NewBlueFX_logo.png)](Home.md)

## Titler Live Commands

JSON Object
*channel and input are optional*
```json
{ "command": "animateIn",
    "attributes": [
        "channel": "-1",
        "input": "INPUT_NAME",
        "attribute1": "attribute1Value",
        "attribute2": "attribute2Value",
        "attribute3": "attribute3Value",
    ],
}
```

REST command
```js

```

Websocket command
```js

```

### Available Commands

| Action | Description |
| :--- | :--- | 
| | ***What to do*** |
| setvars | Set these variables. |
| play | Play it. |
| all | Use all layers. |
| playon | Make this a fresh playback of this title. |
| playoff | Make this finish the playback of this title. |
| curate | Require this to be blessed by the user first. |
| loop | Play the selected layers with a continuous loop. |
| overlap | When updating a value, let the animate in and out overlap. |
| render | If variables change, force a render, even for the background. |
| | ***Region to play. By default it uses the two named In and Out markers. These options override them*** |
| setinvar | Set the in marker at the start of the earliest variable in the list. |
| setoutvar | End at the time of the last variable in the list. |
| setinpause | Start at the pause point in the middle of the template. |
| setoutpause | End at the pause point in the middle of the template. |
| setintemplate | Start at the start of the template. |
| setouttemplate | End at the end of the template. |
| setoutempty | End when the paragraph runs out of image. |
| | ***Timing. These determine when this starts playback, and options for its behavior.*** |
| override | Clear out the queue and put this at the head. |	
| replace | If there is an earlier queued item for this action, replace it. |
| interrupt | Kill the currently playing title as soon as this can start. |
| sync | Make sure all layers are finished playing before starting. |
| first | Put this at the head of the queue. |
| lockend | Lock the end times of all layers with the time. |
| render_wait | If still rendering, force a wait. |
| render_skip | If still rendering, play the paused still frame. |
| render_pickup | If currently playing, just jump in at this point with updated value. |
| hold | Wait until previous play in queue is completed, then wait fTime. |
| time | Cue to play at the specified absolute time. |
| now | Play immediately, or delayed by fTime amount. |
| duration | Make the playback last exactly the value in the duration variable. |
| | ***Combine the above for some useful preset Actions:*** |
| alert | Alert means play the title from start to finish. |
| cutin | Cut In means start playback in the middle and hold there. |
| cutout | Cut Out means stop immediately. |
| animatein | Animate In means start at the beginning and play up to the hold point. This is standard to bring in an overlay. |
| animateout | Animate Out means start at the hold point and play through the end. |
| | ***Make sure all playing variables finish first*** |
| | ***This is standard to conclude an overlay*** |
| update | Refreshes the selected variable(s) at the hold point, with animation. |
| prep | Get the template ready to play, but don't actually do anything. |
| tightloop | Loop the specified var(s) with no delay between loops. |
| intervalloop | Loop the specified vars(s), delay set by the entire template. |
| crawl | Plays the specified vars until they have no letters left. |
| play_once | Plays the selected variables from start to finish. |
