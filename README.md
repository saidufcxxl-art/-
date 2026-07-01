# -<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>China Interview Trainer</title>
<style>
body{margin:0;font-family:Arial;background:#020617;color:white;padding:14px}
.app{max-width:600px;margin:auto}
h1{text-align:center;margin-bottom:4px}
.sub{text-align:center;color:#cbd5e1;margin-top:0;font-size:14px}
.card{background:#111827;border-radius:18px;padding:15px;margin:12px 0}
.label{color:#fde68a;font-size:13px;margin-top:10px}
.big{font-size:22px;font-weight:bold}
.line{background:#020617;border-radius:12px;padding:12px;margin:7px 0;line-height:1.4}
.read{color:#93c5fd}.ru{color:#fca5a5}.tj{color:#86efac}
button{width:100%;border:0;border-radius:12px;padding:14px;margin-top:8px;font-size:16px;font-weight:bold;color:white;background:#2563eb}
.green{background:#16a34a}.gray{background:#475569}
.score{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.score div{background:#020617;border-radius:12px;padding:10px;text-align:center}
.bad{color:#fca5a5}.good{color:#86efac}.small{color:#cbd5e1;font-size:14px}
</style>
</head>
<body>

<div class="app">
<h1>🎓 China Interview Trainer</h1>
<p class="sub">Выучи короткие ответы за 5–6 дней</p>

<div class="card">
<div class="label">Question <span id="num"></span></div>

<div class="label">🇬🇧 English</div>
<div class="big" id="q"></div>

<div class="label">🔤 Как читать</div>
<div class="line read" id="qr"></div>

<div class="label">🇷🇺 Русский</div>
<div class="line ru" id="ru"></div>

<div class="label">🇹🇯 Тоҷикӣ</div>
<div class="line tj" id="tj"></div>

<button onclick="speak(data[i].q)">🔊 Послушать вопрос</button>
<button class="green" onclick="record()">🎤 Ответить голосом</button>
<button class="gray" onclick="next()">➡️ Следующий вопрос</button>
</div>

<div class="card">
<b>🎤 Твой ответ:</b>
<div class="line" id="answer">Пока ответа нет...</div>
</div>

<div class="card">
<b>✅ Короткий правильный ответ</b>

<div class="label">🇬🇧 English</div>
<div class="line" id="se"></div>

<div class="label">🔤 Как читать</div>
<div class="line read" id="sr"></div>

<div class="label">🇷🇺 Русский</div>
<div class="line ru" id="sru"></div>

<div class="label">🇹🇯 Тоҷикӣ</div>
<div class="line tj" id="stj"></div>

<button onclick="speak(data[i].se)">🔊 Послушать ответ</button>
</div>

<div class="card">
<b>📊 Проверка</b>
<div class="score">
<div>Grammar<br><b id="g">0%</b></div>
<div>Pronunciation<br><b id="p">0%</b></div>
<div>Vocabulary<br><b id="v">0%</b></div>
<div>Fluency<br><b id="f">0%</b></div>
</div>
<div id="fb"></div>
</div>
</div>

<script>
const data=[
{
q:"Tell me about yourself.",
qr:"Тел ми эбаут ёрселф.",
ru:"Расскажите о себе.",
tj:"Дар бораи худатон нақл кунед.",
se:"Hello. My name is Said. I am 21 years old. I am from Tajikistan. I finished secondary school. I want to study in China because I want a good education and a successful future.",
sr:"Хэлоу. Май нейм из Саид. Ай эм твэнти уан йирз оулд. Ай эм фром Таджикистан. Ай финишт сэкэндэри скул. Ай уонт ту стади ин Чайна бикоз ай уонт э гуд эджукейшн энд э саксэсфул фьючер.",
sru:"Здравствуйте. Меня зовут Саид. Мне 21 год. Я из Таджикистана. Я окончил среднюю школу. Я хочу учиться в Китае, потому что хочу получить хорошее образование и успешное будущее.",
stj:"Салом. Номи ман Саид аст. Ман 21 сола ҳастам. Ман аз Тоҷикистон ҳастам. Ман мактаби миёнаро хатм кардам. Ман мехоҳам дар Чин таҳсил кунам, зеро мехоҳам таҳсилоти хуб ва ояндаи муваффақ дошта бошам.",
keys:["said","21","tajikistan","school","china","education","future"]
},
{
q:"Where are you from?",
qr:"Вэа ар ю фром?",
ru:"Откуда вы?",
tj:"Шумо аз куҷо ҳастед?",
se:"I am from Tajikistan. It is a beautiful country in Central Asia.",
sr:"Ай эм фром Таджикистан. Ит из э бьютифул кантри ин Сентрал Эйжа.",
sru:"Я из Таджикистана. Это красивая страна в Центральной Азии.",
stj:"Ман аз Тоҷикистон ҳастам. Ин кишвари зебо дар Осиёи Марказӣ аст.",
keys:["tajikistan","country"]
},
{
q:"How old are you?",
qr:"Хау оулд ар ю?",
ru:"Сколько вам лет?",
tj:"Шумо чандсола ҳастед?",
se:"I am 21 years old.",
sr:"Ай эм твэнти уан йирз оулд.",
sru:"Мне 21 год.",
stj:"Ман 21 сола ҳастам.",
keys:["21","years old"]
},
{
q:"What school did you finish?",
qr:"Вот скул дид ю финиш?",
ru:"Какую школу вы окончили?",
tj:"Шумо кадом мактабро хатм кардед?",
se:"I finished secondary school in Tajikistan.",
sr:"Ай финишт сэкэндэри скул ин Таджикистан.",
sru:"Я окончил среднюю школу в Таджикистане.",
stj:"Ман мактаби миёнаро дар Тоҷикистон хатм кардам.",
keys:["finished","school","tajikistan"]
},
{
q:"Why do you want to study in China?",
qr:"Вай ду ю уонт ту стади ин Чайна?",
ru:"Почему вы хотите учиться в Китае?",
tj:"Чаро мехоҳед дар Чин таҳсил кунед?",
se:"China has good universities. I want a good education and new opportunities.",
sr:"Чайна хэз гуд юниверситиз. Ай уонт э гуд эджукейшн энд нью опортьюнитиз.",
sru:"В Китае хорошие университеты. Я хочу получить хорошее образование и новые возможности.",
stj:"Дар Чин донишгоҳҳои хуб ҳастанд. Ман мехоҳам таҳсилоти хуб ва имкониятҳои нав гирам.",
keys:["china","universities","education"]
},
{
q:"Why did you choose this university?",
qr:"Вай дид ю чуз зис юниверсити?",
ru:"Почему вы выбрали этот университет?",
tj:"Чаро ин донишгоҳро интихоб кардед?",
se:"This university has a good reputation. I think it is the right place for me.",
sr:"Зис юниверсити хэз э гуд репьютэйшн. Ай синк ит из зэ райт плэйс фор ми.",
sru:"У этого университета хорошая репутация. Я думаю, это правильное место для меня.",
stj:"Ин донишгоҳ обрӯи хуб дорад. Ман фикр мекунам, ки ин ҷой барои ман мувофиқ аст.",
keys:["university","reputation"]
},
{
q:"Why did you choose your major?",
qr:"Вай дид ю чуз ё мэйджор?",
ru:"Почему вы выбрали специальность?",
tj:"Чаро ин ихтисосро интихоб кардед?",
se:"I like this field. I want to build my future in this profession.",
sr:"Ай лайк зис филд. Ай уонт ту билд май фьючер ин зис профэшн.",
sru:"Мне нравится эта сфера. Я хочу построить своё будущее в этой профессии.",
stj:"Ин соҳа ба ман маъқул аст. Ман мехоҳам ояндаи худро дар ин касб созам.",
keys:["field","future","profession"]
},
{
q:"What are your future plans?",
qr:"Вот ар ё фьючер плэнс?",
ru:"Какие у вас планы на будущее?",
tj:"Нақшаҳои ояндаи шумо чист?",
se:"I want to graduate, get a good job, and help my family.",
sr:"Ай уонт ту грэджуэйт, гет э гуд джоб, энд хэлп май фэмили.",
sru:"Я хочу окончить университет, получить хорошую работу и помогать семье.",
stj:"Ман мехоҳам донишгоҳро хатм кунам, кори хуб гирам ва ба оилаам кӯмак кунам.",
keys:["graduate","job","family"]
},
{
q:"What are your strengths?",
qr:"Вот ар ё стрэнгс?",
ru:"Какие у вас сильные стороны?",
tj:"Ҷиҳатҳои қавии шумо кадомҳоянд?",
se:"I am responsible, hardworking, and always ready to learn.",
sr:"Ай эм риспонсибл, хардворкинг, энд олвэйз рэди ту лёрн.",
sru:"Я ответственный, трудолюбивый и всегда готов учиться.",
stj:"Ман масъулиятнок, меҳнатдӯст ва ҳамеша омодаи омӯзиш ҳастам.",
keys:["responsible","hardworking","learn"]
},
{
q:"What are your weaknesses?",
qr:"Вот ар ё викнэсэз?",
ru:"Какие у вас слабые стороны?",
tj:"Ҷиҳатҳои заифи шумо кадомҳоянд?",
se:"My English is not perfect, but I practice every day.",
sr:"Май Инглиш из нот пёрфэкт, бат ай прэктис эври дэй.",
sru:"Мой английский не идеальный, но я практикуюсь каждый день.",
stj:"Забони англисии ман комил нест, аммо ман ҳар рӯз машқ мекунам.",
keys:["english","practice"]
},
{
q:"How will you pay for your studies?",
qr:"Хау вил ю пэй фор ё стадиз?",
ru:"Как вы будете оплачивать обучение?",
tj:"Шумо таҳсилро чӣ гуна пардохт мекунед?",
se:"My family will support me. We are ready for tuition and living costs.",
sr:"Май фэмили вил сапорт ми. Ви ар рэди фор тьюишн энд ливинг костс.",
sru:"Моя семья будет поддерживать меня. Мы готовы к оплате обучения и проживания.",
stj:"Оилаи ман маро дастгирӣ мекунад. Мо барои пардохти таҳсил ва зиндагӣ омодаем.",
keys:["family","support"]
},
{
q:"Do you know Chinese language?",
qr:"Ду ю ноу Чайниз лэнгвидж?",
ru:"Вы знаете китайский язык?",
tj:"Шумо забони чиниро медонед?",
se:"I do not speak Chinese well yet, but I am ready to learn it.",
sr:"Ай ду нот спик Чайниз вел йет, бат ай эм рэди ту лёрн ит.",
sru:"Пока я не говорю хорошо по-китайски, но я готов его изучать.",
stj:"Ҳоло ман бо забони чинӣ хуб гап зада наметавонам, аммо омодаам онро омӯзам.",
keys:["chinese","learn","ready"]
},
{
q:"Are you ready to study abroad?",
qr:"Ар ю рэди ту стади эброд?",
ru:"Вы готовы учиться за границей?",
tj:"Оё шумо барои таҳсил дар хориҷ омодаед?",
se:"Yes, I am ready. I will study hard and follow university rules.",
sr:"Йес, ай эм рэди. Ай вил стади хард энд фоллоу юниверсити рулз.",
sru:"Да, я готов. Я буду усердно учиться и соблюдать правила университета.",
stj:"Бале, ман омодаам. Ман сахт таҳсил мекунам ва қоидаҳои донишгоҳро риоя мекунам.",
keys:["ready","study","rules"]
},
{
q:"How will you adapt to China?",
qr:"Хау вил ю эдэпт ту Чайна?",
ru:"Как вы адаптируетесь в Китае?",
tj:"Шумо дар Чин чӣ гуна мутобиқ мешавед?",
se:"I will respect Chinese culture, make friends, and study every day.",
sr:"Ай вил риспэкт Чайниз калчер, мэйк фрэндз, энд стади эври дэй.",
sru:"Я буду уважать китайскую культуру, заводить друзей и учиться каждый день.",
stj:"Ман фарҳанги чиниро эҳтиром мекунам, дӯст пайдо мекунам ва ҳар рӯз таҳсил мекунам.",
keys:["respect","culture","friends","study"]
},
{
q:"What languages do you speak?",
qr:"Вот лэнгвиджиз ду ю спик?",
ru:"На каких языках вы говорите?",
tj:"Шумо бо кадом забонҳо гап мезанед?",
se:"I speak Tajik and Russian. I am also learning English.",
sr:"Ай спик Таджик энд Рашн. Ай эм олсо лёрнинг Инглиш.",
sru:"Я говорю на таджикском и русском. Также я изучаю английский.",
stj:"Ман бо забонҳои тоҷикӣ ва русӣ гап мезанам. Ҳамчунин англисиро меомӯзам.",
keys:["tajik","russian","english"]
},
{
q:"Tell us about your family.",
qr:"Тел ас эбаут ё фэмили.",
ru:"Расскажите о своей семье.",
tj:"Дар бораи оилаатон нақл кунед.",
se:"My family is very important to me. They support my education.",
sr:"Май фэмили из вэри импортэнт ту ми. Зэй сапорт май эджукейшн.",
sru:"Моя семья очень важна для меня. Они поддерживают моё образование.",
stj:"Оилаи ман барои ман хеле муҳим аст. Онҳо таҳсили маро дастгирӣ мекунанд.",
keys:["family","important","education"]
},
{
q:"What are your hobbies?",
qr:"Вот ар ё хобиз?",
ru:"Какие у вас хобби?",
tj:"Шавқҳои шумо кадомҳоянд?",
se:"I like learning new things, watching useful videos, and doing sports.",
sr:"Ай лайк лёрнинг нью сингз, вотчинг юсфул видиоз, энд дуинг спортс.",
sru:"Мне нравится учиться новому, смотреть полезные видео и заниматься спортом.",
stj:"Ба ман омӯхтани чизҳои нав, тамошои видеоҳои фоиданок ва варзиш маъқул аст.",
keys:["learning","videos","sports"]
},
{
q:"What do you know about China?",
qr:"Вот ду ю ноу эбаут Чайна?",
ru:"Что вы знаете о Китае?",
tj:"Шумо дар бораи Чин чӣ медонед?",
se:"China has a long history, rich culture, and modern technology.",
sr:"Чайна хэз э лонг хистори, рич калчер, энд модерн технолоджи.",
sru:"У Китая древняя история, богатая культура и современные технологии.",
stj:"Чин таърихи қадимӣ, фарҳанги бой ва технологияҳои муосир дорад.",
keys:["china","history","culture","technology"]
},
{
q:"Why should we choose you?",
qr:"Вай шуд ви чуз ю?",
ru:"Почему мы должны выбрать вас?",
tj:"Чаро мо бояд шуморо интихоб кунем?",
se:"I am motivated, responsible, and ready to study hard.",
sr:"Ай эм мотивэйтид, риспонсибл, энд рэди ту стади хард.",
sru:"Я мотивированный, ответственный и готов усердно учиться.",
stj:"Ман боғайрат, масъулиятнок ва омодаам сахт таҳсил кунам.",
keys:["motivated","responsible","study"]
},
{
q:"Do you have any questions for us?",
qr:"Ду ю хэв эни квэстчэнз фор ас?",
ru:"У вас есть вопросы к нам?",
tj:"Оё шумо ба мо савол доред?",
se:"Yes. I want to know more about student life and language support.",
sr:"Йес. Ай уонт ту ноу мор эбаут стьюдент лайф энд лэнгвидж сапорт.",
sru:"Да. Я хочу узнать больше о студенческой жизни и языковой поддержке.",
stj:"Бале. Ман мехоҳам дар бораи ҳаёти донишҷӯӣ ва дастгирии забонӣ бештар донам.",
keys:["student","life","language"]
}
];

let i=0;

function show(){
num.innerText=(i+1)+"/"+data.length;
q.innerText=data[i].q;
qr.innerText=data[i].qr;
ru.innerText=data[i].ru;
tj.innerText=data[i].tj;
se.innerText=data[i].se;
sr.innerText=data[i].sr;
sru.innerText=data[i].sru;
stj.innerText=data[i].stj;
}

function speak(text){
speechSynthesis.cancel();
let u=new SpeechSynthesisUtterance(text);
u.lang="en-US";
u.rate=.8;
speechSynthesis.speak(u);
}

function next(){
i=(i+1)%data.length;
answer.innerText="Пока ответа нет...";
fb.innerHTML="";
g.innerText=p.innerText=v.innerText=f.innerText="0%";
show();
}

function record(){
let SR=window.SpeechRecognition||window.webkitSpeechRecognition;
if(!SR){
alert("Голос не работает в этом браузере. Попробуй Chrome или Safari.");
return;
}
let rec=new SR();
rec.lang="en-US";
rec.interimResults=false;
rec.maxAlternatives=1;
answer.innerText="Слушаю... говори по-английски.";
rec.start();

rec.onresult=e=>{
let text=e.results[0][0].transcript;
let conf=Math.round(e.results[0][0].confidence*100);
answer.innerText=text;
check(text,conf);
};

rec.onerror=()=>{
answer.innerText="Не понял голос. Попробуй ещё раз.";
};
}

function check(text,conf){
let lower=text.toLowerCase();
let mistakes=[];
let grammar=100;
let pronunciation=conf||80;
let vocabulary=90;
let fluency=90;

function error(wrong,correct,why){
grammar-=15;
mistakes.push(`
<div class="line">
<div class="bad"><b>❌ ${wrong}</b></div>
<div class="good"><b>✅ ${correct}</b></div>
<div class="small">${why}</div>
</div>
`);
setTimeout(()=>speak(correct),300);
}

if(lower.includes("i want study")){
error("I want study","I want to study","После want нужно говорить to.");
}
if(lower.includes("study china")){
error("study China","study in China","Правильно: study in China.");
}
if(lower.includes("i am study")){
error("I am study","I am studying","После am нужен глагол с -ing.");
}
if(lower.includes("i from")){
error("I from Tajikistan","I am from Tajikistan","После I нужен глагол am.");
}
if(lower.includes("my english no good")){
error("My English no good","My English is not good yet","В английском нужен глагол is.");
}
if(lower.includes("i finished school")){
error("I finished school","I finished secondary school","Для интервью лучше сказать secondary school.");
}

grammar=Math.max(50,grammar);

g.innerText=grammar+"%";
p.innerText=pronunciation+"%";
v.innerText=vocabulary+"%";
f.innerText=fluency+"%";

if(mistakes.length){
fb.innerHTML="<h3>Исправь эти ошибки:</h3>"+mistakes.join("");
}else{
fb.innerHTML="<p class='good'><b>✅ Хорошо. Больших ошибок нет.</b></p>";
}
}

show();
</script>

</body>
</html>
