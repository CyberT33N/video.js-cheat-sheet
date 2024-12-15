# video.js-cheat-sheet


# VAST


## Example Code
- Works with any advertiser that give you vast tags
- https://codepen.io/imasdk/pen/wpyQXP
- https://github.com/googleads/videojs-ima
  
```html
<html>
  <head>
    <!-- Load dependent stylesheets. -->
    <link rel="stylesheet" href="https://googleads.github.io/videojs-ima/node_modules/video.js/dist/video-js.min.css" />
    <link rel="stylesheet" href="https://googleads.github.io/videojs-ima/node_modules/videojs-contrib-ads/dist/videojs.ads.css" />
    <link rel="stylesheet" href="https://googleads.github.io/videojs-ima/dist/videojs.ima.css" />
  </head>

  <body>
    <video id="content_video" class="video-js vjs-default-skin"
        controls preload="auto" width="640" height="360">
      <source src="https://storage.googleapis.com/gvabox/media/samples/android.mp4"
          type="video/mp4" />
    </video>

    <!-- Load dependent scripts -->
    <script src="https://googleads.github.io/videojs-ima/node_modules/video.js/dist/video.min.js"></script>
    <script src="https://imasdk.googleapis.com/js/sdkloader/ima3.js"></script>
    <script src="https://googleads.github.io/videojs-ima/node_modules/videojs-contrib-ads/dist/videojs.ads.min.js"></script>
    <script src="https://googleads.github.io/videojs-ima/dist/videojs.ima.js"></script>
  </body>
</html>
```

```javascript
const player = videojs('content_video');

const options = {
  id: 'content_video',
  // Sample Tag for pre-roll, mid-roll and post-roll
  adTagUrl: 'http://pubads.g.doubleclick.net/gampad/ads?sz=640x480&iu=/124319096/external/ad_rule_samples&ciu_szs=300x250&ad_rule=1&impl=s&gdfp_req=1&env=vp&output=xml_vmap1&unviewed_position_start=1&cust_params=sample_ar%3Dpremidpostpod%26deployment%3Dgmf-js&cmsid=496&vid=short_onecue&correlator='
};

player.ima(options);
// On mobile devices, you must call initializeAdDisplayContainer as the result
// of a user action (e.g. button click). If you do not make this call, the SDK
// will make it for you, but not as the result of a user action. For more info
// see our examples, all of which are set up to work on mobile devices.
// player.ima.initializeAdDisplayContainer();
```
