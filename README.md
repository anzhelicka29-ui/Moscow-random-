# Moscow-random-
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Московская Рулетка 3.0</title>
<style>
:root{
  --bg:#f4f6fb;
  --card:#ffffff;
  --text:#222;
  --accent:#ff4d6d;
}
body.dark{
  --bg:#0f1115;
  --card:#1c1f26;
  --text:#f1f1f1;
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
  padding:20px;
  text-align:center;
}
h1{margin-top:20px;}
.card{
  background:var(--card);
  padding:20px;
  border-radius:20px;
  margin:25px 0;
  box-shadow:0 10px 25px rgba(0,0,0,0.1);
  transition:0.3s;
}
button{
  background:var(--accent);
  color:white;
  border:none;
  padding:12px 22px;
  border-radius:30px;
  font-size:15px;
  cursor:pointer;
  margin:8px;
  transition:0.2s;
}
button:hover{transform:scale(1.05);}
img{
  width:100%;
  border-radius:15px;
  margin-top:15px;
  max-height:260px;
  object-fit:cover;
}
.result{
  font-size:18px;
  font-weight:600;
  margin-top:10px;
  min-height:40px;
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
<img id="placeImg">
</div>
<div class="card">
<button onclick="spinActivity()">Чем заняться?</button>
<div id="activity" class="result"></div>
<img id="activityImg">
</div>
<div class="card">
<button onclick="spinOutfit()">В чем пойти?</button>
<div id="outfit" class="result"></div>
<img id="outfitImg">
</div>
</div>
<script>
// 30 мест
const places=[
"Парк Горького","ВДНХ","Красная площадь","Москва-Сити",
"Патриаршие пруды","Хлебозавод","Флакон","Измайловский парк",
"Сад Эрмитаж","Серебряный бор","Коломенское","Винзавод",
"Чистые пруды","Кусково","Ботанический сад","Зарядье",
"Лосиный остров","Китай-город","Таганка","Даниловский рынок",
"Крутицкое подворье","Сад Баумана","Аптекарский огород",
"Парк Сокольники","Музеон","Симонов монастырь",
"Новодевичий монастырь","ГЭС-2","Парк Яуза","Северный речной вокзал"
];
// 30 занятий
const activities=[
"Фотосессия","Новое кафе","Самокат","Атмосферное видео","Пикник","Настолки",
"Музыка","15000 шагов","Познакомиться","Лучший кофе","Скетч","Книга на лавке",
"Лодка","Стритфуд","Снять reels","Необычные двери","Челлендж 500₽",
"Плейлист","Бумажный самолетик","Бадминтон","10 собак","Мини-влог","Скрытый дворик",
"Поговорить о мечтах","Маршрут на карте","Дегустация десертов","Самая красивая лавка",
"Придумать историю прохожему","Посидеть в тишине","Смешной челлендж"
];
// 20 образов
const outfits=[
"Спортивный кэжуал","Минимализм","Street-style","Романтичный","Total white",
"Оверсайз худи","Пиджак + кроссовки","Летнее платье","Гранж","Бежевый монохром",
"Винтаж","Smart casual","Кожаная куртка","Джинсы + рубашка","Яркие аксессуары",
"Total denim","Пастель","Темный стиль","Сканди","Арт-образ"
];
function randomFrom(arr){return arr[Math.floor(Math.random()*arr.length)];}
function spinEffect(el,callback){
el.classList.add("spin");
let count=0;
let interval=setInterval(()=>{
el.innerText="...";
count++;
if(count>10){clearInterval(interval);el.classList.remove("spin");callback();}
},100);
}
function spinPlace(){
let el=document.getElementById("place");
spinEffect(el,()=>{
let r=randomFrom(places);
el.innerText=r;
document.getElementById("placeImg").src="https://source.unsplash.com/600x400/?moscow,"+r;
});
}
function spinActivity(){
let el=document.getElementById("activity");
spinEffect(el,()=>{
let r=randomFrom(activities);
el.innerText=r;
document.getElementById("activityImg").src="https://source.unsplash.com/600x400/?"+r;
});
}
function spinOutfit(){
let el=document.getElementById("outfit");
spinEffect(el,()=>{
let r=randomFrom(outfits);
el.innerText=r;
document.getElementById("outfitImg").src="https://source.unsplash.com/600x400/?fashion,"+r;
});
}
function surprise(){
spinPlace();
setTimeout(spinActivity,1200);
setTimeout(spinOutfit,2400);
}
function toggleDark(){document.body.classList.toggle("dark");}
</script>
</body>
</html>
