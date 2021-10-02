# fallworkshops2021
fallworkshops2021
//cloud-related code
let cloud;
var changeDirection;
var posX = 0;

//leaf-related code
let redLeaf;
let yellowLeaf;
let multiLeaf;
var leaves = [];

function preload() {
  cloud = loadImage("cloud.png");
  redLeaf = loadImage("redleaf.png");
  yellowLeaf = loadImage("yellowleaf.png");
  multiLeaf = loadImage("multicolorleaf.png");
}

function setup() {
  bg = loadImage("kinkade.jpg");
  createCanvas(400, 400);
  //cloud-related code
  changeDirection = false;

  //createLoop({duration:5,gif:true})
}

function draw() {
  background(bg);
  //cloud-related code
  makecloudmove();
  //leaf-related code
  for (var i = 0; i < leaves.length; i++) {
    leaves[i].move();
    leaves[i].display();
  }
}

function leafImage(num) {
  switch (num) {
    case 0:
      leaf = redLeaf;
      break;
    case 1:
      leaf = yellowLeaf;
      break;
    case 2:
      leaf = multiLeaf;
      break;
  }
  return leaf;
}

function mousePressed() {
  randomNum = floor(random() * 3);
  leaves.push(
    new Leaf(
      mouseX,
      mouseY,
      random(-2, 2),
      random(200, 375),
      leafImage(randomNum)
    )
  );
}

function Leaf(inX, inY, dir, fall, img) {
  this.x = inX;
  this.y = inY;

  this.move = function () {
    if (this.y >= fall) {
      this.x += 0; //this.x = this.x + 0
      this.y += 0;
    } else {
      this.x += dir;
      this.y += 1;
    }
  };
}

this.display = function () {
  image(img, this.x, this.y, 10, 10);
};
function makecloudmove() {
  image(cloud, 50 - posX, 0, 180, 120);

  if (posX > 10) {
    changeDirection = true;
  } else if (round(posX) <= 0) {
    changeDirection = false;
  }

  if (round(posX) >= 0 && changeDirection == false) {
    posX += 0.1;
  } else if (changeDirection == true) {
    posX -= 0.1;
  }
}
