---
layout: post
title: Cyrus about me
permalink: /about/
comments: true
---


## As a conversation Starter


<comment>``
Here are some places I lived in.
Harbin, China
Austin, Texas
San Diego, California
</comment>


<style>
    /* Style looks pretty compact,
       - grid-container and grid-item are referenced the code
    */
    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); /* Dynamic columns */
        gap: 10px;
    }
    .grid-item {
        text-align: center;
    }
    .grid-item img {
        width: 100%;
        height: 100px; /* Fixed height for uniformity */
        object-fit: contain; /* Ensure the image fits within the fixed height */
    }
    .grid-item p {
        margin: 5px 0; /* Add some margin for spacing */
    }


    .image-gallery {
        display: flex;
        flex-wrap: nowrap;
        overflow-x: auto;
        gap: 10px;
        }


    .image-gallery img {
        max-height: 150px;
        object-fit: cover;
        border-radius: 5px;
    }
</style>


<!-- This grid_container class is used by CSS styling and the id is used by JavaScript connection -->
<div class="grid-container" id="grid_container">
    <!-- content will be added here by JavaScript -->
</div>


<script>
  // --- Fallbacks to prevent ReferenceErrors without changing your loops ---
  window.http_source = window.http_source || "";


  window.living_in_the_world = window.living_in_the_world || [
    {
      flag: "https://flagcdn.com/w320/cn.png",
      description: "Harbin, China",
      greeting: "你好 (Nǐ hǎo)"
    },
    {
      flag: "https://flagcdn.com/w320/us.png",
      description: "Austin, Texas",
      greeting: "Howdy!"
    },
    {
      flag: "https://flagcdn.com/w320/us.png",
      description: "San Diego, California",
      greeting: "Hey! 🌊"
    }
  ];
</script>


<!-- Tree -->
<div class="sakura-wrap">
  <div class="sakura-tree">
    <div class="trunk"></div>
    <div class="branch b1"></div>
    <div class="branch b2"></div>
    <div class="branch b3"></div>
    <div class="canopy"></div>
    <div class="petals" id="petals"></div>
  </div>
