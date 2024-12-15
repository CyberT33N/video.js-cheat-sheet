# video.js-cheat-sheet



# Init












<br><br>
<br><br>






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
// ===================================================
// Optimized VAST Ads Configuration with videojs-ima
// ===================================================

const playerId = 'content_video';
const adTagUrl = 'https://xxxxxxxxxxxxxxxxxxxxxxx';

// Video.js Player Initialization
const player = videojs(playerId);

// Check if the user is on a mobile device
const mobileCheck = () => {
	const userAgent = navigator.userAgent || navigator.vendor || window.opera;
	const mobileRegex = /(android|bb\d+|meego).+mobile|avantgo|bada\/|blackberry|blazer|compal|elaine|fennec|hiptop|iemobile|ip(hone|od|ad)|iris|kindle|lge |maemo|midp|mmp|mobile.+firefox|netfront|opera m(ob|in)i|palm( os)?|phone|p(ixi|re)\/|plucker|pocket|psp|series(4|6)0|symbian|treo|up\.(browser|link)|vodafone|wap|windows (ce|phone)|xda|xiino|crkey/i;
	const additionalMobileRegex = /(mobile|tablet|ipad|playbook|silk|kindle|opera mini|opera mobi|blackberry|bb10|playstation vita|nokia|lumia|webos|samsung|huawei|oppo|vivo|xiaomi|miui)/i;
	return mobileRegex.test(userAgent) || additionalMobileRegex.test(userAgent);
};

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
// Must be done here!
player.ima(imaOptions);

// Event-Listener für das Ende des Videos
player.on('ended', function() {
	console.log('Das Video ist fertig abgespielt!');

	
	// Optional: Weiterleitung oder andere Aktionen
	// window.location.href = "https://example.com";
});

// ===================================================

const generateButton = document.querySelector('#generateButton');

if (generateButton) {

// ...
   
      setTimeout(function() {
			// Mobile-specific logic for user interaction
			if (mobileCheck()) {
				// Wait for user interaction to initialize ad display container
				const generateButton = document.getElementById('generateButton');
				generateButton.addEventListener('click', () => {
					player.ima.initializeAdDisplayContainer();
					player.play();
				});
			} else {
				// Desktop users: Initialize ad container immediately
				player.ima.initializeAdDisplayContainer();
				player.play();
			}
		     }, 1250);
    });
}

```


```
