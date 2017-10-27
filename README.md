
Installation: `npm install --save jimp`

## Basic usage ##

The static `Jimp.read` method takes the path to a PNG, JPEG or BMP file and (optionally) a Node-style callback and returns a Promise:

```js
Jimp.read("./path/to/image.jpg", function (err, image) {
    // do stuff with the image (if no exception)
});
```

The method can also read a PNG, JPEG or BMP buffer or from a URL:

```js
Jimp.read("http://www.example.com/path/to/lenna.jpg", function (err, image) {
    // do stuff with the image (if no exception)
});
```

### Creating new images ###

If you want to begin with an empty Jimp image, you can call the Jimp constructor passing the width and height of the image to create and (optionally) a Node-style callback:

```js
var image = new Jimp(256, 256, 0xFF0000FF, function (err, image) {
    // this image is 256 x 256, every pixel is set to 0xFF0000FF
});
```

### Low-level manipulation ###

Jimp enables low-level manipulation of images in memory through the bitmap property of each Jimp object:
```js
image.bitmap.data;  // a Buffer of the raw bitmap data
image.bitmap.width; // the width of the image
image.bitmap.height // the height of the image
```

Alternatively, you can manipulate individual pixels using the following these functions:

```js
image.getPixelColor(x, y);      // returns the colour of that pixel e.g. 0xFFFFFFFF
image.setPixelColor(hex, x, y); // sets the colour of that pixel
```

Two static helper functions exist to convert RGBA values into single integer (hex) values:

```js
Jimp.rgbaToInt(r, g, b, a); // e.g. converts 255, 255, 255, 255 to 0xFFFFFFFF
Jimp.intToRGBA(hex);        // e.g. converts 0xFFFFFFFF to {r: 255, g: 255, b: 255, a:255}
```


