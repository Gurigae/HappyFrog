let bubble = [];
let score = 0;
let maxbubble;
let amount = 5;
let speed = 1;
let timer = 2;
let chapter = 1;
let popped;
let total = 0;
let frog;
let food;

function preload() {
  popped = loadSound("pop.wav");
  frog = loadImage("Frog.png");
  dragonfly = loadImage("food.png");
  cloud = loadImage("cloud.png");
}

function setup() {
  createCanvas(800, 800);
  colorMode(HSB);

  createBouncerArray(amount, speed);
}

function createBouncerArray(level, multiplier) {
  maxbubble = level;

  for (let i = 0; i < maxbubble; i++) {
    let x = random(width);
    let y = random(height);
    let speedX = random(-0.5, 0.5) * multiplier;
    let speedY = random(-0.5, 0.5) * multiplier;
    let radius = random(10, 25);

    let b = new Bouncer(x, y, speedX, speedY, radius);
    bubble.push(b);
  }
}

function gameOver() {
  noLoop();
  background(200, 90, 30);
  //image(gameover,50,20);
  textSize(40);
  text("SCORE:" + total, width / 2 - 60, height / 2 + 70);
  textSize(40);
  text("LEVEL:" + chapter, width / 2 - 50, height / 2 + 120);
  textSize(80);
  text("GAME OVER!", width / 2 - 220, height / 2);
}

function draw() {
  background(195, 100, 100);
  fill(120, 100, 100);
  rect(0, 780, 800, 50);
  image(frog, 350, 700, width / 6, height / 6);
  image(cloud, 40, 100, width / 4, height / 4);
  image(cloud, 300, 50, width / 4, height / 4);
  image(cloud, 600, 110, width / 4, height / 4);
  stroke(255, 0, 10);
  if (mouseIsPressed) {
    stroke(0, 100, 90);
    strokeWeight(3);
    line(pmouseX, pmouseY, width / 4 + 210, height - 40);
  }

  let i = 0;
  for (let bounce of bubble) {
    bounce.show();
    bounce.move();
    bounce.bounce();

    if (
      mouseIsPressed &&
      dist(mouseX - 30, mouseY - 20, bounce.x, bounce.y) < bounce.radius
    ) {
      bubble.splice(i, 1);
      score++;
      total++;
      popped.play();
    }

    i++;
  }

  textSize(30);
  fill(0);
  stroke(0, 0, 0);
  strokeWeight(0);
  if (score == maxbubble) {
    textSize(40);
    text("성공!", 370, 400);
    //image(clearscreen,130,200);
    textSize(20);
    text("스페이스 바를 누르세요!", 300, 450);
    if (key == " " && keyIsPressed) {
      amount *= 2;
      speed *= 1.7;

      createBouncerArray(amount, speed);
      score = 0;
      chapter++;
    }
  } else {
    textSize(18);
    text("SCORE: " + total, 10, 30);
    textSize(18);
    text("TIME: " + timer, 10, 60);
    textSize(18);
    text("LEVEL: " + chapter, 10, 90);
    if (frameCount % 60 == 0 && timer > 0) {
      timer--;
      if (timer == 0) {
        gameOver();
      }
    }
  }
}

class Bouncer {
  constructor(tempX, tempY, tempSpeedX, tempSpeedY, tempRadius) {
    this.x = tempX;
    this.y = tempY;
    this.speedX = tempSpeedX;
    this.speedY = tempSpeedY;
    this.radius = tempRadius;
  }

  show() {
    fill(this.color, 60, 100);
    //stroke();
    image(dragonfly, this.x, this.y, width / this.radius, height / this.radius);
  }

  move() {
    this.x += this.speedX;
    this.y += this.speedY;
  }

  bounce() {
    if (this.x < 0 || this.x > width) {
      this.speedX = -this.speedX;
    }

    if (this.y < 0 || this.y > height) {
      this.speedY = -this.speedY;
    }
  }
}