</div>
<style>
  /* Sakura layout */
  .sakura-wrap{
    position: relative;
    width: 100%;
    height: 280px;
    margin: 20px 0 10px 0;
    overflow: hidden;
    background: linear-gradient(#f9fbff, #f2f7ff);
    border-radius: 10px;
  }
  .sakura-tree{
    position: absolute;
    bottom: 0;
    left: 50%;
    transform: translateX(-35%);
    width: 260px;
    height: 260px;
  }
  .trunk{
    position: absolute;
    bottom: 0;
    left: 45%;
    width: 30px;
    height: 160px;
    background: linear-gradient(180deg, #6b3e2e, #4d2b20);
    border-radius: 15px;
    box-shadow: inset 0 0 6px rgba(0,0,0,.25);
    transform: skewX(-3deg);
  }
  .branch{
    position: absolute;
    width: 90px;
    height: 14px;
    background: #5a3528;
    border-radius: 7px;
    transform-origin: left center;
    box-shadow: inset 0 0 4px rgba(0,0,0,.25);
  }
  .branch.b1{ bottom: 120px; left: 45%; transform: rotate(-12deg); }
  .branch.b2{ bottom: 95px;  left: 45%; transform: rotate(15deg); width: 110px; }
  .branch.b3{ bottom: 70px;  left: 45%; transform: rotate(-22deg); width: 100px; }


  .canopy{
    position: absolute;
    bottom: 135px;
    left: 10px;
    width: 220px;
    height: 140px;
    background: radial-gradient(circle at 50% 60%, #ffd6e7 0%, #ffc2dc 55%, #ffb1d3 80%, #ffa6cd 100%);
    border-radius: 50% 55% 45% 55% / 55% 55% 45% 45%;
    filter: drop-shadow(0 6px 6px rgba(0,0,0,.1));
  }


  /* Petals */
  .petals{ position: absolute; inset: 0; pointer-events: none; }
  .petal{
    position: absolute;
    top: -20px;
    width: 10px;
    height: 14px;
    background: radial-gradient(ellipse at 60% 40%, #ffe1ed 0%, #ffc9df 60%, #ffb1d3 100%);
    border-radius: 60% 60% 60% 60% / 70% 70% 40% 40%;
    opacity: .9;
    transform: rotate(0deg) translateZ(0);
    will-change: transform, opacity;
    animation-name: fall, sway, spin;
    animation-duration: 6s, 3.5s, 7s;
    animation-timing-function: linear, ease-in-out, linear;
    animation-iteration-count: infinite, infinite, infinite;
  }
  .petal::after{
    /* subtle notch */
    content: "";
    position: absolute;
    left: 3px; top: 2px;
    width: 6px; height: 6px;
    background: radial-gradient(circle at 70% 30%, #fff1f7 0%, transparent 70%);
    border-radius: 50%;
  }


  @keyframes fall {
    0%   { transform: translateY(-20px) translateX(0) rotate(0deg); opacity: .95; }
    100% { transform: translateY(320px) translateX(0) rotate(360deg); opacity: .2; }
  }
  @keyframes sway {
    0%,100% { transform: translateX(0); }
    50%     { transform: translateX(30px); }
  }
  @keyframes spin {
    0%   { transform: rotate(0deg); }
    100% { transform: rotate(720deg); }
  }


  /* Small screens: shrink a bit */
  @media (max-width: 520px){
    .sakura-wrap{ height: 220px; }
    .sakura-tree{ transform: translateX(-40%) scale(.9); }
  }
</style>


<script>
  // Generate petals with randomized positions, delays, and speeds
  (function(){
    const petalContainer = document.getElementById('petals');
    if (!petalContainer) return;


    const PETAL_COUNT = 45; // tweak to your taste


    function spawnPetal(){
      const p = document.createElement('div');
      p.className = 'petal';


      // Random horizontal start within container
      const wrapWidth = petalContainer.clientWidth || 600;
      p.style.left = Math.random() * wrapWidth + 'px';


      // Randomize animation durations/delays for natural feel
      const fallDur = 5 + Math.random() * 4;   // 5–9s
      const swayDur = 3 + Math.random() * 2.5; // 3–5.5s
      const spinDur = 6 + Math.random() * 4;   // 6–10s
      const delay   = Math.random() * 5;


      p.style.animationDuration = `${fallDur}s, ${swayDur}s, ${spinDur}s`;
      p.style.animationDelay = `${delay}s, ${delay/2}s, ${delay/3}s`;


      // Slight size/shape variation
      const w = 8 + Math.random()*6;
      const h = 10 + Math.random()*7;
      p.style.width  = `${w}px`;
      p.style.height = `${h}px`;
      p.style.opacity = (0.7 + Math.random()*0.3).toFixed(2);


      // When a petal finishes falling, recycle it
      p.addEventListener('animationend', () => {
        p.remove();
        // respawn after a small random pause
        setTimeout(spawnPetal, 300 + Math.random()*1200);
      });


      petalContainer.appendChild(p);
    }


    // Initial batch
    for (let i = 0; i < PETAL_COUNT; i++){
      setTimeout(spawnPetal, Math.random()*1200);
    }
  })();
</script>
### Journey through Life


Here is what I did at those places


- 🏫 Kindergarden and elementary school until 4th grade in China
- 🏫 4th grade in Austin, Texas
- 🎓 5th grade + middle school + 9th grade of high school in San Diego


I learned a bit of Python a really long time ago and I forgot most of it already. I'm relearning Python right now and I want to learn about how I can apply Python in real life.


### Culture, Family, and Fun


Everything for me, as for many others, revolves around family and faith.


- My mother told me that I was Chinese.
Here is a picture of my hometown
<img src= "https://www.globaltimes.cn/Portals/0/attachment/2025/2025-02-06/aad5cbd6-92c1-4958-8a55-6f45b07cf2bf.jpeg" alt="Home Image">
- I'm an only child in my family, I do have a lot of cousins though. My parents lived in a small rural town in China, and later moved to Harbin. I moved to the U.S. in 4th grade. I've always wanted to get a golden retriever but my parents would never allow me to.


<comment>
Gallery of Pics, scroll to the right for more ...
</comment>
<div class="image-gallery">
  <img src="https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExaDA4N3p5NmZiYzJqZGxlcTI1b2MwaDljYXJpaXcxMjhnMXV5YjI1cCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/BDucPOizdZ5AI/giphy.gif" alt="Snow gif">
  <img src="https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExNDVzc3FubzlobjVieXE2YnBnbzE5Nmp6cmx4eGFuNXg0OWg5aGR3cyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/iicDrNGWxHmDrIni6j/giphy.gif" alt="Galaxy gif">
  <img src="https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExZThjbHBnMDI5dHIzemsxcjQ3OXU5bWU1enZoMHRlbXQ1OXU5c3c2ayZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/gQJyPqc6E4xoc/giphy.gif" alt="Headphones for music">
  <img src="https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExZTl6Ynhja2xmeXdjNzBnOGU2dWZjNmtmdzRmc2x2ZW5pNHF0cG9jaiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/myWd3Omj7KToQ/giphy.gif" alt="Image 4">
  <img src="https://ychef.files.bbci.co.uk/1280x720/p04nm71d.jpg" alt="Image 5">
</div>




<script>


  living_in_the_world.forEach(location => {
    const gridItem = document.createElement("div");
    gridItem.className = "grid-item";


    const img = document.createElement("img");
    img.src = http_source + location.flag;
    img.alt = location.flag + " Flag";


    const greeting = document.createElement("p");
    greeting.textContent = location.greeting;


    const description = document.createElement("p");
    description.textContent = location.description;


    gridItem.appendChild(img);
    gridItem.appendChild(greeting);
    gridItem.appendChild(description);


    container.appendChild(gridItem);
  });


  container.addEventListener('click', function(e) {
    if (e.target.tagName === 'IMG') {
      alert(`You clicked the flag of ${e.target.alt.replace(' Flag', '')}! 🌟 Hope you're having a great day!`);
    }
  });


</script>








