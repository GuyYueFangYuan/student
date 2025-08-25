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
.cultivation-platform, .grid-container, .image-gallery, h2, h3, p, img { position: relative; z-index: 1; }


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


/* simple grid styles */
.grid-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  gap: 10px;
}
.grid-item { text-align: center; }
.grid-item img {
  width: 100%; height: 100px; object-fit: contain;
}
.grid-item p { margin: 5px 0; }
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


  <!-- Reset button (visible HTML, not inside a <script>) -->
  <button id="reset-cultivation" type="button" class="jade-reset" style="display:block;margin:10px auto 0;padding:6px 12px;border-radius:999px;border:1px solid #bfeee1;background:#f6fffb;color:#0a6b52;cursor:pointer;">
    Reset Progress
  </button>
</div>


<!-- Optional: simple grid container so the grid script has a target -->
<div class="grid-container" id="grid_container"></div>


<script>
/* --- Fallback data so the grid + flags don't crash --- */
window.http_source = window.http_source || "";
window.living_in_the_world = window.living_in_the_world || [
  { flag: "https://flagcdn.com/w320/cn.png", description: "Harbin, China", greeting: "Hello" },
  { flag: "https://flagcdn.com/w320/us.png", description: "Austin, Texas", greeting: "Howdy!" },
  { flag: "https://flagcdn.com/w320/us.png", description: "San Diego, California", greeting: "Hey!" }
];


/* --- Build the grid safely --- */
(function(){
  const container = document.getElementById("grid_container");
  if(!container || !Array.isArray(window.living_in_the_world)) return;


  window.living_in_the_world.forEach(location => {
    const gridItem = document.createElement("div");
    gridItem.className = "grid-item";


    const img = document.createElement("img");
    img.src = (window.http_source || "") + location.flag;
    img.alt = (location.flag || "Flag") + " Flag";


    const greeting = document.createElement("p");
    greeting.textContent = location.greeting || "";


    const description = document.createElement("p");
    description.textContent = location.description || "";


    gridItem.appendChild(img);
    gridItem.appendChild(greeting);
    gridItem.appendChild(description);
    container.appendChild(gridItem);
  });


  container.addEventListener('click', function(e) {
    if (e.target.tagName === 'IMG') {
      alert(`You clicked the flag of ${e.target.alt.replace(' Flag', '')}! 🌟`);
    }
  });
})();
</script>


<script>
/* --- Cultivation logic with increasing steps + reset --- */
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
  const STEPS = [3, 5, 8, 12, 16, 20]; // clicks needed to move to next realm


  const KEY_IDX  = "cultivation_realm_index";
  const KEY_SUB  = "cultivation_realm_sub";


  const stone = document.getElementById('jade-stone');
  const label = document.getElementById('realm-label');
  const bar   = document.getElementById('realm-bar');
  const reset = document.getElementById('reset-cultivation');
  if(!stone || !label || !bar) return;


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
    if(idx >= REALMS.length-1){ label.textContent = REALMS[idx] + " · Achieved"; return; }
    sub += 1;
    const need = STEPS[idx] || 1;
    if(sub >= need){
      idx += 1; sub = 0;
      localStorage.setItem(KEY_IDX, String(idx));
      localStorage.setItem(KEY_SUB, String(sub));
    } else {
      localStorage.setItem(KEY_SUB, String(sub));
    }
    render();
    stone.classList.add('cultivate-flash');
    setTimeout(()=>stone.classList.remove('cultivate-flash'), 550);
  }


  stone.addEventListener('click', cultivate);


  if(reset){
    reset.addEventListener('click', () => {
      localStorage.removeItem(KEY_IDX);
      localStorage.removeItem(KEY_SUB);
      idx = 0; sub = 0;
      render();
      reset.textContent = 'Reset!';
      reset.disabled = true;
      setTimeout(() => { reset.textContent = 'Reset Progress'; reset.disabled = false; }, 700);
    });
  }


  render();
})();
</script>


### Journey through Life















