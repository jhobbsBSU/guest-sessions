---
marp: true
paginate: true
theme: default
---

# Creative Coding Workshop
April 9 2025

---

# Objectives

- Introduce p5.js
- Learn some basic programming techniques
- Build a simple game

---
# What is p5.js?
- Javascript library for creative coding
- Designed to make coding accessible for artists, designers & beginners
- Built on top of web standards (HTML5 canvas, JS)

<!--
Before we dive in, let me give you a quick intro to what p5.js is.

It's a JavaScript library built for creative coding — meaning it's designed to help you make interactive visuals, art, games, and more.

What's cool is it's built to be accessible to everyone, not just experienced coders. Artists, designers, beginners — all can pick it up quickly.

Plus, it's all web-based, so everything you make runs right in your browser.
-->

---
# Why use p5.js?

- Beginner-friendly syntax
- Instant visual feedback
- Interactive 'sketches' can be used for games, art, data visualisations and more
- Lots of community examples and references

<!--
So why use p5.js in a workshop like this?

It’s very beginner-friendly — no complicated setup, and the syntax is simple.

You get instant visual results, which is perfect for learning and experimenting.

It’s great for building games, generative art, and even visualizations.

Plus, there’s a huge community and lots of example projects to get inspired by.
-->

---
# p5.js Examples
- [Snakes](https://openprocessing.org/sketch/469866)
- [Networks](https://openprocessing.org/sketch/111878)
- [Escheresque](https://openprocessing.org/sketch/1223047)

Many [more](https://openprocessing.org/browse) and [more](https://p5js.org/examples/)...

---
# Galactic-orb Bopper

- Simple circle clicking game
- Key Concepts:
    - Basic logic and control structures
    - Canvas drawing
    - Randomisation
    - Event handling
- References: 
    - Slides - https://bit.ly/ob-slides
    - Full Code - https://bit.ly/ob-code

---
# Step 1 - Setup

- Go to [editor.p5js.org](https://editor.p5js.org/)
- Add the following code
```javascript
function setup() {
  createCanvas(windowWidth, windowHeight);
}

function draw() {
  background(220);
}
```
<!--
- Go to editor and give brief overview
- Explain setup and draw
- Demo changing background color
-->
---

# Step 2 - Add an Orb

```javascript
let circleX = 275, circleY = 175, circleSize = 50;

function setup() {
  createCanvas(600, 400);
}

function draw() {
  background(220);
  ellipse(circleX, circleY, circleSize);
}
```

<!--
Introduce variables
Introduce basic drawing - e.g. ellipse
-->

---

# Step 3 - Randomising the Orb

```javascript
let circleX, circleY, circleSize = 50;

function setup() {
  createCanvas(600, 400);
  newCircle();
}

function draw() {
  background(220);
  ellipse(circleX, circleY, circleSize);
}

function newCircle() {
  circleX = random(circleSize, width - circleSize);
  circleY = random(circleSize, height - circleSize);
}
```
<!--
- Introduce random and explain how it works
-->
---


# Step 4 - Detecting clicks

```javascript
function mousePressed(){
  newCircle();
}
```
<!--
Explain mousePressed is an in built function that listens for events on our behalf
-->
---

# Step 5 - Bopping Orbs

```javascript
function mousePressed(){
  let d = dist(mouseX, mouseY, circleX, circleY);
  if (d < circleSize / 2) {
    newCircle();
  }
}
```

<!--
dist(mouseX, mouseY, circleX, circleY) calculates the distance between the mouse pointer (mouseX, mouseY) and the center of the circle (circleX, circleY).

If the distance is less than the radius of the circle, the mousePressed() function recognizes that the circle has been clicked
-->

---
# Step 6 - Adding Score (i)

```javascript
let score = 0; // add score variable
```
<br />

```javascript
function mousePressed(){
  let d = dist(mouseX, mouseY, circleX, circleY);
  if (d < circleSize / 2) {
    score++; // increment score
    newCircle();
  }
}
```

<!--
add the variable and increment in mousePressed
-->

---
# Step 6 - Adding score (ii)

```javascript
function draw() {
  background(220);
  ellipse(circleX, circleY, circleSize);

  // drawing the score to screen
  fill(0);
  textSize(24);
  text("Score: " + score, 10, 30);
}
```

<!--
Draw text to screen

Ask students why the circles are now black?
-->
---
# Step 7 - Add a timer (i)

```javascript
let timeLeft = 30; // add variable
```

<br />

```javascript
function setup() {
  createCanvas(windowWidth, windowHeight);
  newCircle();

  //Create a timer that runs every second
  setInterval(() => {
    if (timeLeft > 0){
        timeLeft--;
    } 
  }, 1000);
}
```
<!--
Add time variable

Implement setInterval
-->
---
# Step 7 - Add a timer (ii)

```javascript
function draw() {
  background(220);
  ellipse(circleX, circleY, circleSize);

  fill(0);
  textSize(24);
  text("Score: " + score, 10, 30);

  //draw time to screen
  text("Time: " + timeLeft, 10, 60);

  //check if time remains
  if (timeLeft == 0) {
    noLoop();
    text("Game Over", width / 2 - 50, height / 2);
  }
}
```
---
# Extending the game

- Fade circles
    - Alter difficulty
- Change circle colours
    - Different points for different circles
- Move the circles
- Store high score
- Add sounds
