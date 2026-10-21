<!doctype html>
<html lang="ja">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no,viewport-fit=cover">
<meta name="theme-color" content="#ff7597"><title>AFTER THE ENCORE</title>
<style>
:root{--bg:#fff0f3;--main:#ff7597;--main-dark:#e65277;--accent:#7209b7;--card:#ffffff;--text:#2b2d42;--sub:#8d99ae;--line:#ffccd5;--green:#38b000}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent;touch-action:manipulation}
body{margin:0;background:var(--bg);color:var(--text);font-family:-apple-system,BlinkMacSystemFont,"Hiragino Sans","Yu Gothic",sans-serif;user-select:none;-webkit-user-select:none}
button{font:inherit;cursor:pointer;border:none;outline:none}

/* スタート画面 */
#start-screen{position:fixed;top:0;left:0;width:100%;height:100%;background:linear-gradient(160deg,#ff7597,#7209b7);z-index:100;display:flex;justify-content:center;align-items:center;padding:20px}
.start-card{background:rgba(255,255,255,0.95);backdrop-filter:blur(10px);padding:35px 25px;border-radius:32px;box-shadow:0 20px 40px rgba(0,0,0,0.2);max-width:340px;width:100%;text-align:center}
.start-card h1{font-size:28px;color:var(--main-dark);margin:0 0 20px;font-weight:900;letter-spacing:-1px}
.input-group input{width:100%;padding:16px;border:2px solid var(--line);border-radius:20px;font-size:16px;outline:none;text-align:center;font-weight:bold;color:var(--text);margin-bottom:20px;background:#fff}
.input-group input:focus{border-color:var(--main)}
.start-btn{width:100%;padding:16px;background:linear-gradient(90deg,var(--main),var(--accent));color:white;border-radius:20px;font-size:18px;font-weight:900;box-shadow:0 8px 20px rgba(255,117,151,0.4);transition:.15s}
.start-btn:active{transform:scale(0.96)}

/* アプリ全体構造 */
.app-frame{max-width:480px;margin:auto;min-height:100dvh;background:var(--bg);display:flex;flex-direction:column;position:relative;box-shadow:0 0 50px rgba(0,0,0,0.1)}

/* 上部ステータスヘッダー */
.top-bar{background:white;padding:12px 20px;border-bottom:2px solid var(--line);display:flex;justify-content:space-between;align-items:center;position:sticky;top:0;z-index:10}
.user-badge{display:flex;align-items:center;gap:8px}
.avatar{width:36px;height:36px;border-radius:50%;background:linear-gradient(135deg,#ff7597,#f72585);display:grid;place-items:center;color:white;font-weight:bold;font-size:14px}
.user-name{font-weight:800;font-size:14px}
.money-pill{background:#e8f5e9;color:#2e7d32;font-weight:900;font-size:15px;padding:6px 14px;border-radius:30px;border:1px solid #c8e6c9}

/* ミニステータス */
.status-bar{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;padding:12px 16px;background:white;margin-bottom:12px;border-bottom:1px solid var(--line)}
.status-item{text-align:center}
.status-item span{display:block;font-size:10px;color:var(--sub);font-weight:bold}
.status-item strong{font-size:16px;font-weight:900;color:var(--main-dark)}

/* コンテンツエリア */
.content{padding:0 16px 90px;flex:1}
.section{display:none}.section.active{display:block}

/* スマホバブル風カード */
.bubble-card{background:white;border-radius:24px;padding:16px;margin-bottom:12px;box-shadow:0 4px 15px rgba(255,117,151,0.08);border:1px solid rgba(255,204,213,0.5)}
.bubble-card h2{font-size:15px;margin:0 0 12px;font-weight:800;display:flex;justify-content:space-between;align-items:center}

/* アクションボタン（SNSボタン風） */
.app-btn{display:flex;align-items:center;gap:12px;background:#fff0f3;border:1.5px solid var(--line);padding:12px 16px;border-radius:18px;margin-bottom:8px;width:100%;text-align:left;transition:.15s}
.app-btn:active{transform:scale(0.97);background:#ffe3e8}
.btn-icon{width:40px;height:40px;border-radius:14px;background:white;display:grid;place-items:center;font-size:20px;box-shadow:0 2px 8px rgba(0,0,0,0.05)}
.btn-info{flex:1}
.btn-info strong{display:block;font-size:14px;color:var(--text)}
.btn-info small{font-size:11px;color:var(--sub)}
.btn-tag{font-size:10px;font-weight:bold;background:var(--main);color:white;padding:4px 8px;border-radius:10px}

/* グッズ一覧 */
.grid-items{display:grid;grid-template-columns:repeat(3,1fr);gap:8px}
.item-box{background:#fff0f3;border-radius:16px;padding:10px;text-align:center;font-size:11px;font-weight:bold}
.item-box span{font-size:24px;display:block;margin-bottom:2px}

/* ボトムSNSナビゲーション */
.app-nav{position:fixed;bottom:0;left:50%;transform:translateX(-50%);width:100%;max-width:480px;background:rgba(255,255,255,0.92);backdrop-filter:blur(15px);border-top:1px solid var(--line);display:grid;grid-template-columns:repeat(5,1fr);padding:8px 0 calc(8px + env(safe-area-inset-bottom));z-index:20}
.nav-btn{background:transparent;color:var(--sub);font-size:10px;font-weight:bold;display:flex;flex-direction:column;align-items:center;gap:3px}
.nav-btn span{font-size:20px}
.nav-btn.active{color:var(--main-dark)}

/* トースト通知 */
.toast{position:fixed;top:80px;left:50%;transform:translateX(-50%) translateY(-20px);background:var(--text);color:white;padding:12px 24px;border-radius:30px;font-size:13px;font-weight:bold;opacity:0;pointer-events:none;transition:.2s;z-index:100;box-shadow:0 8px 20px rgba(0,0,0,0.2)}
.toast.show{opacity:1;transform:translateX(-50%) translateY(0)}

/* ログタイムライン */
.timeline{display:grid;gap:8px}
.timeline-item{background:#fff0f3;padding:10px 14px;border-radius:16px;font-size:12px}
.timeline-item time{color:var(--main-dark);font-size:10px;font-weight:bold;display:block;margin-bottom:2px}
</style>
</head>
<body>

<!-- スタート画面 -->
<div id="start-screen">
 <div class="start-card">
  <h1>AFTER THE<br>ENCORE</h1>
  <div class="input-group">
   <input type="text" id="playerNameInput" placeholder="名前を入力">
  </div>
  <button class="start-btn" onclick="startGame()">アプリを始める ➔</button>
 </div>
</div>

<div class="app-frame">
 <div class="top-bar">
  <div class="user-badge">
   <div class="avatar" id="avatarIcon">✦</div>
   <div class="user-name" id="sideName">ユーザー</div>
  </div>
  <div class="money-pill" id="moneyTop">¥28,000</div>
 </div>

 <div class="status-bar">
  <div class="status-item"><span>満足度</span><strong id="oshiStat">42</strong></div>
  <div class="status-item"><span>信用</span><strong id="trustStat">65</strong></div>
  <div class="status-item"><span>体力</span><strong id="energyStat">78</strong></div>
 </div>

 <div class="content">
  <!-- ホーム -->
  <section class="section active" id="page-home">
   <div class="bubble-card" style="background:linear-gradient(135deg,#ff7597,#f72585);color:white">
    <h2 style="color:white">DAY <span id="sideDay">1</span> <span style="font-size:11px;opacity:0.9" id="dayHint">給料日まであと6日</span></h2>
    <p id="storyText" style="margin:0;font-size:13px;opacity:0.95">今日も自分らしく過ごそう！</p>
   </div>

   <div class="bubble-card">
    <h2>今日のアクション</h2>
    <button class="app-btn" onclick="act('work')"><span class="btn-icon">💼</span><div class="btn-info"><strong>仕事をする</strong><small>評価アップ</small></div><span class="btn-tag">+仕事</span></button>
    <button class="app-btn" onclick="act('oshi')"><span class="btn-icon">💗</span><div class="btn-info"><strong>推し活する</strong><small>満足度アップ</small></div><span class="btn-tag">+満足</span></button>
    <button class="app-btn" onclick="act('rest')"><span class="btn-icon">🌙</span><div class="btn-info"><strong>休む</strong><small>体力回復</small></div><span class="btn-tag">+体力</span></button>
    <button class="app-btn" onclick="act('scroll')"><span class="btn-icon">📱</span><div class="btn-info"><strong>SNSチェック</strong><small>ランダムイベント</small></div><span class="btn-tag">？</span></button>
   </div>

   <div class="bubble-card">
    <h2>Myコレクション</h2>
    <div class="grid-items" id="itemInventory">
     <p style="font-size:12px;color:var(--sub);margin:0;grid-column:1/-1">グッズがありません</p>
    </div>
   </div>
  </section>

  <!-- 仕事 -->
  <section class="section" id="page-work">
   <div class="bubble-card">
    <h2>事務所の仕事</h2>
    <button class="app-btn" onclick="act('announce')"><span class="btn-icon">📝</span><div class="btn-info"><strong>公式告知を作成</strong><small>体力 -8</small></div></button>
    <button class="app-btn" onclick="act('venue')"><span class="btn-icon">🎤</span><div class="btn-info"><strong>ライブ現場の準備</strong><small>体力 -14</small></div></button>
    <button class="app-btn" onclick="act('listen')"><span class="btn-icon">💬</span><div class="btn-info"><strong>メンバーの相談</strong><small>体力 -10</small></div></button>
   </div>
  </section>

  <!-- 推し活 -->
  <section class="section" id="page-oshi">
   <div class="bubble-card">
    <h2>推し活メニュー</h2>
    <button class="app-btn" onclick="act('official')"><span class="btn-icon">👀</span><div class="btn-info"><strong>公式情報をチェック</strong><small>無料</small></div></button>
    <button class="app-btn" onclick="act('cd')"><span class="btn-icon">💿</span><div class="btn-info"><strong>CDを購入</strong><small>¥1,800</small></div></button>
    <button class="app-btn" onclick="act('event')"><span class="btn-icon">🎟️</span><div class="btn-info"><strong>ライブに参加</strong><small>¥3,500</small></div></button>
   </div>
  </section>

  <!-- ショップ -->
  <section class="section" id="page-shop">
   <div class="bubble-card">
    <h2>推し活ショップ</h2>
    <button class="app-btn" onclick="buyItem('チェキ', '📸', 1000, 5)"><span class="btn-icon">📸</span><div class="btn-info"><strong>ランダムチェキ</strong><small>¥1,000</small></div></button>
    <button class="app-btn" onclick="buyItem('アクスタ', '🧍', 2200, 10)"><span class="btn-icon">🧍</span><div class="btn-info"><strong>アクリルスタンド</strong><small>¥2,200</small></div></button>
    <button class="app-btn" onclick="buyItem('ペンライト', '🪄', 3500, 15)"><span class="btn-icon">🪄</span><div class="btn-info"><strong>ペンライト</strong><small>¥3,500</small></div></button>
   </div>
  </section>

  <!-- ログ -->
  <section class="section" id="page-history">
   <div class="bubble-card">
    <h2>アクティビティ</h2>
    <div class="timeline" id="logList"></div>
    <button class="app-btn" style="margin-top:15px;justify-content:center;background:#fff;border-color:var(--line)" onclick="resetGame()">データリセット</button>
   </div>
  </section>
 </div>

 <nav class="app-nav">
  <button class="nav-btn active" data-page="home"><span>🏠</span>ホーム</button>
  <button class="nav-btn" data-page="work"><span>💼</span>仕事</button>
  <button class="nav-btn" data-page="oshi"><span>💗</span>推し活</button>
  <button class="nav-btn" data-page="shop"><span>🛍️</span>ショップ</button>
  <button class="nav-btn" data-page="history"><span>📜</span>ログ</button>
 </nav>
</div>

<div class="toast" id="toast"></div>

<script>
var initial={name:'',day:1,turns:0,money:28000,oshi:42,trust:65,energy:78,work:28,items:[],logs:[{day:1,time:'09:10',text:'アプリを起動しました！'}]};
var s=loadGame()||JSON.parse(JSON.stringify(initial));

function $(id){return document.getElementById(id);}
function clamp(n){return Math.max(0,Math.min(100,Math.round(n)));}
function yen(n){return '¥'+Math.round(n).toLocaleString('ja-JP');}
function loadGame(){try{return JSON.parse(localStorage.getItem('afterEncoreSave'))}catch(e){return null}}
function saveGame(){try{localStorage.setItem('afterEncoreSave',JSON.stringify(s))}catch(e){}}

function startGame(){
 var inputVal=$('playerNameInput').value.trim();
 s.name=inputVal || 'ユーザー';
 $('start-screen').style.display='none';
 saveGame();
 render();
}

function toast(t){var el=$('toast');el.textContent=t;el.classList.add('show');clearTimeout(window.toastTimer);window.toastTimer=setTimeout(function(){el.classList.remove('show')},2000)}
function spend(amount){if(s.money<amount){toast('お金が足りないよ');return false}s.money-=amount;return true}
function tired(n){if(s.energy<n){toast('体力が足りないよ');return false}s.energy-=n;return true}

function buyItem(name, icon, price, oshiGain){
 if(!spend(price))return;
 s.oshi=clamp(s.oshi+oshiGain);
 if(!s.items)s.items=[];
 s.items.push({name:name, icon:icon});
 log(name+' をGET！');
 render();
 saveGame();
 toast(name+' を購入！');
}

function act(type){
 var msg='';
 var isLucky = Math.random() < 0.2;

 switch(type){
  case'work':if(!tired(12))return;var g=isLucky?10:5;s.work=clamp(s.work+g);msg=isLucky?'仕事で大活躍！(+'+g+')':'仕事を進めた！';break;
  case'oshi':var og=isLucky?10:5;s.oshi=clamp(s.oshi+og);s.energy=clamp(s.energy-4);msg=isLucky?'推しからレスをもらった気分！(+'+og+')':'推し活を楽しんだ！';break;
  case'rest':s.energy=clamp(s.energy+25);msg='ゆっくり休んで体力回復！';break;
  case'scroll':if(Math.random()<0.5){s.oshi=clamp(s.oshi+3);msg='尊い写真を発見！'}else{s.energy=clamp(s.energy-5);msg='SNSを見すぎて少し疲れ気味…';}break;
  case'announce':if(!tired(8))return;s.work=clamp(s.work+8);msg='公式告知をアップ！';break;
  case'venue':if(!tired(14))return;s.work=clamp(s.work+12);msg='現場準備を完了！';break;
  case'listen':if(!tired(10))return;s.trust=clamp(s.trust+8);msg='相談に乗って信用アップ！';break;
  case'official':s.oshi=clamp(s.oshi+4);msg='公式をチェック！';break;
  case'cd':if(!spend(1800))return;s.oshi=clamp(s.oshi+10);msg='CDをGET！';break;
  case'event':if(!spend(3500))return;if(!tired(12)){s.money+=3500;return}s.oshi=clamp(s.oshi+18);msg='最高のライブだった！';break;
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
  log('一日が終了。');
  if(s.day%7===0){
   s.money+=18000;
   log('給料日！¥18,000 GET！');
  }
 }
}

function log(text){
 s.logs.unshift({day:s.day,time:new Date().toLocaleTimeString('ja-JP',{hour:'2-digit',minute:'2-digit'}),text:text});
 s.logs=s.logs.slice(0,50);
}

function showPage(page){
 var secs=document.querySelectorAll('.section');
 for(var i=0;i<secs.length;i++){secs[i].classList.toggle('active',secs[i].id==='page-'+page);}
 var btns=document.querySelectorAll('.nav-btn');
 for(var j=0;j<btns.length;j++){btns[j].classList.toggle('active',btns[j].dataset.page===page);}
}

var navBtns=document.querySelectorAll('.nav-btn');
for(var k=0;k<navBtns.length;k++){
 (function(b){
  b.addEventListener('click',function(){showPage(b.dataset.page);});
 })(navBtns[k]);
}

function render(){
 $('moneyTop').textContent=yen(s.money);
 $('oshiStat').textContent=s.oshi;
 $('trustStat').textContent=s.trust;
 $('energyStat').textContent=s.energy;
 $('sideDay').textContent=s.day;
 var remDays=7-(s.day%7);if(remDays===7)remDays=0;
 $('dayHint').textContent='給料日まであと'+remDays+'日';
 $('sideName').textContent=s.name||'ユーザー';
 if(s.name){ $('avatarIcon').textContent = s.name.charAt(0); }

 var html='';
 for(var p=0;p<s.logs.length;p++){
  html+='<div class="timeline-item"><time>DAY '+s.logs[p].day+' '+s.logs[p].time+'</time>'+s.logs[p].text+'</div>';
 }
 $('logList').innerHTML=html;

 if(s.items && s.items.length>0){
  var itemHtml='';
  for(var q=0;q<s.items.length;q++){
   itemHtml+='<div class="item-box"><span>'+s.items[q].icon+'</span>'+s.items[q].name+'</div>';
  }
  $('itemInventory').innerHTML=itemHtml;
 }else{
  $('itemInventory').innerHTML='<p style="font-size:12px;color:var(--sub);margin:0;grid-column:1/-1">グッズがありません</p>';
 }
}

function resetGame(){if(confirm('データリセットしますか？')){s=JSON.parse(JSON.stringify(initial));saveGame();location.reload();}}
if(s.name){$('start-screen').style.display='none';}
render();
</script>
</body>
</html>
