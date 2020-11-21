# p5-glitch-effects
Research on glitch effects in the context of a p5 sketch 

## Basic structure

### Input image https://unsplash.com/photos/YDNvydD1jAY
![flowers](flowers.png)

```javascript
let img;

function preload() {
  img = loadImage('flowers.png');
}

function setup() {
  createCanvas(800, 800);
  image(img, 0, 0);
}
```

## Using the image function creatively
![flowers](flowers-glitch-simple.jpg)

```javascript
let img;

function preload() {
  img = loadImage('flowers-glitch-simple.png');
}

function setup() {
  createCanvas(800, 533);
  image(img, 0, 0);
  for (let t = 5000; t > 0; t -= 1) {
    const x = random(width);
    const y = random(height);
    const ox = random(-20, 20);
    const w = floor(random(1, 100));
    const h = floor(random(1, 100));
    const g = img.get(x, y, w, h);
    image(g, x + ox, y);
  }
  save('flowers-glitch-simple.jpg');
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
  save('flowers-glitch-intermediate.jpg');
}
```
