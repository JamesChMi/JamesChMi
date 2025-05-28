let y = 0;
let colors = [];
let currentInfo = 0;
let infoStrings = [];
let fadeAlpha = 0;
let fadeIn = true;

function setup() {
  createCanvas(800, 600);
  textAlign(CENTER, CENTER);
  textSize(24);
  
  // Create a color palette
  colors = [
    color(255, 100, 100),
    color(100, 255, 100),
    color(100, 100, 255),
    color(255, 255, 100),
    color(255, 100, 255),
    color(100, 255, 255)
  ];
  
  // Set up your introduction info
  infoStrings = [
    "Hello! I'm James C.M",
    "I'm 15 years old",
    "Currently learning: Java & Lua",
    "Find me on Discord: @JamesChMi",
    "Pronouns: He/him",
    "Fun fact: I'm lazy so I often use tutorials or AI help",
    "Born in Brazil 🇧🇷"
  ];
}

function draw() {
  background(0);
  
  // Draw pulsing title
  let pulseSize = sin(frameCount * 0.05) * 5 + 30;
  fill(colors[frameCount % colors.length]);
  textSize(pulseSize);
  text("About Me", width/2, 50);
  
  // Draw current info with fade effect
  if (fadeIn) {
    fadeAlpha += 5;
    if (fadeAlpha >= 255) {
      fadeAlpha = 255;
      if (frameCount % 100 == 0) {
        fadeIn = false;
      }
    }
  } else {
    fadeAlpha -= 5;
    if (fadeAlpha <= 0) {
      fadeAlpha = 0;
      currentInfo = (currentInfo + 1) % infoStrings.length;
      fadeIn = true;
    }
  }
  
  fill(255, fadeAlpha);
  textSize(28);
  text(infoStrings[currentInfo], width/2, height/2);
  
  // Draw footer
  fill(150);
  textSize(16);
  text("(This intro was made with p5.js - because I'm learning!)", width/2, height - 30);
  
  // Draw some floating shapes for decoration
  for (let i = 0; i < 10; i++) {
    let x = (frameCount * 0.5 + i * 100) % (width + 100) - 50;
    let y = height/2 + sin(frameCount * 0.02 + i) * 100;
    fill(colors[i % colors.length], 100);
    noStroke();
    if (i % 3 == 0) {
      ellipse(x, y, 30, 30);
    } else if (i % 3 == 1) {
      rect(x, y, 25, 25);
    } else {
      triangle(x, y, x+20, y+20, x-20, y+20);
    }
  }
}

function mousePressed() {
  // Click to manually advance info
  fadeIn = false;
  fadeAlpha = 255;
}
