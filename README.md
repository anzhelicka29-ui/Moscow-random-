<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Московская Рулетка</title>
<style>
:root{
  --bg:#f0f2f5;
  --card:#fff;
  --text:#222;
  --accent:#ff4d6d;
}
body.dark{
  --bg:#111;
  --card:#1b1e28;
  --text:#f0f0f0;
  --accent:#ff7a90;
}
body{
  margin:0;
  font-family:'Segoe UI',sans-serif;
  background:var(--bg);
  color:var(--text);
  transition:0.3s;
}
.container{
  max-width:500px;
  margin:auto;
  padding:15px;
  text-align:center;
}
h1{
  margin:15px 0;
}
.card{
  background:var(--card);
  border-radius:20px;
  padding:15px;
  margin:20px 0;
  box-shadow:0 10px 25px rgba(0,0,0,0.08);
  transition:0.3s;
}
button{
  background:var(--accent);
  color:#fff;
  border:none;
  border-radius:30px;
  padding:12px 20px;
  font-size:16px;
  cursor:pointer;
  margin:5px;
  transition:0.2s;
}
button:hover{transform:scale(1.05);}
img{
  width:100%;
  border-radius:15px;
  margin-top:10px;
  max-height:250px;
  object-fit:cover;
}
.result{
  font-weight:600;
  margin-top:10px;
  min-height:30px;
  font-size:18px;
}
.spin{
  animation:spin 0.6s linear infinite;
}
@keyframes spin{
  0%{opacity:0.3; transform:translateY(-5px);}
  50%{opacity:1; transform:translateY(5px);}
  100%{opacity:0.3; transform:translateY(-5px);}
}
.top-bar{
  display:flex;
  justify-content:space-between;
  align-items:center;
}
</style>
</head>
<body>
<div class="container">
<div class="top-bar">
<h1>🎲 Московская Рулетка</h1>
<button onclick="toggleDark()">🌙</button>
</div>
<button onclick="surprise()">🔥 Удиви меня</button>

<div class="card">
<button onclick="spinPlace()">Куда пойти?</button>
<div id="place" class="result"></div>
<img id="placeImg" src="">
</div>

<div class="card">
<button onclick="spinActivity()">Чем заняться?</button>
<div id="activity" class="result"></div>
<img id="activityImg" src="">
</div>

<div class="card">
<button onclick="spinOutfit()">В чем пойти?</button>
<div id="outfit" class="result"></div>
<img id="outfitImg" src="">
</div>
</div>

