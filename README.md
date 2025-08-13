 <!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Happy Birthday Momos api</title>
<style>
  body {font-family: Arial, sans-serif; text-align: center; background-color: #ffe6f2; padding: 50px; overflow: hidden; margin:0;}
  h1 {color: #ff3399;}
  p {color: #555; font-size: 1.2em;}
  button {background-color: #ff66b2; color: white; border: none; padding: 15px 30px; font-size: 1.2em; border-radius: 8px; cursor: pointer; margin-top: 20px;}
  button:hover {background-color: #ff3385;}

  .layer {position: fixed; top:0; left:0; width:100%; height:100%; pointer-events:none; z-index:999;}
  .fall {position: absolute; top: -50px; will-change: transform; filter: drop-shadow(0 6px 16px rgba(0,0,0,.35));}
  .emoji, .card, .paper {font-size: clamp(20px, 3.8vw, 38px);}
  .card {min-width:140px; max-width:220px; padding:12px 14px; border-radius:16px; text-align:center; font-weight:800; background:linear-gradient(180deg, rgba(255,255,255,.22), rgba(255,255,255,.10)); border:1px solid rgba(255,255,255,.22); color:#fff;}
  .card small {display:block; font-weight:600; opacity:.9;}
  .paper {width:40px; height:40px; background:linear-gradient(45deg,#ffd700,#ff69b4); border-radius:3px; display:inline-block;}

  @keyframes fall-sway{
    0%{transform:translate(var(--x),-50px) rotate(var(--r0))}
    50%{transform:translate(calc(var(--x)+var(--sx)),50vh) rotate(var(--r1))}
    100%{transform:translate(calc(var(--x)+calc(var(--sx)*2)),110vh) rotate(var(--r2))}
  }
</style>
</head>
<body>
<h1>🥳Happy Birthday Momos api🥳</h1>
<p>May Allah live you long and give success or many many chocolate</p>
<button id="confettiBtn">🎉 Touch me!</button>
<div class="layer" id="layer"></div>

<script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
<script>
window.onload = function() {
const layer = document.getElementById('layer');
function rand(min,max){ return Math.random()*(max-min)+min; }
function px(v){ return `${v}px`; }

function makeFaller(el,dur){
  const sw = window.innerWidth;
  const startX = rand(0, sw);
  const sway = rand(-120, 120);
  el.style.setProperty('--x', px(startX));
  el.style.setProperty('--sx', px(sway));
  el.style.setProperty('--r0', `${rand(-20,20)}deg`);
  el.style.setProperty('--r1', `${rand(-120,120)}deg`);
  el.style.setProperty('--r2', `${rand(-360,360)}deg`);
  el.classList.add('fall');
  el.style.animation = `fall-sway ${dur}ms linear forwards`;
  el.style.left='0'; el.style.top='-50px';
  layer.appendChild(el);
  setTimeout(()=> { if(el.parentNode) el.parentNode.removeChild(el); }, dur + 500);
}

function burstFlowers(count=100){
  const EMOJI=['🌸','🌷','💐','🌺','🌼','🌻','🌹','❤️','🫠','💕'];
  for(let i=0;i<count;i++){
    const e=document.createElement('div');
    e.className='emoji'; e.textContent=EMOJI[Math.floor(Math.random()*EMOJI.length)];
    e.style.fontSize=`${rand(18,38)}px`; e.style.opacity=`${rand(0.7,1)}`;
    makeFaller(e, rand(8000,15000));
  }
}

function dropCards(){
  const texts=[
    'Happy birthday My 💗Elder Sister',
    'Happy💖 birthday Momos api',
    'Happy birthday cute',
    '❤️💕💖💗💘💞💓💝'
  ];
  for(let c=0;c<3;c++){
    texts.forEach(t=>{
      const card=document.createElement('div');
      card.className='card'; card.innerHTML=`<small>🎁</small>${t}`;
      card.style.transform=`rotate(${rand(-6,6)}deg)`;
      makeFaller(card, rand(10000,18000));
    });
  }
}

function dropPapers(count=40){
  for(let i=0;i<count;i++){
    const paper=document.createElement('div');
    paper.className='paper';
    makeFaller(paper, rand(10000,18000));
  }
}

document.getElementById('confettiBtn').addEventListener('click',()=>{
  burstFlowers(150);
  dropCards();
  dropPapers(60);

  const duration = 5000; const end = Date.now()+duration;
  (function frame(){
    confetti({particleCount:5, angle:60, spread:55, origin:{x:0}});
    confetti({particleCount:5, angle:120, spread:55, origin:{x:1}});
    if(Date.now()<end) requestAnimationFrame(frame);
  }());
});
};
</script>
</body>
</html>
