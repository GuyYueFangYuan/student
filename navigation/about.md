---
layout: page
title: About
permalink: /about/
comments: true
---

## As a conversation Starter


<comment>
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
   // 1. Make a connection to the HTML container defined in the HTML div
   var container = document.getElementById("grid_container"); // This container connects to the HTML div


   // 2. Define a JavaScript object for our http source and our data rows for the Living in the World grid


   // 3a. Consider how to update style count for size of container
   // The grid-template-columns has been defined as dynamic with auto-fill and minmax


   // 3b. Build grid items inside of our container for each row of data
   for (const location of living_in_the_world) {
       // Create a "div" with "class grid-item" for each row
       var gridItem = document.createElement("div");
       gridItem.className = "grid-item";  // This class name connects the gridItem to the CSS style elements
       // Add "img" HTML tag for the flag
       var img = document.createElement("img");
       img.src = http_source + location.flag; // concatenate the source and flag
       img.alt = location.flag + " Flag"; // add alt text for accessibility


       // Add "p" HTML tag for the description
       var description = document.createElement("p");
       description.textContent = location.description; // extract the description


       // Add "p" HTML tag for the greeting
       var greeting = document.createElement("p");
       greeting.textContent = location.greeting;  // extract the greeting


       // Append img and p HTML tags to the grid item DIV
       gridItem.appendChild(img);
       gridItem.appendChild(description);
       gridItem.appendChild(greeting);


       // Append the grid item DIV to the container DIV
       container.appendChild(gridItem);
   }
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




 // Snow effect code


<!-- Snow effect -->
<div id="snow"></div>


<style>
 body {
   margin: 0;
   padding: 0;
   background: #0b1d3a; /* nice dark sky */
   overflow: hidden;
   color: white;
   font-family: Arial, sans-serif;
 }
 #snow {
   position: fixed;
   top: 0; left: 0;
   width: 100%; height: 100%;
   pointer-events: none;
   z-index: 9999;
 }
 .snowflake {
   position: absolute;
   color: white;
   font-size: 1em;
   animation: fall linear infinite;
 }
 @keyframes fall {
   0% { transform: translateY(-10px); opacity: 1; }
   100% { transform: translateY(100vh); opacity: 0; }
 }
</style>


<script>
 function createSnowflake() {
   const snowflake = document.createElement("div");
   snowflake.classList.add("snowflake");
   snowflake.textContent = "❄";
   snowflake.style.left = Math.random() * window.innerWidth + "px";
   snowflake.style.animationDuration = (Math.random() * 3 + 2) + "s";
   snowflake.style.fontSize = (Math.random() * 10 + 10) + "px";
   document.getElementById("snow").appendChild(snowflake);


   setTimeout(() => { snowflake.remove(); }, 5000);
 }
 setInterval(createSnowflake, 200);
















