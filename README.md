# Welcome to Dennis Mellican's Github profile. 

Here are some side projects I am currently working on:

* <a href="#youtube-retitler-updates-a-video-title-and-thumbnail-with-view-counts">YouTube Retitler: Updates a video title and thumbnail with view counts.</a>
* <a href="#musicfig-the-raspberry-pi-lego-minifigure-jukebox">Musicfig: The Raspberry Pi LEGO Minifigure jukebox.</a>
* <a href="#solariot-communicate-with-a-solar-inverter-using-modbus-tcp">Solariot: Communicate with a Solar Inverter using Modbus TCP.</a>
* <a href="#slackview-stream-a-slack-channel-to-a-web-page">SlackView: Stream a Slack channel to a web page.</a>

A screenshot is worth a thousand lines of code</i><a href="https://github.com/meltaxa/meltaxa/blob/master/README.md#a-screenshot-is-worth-a-thousand-lines-of-code">*</a>.

## My Astronomy Picture of the Moment
<p align="left"> 
Showcase your astronomy images online. A glorified slideshow that is designed to be plug and play for technologically challenged folks :smile:.<br>
<img src="https://mellican.com/images/apom.png?github=profile" width=400px><br>
Check out: <a href="https://github.com/meltaxa/yapom">https://github.com/meltaxa/apom</a>
</p>

## YouTube Retitler: Updates a video title and thumbnail with view counts
<p align="left"> 
Smash that like button :laughing:<br>
<img src="https://mellican.com/images/youtube.png?github=youtube-retitler" width=400px><br>
Check out: <a href="https://github.com/meltaxa/youtube-retitler">https://github.com/meltaxa/youtube-retitler</a>
</p>

## Musicfig: The Raspberry Pi LEGO Minifigure jukebox
<p align="left">
Currently Dennis' Minifigures are playing:<br>
<img src="https://musicfig.com/images/nowplaying.png?github=profile" width=400px><br>
Check out: <a href="https://github.com/meltaxa/musicfig">https://github.com/meltaxa/musicfig</a>
</p>

## Solariot: Communicate with a Solar Inverter using Modbus TCP
<p align="left">
Dennis monitors his home energy usage in real-time:<br>
<img src="https://mellican.com/images/solarspy-live.png?github=profile" width=400px><br>
Check out: <a href="https://github.com/meltaxa/solariot">https://github.com/meltaxa/solariot</a>
</p>

## SlackView: Stream a Slack channel to a web page
<p align="left">
These bad actors aren't from Hollywood:<br>
<img src="https://mellican.com/images/badactors.png?github=profile" width=400px><br>
Check out: <a href="https://github.com/meltaxa/slackview">https://github.com/meltaxa/slackview</a>
</p>

<hr/>

#### *A screenshot is worth a thousand lines of code
A worthy adage meaning that the complex and sometimes multiple ideas can be conveyed by a single project snapshot, which conveys the meaning or essence more effectively than a long descriptive README.

Each project screenshot is dynamic and updated every minute. Click on the screenshot or reload this page to see the latest! To add a dynamic screenshot to your Github profile, view this <a href="https://github.com/meltaxa/meltaxa/raw/master/README.md">README.md</a> file in raw format for instructions.

<!---
To add a dynamic screenshot to your Github profile
==================================================

Dynamic images are served from a web server. The screenshots are taken periodically by Puppeteer.
The web server must disable caching for the images using headers. Any CDN must respect these headers.
Github uses it's own CDN service called Camo. You may need to purge any images in it's cache too.

Instructions are for Ubuntu systems. Ironically, a screenshot doesn't cover 100 comment lines in these instructions. :-)

# Install Google Chrome
sudo apt-get install libxss1 libappindicator1 libindicator7
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome*.deb  # Might show "errors", fixed by next line
sudo apt-get install -f

# Install Node Stable (v10)
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs

# Run Chrome as a background process
# https://chromium.googlesource.com/chromium/src/+/lkgr/headless/README.md
# --disable-gpu currently required, see link above
google-chrome --headless --hide-scrollbars --remote-debugging-port=9222 --disable-gpu &

# Install script dependencies
npm install chrome-remote-interface minimist

# Install Puppeteer
npm i puppeteer

# Install fs
npm i fs

# Use Puppeteer to take the screenshots of the website. Because we are saving directly to the 
# web site folder, using symlinks will reduce a race condition when the same file is being 
# accessed and written to at the same time. Save this file as
# <PATH_TO>/website-screenshot.js:

const puppeteer = require('puppeteer');
const fs = require('fs');

var ts_hms = new Date();
var timestamp = ts_hms.getFullYear() +
    ("0" + (ts_hms.getMonth() + 1)).slice(-2) +
    ("0" + (ts_hms.getDate())).slice(-2) + '-' +
    ("0" + ts_hms.getHours()).slice(-2) +
    ("0" + ts_hms.getMinutes()).slice(-2);

function callback(err) {
}

(async () => {
  const browser = await puppeteer.launch({ignoreHTTPSErrors: true});
  const page = await browser.newPage();
  await page.setCacheEnabled(false);
  await page.setDefaultNavigationTimeout(120000);

  let VIEWPORT = { width: 1280, height: 1270, deviceScaleFactor: 1 }; 
  await page.setViewport(VIEWPORT);
  await page.goto('<IMG_URL>', {waitUntil: 'networkidle0'});
  await page.screenshot({ path: '<SAVE_SCREENSHOT_PATH>/screenshot-' + timestamp + '.png' });
  try {
    var symtarget = fs.readlinkSync('<SAVE_SCREENSHOT_PATH>/screenshot.png');
    fs.unlink(symtarget, callback);
  } catch (e) {
    // Symlink doesn't exist yet. Just ignore.
  }
  fs.unlink('<SAVE_SCREENSHOT_PATH>/screenshot.png', callback);
  fs.symlink('<SAVE_SCREENSHOT_PATH>/screenshot-' + timestamp + '.png',
             '<SAVE_SCREENSHOT_PATH>/screenshot.png',
             'file',
             callback);
  await browser.close();

})();

# Use cron to schedule the Puppeteer to run every 5 minutes:
*/5 * * * * node <PATH_TO>/website-screenshots.js

# Update nginx to disable cache control for the image file:

    location /<WEB_FOLDER>/screenshot.png {
        add_header Cache-Control no-cache;
    }

# If Cloudflare is being used as a CDN, set the "Browser Cache TTL" to "Respect Existing Headers".

# Github cache can be flushed manually by firstly confirming cache-control is set to no-cache:

curl -I <url_image>

# and then Purging the image from Github's Camo CDN. To get the CAMO_URL of the cached image, right
# click on the target image in the README webpage:

curl -X PURGE <CAMO_URL>

# References:
https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/about-anonymized-image-urls

--->
