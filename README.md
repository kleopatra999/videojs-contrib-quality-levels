# videojs-contrib-quality-levels

Exposes a list of quality levels available for the source.

## Table of Contents

<!-- START doctoc -->
<!-- END doctoc -->
## Installation

```sh
npm install --save videojs-contrib-quality-levels
```

The npm installation is preferred, but Bower works, too.

```sh
bower install  --save videojs-contrib-quality-levels
```

## Using

The list of `QualiyLevel`s can be accessed using `qualityLevels()` on the Player object.
With this list, you can:
 * see which quality levels are available for the current source
 * enable or disable specific quality levels to change which levels are selected by ABR
 * see which quality level is currently selected by ABR

Example
```js
let player = videojs('my-video');

let qualityLevels = player.qualityLevels();

// Loop through the list of quality levels and disable all qualities with more than
// 720 horizontal lines of resolution.
for (let i = 0; i < qualityLevels.length; i++) {
  let qualityLevel = qualityLevels[i];
  if (qualityLevel.height > 720) {
    qualityLevel.enabled = false;
  } else {
    qualityLevel.enabled = true;
  }
}

let currentSelectedQualityLevelIndex = qualityLevels.selectedIndex;
```

### HLS

Quality levels for an HLS source will be automatically populated when using [videojs-contrib-hls](https://github.com/videojs/videojs-contrib-hls).

### Dash

Quality levels for a Dash source will only be automatically populated when using [videojs-contrib-dash](https://github.com/videojs/videojs-contrib-dash) and if the function`player.dash.representations` exists,
which should return a list of `Representation`s.

### Other

Other sources quality levels are not yet automatically populated. This can be done manually
by using a `Representation` object for each quality level availble for your source to create
a corresponding `QualityLevel` and add it by using `addQualityLevel`.

## Including the Plugin

To include videojs-contrib-quality-levels on your website or web application, use any of the following methods.

### `<script>` Tag

This is the simplest case. Get the script in whatever way you prefer and include the plugin _after_ you include [video.js][videojs], so that the `videojs` global is available.

```html
<script src="//path/to/video.min.js"></script>
<script src="//path/to/videojs-contrib-quality-levels.min.js"></script>
<script>
  var player = videojs('my-video');

  player.qualityLevels();
</script>
```

### Browserify

When using with Browserify, install videojs-contrib-quality-levels via npm and `require` the plugin as you would any other module.

```js
var videojs = require('video.js');

// The actual plugin function is exported by this module, but it is also
// attached to the `Player.prototype`; so, there is no need to assign it
// to a variable.
require('videojs-contrib-quality-levels');

var player = videojs('my-video');

player.qualityLevels();
```

### RequireJS/AMD

When using with RequireJS (or another AMD library), get the script in whatever way you prefer and `require` the plugin as you normally would:

```js
require(['video.js', 'videojs-contrib-quality-levels'], function(videojs) {
  var player = videojs('my-video');

  player.qualityLevels();
});
```

## License

Apache-2.0. Copyright (c) Brightcove, Inc.


[videojs]: http://videojs.com/
