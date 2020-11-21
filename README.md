# p5-glitch-effects
Research on glitch effects in the context of a p5 sketch 

## Basic structure

### Input image https://unsplash.com/photos/YDNvydD1jAY
![flowers](flowers.png)

```javascript
// A variable to store image data
let img;

// Load the image data into the variable
function preload() {
  img = loadImage('flowers.png');
}

// Use the image data
function setup() {
  // Same size as the image
  createCanvas(800, 533);
  // Render the image data with p5's image()
  // https://p5js.org/reference/#/p5/image
  image(img, 0, 0);
}
```

## Using the image function creatively
![flowers](flowers-glitch-simple.jpg)

```javascript
// A variable to store image data
let img;

// Load the image data into the variable
function preload() {
  img = loadImage('flowers.png');
}

// Use the image data
function setup() {
  // Same size as the image
  createCanvas(800, 533);
  // Render the image
  image(img, 0, 0);
  // Render 5000 smaller sections 
  // of the image with a random offset on top
  for (let t = 5000; t > 0; t -= 1) {
    const x = random(width);
    const y = random(height);
    const ox = random(-20, 20);
    const w = floor(random(1, 100));
    const h = floor(random(1, 100));
    const g = img.get(x, y, w, h);
    image(g, x + ox, y);
  }
}
```

## Using the image function creatively
![flowers](flowers-glitch-intermediate.jpg)

```javascript
let img; 

function preload() {
  img = loadImage('flowers.png');
}

function setup() {
  createCanvas(800, 533);
  for (let x = 0; x < width; x += 1) {
    const colors = [];
    for (let y = 0; y < img.height; y += 1) {
      const col = img.get(x, y);
      colors.push(col);
    }
    if (random(0, 1) > 0.5) {
      if (random(0, 1) > 0.5) colors.sort();
      if (random(0, 1) > 0.5) colors.reverse();
    }
    for (let y = 0; y < height; y += 1) {
      stroke(colors[y]);
      point(x, y);
    }
  }
}
```

## Using the image function creatively
![flowers](flowers-glitch-advanced.jpg)

```javascript
let img;

function effect(buffer) {
  const gfx = createGraphics(buffer.width, buffer.height);
  gfx.loadPixels();
  for (let x = 0; x < gfx.width; x += 1) {
    const colors = [];
    for (let y = 0; y < buffer.height; y += 1) {
      colors.push(buffer.get(x, y));
    }
    if (random(0, 1) > 0.5) {
      if (random(0, 1) > 0.5) { colors.sort(); }
      if (random(0, 1) > 0.5) { colors.reverse(); }
    }
    for (let y = 0; y < gfx.height; y += 1) {
      gfx.set(x, y, colors[y]);
    }
  }
  gfx.updatePixels();
  return gfx;
}

function preload() {
  img = loadImage(name + ext);
}

function setup() {
  createCanvas(800, 533);
  image(img, 0, 0);
  for (let t = 0; t < 550; t += 1) {
    const x = random(width);
    const y = random(height);
    const ox = random(-20, 20);
    const w = floor(random(1, 100));
    const h = floor(random(1, 100));
    const g = img.get(x, y, w, h);
    image(effect(g), x + ox, y);
  }
}
```
