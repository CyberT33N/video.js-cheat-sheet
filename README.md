# video.js-cheat-sheet




# docs
- https://docs.videojs.com/docs/api/player.html#Methodserror







<br><br>
<br><br>


# Attributes


<br><br>


## poster (Thumbnail)
- You can use poster attribute
```
<video id="content_video" class="video-js vjs-default-skin"
  controls
  preload="auto"
  playsinline
  poster="./assets/img/hero-7-video-frame.png"
  data-setup='{ "controls": false, "autoplay": false, "preload": "auto" }'>
>
<source src="./assets/videos/loading.webm" type="video/webm">
<source src="./assets/videos/loading.mp4"
    type="video/mp4" />
</video>
```








<br><br>
______________________
<br><br>



# API

## src
- Change video source of current player instance
```javascript
// Event-Listener für das Ende des Videos
player.on('ended', function() {
	// Neues Video setzen
	 player.src([
		{
		    type: 'video/webm',
		    src: './assets/videos/loading2.webm'
		},
		{
		    type: 'video/mp4',
		    src: './assets/videos/loading2.mp4'
		}
	 ]);

   player.play();
});

```








<br><br>
<br><br>
_____________________________
<br><br>
<br><br>


# Events

## Player
- https://docs.videojs.com/player#events


### ads-request
- Do something when ads request was sended..
```
 player.on('ads-request', () => {
               console.log('Anzeigeanfrage gesendet.');
           });
           
```

### ended
- Do something when video has ended
```javascript
// Event-Listener für das Ende des Videos
player.on('ended', function() {
	console.log('Das Video ist fertig abgespielt!');

	
	// Optional: Weiterleitung oder andere Aktionen
	// window.location.href = "https://example.com";
});
```


<br><br>

# Adend
- Do something when ad has ended
```javascript
player.on('adend', function() {
	//..
```


<br><br>


### playing
- Do something when video starts playing
```javascript
// Event-Listener für das Ende des Videos
player.on('playing', function() {
	console.log('Video is playing..');
});

```










<br><br>
<br><br>
_____________________________
<br><br>
<br><br>

