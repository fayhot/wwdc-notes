## [Performance](2-performance.md) | Shloka Kini | 1330 | p44


- Font Collections
- font-display Descriptor 
- Videos in Image Elements
- Passive Event Listeners
- Async Image Decoding
- Beacon API

### Font Collections

Similar Unicode fonts downloaded more quickly

### `font-display` Descriptor

```css
@font-face {
font-family: ExampleFont;
src: url(/path/to/fonts/myfont.woff) format('woff'); font-weight: 400;
font-style: normal;
font-display: fallback;
}
```

### Videos in Image Elements

MP4 with H.264 encoding (NEW)

```html
<img src="explosion.mp4" alt="Color Explosion">
```

In CSS background image property:

```html
<style>
    body {
background-image: url("explosion.mp4"); }
</style>
```

Fallback images

```html
<picture>
    <source srcset="explosion.mp4" type="video/mp4"> <img src="explosion.jpg">
</picture>
```

Passive Event Listeners
Enabled on document, window, and body elements by default Flag to always allow scrolling
No interruptions
NEW

```js
document.addEventListener('touchstart', (e) => { ...
}, { passive: true })
```


### Image Decoding

Synchronous
- Main thread is blocked
- User interactions prevented until   all images are decoded

Asynchronous
- On separate thread
- Parallel decoding operations
- User interactions aren't blocked


### Async Image Decoding

Markup: Add the decoding attribute to an element JavaScript: Use HTMLImageElement.decode()

### Beacon API

Asynchronous request on unload event

- Sends data on unload without   waiting for a response
- Smooth browser navigation while   waiting for response
- Ensures delivery of data while   Safari is running

### Demo - Jason Sandmeyer, Marketing Communications

