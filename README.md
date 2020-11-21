# p5-glitch-effects
Research on glitch effects in the context of a p5 sketch 

## Basic structure

### Input image
[flowers](flowers.png)

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
```javascript
let img;

function preload() {
  img = loadImage('flowers.png');
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
