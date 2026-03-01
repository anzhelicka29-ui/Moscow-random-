<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Московская Рулетка</title>

<style>
:root{
  --bg:#f3f4f8;
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
  font-family:system-ui,-apple-system,sans-serif;
  background:var(--bg);
  color:var(--text);
  transition:0.3s;
}
.container{
  max-width:520px;
  margin:auto;
  padding:15px;
}
h1{
  text-align:center;
}
.card{
  background:var(--card);
  border-radius:18px;
  padding:15px;
  margin:20px 0;
  box-shadow:0 10px 25px rgba(0,0,0,0.08);
  text-align:center;
}
button{
  background:var(--accent);
  color:white;
  border:none;
  border-radius:30px;
  padding:12px 18px;
  font-size:16px;
  cursor:pointer;
  margin:6px;
}
img{
  width:100%;
  border-radius:12px;
  margin-top:10px;
  max-height:260px;
  object-fit:cover;
  display:none;
}
.result{
  font-weight:600;
  margin-top:10px;
  min-height:28px;
}
.spin{
  animation:pulse 0.6s infinite;
}
@keyframes pulse{
  0%{opacity:0.4;}
  50%{opacity:1;}
  100%{opacity:0.4;}
}
.top{
  display:flex;
  justify-content:space-between;
  align-items:center;
}
</style>
</head>

<body>

<div class="container">

<div class="top">
<h1>🎲 Московская Рулетка</h1>
<button onclick="toggleDark()">🌙</button>
</div>

<button onclick="surprise()">🔥 Удиви меня</button>

<div class="card">
<button onclick="spin('place')">Куда пойти?</button>
<div id="placeText" class="result"></div>
<img id="placeImg">
</div>

<div class="card">
<button onclick="spin('activity')">Чем заняться?</button>
<div id="activityText" class="result"></div>
<img id="activityImg">
</div>

<div class="card">
<button onclick="spin('outfit')">В чем пойти?</button>
<div id="outfitText" class="result"></div>
<img id="outfitImg">
</div>

</div>

<script>

const places = [
"Парк Горького","ВДНХ","Красная площадь","Москва-Сити",
"Патриаршие пруды","Зарядье","Коломенское","Серебряный бор",
"Сокольники","Кусково","Новодевичий монастырь",
"Лосиный остров","Музеон","ГЭС-2","Китай-город",
"Хлебозавод","Флакон","Сад Баумана
