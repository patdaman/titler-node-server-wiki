![NewBlueFX](img/NewBlueFX_logo.png)

## Titler Live Commands

```json
{ "command": "animateIn",
    "attributes": [
        "attribute1": true,
        "attribute2": true,
    ],
}
```

### Available Commands

        | actions                  | value                  | description |
        | :--- | :--- | :--- |
        | What to do | | |
        | name: "setvars" |         value: "SetVars" |        description: "Set these variables." |
        | name: "play" |            value: "Play" |	   	    description: "Play it." |
        | name: "all" |             value: "All" |	        description: "Use all layers." |
        | name: "playon" |          value: "PlayOn" |	        description: "Make this a fresh playback of this title." |
        | name: "playoff" |         value: "PlayOff" |	    description: "Make this finish the playback of this title." |
        | name: "curate" |          value: "Curate" |	        description: "Require this to be blessed by the user first." |
        | name: "loop" |            value: "Loop" |           description: "Play the selected layers with a continuous loop." |
        | name: "overlap" |         value: "Overlap" |        description: "When updating a value, let the animate in and out overlap." |
        | name: "render"|          value: "Render"|         description: "If variables change, force a render, even for the background." |

        | Region to play. By default it uses the two named In and Out markers. These options override them | | |
        | name: "setinvar"|        value: "SetInVar"|	    description: "Set the in marker at the start of the earliest variable in the list." |
        | name: "setoutvar"|       value: "SetOutVar"|	    description: "End at the time of the last variable in the list." |
        | name: "setinpause"|      value: "SetInPause"|	    description: "Start at the pause point in the middle of the template." |
        | name: "setoutpause"|     value: "SetOutPause"|	description: "End at the pause point in the middle of the template." |
        | name: "setintemplate"|   value: "SetInTemplate"|  description: "Start at the start of the template." |
        | name: "setouttemplate"|  value: "SetOutTemplate"| description: "End at the end of the template." |
        | name: "setoutempty"|     value: "SetOutEmpty"|    description: "End when the paragraph runs out of image." |

        | Timing. These determine when this starts playback, and options for its behavior.| | |
        | name: "override"|        value: "Override"|	    description: "Clear out the queue and put this at the head." |	
        | name: "replace"|         value: "Replace"|        description: "If there is an earlier queued item for this action, replace it." |
        | name: "interrupt"|       value: "Interrupt"|	    description: "Kill the currently playing title as soon as this can start." |
        | name: "sync"|            value: "Sync"|	        description: "Make sure all layers are finished playing before starting." |
        | name: "first"|           value: "First"|          description: "Put this at the head of the queue." |
        | name: "lockend"|         value: "LockEnd"|	    description: "Lock the end times of all layers with the time." |
        | name: "render_wait"|     value: "Render_Wait"|	description: "If still rendering, force a wait." |
        | name: "render_skip"|     value: "Render_Skip"|    description: "If still rendering, play the paused still frame." |
        | name: "render_pickup" |   value: "Render_PickUp" |  description: "If currently playing, just jump in at this point with updated value." |
        | name: "hold" |            value: "Hold" |	        description: "Wait until previous play in queue is completed, then wait fTime." |
        | name: "time" |            value: "Time" |	        description: "Cue to play at the specified absolute time." |
        | name: "now" |             value: "Now" |	        description: "Play immediately, or delayed by fTime amount." |
        | name: "duration" |        value: "Duration" |	    description: "Make the playback last exactly the value in the duration variable." |

        | Combine the above for some useful preset Actions:	 | | |
        | name: "alert" |           value: "Alert" |          description: "Alert means play the title from start to finish." |
        | name: "cutin" |           value: "CutIn" |          description: "Cut In means start playback in the middle and hold there." |
        | name: "cutout" |          value: "CutOut" |         description: "Cut Out means stop immediately." |
        | name: "animatein" |       value: "AnimateIn" |      description: "Animate In means start at the beginning and play up to the hold point. This is standard to bring in an overlay." |
        | name: "animateout" |      value: "AnimateOut" |     description: "Animate Out means start at the hold point and play through the end." |
                        // "Also, make sure all playing variables finish first." |
                        // "This is standard to conclude an overlay.
        | name: "update" |          value: "Update" |         description: "Refreshes the selected variable(s) at the hold point, with animation." |
        | name: "prep" |            value: "Prep" |           description: "Get the template ready to play, but don't actually do anything." |
        | name: "tightloop" |       value: "TightLoop" |      description: "Loop the specified var(s) with no delay between loops." |
        | name: "intervalloop" |    value: "IntervalLoop" |   description: "Loop the specified vars(s), delay set by the entire template." |
        | name: "crawl" |           value: "Crawl" |          description: "Plays the specified vars until they have no letters left." |
        | name: "play_once" |       value: "Play_Once" |      description: "Plays the selected variables from start to finish." |
    ]
|;