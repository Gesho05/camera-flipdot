# Flipboard Camera

A small web app that samples the camera feed and renders a low-resolution "flipboard" dot display (84×28) based on the camera image.

## What it does
- Captures the user's webcam stream.
- Draws the camera frame into a hidden canvas at a fixed logical resolution.
- Samples pixels from the canvas to decide whether each flipdot is on/off and updates a grid of dots accordingly.

## Project structure
- `index.html` — main page containing `<video>` and `<canvas>` elements and the flipboard container (`<section>`).
- `css/index.css` — styles for the flipboard dots and canvas/video borders.
- `js/js.js` — application logic: camera setup, drawing to canvas, sampling pixels, and updating the flipboard grid.

## How to run
Browsers typically restrict camera access on file:// pages, so run a simple local server (using Live server or 5 server extention) and open the page in a browser.

## Usage
1. Open the page in the browser and allow camera permission.
2. The canvas (green border) draws the live camera feed at the configured resolution. The flipboard dots will update based on brightness.

## Key implementation notes
- The canvas has an internal pixel buffer (its `width`/`height` attributes) and a CSS display size. The app sets the canvas internal size to 640×360 and uses the same dimensions when drawing and sampling. This prevents sampling only the top-left portion of the camera feed.
- The sampling grid is defined by `flipboard_display_size = [84, 28]` in `js/js.js`.
- Video/canvas logical resolution constants are defined as `VIDEO_W = 640` and `VIDEO_H = 360` in `js/js.js`. If you change these, update both the canvas attributes in `index.html` and the constants in `js/js.js`.

## Troubleshooting
- Camera not allowed: make sure the browser prompt was accepted and no other application is blocking the camera.
- Still seeing only a portion of the feed:
  - Confirm `canvas.width` and `canvas.height` are set (the repository sets them to 640×360 by default).
  - Check the browser console for errors.
  - Try a different camera resolution by editing `VIDEO_W`/`VIDEO_H` in `js/js.js` and matching the canvas attributes in `index.html`.
- If the feed is black or frozen, ensure the `video_element.srcObject` is set and `video_element.play()` is called (current code handles this).

## Files changed (session)
- `index.html` — added `playsinline` attribute to `<video>` and set `<canvas width="640" height="360">` so the canvas internal size matches expected sampling coordinates.
- `js/js.js` — introduced `VIDEO_W`/`VIDEO_H` constants and made draw/sampling use those constants.