<script>
const places=[
{ name:"Парк Горького", img:"https://source.unsplash.com/600x400/?gorky-park,moscow" },
{ name:"ВДНХ", img:"https://source.unsplash.com/600x400/?vdnh,moscow" },
{ name:"Красная площадь", img:"https://source.unsplash.com/600x400/?red-square,moscow" },
{ name:"Москва-Сити", img:"https://source.unsplash.com/600x400/?moscow-city" },
{ name:"Патриаршие пруды", img:"https://source.unsplash.com/600x400/?patriarch-ponds,moscow" },
{ name:"Хлебозавод", img:"https://source.unsplash.com/600x400/?bread-factory,moscow" },
{ name:"Флакон", img:"https://source.unsplash.com/600x400/?flacon,moscow" },
{ name:"Измайловский парк", img:"https://source.unsplash.com/600x400/?izmailovsky-park" },
{ name:"Сад Эрмитаж", img:"https://source.unsplash.com/600x400/?hermitage-garden,moscow" },
{ name:"Серебряный бор", img:"https://source.unsplash.com/600x400/?silver-forest,moscow" },
{ name:"Коломенское", img:"https://source.unsplash.com/600x400/?kolomenskoye,moscow" },
{ name:"Винзавод", img:"https://source.unsplash.com/600x400/?winzavod,moscow" },
{ name:"Чистые пруды", img:"https://source.unsplash.com/600x400/?chistye-prudy,moscow" },
{ name:"Кусково", img:"https://source.unsplash.com/600x400/?kuskovo,moscow" },
{ name:"Ботанический сад", img:"https://source.unsplash.com/600x400/?botanical-garden,moscow" },
{ name:"Зарядье", img:"https://source.unsplash.com/600x400/?zaryadye-park,moscow" },
{ name:"Лосиный остров", img:"https://source.unsplash.com/600x400/?losiny-island,moscow" },
{ name:"Китай-город", img:"https://source.unsplash.com/600x400/?kitay-gorod,moscow" },
{ name:"Таганка", img:"https://source.unsplash.com/600x400/?taganka,moscow" },
{ name:"Даниловский рынок", img:"https://source.unsplash.com/600x400/?danilovsky-market,moscow" },
{ name:"Крутицкое подворье", img:"https://source.unsplash.com/600x400/?krutitskoye,moscow" },
{ name:"Сад Баумана", img:"https://source.unsplash.com/600x400/?bauman-garden,moscow" },
{ name:"Аптекарский огород", img:"https://source.unsplash.com/600x400/?aptekarsky-garden,moscow" },
{ name:"Парк Сокольники", img:"https://source.unsplash.com/600x400/?sokolniki-park,moscow" },
{ name:"Музеон", img:"https://source.unsplash.com/600x400/?muzeon,moscow" },
{ name:"Симонов монастырь", img:"https://source.unsplash.com/600x400/?simon-monastery,moscow" },
{ name:"Новодевичий монастырь", img:"https://source.unsplash.com/600x400/?novodevichy,moscow" },
{ name:"ГЭС-2", img:"https://source.unsplash.com/600x400/?ges2,moscow" },
{ name:"Парк Яуза", img:"https://source.unsplash.com/600x400/?yauza-park,moscow" },
{ name:"Северный речной вокзал", img:"https://source.unsplash.com/600x400/?north-river-station,moscow" }
];

const activities=[
{ name:"Фотосессия", img:"https://source.unsplash.com/600x400/?photography,moscow" },
{ name:"Новое кафе", img:"https://source.unsplash.com/600x400/?cafe,moscow" },
{ name:"Самокат", img:"https://source.unsplash.com/600x400/?scooter,moscow" },
{ name:"Атмосферное видео", img:"https://source.unsplash.com/600x400/?video,moscow" },
{ name:"Пикник", img:"https://source.unsplash.com/600x400/?picnic,moscow" },
{ name:"Настолки", img:"https://source.unsplash.com/600x400/?board-games" },
{ name:"Музыка", img:"https://source.unsplash.com/600x400/?street-music" },
{ name:"15000 шагов", img:"https://source.unsplash.com/600x400/?walking,moscow" },
{ name:"Познакомиться", img:"https://source.unsplash.com/600x400/?meeting,people" },
{ name:"Лучший кофе", img:"https://source.unsplash.com/600x400/?coffee,moscow" },
{ name:"Скетч", img:"https://source.unsplash.com/600x400/?drawing,sketch" },
{ name:"Книга на лавке", img:"https://source.unsplash.com/600x400/?reading,park" },
{ name:"Лодка", img:"https://source.unsplash.com/600x400/?boat,park" },
{ name:"Стритфуд", img:"https://source.unsplash.com/600x400/?street-food" },
{ name:"Снять reels", img:"https://source.unsplash.com/600x400/?reels,video" },
{ name:"Необычные двери", img:"https://source.unsplash.com/600x400/?doors,moscow" },
{ name:"Челлендж 500₽", img:"https://source.unsplash.com/600x400/?challenge,moscow" },
{ name:"Плейлист", img:"https://source.unsplash.com/600x400/?playlist,music" },
{ name:"Бумажный самолетик", img:"https://source.unsplash.com/600x400/?paper-plane" },
{ name:"Бадминтон", img:"https://source.unsplash.com/600x400/?badminton" },
{ name:"10 собак", img:"https://source.unsplash.com/600x400/?dogs,moscow" },
{ name:"Мини-влог", img:"https://source.unsplash.com/600x400/?vlog,moscow" },
{ name:"Скрытый дворик", img:"https://source.unsplash.com/600x400/?hidden-courtyard" },
{ name:"Поговорить о мечтах", img:"https://source.unsplash.com/600x400/?talk,people" },
{ name:"Маршрут на карте", img:"https://source.unsplash.com/600x400/?map" },
{ name:"Дегустация десертов", img:"https://source.unsplash.com/600x400/?dessert" },
{ name:"Самая красивая лавка", img:"https://source.unsplash.com/600x400/?bench,moscow" },
{ name:"Придумать историю прохожему", img:"https://source.unsplash.com/600x400/?story-telling" },
{ name:"Посидеть в тишине 20 минут", img:"https://source.unsplash.com/600x400/?quiet,park" },
{ name:"Смешной челлендж", img:"https://source.unsplash.com/600x400/?fun-challenge" }
];

