# Radar Project #
ไลบรารี่ในการตัดภาพพื้นหลังและคำนวณระดับปริมาณน้ำฝนในบริเวณพื้นที่ที่สนใจ ใช้สำหรับ Javascript และ Node.js 

## Installation ## 
`npm install --save jimp`

## Basic usage ##
เมธอด `Jimp.read` ใช้ในการอ่านไฟล์ภาพไม่ว่าจะเป็นไฟล์ PNG, JPEG, BMP หรือจาก URL ก็ได้เช่นกัน
```js
Jimp.read("./path/to/image.jpg", function (err, image) {
    // do stuff with the image (if no exception)
});

Jimp.read("http://www.example.com/path/to/lenna.jpg", function (err, image) {
    // do stuff with the image (if no exception)
});
```

### Creating new images ###
หากคุณมีความต้องการสร้างรูปภาพเปล่าๆ พร้อมทั้งกำหนดความกว้างและความยาวของภาพ สามารถใช้คำสั่งได้ดังนี้:
```js
var image = new Jimp(256, 256, 0xFF0000FF, function (err, image) {
    // สร้างภาพขนาด 256 x 256 ทุกพิกเซลจะถูก set ด้วยสี 0xFF0000FF
});
```

### Low-level manipulation ###

หากต้องการทราบความกว้างและความยาวของรูปภาพ สามารถใช้คำสั่งได้ดังนี้:
```js
image.bitmap.width; // the width of the image
image.bitmap.height // the height of the image
```

คุณสามารถจัดการกับสีของแต่ละพิกเซลด้วยฟังก์ชั่นเหล่านี้
```js
image.getPixelColor(x, y);      // เก็บค่าสีที่ตำแหน่ง x,y และรีเทิร์นสีออกมาในรูปแบบจำนวนเต็ม อย่างเช่น 0xFFFFFFFF
image.setPixelColor(hex, x, y); // เซตค่าสีของแต่ละพิกเซล
```

ใน 2 ฟังก์ชั่นนี้จะช่วยในการ convert ค่าสี RGBA ให้กลายเป็นค่าสี single integer (hex)
```js
Jimp.rgbaToInt(r, g, b, a); // e.g. converts 255, 255, 255, 255 to 0xFFFFFFFF
Jimp.intToRGBA(hex);        // e.g. converts 0xFFFFFFFF to {r: 255, g: 255, b: 255, a:255}
```

## Writing to files and buffers ##

### Writing to files ###

สามารถ writing รูปภาพในไฟล์ PNG, JPEG หรือ BMP ลง disk โดยใช้คำสั่งดังนี้:

```js
image.write( path, cb ); 
```

### Writing to Buffers ###


A PNG, JPEG or BMP binary Buffer of an image:

```js
image.getBuffer( mime, cb ); // Node-style callback will be fired with result
```

MIME types:
```js
Jimp.MIME_PNG;  // "image/png"
Jimp.MIME_JPEG; // "image/jpeg"
Jimp.MIME_BMP;  // "image/bmp"
```

