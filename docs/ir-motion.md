# Ir Motion

Run with:
```bash
node eg/ir-motion.js
```


```javascript
var five = require("johnny-five"),
  board, motion;

board = new five.Board();

board.on("ready", function() {

  // Create a new `motion` hardware instance.
  motion = new five.IR.Motion(7);

  // Inject the `motion` hardware into
  // the Repl instance's context;
  // allows direct command line access
  this.repl.inject({
    motion: motion
  });

  // Pir Event API

  // "calibrated" occurs once, at the beginning of a session,
  motion.on("calibrated", function(err, ts) {
    console.log("calibrated", ts);
  });

  // "motionstart" events are fired when the "calibrated"
  // proximal area is disrupted, generally by some form of movement
  motion.on("motionstart", function(err, ts) {
    console.log("motionstart", ts);
  });

  // "motionstart" events are fired following a "motionstart event
  // when no movement has occurred in X ms
  motion.on("motionend", function(err, ts) {
    console.log("motionend", ts);
  });
});

```









## License
Copyright (c) 2012-2013 Rick Waldron <waldron.rick@gmail.com>
Licensed under the MIT license.
Copyright (c) 2014 The Johnny-Five Contributors
Licensed under the MIT license.
