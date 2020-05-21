# Canvas Image Resizer

HTML canvases resize automatically when you resize the HTML element, but they do not automatically resize the images.

I was kinda getting annoyed that it wasn't easy, so I wanted to figure it out. :p

This is an example of how to pin an image to a resolution (or the canvas resolution), and scale it proportionally. I added the ability to lock the X and Y to a maximum of 1.0 as well, if that's desired.

No frameworks, one big file, raw JS. Only tested in Chrome.

## Important Code Bits

```js
// Target 1920 x 1080
let targetResolution = { width: 1920, height: 1080 };

// These will be small numbers, usually between 0 (exclusive) and 5.0. Depends on the screen size. :p
let xscale = canvas.innerWidth / targetResolution.width;
let yscale = canvas.innerHeight / targetResolution.height;

// Setup a resize event for the window.
window.addEventListener('resize', () => {
  xscale = canvas.innerWidth / targetResolution.width;
  yscale = canvas.innerHeight / targetResolution.height;
});


// When drawing an image
let xwidth = Math.round(image.width * xscale);
let xheight = Math.round(image.height * yscale);

// drawImage()
// arg[0] - image = image source
// arg[1] - 0 = useful for tilesets, start from X 0 on the source image
// arg[2] - 0 = useful for tilesets, start from X 0 on the source image
// arg[3] - image.width = take the full width of the source image, would be smaller for tilesets
// arg[4] - image.height = take the full height of the source image, would be smaller for tilesets
// arg[5] - x = where to draw the leftmost point of the image on the canvas
// arg[6] - y = where to draw the topmost point of the image on the canvas
// arg[7] - xwidth = taking the source image width from arg[3], how big/small should it be in width (this is the squash/stretch)
// arg[8] - xheight = taking the source image height from arg[4], how big/small should it be in height (this is the squash/stretch)
ctx.drawImage(image, 0, 0, image.width, image.height, x, y, xwidth, xheight);
```

Also check this out: <https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/drawImage>

## Contributing

Create a pull request into master and @ me.

## License

MIT, go nuts.
