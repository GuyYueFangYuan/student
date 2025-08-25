---
layout: post
title: Cyrus about me
permalink: /about/
comments: true
---

## As a conversation Starter


<comment>``
Here are some places I lived in.
Harbin, China.
Austin, Texas.
San Diego, California.
</comment>


<!-- Cultivation Platform -->
<div class="cultivation-platform jade-card" id="cultivation-card">
  <div style="font-weight:700; color:#0a6b52; margin-bottom:10px; text-align:center;">
    Realm Progress · Cultivation
  </div>


  <!-- glowing jade stone -->
  <div id="jade-stone"></div>


  <!-- realm + bar -->
  <div style="display:flex; align-items:center; gap:10px; margin-top:12px;">
    <div id="realm-label" style="min-width:170px; color:#0a6b52;">Mortal</div>
    <div style="flex:1; height:10px; border-radius:999px; background:#eefaf6; box-shadow: inset 0 0 0 1px #aeeedd;">
      <div id="realm-bar" style="height:10px; width:0%; border-radius:999px; background:linear-gradient(90deg,#86e8c8,#bdf5e5,#e8fff9); transition: width .5s;"></div>
    </div>
  </div>


  <p style="font-size:.9rem; color:#0a6b52; opacity:.9; margin-top:8px; text-align:center;">
    Click the jade stone to cultivate and ascend realms.
  </p>
</div>


<style>
/* Cultivation Platform Styles */
.cultivation-platform{
  text-align:center;
  padding:16px;
}


/* glowing jade stone */
#jade-stone{
  width:100px;
  height:100px;
  margin:0 auto;
  border-radius:50%;
  background: radial-gradient(circle at 30% 30%, #9ef5d5, #4fc4a1 70%, #2a7a63 100%);
  box-shadow: 0 0 20px rgba(134,232,200,.7), 0 0 40px rgba(134,232,200,.4);
  cursor:pointer;
  transition: transform .2s ease, box-shadow .3s ease;
}
#jade-stone:hover{
  transform: scale(1.08);
  box-shadow: 0 0 30px rgba(134,232,200,.9), 0 0 60px rgba(134,232,200,.6);
}


/* flash effect when cultivating */
.cultivate-flash {
  animation: flashJade .6s ease;
}
@keyframes flashJade {
  0%   { box-shadow: 0 0 0 rgba(134,232,200,0); }
  40%  { box-shadow: 0 0 18px rgba(134,232,200,.75); }
  100% { box-shadow: 0 0 0 rgba(134,232,200,0); }
}
</style>


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


<style>
  /* --- Xianxia theme accents --- */
  .xianxia-banner{
    position: relative;
    padding: 28px 18px;
    margin: 18px 0 8px;
    border-radius: 12px;
    background:
      radial-gradient(1200px 200px at 50% 0%, rgba(255,255,255,.45), transparent 60%),
      linear-gradient(180deg, #e6fff7 0%, #eafbf6 38%, #f7fffd 100%);
    border: 2px solid #b2e4d6;
    box-shadow: 0 6px 18px rgba(0,0,0,.06), inset 0 0 0 1px #e0fff5;
  }
  .xianxia-title{
    font-family: "Zhi Mang Xing","Noto Serif SC", serif;
    font-size: 2rem;
    letter-spacing: 2px;
    color: #137a5d;
    text-align: center;
    text-shadow: 0 2px 0 rgba(255,255,255,.8);
  }
  .jade-divider{
    height: 12px;
    margin: 12px auto 0;
    width: 180px;
    border-radius: 999px;
    background: linear-gradient(90deg,#c6f3e5,#8be0c9,#c6f3e5);
    filter: drop-shadow(0 2px 2px rgba(0,0,0,.08));
  }


  /* soft moving clouds behind content */
  .xianxia-sky{
    position: relative;
    overflow: hidden;
    border-radius: 12px;
    background: linear-gradient(#f8fffe, #eefcfe);
  }
  .cloud{
    position: absolute;
    top: 10%;
    width: 220px; height: 80px;
    background: radial-gradient(closest-side at 30% 50%, #fff 0%, #fff 60%, transparent 61%) 0 0/60% 100% no-repeat,
                radial-gradient(closest-side at 70% 50%, #fff 0%, #fff 60%, transparent 61%) 100% 0/60% 100% no-repeat,
                radial-gradient(closest-side, #fff 0%, #fff 60%, transparent 61%) 50% 0/90% 100% no-repeat;
    opacity: .7;
    filter: blur(0.5px);
    animation: drift 60s linear infinite;
  }
  .cloud.c2{ top: 35%; transform: scale(1.2); animation-duration: 75s; opacity: .6;}
  .cloud.c3{ top: 60%; transform: scale(0.9); animation-duration: 85s; opacity: .55;}


  @keyframes drift{
    0%   { left: -260px }
    100% { left: calc(100% + 260px) }
  }


  /* faint qi motes */
  .qi-layer{ position: relative; }
  .qi{
    position: absolute;
    width: 6px; height: 6px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(160,255,230,.95), rgba(160,255,230,0) 70%);
    filter: blur(.3px);
    animation: floatUp 7s linear infinite;
    opacity: .8;
  }
  @keyframes floatUp{
    0%   { transform: translateY(0) translateX(0); opacity: .0;}
    10%  { opacity: .9;}
    100% { transform: translateY(-180px) translateX(40px); opacity: 0;}
  }


  /* optional: jade card look for existing sections without touching their HTML */
  .jade-card{
    border: 1.5px solid #cdeee4;
    border-radius: 10px;
    padding: 12px;
    background: linear-gradient(180deg, rgba(240,255,250,.8), rgba(255,255,255,.7));
  }
</style>


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


<script>
(function(){
  const REALMS = [
    "Mortal",
    "Qi Refinement",
    "Foundation Establishment (Zhuji)",
    "Core Formation (Jindan)",
    "Nascent Soul (Yuanying)",
    "Soul Transformation",
    "Ascension"
  ];


  const KEY = "cultivation_realm_index";
  const stone = document.getElementById('jade-stone');
  const label = document.getElementById('realm-label');
  const bar = document.getElementById('realm-bar');
  const card = document.getElementById('cultivation-card');


  if(!stone || !label || !bar || !card) return;


  let idx = parseInt(localStorage.getItem(KEY) || "0", 10);
  if(isNaN(idx) || idx < 0) idx = 0;
  if(idx >= REALMS.length) idx = REALMS.length - 1;


  function render(){
    label.textContent = REALMS[idx];
    const pct = (idx/(REALMS.length-1))*100;
    bar.style.width = pct + "%";
  }


  function cultivate(){
    if(idx < REALMS.length - 1){
      idx++;
      localStorage.setItem(KEY, String(idx));
      render();
      stone.classList.add('cultivate-flash');
      setTimeout(()=>stone.classList.remove('cultivate-flash'), 650);
    } else {
      label.textContent = REALMS[idx] + " · Achieved";
    }
  }


  stone.addEventListener('click', cultivate);


  render();
})();
</script>