const outfits=[
{ name:"Спортивный кэжуал", img:"https://source.unsplash.com/600x400/?sport,casual" },
{ name:"Минимализм", img:"https://source.unsplash.com/600x400/?minimal,style" },
{ name:"Street-style", img:"https://source.unsplash.com/600x400/?street-style" },
{ name:"Романтичный", img:"https://source.unsplash.com/600x400/?romantic,style" },
{ name:"Total white", img:"https://source.unsplash.com/600x400/?white,clothes" },
{ name:"Оверсайз худи", img:"https://source.unsplash.com/600x400/?hoodie,oversize" },
{ name:"Пиджак + кроссовки", img:"https://source.unsplash.com/600x400/?jacket,sneakers" },
{ name:"Летнее платье", img:"https://source.unsplash.com/600x400/?summer,dress" },
{ name:"Гранж", img:"https://source.unsplash.com/600x400/?grunge,style" },
{ name:"Бежевый монохром", img:"https://source.unsplash.com/600x400/?beige,clothes" },
{ name:"Винтаж", img:"https://source.unsplash.com/600x400/?vintage,style" },
{ name:"Smart casual", img:"https://source.unsplash.com/600x400/?smart-casual" },
{ name:"Кожаная куртка", img:"https://source.unsplash.com/600x400/?leather,jacket" },
{ name:"Джинсы + рубашка", img:"https://source.unsplash.com/600x400/?jeans,shirt" },
{ name:"Яркие аксессуары", img:"https://source.unsplash.com/600x400/?fashion,accessories" },
{ name:"Total denim", img:"https://source.unsplash.com/600x400/?denim" },
{ name:"Пастель", img:"https://source.unsplash.com/600x400/?pastel,clothes" },
{ name:"Темный стиль", img:"https://source.unsplash.com/600x400/?dark,fashion" },
{ name:"Сканди", img:"https://source.unsplash.com/600x400/?scandi,style" },
{ name:"Арт-образ", img:"https://source.unsplash.com/600x400/?art,style" }
];

function spinEffect(el,callback){
  el.classList.add("spin");
  let count=0;
  let interval=setInterval(()=>{
    el.innerText="...";
    count++;
    if(count>10){clearInterval(interval);el.classList.remove("spin");callback();}
  },100);
}
function randomFrom(arr){return arr[Math.floor(Math.random()*arr.length)];}
function spinPlace(){spinEffect(document.getElementById("place"),()=>{
  let r=randomFrom(places);
  document.getElementById("place").innerText=r.name;
  document.getElementById("placeImg").src=r.img;
});}
function spinActivity(){spinEffect(document.getElementById("activity"),()=>{
  let r=randomFrom(activities);
  document.getElementById("activity").innerText=r.name;
  document.getElementById("activityImg").src=r.img;
});}
function spinOutfit(){spinEffect(document.getElementById("outfit"),()=>{
  let r=randomFrom(outfits);
  document.getElementById("outfit").innerText=r.name;
  document.getElementById("outfitImg").src=r.img;
});}
function surprise(){spinPlace(); setTimeout(spinActivity,1200); setTimeout(spinOutfit,2400);}
function toggleDark(){document.body.classList.toggle("dark");}
</script>
</body>
</html>
