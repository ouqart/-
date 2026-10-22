<!doctype html>
<html lang="ja">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no,viewport-fit=cover">
<meta name="theme-color" content="#f7f6f3">
<title>AFTER THE ENCORE</title>
<style>
:root{--bg:#f7f6f3;--card:#ffffff;--text:#2b2b2b;--sub:#767676;--line:#e5e3de;--accent:#c9708f;--tint:#faf9f6}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent;touch-action:manipulation}
body{margin:0;background:var(--bg);color:var(--text);font-family:-apple-system,BlinkMacSystemFont,"Hiragino Sans","Yu Gothic",sans-serif;line-height:1.7;letter-spacing:0.02em;user-select:none;-webkit-user-select:none}
button{font:inherit;cursor:pointer;border:none;outline:none}

.app{max-width:540px;margin:0 auto;min-height:100dvh;display:flex;flex-direction:column;padding:24px 16px}

header{padding-bottom:16px;display:flex;justify-content:space-between;align-items:baseline;border-bottom:1px solid var(--line);margin-bottom:20px}
.brand{font-size:11px;letter-spacing:0.15em;color:var(--sub);font-weight:600}
.user-status{font-size:12px;color:var(--sub)}

.stats-bar{display:grid;grid-template-columns:repeat(4,1fr);background:var(--card);border:1px solid var(--line);border-radius:8px;padding:12px;text-align:center;margin-bottom:20px}
.stat-item span{display:block;font-size:10px;color:var(--sub);margin-bottom:2px}
.stat-item strong{font-size:13px;font-weight:500;color:var(--text)}

.main-layout{display:grid;gap:16px;flex:1}

.panel{background:var(--card);border:1px solid var(--line);border-radius:8px;padding:20px}
.panel-title{font-size:11px;letter-spacing:0.1em;color:var(--sub);margin-bottom:12px;font-weight:600}

.action-list{display:grid;gap:8px}
.action-row{background:var(--tint);border:1px solid var(--line);border-radius:6px;padding:14px 16px;display:flex;justify-content:space-between;align-items:center;text-align:left;width:100%;transition:all 0.2s}
.action-row:hover{border-color:var(--accent);background:var(--card)}
.action-row strong{display:block;font-size:13px;font-weight:500;color:var(--text);margin-bottom:2px}
.action-row small{font-size:11px;color:var(--sub)}
.action-tag{font-size:11px;color:var(--accent);font-weight:500}

.log-stream{display:grid;gap:6px;max-height:180px;overflow-y:auto}
.log-entry{background:var(--tint);border:1px solid var(--line);border-radius:6px;padding:10px 14px;font-size:11px}
.log-time{font-size:9px;color:var(--sub);margin-bottom:2px;display:block}

.toast{position:fixed;top:20px;left:50%;transform:translateX(-50%) translateY(-20px);background:var(--text);color:white;padding:8px 16px;border-radius:4px;font-size:11px;opacity:0;pointer-events:none;transition:all 0.2s;z-index:100}
.toast.show{opacity:1;transform:translateX(-50%) translateY(0)}
</style>
</head>
<body>

<div class="app">
 <header>
  <div class="brand">AFTER THE ENCORE</div>
  <div class="user-status">残高 <strong id="moneyTop" style="color:var(--text);font-weight:500">¥28,000</strong></div>
 </header>

 <div class="stats-bar">
  <div class="stat-item"><span>満足度</span><strong id="oshiStat">42</strong></div>
  <div class="stat-item"><span>信用度</span><strong id="trustStat">65</strong></div>
  <div class="stat-item"><span>体力</span><strong id="energyStat">78</strong></div>
  <div class="stat-item"><span>給料日まで</span><strong id="dayHint">6日</strong></div>
 </div>

 <div class="main-layout">
  <div class="panel">
   <div class="panel-title">日々の選択 (DAY <span id="sideDay">1</span>)</div>
   <div class="action-list">
    <button class="action-row" onclick="act('work')"><div><strong>仕事をする</strong><small>事務所の業務を進めて評価を高める</small></div><span class="action-tag">+仕事</span></button>
    <button class="action-row" onclick="act('oshi')"><div><strong>推し活をする</strong><small>情報を追い、心を満たす</small></div><span class="action-tag">+満足</span></button>
    <button class="action-row" onclick="act('rest')"><div><strong>休息を取る</strong><small>すり減った体力を回復させる</small></div><span class="action-tag">+体力</span></button>
    <button class="action-row" onclick="act('cd')"><div><strong>CDを購入する</strong><small>作品を手元に迎える (¥1,800)</small></div><span class="action-tag">¥1,800</span></button>
   </div>
  </div>

  <div class="panel">
   <div class="panel-title">記録</div>
   <div class="log-stream" id="logList"></div>
  </div>
 </div>
</div>

<div class="toast" id="toast"></div>

<script>
var s={day:1,turns:0,money:28000,oshi:42,trust:65,energy:78,work:28,logs:[{day:1,time:'09:10',text:'物語が始まった。'}]};
function loadGame(){try{var d=localStorage.getItem('afterEncoreSave');return d?JSON.parse(d):null}catch(e){return null}}
var saved=loadGame();if(saved)s=saved;

function $(id){return document.getElementById(id);}
function clamp(n){return Math.max(0,Math.min(100,Math.round(n)));}
function yen(n){return '¥'+Math.round(n).toLocaleString('ja-JP');}
function saveGame(){try{localStorage.setItem('afterEncoreSave',JSON.stringify(s))}catch(e){}}

function toast(t){var el=$('toast');el.textContent=t;el.classList.add('show');clearTimeout(window.toastTimer);window.toastTimer=setTimeout(function(){el.classList.remove('show')},2000)}
function spend(amount){if(s.money<amount){toast('資金が足りません');return false}s.money-=amount;return true}
function tired(n){if(s.energy<n){toast('体力が限界です。休息を取ってください');return false}s.energy-=n;return true}

function act(type){
 var msg='';
 var isLucky = Math.random() < 0.2;

 switch(type){
  case'work':if(!tired(12))return;var g=isLucky?10:5;s.work=clamp(s.work+g);msg=isLucky?'丁寧な仕事ぶりが評価された。':'業務を堅実にこなした。';break;
  case'oshi':var og=isLucky?10:5;s.oshi=clamp(s.oshi+og);s.energy=clamp(s.energy-4);msg=isLucky?'心動かされる瞬間に出会えた。':'推しの気配を感じて心が満たされた。';break;
  case'rest':s.energy=clamp(s.energy+25);msg='静かな部屋でしっかりと休息を取った。';break;
  case'cd':if(!spend(1800))return;s.oshi=clamp(s.oshi+10);msg='届いたパッケージを開封した。';break;
 }
 if(!msg)return;
 log(msg);
 advanceMaybe();
 render();
 saveGame();
 toast(msg);
}

function advanceMaybe(){
 s.turns=(s.turns||0)+1;
 if(s.energy<=10||s.turns>=3){
  s.day++;
  s.turns=0;
  s.energy=clamp(s.energy+10);
  log('一日が静かに暮れていく。');
  if(s.day%7===0){
   s.money+=18000;
   log('給与が振り込まれた (¥18,000)');
  }
 }
}

function log(text){
 s.logs.unshift({day:s.day,time:new Date().toLocaleTimeString('ja-JP',{hour:'2-digit',minute:'2-digit'}),text:text});
 s.logs=s.logs.slice(0,30);
}

function render(){
 $('moneyTop').textContent=yen(s.money);
 $('oshiStat').textContent=s.oshi;
 $('trustStat').textContent=s.trust;
 $('energyStat').textContent=s.energy;
 $('sideDay').textContent=s.day;
 var remDays=7-(s.day%7);if(remDays===7)remDays=0;
 $('dayHint').textContent=remDays+'日';

 var html='';
 for(var p=0;p<s.logs.length;p++){
  html+='<div class="log-entry"><span class="log-time">DAY '+s.logs[p].day+' / '+s.logs[p].time+'</span>'+s.logs[p].text+'</div>';
 }
 $('logList').innerHTML=html;
}

render();
</script>
</body>
</html>
