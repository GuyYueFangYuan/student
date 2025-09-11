---
layout: default
# Changes layout form
title: Background with Object
description: Use JavaScript to have an in-motion background.
#Change the flying UFO part to change the image
#Need to save before regenerating
sprite: images/platformer/sprites/bird.png
#background of the animation
background: images/platformer/backgrounds/OIP.webp
permalink: /background/
---

<style>
  html, body { margin: 0; padding: 0; }
  #world {
    position: fixed; inset: 0;  /* full screen */
    width: 100vw; height: 100vh; display: block;
  }
</style>

<canvas id="world"
        data-bg="{{ page.background | relative_url }}"
        data-sprite="{{ page.sprite | relative_url }}"></canvas>

<script>
document.addEventListener('DOMContentLoaded', () => {
  const canvas = document.getElementById('world');
  const ctx = canvas.getContext('2d');

  function sizeCanvas() {
    canvas.width  = window.innerWidth;
    canvas.height = window.innerHeight;
  }
  sizeCanvas();
  window.addEventListener('resize', sizeCanvas);

  // Resolve image paths via data-attributes (already passed through relative_url)
  const backgroundImg = new Image();
  const spriteImg = new Image();
  backgroundImg.src = canvas.dataset.bg;
  spriteImg.src = canvas.dataset.sprite;

  Promise.all([
    new Promise(r => backgroundImg.onload = r),
    new Promise(r => spriteImg.onload = r),
  ]).then(startGameWorld);
//This starts the game
  function startGameWorld() {
    class GameObject {
      constructor(image, width, height, x = 0, y = 0, speedRatio = 0) {
        this.image = image;
        this.width = width;
        this.height = height;
        this.x = x;
        this.y = y;
        this.speedRatio = speedRatio;
        this.speed = GameWorld.gameSpeed * this.speedRatio;
      }
      update() {}
      draw(ctx) { ctx.drawImage(this.image, this.x, this.y, this.width, this.height); }
    }
//This ensures that the background scrolls off the screen
    class Background extends GameObject {
      constructor(image, gw) {
        super(image, gw.width, gw.height, 0, 0, 0.1);
      }
      update() { this.x = (this.x - this.speed) % this.width; }
      draw(ctx) {
        ctx.drawImage(this.image, this.x, this.y, this.width, this.height);
        ctx.drawImage(this.image, this.x + this.width, this.y, this.width, this.height);
      }
    }

    class Player extends GameObject {
      constructor(image, gw) {
        const w = Math.floor(image.naturalWidth  / 2);
        const h = Math.floor(image.naturalHeight / 2);
        const x = Math.floor((gw.width  - w) / 2);
        const y = Math.floor((gw.height - h) / 2);
        super(image, w, h, x, y);
        this.baseY = y; this.frame = 0;
      }
      update() {
        this.y = this.baseY + Math.sin(this.frame * 0.05) * 20;
        this.frame++;
      }
    }
/* 
This code
Resizes background to fill the canvas
Recenters the player to stay in the middle
*/
    class GameWorld {
      static gameSpeed = 5;
      constructor(bgImg, spImg) {
        this.canvas = canvas; this.ctx = ctx;
        this.width = canvas.width; this.height = canvas.height;
        this.objects = [ new Background(bgImg, this), new Player(spImg, this) ];

        window.addEventListener('resize', () => {
          this.width = canvas.width; this.height = canvas.height;
          const bg = this.objects[0];
          bg.width = this.width; bg.height = this.height;
          const p = this.objects[1];
          p.x = Math.floor((this.width - p.width)/2);
          p.baseY = Math.floor((this.height - p.height)/2);
        });
      }
      gameLoop() {
        this.ctx.clearRect(0, 0, this.width, this.height);
        for (const o of this.objects) { o.update(); o.draw(this.ctx); }
        requestAnimationFrame(this.gameLoop.bind(this));
      }
      start() { this.gameLoop(); }
    }

    const world = new GameWorld(backgroundImg, spriteImg);
    world.start();
  }
});
</script>
