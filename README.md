# Russian-People-and-Holidays
Практические задания для обучающихся по подготовке к ЕГЭ
from pathlib import Path

html = r'''<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Russia Quiz — тренажёр</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700;800;900&display=swap');
  :root{
    --ink:#29264b; --muted:#77748f; --purple:#7866df; --purple-dark:#5e4bc7;
    --pink:#ff8eae; --yellow:#ffd66b; --mint:#8ee2c1; --paper:#fff;
    --bg:#f5f2ff; --line:#e9e5f7; --good:#21875e; --bad:#c94e69;
  }
  *{box-sizing:border-box}
  body{margin:0;background:var(--bg);color:var(--ink);font-family:'Nunito',system-ui,sans-serif;min-height:100vh}
  .page{max-width:1040px;margin:auto;padding:24px 20px 50px}
  header{display:flex;align-items:center;justify-content:space-between;gap:14px;margin-bottom:25px}
  .brand{display:flex;align-items:center;gap:11px;font-weight:900;font-size:1.25rem}
  .logo{width:43px;height:43px;border-radius:15px;background:var(--yellow);display:grid;place-items:center;font-size:24px;box-shadow:0 4px 0 #e8b94d}
  .tag{font-size:.78rem;color:var(--muted);font-weight:800;background:#fff;padding:8px 13px;border-radius:20px}
  .hero{text-align:center;padding:24px 10px 25px}
  .eyebrow{display:inline-block;background:#e9e4ff;color:var(--purple-dark);font-weight:900;font-size:.78rem;letter-spacing:.08em;text-transform:uppercase;padding:7px 13px;border-radius:30px}
  h1{font-size:clamp(2rem,5vw,3.35rem);line-height:1.08;margin:16px 0 10px;font-weight:900;letter-spacing:-.04em}
  .hero p{color:var(--muted);font-size:1.05rem;margin:0 auto;max-width:580px}
  .tabs{display:grid;grid-template-columns:1fr 1fr;gap:12px;max-width:680px;margin:24px auto 26px}
  .tab{border:2px solid var(--line);background:#fff;border-radius:18px;padding:15px 18px;text-align:left;cursor:pointer;color:var(--ink);font:inherit;transition:.18s}
  .tab strong{display:block;font-weight:900;font-size:1rem}.tab span{font-size:.83rem;color:var(--muted)}
  .tab.active{border-color:var(--purple);background:#f0edff;box-shadow:0 4px 0 #d9d1ff;transform:translateY(-2px)}
  .tab .emoji{font-size:1.5rem;float:right}
  .card{max-width:760px;margin:auto;background:#fff;border:2px solid var(--line);border-radius:26px;padding:clamp(18px,4vw,34px);box-shadow:0 9px 0 #e8e3f5}
  .topline{display:flex;align-items:center;justify-content:space-between;gap:12px;margin-bottom:15px}
  .counter{font-weight:900;color:var(--muted);font-size:.9rem}
  .progress{height:10px;background:#eeeaf8;border-radius:20px;overflow:hidden;flex:1;max-width:360px}
  .progress i{display:block;height:100%;width:0;background:linear-gradient(90deg,var(--purple),var(--pink));border-radius:20px;transition:width .3s}
  .score{font-size:.85rem;font-weight:900;background:#fff5d8;padding:7px 11px;border-radius:20px}
  .instruction{color:var(--muted);font-weight:800;font-size:.9rem;margin:0 0 9px}
  h2{font-size:clamp(1.35rem,3vw,1.8rem);line-height:1.2;margin:0 0 20px;font-weight:900}
  .question{background:#f7f5ff;border:1px solid #ece8fb;border-radius:17px;padding:18px;margin-bottom:19px;font-size:1.06rem;font-weight:700;line-height:1.55}
  .options{display:grid;gap:10px}
  .option{display:flex;align-items:center;gap:12px;width:100%;text-align:left;background:white;border:2px solid var(--line);border-radius:15px;padding:13px 15px;color:var(--ink);font:700 1rem 'Nunito',sans-serif;cursor:pointer;transition:.15s}
  .option:hover:not(:disabled){border-color:#b9aff5;background:#faf9ff;transform:translateY(-1px)}
  .option .letter{width:30px;height:30px;flex:0 0 30px;border-radius:10px;background:#f0edff;color:var(--purple-dark);display:grid;place-items:center;font-weight:900}
  .option.correct{border-color:#69c99d;background:#edfff6;color:#176c49}
  .option.wrong{border-color:#f09aad;background:#fff1f4;color:#a83450}
  .option:disabled{cursor:default;opacity:1}
  .feedback{display:none;margin-top:17px;border-radius:15px;padding:14px 16px;line-height:1.45;font-weight:700}
  .feedback.show{display:block}.feedback.good{background:#eafff3;color:#176c49}.feedback.bad{background:#fff0f3;color:#a83450}
  .feedback strong{display:block;margin-bottom:3px}
  .actions{display:flex;justify-content:space-between;gap:10px;margin-top:22px;align-items:center}
  button.primary,button.secondary{border:0;border-radius:14px;padding:13px 21px;font:900 .98rem 'Nunito',sans-serif;cursor:pointer}
  .primary{background:var(--purple);color:#fff;box-shadow:0 4px 0 var(--purple-dark)}
  .primary:hover{background:var(--purple-dark)}.primary:disabled{opacity:.4;cursor:not-allowed}
  .secondary{background:#f1eff8;color:var(--muted)}
  .hint{font-size:.8rem;color:var(--muted);font-weight:700}
  .result{display:none;text-align:center;padding:25px 5px 12px}
  .result .big{font-size:4rem}.result h2{margin:10px 0}.result p{color:var(--muted);font-weight:700}
  .result .primary{margin-top:12px}
  .footer{text-align:center;color:#9a96ad;font-size:.8rem;font-weight:700;margin:25px 0 0}
  @media(max-width:560px){.page{padding:15px 12px 35px}.tag{display:none}.tabs{gap:8px}.tab{padding:12px}.tab span{font-size:.75rem}.card{border-radius:20px}.topline{flex-wrap:wrap}.progress{order:3;max-width:none;flex-basis:100%}.actions{align-items:stretch}.actions button{flex:1}.hint{display:none}}
</style>
</head>
<body>
<div class="page">
  <header>
    <div class="brand"><div class="logo">🇷🇺</div><span>Russia Quiz</span></div>
    <div class="tag">Учись · играй · запоминай</div>
  </header>
  <section class="hero">
    <span class="eyebrow">Тренажёр знаний</span>
    <h1>Проверь, что ты<br>знаешь о России!</h1>
    <p>Выбирай ответы, набирай баллы и сразу узнавай правильный вариант. Поехали! ✨</p>
  </section>

  <nav class="tabs" aria-label="Разделы тренажёра">
    <button class="tab active" data-part="people"><span class="emoji">🧠</span><strong>Часть 1</strong><span>Russian Famous People</span></button>
    <button class="tab" data-part="holidays"><span class="emoji">🎉</span><strong>Часть 2</strong><span>Russian National Holidays</span></button>
  </nav>

  <main class="card">
    <div id="quiz">
      <div class="topline">
        <span class="counter" id="counter">Вопрос 1 из 11</span>
        <div class="progress"><i id="bar"></i></div>
        <span class="score" id="score">⭐ 0</span>
      </div>
      <p class="instruction" id="instruction">Выбери одного человека</p>
      <h2 id="title">Кто это?</h2>
      <div class="question" id="question"></div>
      <div class="options" id="options"></div>
      <div class="feedback" id="feedback" aria-live="polite"></div>
      <div class="actions">
        <span class="hint" id="hint">Выбери ответ, чтобы продолжить</span>
        <button class="primary" id="next" disabled>Далее →</button>
      </div>
    </div>
    <div class="result" id="result">
      <div class="big" id="resultEmoji">🏆</div>
      <h2 id="resultTitle">Отличная работа!</h2>
      <p id="resultText"></p>
      <button class="primary" id="restart">Пройти ещё раз ↻</button>
    </div>
  </main>
  <p class="footer">Сделано для практики английского и страноведения 💜</p>
</div>

<script>
const people = [
 ["Pavel Yablochkov","Inventor of the Yablochkov candle (electric carbon arc lamp) and the transformer."],
 ["Ivan Sechenov","Outstanding scientist in psychology, physiology, and anatomy."],
 ["Andrei Sakharov","Nuclear physicist and human rights activist; Nobel Peace Prize winner."],
 ["Mikhail Vrubel","Painter who worked in graphics and sculpture."],
 ["Alexander Blok","Russian lyrical poet, a major figure of the Symbolism style."],
 ["Evgenia Medvedeva","Two-time European and World champion figure skater; two-time Olympic silver medalist."],
 ["Anton Shipulin","Retired biathlete, Olympic gold medalist (relay) at the 2014 Sochi Olympics."],
 ["Sergey Bezrukov","Screen and stage actor and singer."],
 ["Denis Matsuev","World-famous classical pianist."],
 ["Kuzma Minin and Dmitry Pozharsky","Heroes who defeated the Polish army in 1612."],
 ["Peter the Great","Tsar who founded St. Petersburg and initiated many developments."]
];
const holidays = [
 {name:"New Year Holidays (January 1)",symbol:"The start of the new calendar year.",celebrate:"Families gather for lavish meals, exchange gifts, and watch the President's televised address before the Kremlin's chimes ring in the new year at midnight. The holiday is marked by decorated fir trees (yolka) and fireworks."},
 {name:"Orthodox Christmas Day (January 7)",symbol:"The birth of Jesus Christ.",celebrate:"This is a more solemn and religious holiday than in the West, marked by attending church services. It is a day for family and spiritual reflection."},
 {name:"Defender of the Fatherland Day (February 23)",symbol:"Military valor and strength, but is now widely celebrated as a day for all men.",celebrate:"Women give gifts and congratulations to the men in their lives. It is also a day to honor military veterans and active servicemen, sometimes with parades."},
 {name:"International Women's Day (March 8)",symbol:"Women, their achievements, and the arrival of spring.",celebrate:"Men give flowers (especially tulips), gifts, and compliments to their wives, mothers, daughters, and female colleagues."},
 {name:"Spring and Labour Day (May 1)",symbol:"The arrival of spring and the dignity of labor.",celebrate:"In the Soviet era, it was marked with massive parades and demonstrations. Today, it is primarily a day off for rest and relaxation."}
];
let part="people", index=0, score=0, answered=false, questions=[];
const $=id=>document.getElementById(id);
const shuffle=a=>[...a].sort(()=>Math.random()-.5);
function makePeople(){return shuffle(people).map(([name,desc])=>({kind:"one",prompt:desc,correct:[name],choices:shuffle(people.map(p=>p[0]))}));}
function makeHolidays(){
 const qs=[];
 holidays.forEach(h=>{
  qs.push({kind:"one",prompt:`${h.name}: What does this holiday symbolise?`,correct:[h.symbol],choices:shuffle(holidays.map(x=>x.symbol))});
  qs.push({kind:"one",prompt:`${h.name}: How do people celebrate it?`,correct:[h.celebrate],choices:shuffle(holidays.map(x=>x.celebrate))});
 });
 return shuffle(qs);
}
function start(p=part){
 part=p;index=0;score=0;answered=false;
 questions=p==="people"?makePeople():makeHolidays();
 $("quiz").style.display="block";$("result").style.display="none";
 document.querySelectorAll(".tab").forEach(b=>b.classList.toggle("active",b.dataset.part===part));
 render();
}
function render(){
 const q=questions[index];answered=false;
 $("counter").textContent=`Вопрос ${index+1} из ${questions.length}`;
 $("bar").style.width=`${index/questions.length*100}%`;
 $("score").textContent=`⭐ ${score}`;
 $("instruction").textContent=part==="people"?"Выбери одного человека":"Выбери правильный вариант";
 $("title").textContent=part==="people"?"Who is this person?":"Russian National Holidays";
 $("question").textContent=q.prompt;
 $("options").innerHTML="";
 q.choices.forEach((choice,i)=>{
  const b=document.createElement("button");b.className="option";
  const letter=document.createElement("span");letter.className="letter";letter.textContent=String.fromCharCode(65+i);
  const text=document.createElement("span");text.textContent=choice;
  b.append(letter,text);b.addEventListener("click",()=>choose(b,choice,q));$("options").append(b);
 });
 $("feedback").className="feedback";$("feedback").innerHTML="";
 $("next").disabled=true;$("next").textContent=index===questions.length-1?"Результат →":"Далее →";
 $("hint").textContent="Выбери ответ, чтобы продолжить";
}
function choose(button,choice,q){
 if(answered)return;answered=true;
 const correct=choice===q.correct[0];
 if(correct)score++;
 document.querySelectorAll(".option").forEach(b=>{
  b.disabled=true;
  if(b.querySelector("span:last-child").textContent===q.correct[0])b.classList.add("correct");
 });
 if(!correct)button.classList.add("wrong");
 const fb=$("feedback");fb.className=`feedback show ${correct?"good":"bad"}`;
 fb.innerHTML=correct?`<strong>Верно! 🎉</strong>Отличный ответ!`:`<strong>Не совсем! 💡 Правильный ответ:</strong>${escapeHtml(q.correct[0])}`;
 $("score").textContent=`⭐ ${score}`;$("next").disabled=false;$("hint").textContent=correct?"Так держать!":"Запомни правильный ответ";
}
function escapeHtml(s){return s.replace(/[&<>"']/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]));}
function finish(){
 $("quiz").style.display="none";$("result").style.display="block";
 const pct=Math.round(score/questions.length*100);
 $("resultEmoji").textContent=pct===100?"🏆":pct>=70?"🌟":pct>=40?"💪":"🌱";
 $("resultTitle").textContent=pct===100?"Идеально!":pct>=70?"Отличная работа!":pct>=40?"Хорошая попытка!":"Продолжай тренироваться!";
 $("resultText").textContent=`Твой результат: ${score} из ${questions.length} (${pct}%). ${pct===100?"Все ответы правильные!":"Повтори материал и попробуй ещё раз."}`;
}
$("next").addEventListener("click",()=>{if(!answered)return;if(index<questions.length-1){index++;render();}else finish();});
$("restart").addEventListener("click",()=>start(part));
document.querySelectorAll(".tab").forEach(b=>b.addEventListener("click",()=>start(b.dataset.part)));
start("people");
</script>
</body>
</html>'''
path = Path("/mnt/data/russia_quiz.html")
path.write_text(html, encoding="utf-8")
print(path)