# videojs-ima
- **Make sure that you have this order and that your player init will happen directly in the next tick after you loaded videojs.ads.min.js(https://github.com/videojs/videojs-contrib-ads)**
```html
  <!-- VIDEOJS -->
  <script src="./assets/js/lib/video.min.js"></script>
  <script src="./assets/js/lib/videojs.ads.min.js"></script>
  <script src="./assets/js/lib/ima3.js"></script>
  <script src="./assets/js/lib/videojs.ima.js"></script>
  <script type="module" src="./assets/js/ad5.js"></script>

```

<br><br>

# VAST

<br><br>

## Basic Example Code
- Works with any advertiser that give you vast tags
- https://codepen.io/imasdk/pen/wpyQXP
- https://github.com/googleads/videojs-ima/tree/main/examples/simple
- https://github.com/googleads/videojs-ima

index.html
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

ads.js
```javascript
/**
 * Copyright 2014 Google Inc.
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

var player = videojs('content_video');

var options = {
  id: 'content_video',
  adTagUrl: 'http://pubads.g.doubleclick.net/gampad/ads?sz=640x480&' +
      'iu=/124319096/external/ad_rule_samples&ciu_szs=300x250&ad_rule=1&' +
      'impl=s&gdfp_req=1&env=vp&output=xml_vmap1&unviewed_position_start=1&' +
      'cust_params=sample_ar%3Dpremidpostpod%26deployment%3Dgmf-js&cmsid=496&' +
      'vid=short_onecue&correlator='
};

player.ima(options);

// Remove controls from the player on iPad to stop native controls from stealing
// our click
var contentPlayer =  document.getElementById('content_video_html5_api');
if ((navigator.userAgent.match(/iPad/i) ||
      navigator.userAgent.match(/Android/i)) &&
    contentPlayer.hasAttribute('controls')) {
  contentPlayer.removeAttribute('controls');
}

// Initialize the ad container when the video player is clicked, but only the
// first time it's clicked.
var initAdDisplayContainer = function() {
  player.ima.initializeAdDisplayContainer();
  wrapperDiv.removeEventListener(startEvent, initAdDisplayContainer);
}

var startEvent = 'click';
if (navigator.userAgent.match(/iPhone/i) ||
    navigator.userAgent.match(/iPad/i) ||
    navigator.userAgent.match(/Android/i)) {
  startEvent = 'touchend';
}

var wrapperDiv = document.getElementById('content_video');
wrapperDiv.addEventListener(startEvent, initAdDisplayContainer);
```





<br><br>
<br><br>

## Advanced Examples

<br><br>

### Click

<br><br>

#### Video after Video - Unique HTML Video elements
- Works mobile and desktop
- I guess this approach is more valid than the example below `Video after Video - Replace src and Ad Tag` because we do not re-use the same video.js player instead we create new instances.
- This approach also contains adding a native banner while the video is running and also is adding one after the second run and hide it againa fter 5 seconds

index.html
```html
<div class="video-container">
	<video id="content_video" class="video-js vjs-default-skin vjs-fluid"
	       controls
	       preload="auto"
	       playsinline
	       data-setup='{ "controls": false, "autoplay": false, "preload": "auto", "fluid": true, "poster": "./assets/img/black.png" }'>
	  <source src="./assets/videos/loading.webm" type="video/webm">
	  <source src="./assets/videos/loading.mp4" type="video/mp4" />
	</video>
	<div class="overlay-banner">
	  <script>
	     (function(pqlp){
		xxxxxxxxxxx
	    })({})
	  </script>
	</div>
	<!-- Play Button Overlay -->
	<img src="./assets/img/start-button.png" id="playButton" class="play-button" />
      </div>
      <div class="video-container2">
	<video id="content_video2" class="video-js vjs-default-skin vjs-fluid"
	       controls
	       preload="auto"
	       playsinline
	       data-setup='{ "controls": false, "autoplay": false, "preload": "auto", "fluid": true, "poster": "./assets/img/black.png" }'>
	  <source src="./assets/videos/loading.webm" type="video/webm">
	  <source src="./assets/videos/loading.mp4" type="video/mp4" />
	</video>
	<div class="overlay-banner">
	  <script>
	     (function(pqlp){
		 xxxxxxx
	    })({})
	  </script>
	</div>
	<!-- Play Button Overlay -->
	<img src="./assets/img/start-button.png" id="playButton" class="play-button" />
</div>
```

ads.js:
```
"use strict";

import mobileCheck from "./mobile-check.js";

const adTags = {
     // google
     first: 'https://pubads.g.doubleclick.net/gampad/ads?iu=/21775744923/external/single_preroll_skippable&sz=640x480&ciu_szs=300x250%2C728x90&gdfp_req=1&output=vast&unviewed_position_start=1&env=vp&impl=s&correlator=',
     // google
     second: 'https://pubads.g.doubleclick.net/gampad/ads?iu=/21775744923/external/single_preroll_skippable&sz=640x480&ciu_szs=300x250%2C728x90&gdfp_req=1&output=vast&unviewed_position_start=1&env=vp&impl=s&correlator=',
     // google
     third: 'https://pubads.g.doubleclick.net/gampad/ads?iu=/21775744923/external/single_preroll_skippable&sz=640x480&ciu_szs=300x250%2C728x90&gdfp_req=1&output=vast&unviewed_position_start=1&env=vp&impl=s&correlator=',
     // google
     four: 'https://pubads.g.doubleclick.net/gampad/ads?iu=/21775744923/external/single_preroll_skippable&sz=640x480&ciu_szs=300x250%2C728x90&gdfp_req=1&output=vast&unviewed_position_start=1&env=vp&impl=s&correlator='
};


// Player configurations
const playerConfigs = [
     { id: '#content_video', container: '.video-container', adTag: adTags.first },
     { id: '#content_video2', container: '.video-container2', adTag: adTags.second }
];

// Create IMA options
const createImaOptions = (adTagUrl) => ({
     adTagUrl,
     adsRenderingSettings: {
          enablePreloading: true,
          uiElements: ['adAttribution', 'countdown'],
     },
     autoPlayAdBreaks: true,
     disableAdControls: true,
     showCountdown: true,
     forceNonLinearFullSlot: true,
     vastLoadTimeout: 3000,
     preventLateAdStart: true,
     vpaidMode: google.ima.ImaSdkSettings.VpaidMode.ENABLED,
});

// Initialize players
const players = playerConfigs.map(config => {
     const player = videojs(config.id)
     player.ima(createImaOptions(config.adTag))

     return {
          player,
          config
     }
})

$(document).ready(function () {
     const $playButton = $(".play-button");
     const $overlayBanner = $(".overlay-banner");
     let activePlayerIndex = 0;
     let count = 0;

     // Initialize containers
     const containers = playerConfigs.map(config => ({
          $element: $(config.container),
          $player: $(config.id)
     }));

     // Show only first container initially
     containers.forEach(($container, index) => {
          $container.$element.toggle(index === 0);
     });

     // Initialize ad display container for a player
     const initAdDisplayContainer = (playerInstance) => {
          console.log('initAdDisplayContainer()')
          $playButton.hide();
          playerInstance.ima.initializeAdDisplayContainer();
          playerInstance.play();
     };

     // Handle mobile devices
     const startEvent = mobileCheck() ? "touchend" : "click";
     if (mobileCheck()) {
          containers.forEach(container => container.$player.removeAttr("controls"));
     }

     // Attach event listeners to players
     players.forEach(({ player, config }, index) => {
          // Click/touch event for ad container initialization
          $(config.id).on(startEvent, () => initAdDisplayContainer(player));

          player.on('playing', () => {
               setTimeout(() => {
                    $overlayBanner.css('display', 'flex');
               }, 3000)
          });

          // Video end event
          player.on("ended", function () {
               count++;

               $overlayBanner.hide();

               if (count === 2) {
                    $overlayBanner.css('display', 'flex');

                    setTimeout(() => {
                         $overlayBanner.hide();
                         count = 0;
                    }, 5000);
               }

               // Toggle containers
               activePlayerIndex = (activePlayerIndex + 1) % players.length;

               containers.forEach((container, i) => {
                    container.$element.toggle(i === activePlayerIndex);
               });

               // Reset for tdisplay of thumbnail
               player.src([
                    {
                        type: "video/webm",
                        src: "./assets/videos/loading.webm",
                    },
                    {
                        type: "video/mp4",
                        src: "./assets/videos/loading.mp4",
                    },
               ]);

               $playButton.show();
          });
     });
});
```



<br><br>

#### Video after Video - Replace src and Ad Tag
- Works mobile and desktop
- **Not 100% sure but sometimes the second VAST is not playing. Maybe something wrong in code or the google IMA sdk is not allowing it**
```javascript
"use strict";

import mobileCheck from "./mobile-check.js";

// Hiltopads
const adTagUrl = 'xxxxxxxxxx';
const adTagUrl2 = 'xxxxxxxxxxxxxxx'

const playerId = '#content_video';
const generateButtonId = '#generateButton';

// Video.js Player Initialization
const player = videojs(playerId)

// IMA Plugin Configuration with Optimized Settings
const imaOptions = {
     adTagUrl,
     adsRenderingSettings: {
          enablePreloading: true, // Preload ads for faster playback
          // bitrate: 1500,         // Optimize for mobile and slow connections
          uiElements: ['adAttribution', 'countdown'], // Essential UI elements
     },
     autoPlayAdBreaks: true,    // Automatically play VMAP or ad rules
     disableAdControls: true,   // Remove player controls during ads
     showCountdown: true,       // Display ad countdown timer
     forceNonLinearFullSlot: true, // Pause video for non-linear ads
     vastLoadTimeout: 3000,     // Lower timeout to reduce user frustration
     preventLateAdStart: true,  // Avoid starting ads late
     numRedirects: 2,           // Limit VAST redirects for better performance
     vpaidMode: google.ima.ImaSdkSettings.VpaidMode.ENABLED, // Enable interactive ads
};

// Initialize video.js IMA plugin
player.ima(imaOptions)

// ===================================================
// Optimized VAST Ads Configuration with videojs-ima
// ===================================================
document.addEventListener("DOMContentLoaded", function () {
     const contentPlayer = document.querySelector(playerId);
     const generateButton = document.querySelector(generateButtonId);

     if (contentPlayer && generateButton) {
          // Initialize the ad container when the video player is clicked, but only the
          // first time it's clicked.
          const initAdDisplayContainer = function () {
               player.ima.initializeAdDisplayContainer();
               //wrapperDiv.removeEventListener(startEvent, initAdDisplayContainer);
               player.play();
          }

          let startEvent = 'click';
          if (mobileCheck()) {
               startEvent = 'touchend';
               contentPlayer.removeAttribute('controls');
          }

          const wrapperDiv = document.getElementById('content_video');
          wrapperDiv.addEventListener(startEvent, initAdDisplayContainer);

          // Event-Listener für das Ende des Videos
          player.on('ended', function () {
               // AdsManager zerstör
               if (player.ima.getAdsManager()) {
                    player.ima.getAdsManager().destroy();
                    // console.log('AdsManager destroyed.');
               }

               // Content als abgeschlossen signalisieren
               if (player.ima.adsLoader) {
                    player.ima.adsLoader.contentComplete();
                    // console.log('Content complete signaled to AdsLoader.');
               }

               // Neues Video setzen
               player.src([
                    {
                         type: 'video/webm',
                         src: './assets/videos/loading2.webm'
                    },
                    {
                         type: 'video/mp4',
                         src: './assets/videos/loading2.mp4'
                    }
               ]);

               player.ima.changeAdTag(adTagUrl2);
               player.ima.requestAds();
          });
     }
})
```
