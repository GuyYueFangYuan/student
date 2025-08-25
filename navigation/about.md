---
layout: post
title: Cyrus about me
permalink: /about/
comments: true
---
<link href="https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@700;900&family=Zhi+Mang+Xing&display=swap" rel="stylesheet">


## As a conversation Starter


<!--
Here are some places I lived in.
Harbin, China.
Austin, Texas.
San Diego, California.
-->


<!-- Fog overlay (non-interactive) -->
<div class="fog" aria-hidden="true">
  <div class="fog-layer l1"></div>
  <div class="fog-layer l2"></div>
  <div class="fog-layer l3"></div>
</div>


<style>
/* --- Gentle drifting fog --- */
.fog{ position:fixed; inset:0; pointer-events:none; z-index:0; }
.fog-layer{
  position:fixed; inset:0; pointer-events:none;
  opacity:.22; filter: blur(10px) saturate(1.05);
  background:
    radial-gradient(220px 130px at 12% 20%, rgba(255,255,255,.11), transparent 60%),
    radial-gradient(280px 160px at 65% 8%,  rgba(255,255,255,.08), transparent 60%),
    radial-gradient(260px 140px at 82% 58%, rgba(255,255,255,.10), transparent 60%),
    radial-gradient(240px 140px at 28% 82%, rgba(255,255,255,.07), transparent 60%);
  animation: fogSlide 120s linear infinite, fogBob 20s ease-in-out infinite alternate;
  mix-blend-mode: normal;
}
.fog-layer.l2{ opacity:.18; filter: blur(16px); animation-duration: 160s, 28s; transform: scale(1.05); }
.fog-layer.l3{ opacity:.14; filter: blur(20px); animation-duration: 220s, 36s; transform: scale(1.1); }


@keyframes fogSlide { 0%{transform:translateX(-6%)} 50%{transform:translateX(6%)} 100%{transform:translateX(-6%)} }
@keyframes fogBob   { 0%{transform:translateY(0)} 100%{transform:translateY(-2%)} }


/* ensure content sits above fog */
.cultivation-platform, h2, h3, p, img { position: relative; z-index: 1; }


/* --- Cultivation platform + jade styles --- */
.jade-card{
  border: 1.5px solid #cdeee4;
  border-radius: 10px;
  padding: 12px;
  background: linear-gradient(180deg, rgba(240,255,250,.8), rgba(255,255,255,.7));
}
.cultivation-platform{ text-align:center; padding:16px; }


/* glowing jade stone */
#jade-stone{
  width:100px; height:100px; margin:0 auto; border-radius:50%;
  background: radial-gradient(circle at 30% 30%, #9ef5d5, #4fc4a1 70%, #2a7a63 100%);
  box-shadow: 0 0 20px rgba(134,232,200,.7), 0 0 40px rgba(134,232,200,.4);
  cursor:pointer; transition: transform .2s ease, box-shadow .3s ease;
}
#jade-stone:hover{ transform: scale(1.08); box-shadow: 0 0 30px rgba(134,232,200,.9), 0 0 60px rgba(134,232,200,.6); }


/* flash effect when cultivating */
.cultivate-flash { animation: flashJade .6s ease; }
@keyframes flashJade {
  0%{ box-shadow: 0 0 0 rgba(134,232,200,0); }
  40%{ box-shadow: 0 0 18px rgba(134,232,200,.75); }
  100%{ box-shadow: 0 0 0 rgba(134,232,200,0); }
}
</style>


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
  // clicks needed to advance from the current realm to the next
  const STEPS = [3, 5, 8, 12, 16, 20];


  const KEY_IDX  = "cultivation_realm_index";
  const KEY_SUB  = "cultivation_realm_sub";


  const stone = document.getElementById('jade-stone');
  const label = document.getElementById('realm-label');
  const bar   = document.getElementById('realm-bar');
  const card  = document.getElementById('cultivation-card');
  if(!stone || !label || !bar || !card) return;


  let idx = parseInt(localStorage.getItem(KEY_IDX) || "0", 10);
  let sub = parseInt(localStorage.getItem(KEY_SUB) || "0", 10);
  idx = isNaN(idx) ? 0 : Math.min(Math.max(idx,0), REALMS.length-1);
  sub = isNaN(sub) ? 0 : Math.max(sub,0);


  function render(){
    if(idx >= REALMS.length-1){
      label.textContent = REALMS[idx] + " · Achieved";
      bar.style.width = "100%";
      return;
    }
    const need = STEPS[idx] || 1;
    const pct = ((idx + (sub/need)) / (REALMS.length-1)) * 100;
    label.textContent = `${REALMS[idx]}  ${sub}/${need}`;
    bar.style.width = pct + "%";
  }


  function cultivate(){
    if(idx >= REALMS.length-1){
      label.textContent = REALMS[idx] + " · Achieved";
      return;
    }
    sub += 1;
    const need = STEPS[idx] || 1;
    if(sub >= need){
      idx += 1;
      sub = 0;
      localStorage.setItem(KEY_IDX, String(idx));
      localStorage.setItem(KEY_SUB, String(sub));
    }else{
      localStorage.setItem(KEY_SUB, String(sub));
    }
    render();
    stone.classList.add('cultivate-flash');
    setTimeout(()=>stone.classList.remove('cultivate-flash'), 550);
  }


  stone.addEventListener('click', cultivate);
  render();
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










