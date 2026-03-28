<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Zenithal Ahsan</title>  <!-- Tailwind CDN -->  <script src="https://cdn.tailwindcss.com"></script>  <style>
    body { background: black; color: white; }

    /* Star background */
    .stars {
      background-image: radial-gradient(white 1px, transparent 1px);
      background-size: 20px 20px;
      opacity: 0.2;
      position: fixed;
      width: 100%;
      height: 100%;
      z-index: 0;
    }

    /* Milky Way Glow */
    .milkyway {
      position: fixed;
      width: 100%;
      height: 100%;
      background: radial-gradient(circle at 30% 40%, rgba(128,0,255,0.3), transparent 40%),
                  radial-gradient(circle at 70% 60%, rgba(0,200,255,0.3), transparent 40%),
                  radial-gradient(circle at 50% 80%, rgba(0,255,150,0.2), transparent 40%);
      filter: blur(80px);
      animation: glow 6s infinite alternate;
      z-index: 0;
    }

    @keyframes glow {
      from { opacity: 0.3; }
      to { opacity: 0.6; }
    }

    .modal {
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.95);
      display: none;
      z-index: 50;
    }
  </style></head>
<body><div class="milkyway"></div>
<div class="stars"></div><div class="relative z-10">  <!-- Header -->  <header class="p-4 flex justify-between items-center border-b border-gray-800">
    <h1 class="text-xl font-bold">Zenithal Ahsan</h1>
  </header>  <!-- Hero -->  <section class="text-center py-16 px-4">
    <h2 class="text-3xl font-bold mb-4">Astrophotography by Zenithal Ahsan</h2>
    <p class="text-gray-400">Explore the universe in ultra high resolution.</p>
  </section>  <!-- Categories -->  <section class="px-4 py-6">
    <div id="filters" class="flex flex-wrap gap-2"></div>
  </section>  <!-- Gallery -->  <section id="gallery" class="px-4 py-6 grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4"></section></div><!-- Modal --><div id="modal" class="modal flex flex-col md:flex-row">
  <div class="flex-1 flex items-center justify-center p-4">
    <img id="modalImg" class="max-w-full max-h-full" />
  </div>  <div class="w-full md:w-80 bg-gray-900 p-6 border-l border-gray-800">
    <h2 id="title" class="text-xl font-bold mb-2"></h2>
    <p id="category" class="text-sm text-gray-400 mb-4"></p><div class="space-y-2 text-sm">
  <p><strong>Camera:</strong> <span id="camera"></span></p>
  <p><strong>Exposure:</strong> <span id="exposure"></span></p>
  <p><strong>Location:</strong> <span id="location"></span></p>
</div>

<a id="download" class="block mt-6">
  <button class="w-full bg-green-600 py-2 rounded">Download Full Resolution</button>
</a>

<button onclick="closeModal()" class="mt-4 w-full bg-gray-700 py-2 rounded">Close</button>

  </div>
</div><script>
const categories = ["All","Comets","Nebulae","Galaxies"];
let active = "All";

const images = [
  {
    title:"Comet C/2023 A3",
    category:"Comets",
    url:"https://images.unsplash.com/photo-1462331940025-496dfbfc7564",
    camera:"Canon EOS R",
    exposure:"30s ISO1600",
    location:"Bangladesh"
  },
  {
    title:"Orion Nebula",
    category:"Nebulae",
    url:"https://images.unsplash.com/photo-1446776811953-b23d57bd21aa",
    camera:"Nikon D750",
    exposure:"45s ISO3200",
    location:"Rajshahi"
  }
];

function renderFilters(){
  const f = document.getElementById("filters");
  f.innerHTML="";
  categories.forEach(c=>{
    const btn=document.createElement("button");
    btn.innerText=c;
    btn.className="px-3 py-1 rounded bg-gray-800";
    btn.onclick=()=>{active=c; renderGallery();};
    f.appendChild(btn);
  });
}

function renderGallery(){
  const g=document.getElementById("gallery");
  g.innerHTML="";
  const filtered = active==="All"?images:images.filter(i=>i.category===active);

  filtered.forEach(img=>{
    const div=document.createElement("div");
    div.className="bg-gray-900 p-2 rounded cursor-pointer";

    div.innerHTML=`<img src="${img.url}" class="w-full h-52 object-cover"><h4>${img.title}</h4>`;

    div.onclick=()=>openModal(img);
    g.appendChild(div);
  });
}

function openModal(img){
  document.getElementById("modal").style.display="flex";
  document.getElementById("modalImg").src=img.url;
  document.getElementById("title").innerText=img.title;
  document.getElementById("category").innerText=img.category;
  document.getElementById("camera").innerText=img.camera;
  document.getElementById("exposure").innerText=img.exposure;
  document.getElementById("location").innerText=img.location;
  document.getElementById("download").href=img.url;
}

function closeModal(){
  document.getElementById("modal").style.display="none";
}

renderFilters();
renderGallery();
</script></body>
</html> 
