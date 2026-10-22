<!doctype html>
<html lang="ja">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no,viewport-fit=cover">
<meta name="theme-color" content="#fff0f5"><title>AFTER THE ENCORE</title>
<style>
:root{--bg:#fff0f5;--panel:#ffffff;--panel2:#ffe4e9;--ink:#4a2e35;--muted:#a07883;--line:#f7c8d3;--pink:#ff6b8b;--pink-hover:#ff4770;--green:#48bb78;--gold:#ed8936;--red:#f56565}*{box-sizing:border-box;-webkit-tap-highlight-color:transparent;touch-action:manipulation}body{margin:0;background:var(--bg);color:var(--ink);font-family:-apple-system,BlinkMacSystemFont,"Hiragino Kaku Gothic ProN","Yu Gothic",sans-serif;line-height:1.5}button{font:inherit;cursor:pointer;border:none;outline:none}

/* スタート画面 */
#start-screen{position:fixed;top:0;left:0;width:100%;height:100%;background:linear-gradient(135deg,#ffdde1,#ee9ca7);z-index:100;display:flex;flex-direction:column;justify-content:center;align-items:center;padding:20px}
.start-card{background:var(--panel);padding:35px 25px;border-radius:24px;border:2px solid var(--line);box-shadow:0 15px 35px rgba(255,107,139,0.2);max-width:360px;width:100%;text-align:center}
.start-card h1{font-size:28px;color:var(--pink);margin:0 0 20px;font-weight:900;letter-spacing:.05em}
.input-group{margin-bottom:20px;text-align:left}
.input-group label{display:block;font-size:12px;font-weight:bold;color:var(--muted);margin-bottom:6px}
.input-group input{width:100%;padding:12px 14px;border:2px solid var(--line);border-radius:14px;font-size:15px;outline:none;color:var(--ink);background:#fff}
.input-group input:focus{border-color:var(--pink)}
.start-btn{width:100%;padding:14px;border:none;background:linear-gradient(135deg,var(--pink),#ff4770);color:white;border-radius:14px;font-size:16px;font-weight:bold;letter-spacing:.1em;box-shadow:0 6px 15px rgba(255,107,139,0.3);transition:.2s}
.start-btn:hover{transform:translateY(-2px)}

.app{max-width:1000px;margin:auto;min-height:100dvh;display:grid;grid-template-columns:220px 1fr}.sidebar{border-right:1px solid var(--line);padding:24px 16px;display:flex;flex-direction:column;gap:20px;background:#fff8fa}.brand{font-size:20px;font-weight:900;color:var(--pink);padding:0 6px}.profile{background:var(--panel);border:1px solid var(--line);border-radius:16px;padding:12px;box-shadow:0 4px 10px rgba(255,107,139,0.05)}.profile strong{display:block;font-size:14px;color:var(--ink)}.profile small{color:var(--muted);font-size:11px}.nav{display:grid;gap:6px}.nav button{border:0;background:transparent;color:var(--muted);text-align:left;padding:11px 14px;border-radius:12px;font-size:13px;font-weight:bold}.nav button.active,.nav button:hover{background:var(--panel2);color:var(--pink)}.main{min-width:0;padding:24px clamp(14px,3vw,32px) 36px}.topline{display:flex;justify-content:space-between;align-items:center;gap:10px;margin-bottom:20px}h1{font-size:24px;font-weight:900;margin:0;color:var(--ink)}.balance{border:2px solid var(--line);border-radius:14px;padding:8px 14px;text-align:right;background:var(--panel);box-shadow:0 4px 10px rgba(255,107,139,0.05)}.balance small{display:block;color:var(--muted);font-size:10px;font-weight:bold}.balance strong{font-size:18px;color:var(--pink)}.stats{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:10px;margin:18px 0}.stat{background:var(--panel);border:1px solid var(--line);border-radius:14px;padding:12px;box-shadow:0 4px 10px rgba(255,107,139,0.05)}.stat label{display:block;color:var(--muted);font-size:11px;margin-bottom:4px;font-weight:bold}.stat strong{font-size:18px;font-weight:900;color:var(--ink)}.stat small{font-size:10px;color:var(--muted);display:block;margin-top:2px}.layout{display:grid;grid-template-columns:minmax(0,1.3fr) minmax(220px,.8fr);gap:16px}.card{background:var(--panel);border:1px solid var(--line);border-radius:18px;padding:18px;margin-bottom:14px;min-width:0;box-shadow:0 4px 12px rgba(255,107,139,0.05)}.card-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:12px}.card h2{font-size:15px;font-weight:800;margin:0;color:var(--ink)}.story{background:linear-gradient(135deg,#fff0f5,#ffe4e9);border-color:var(--line)}.story .scene{color:var(--pink);font-size:11px;font-weight:bold;margin-bottom:6px}.story h2{font-size:18px;margin-bottom:6px;color:var(--ink)}.story p{font-size:13px;color:var(--muted);margin:0 0 12px}.actions{display:grid;gap:8px}.action{display:flex;align-items:center;gap:12px;text-align:left;background:var(--panel);border:2px solid var(--line);border-radius:14px;color:var(--ink);padding:12px;width:100%;transition:.15s}.action:hover{border-color:var(--pink);background:#fff5f8;transform:translateY(-1px)}.action .symbol{width:34px;height:34px;flex:none;border-radius:10px;background:var(--panel2);display:grid;place-items:center;color:var(--pink);font-size:16px}.action .copy{flex:1;min-width:0}.action strong{display:block;font-size:13px;font-weight:700;color:var(--ink)}.action small{display:block;font-size:11px;color:var(--muted)}.action .gain{font-size:11px;color:var(--green);font-weight:bold;white-space:nowrap}.feed{display:grid;gap:10px}.event{display:grid;grid-template-columns:28px 1fr;gap:8px}.event .dot{width:28px;height:28px;border-radius:8px;background:var(--panel2);display:grid;place-items:center;color:var(--pink);font-size:12px;font-weight:bold}.event strong{font-size:12px;display:block;color:var(--ink)}.event p{font-size:11px;color:var(--muted);margin:2px 0 0}.barrow{display:flex;justify-content:space-between;font-size:11px;color:var(--muted);margin:10px 0 4px;font-weight:bold}.bar{height:7px;background:var(--panel2);border-radius:10px;overflow:hidden}.bar i{display:block;height:100%;background:var(--pink);border-radius:10px;transition:width .25s}.bar.green i{background:var(--green)}.bar.gold i{background:var(--gold)}.section{display:none}.section.active{display:block}.choice-list{display:grid;gap:10px}.choice{padding:14px;border-radius:14px;border:1px solid var(--line);background:var(--panel)}.choice p{font-size:12px;color:var(--muted);margin:4px 0 10px}.choice strong{font-size:13px;color:var(--ink)}.btn{border:none;background:linear-gradient(135deg,var(--pink),#ff4770);color:white;border-radius:10px;padding:9px 14px;font-size:12px;font-weight:bold;box-shadow:0 4px 10px rgba(255,107,139,0.2)}.btn:hover{opacity:.9}.btn.secondary{background:transparent;border:1px solid var(--line);color:var(--muted);box-shadow:none}.btn:disabled{opacity:.4;cursor:not-allowed}.chips{display:flex;flex-wrap:wrap;gap:6px}.chip{background:var(--panel);border:1px solid var(--line);border-radius:8px;padding:4px 10px;color:var(--pink);font-size:11px;font-weight:bold}.log{display:grid;gap:0}.log-item{padding:10px 0;border-bottom:1px solid var(--line);display:grid;grid-template-columns:65px 1fr;gap:10px}.log-item:last-child{border-bottom:0}.log-item time{color:var(--pink);font-size:10px;font-weight:bold}.log-item p{margin:0;font-size:12px;color:var(--ink)}.toast{position:fixed;bottom:20px;left:50%;transform:translate(-50%,20px);background:var(--ink);color:white;padding:12px 20px;border-radius:14px;font-size:12px;font-weight:bold;opacity:0;pointer-events:none;transition:.2s;box-shadow:0 8px 20px rgba(0,0,0,0.15);max-width:90vw;z-index:5}.toast.show{opacity:1;transform:translate(-50%,0)}.footer-actions{display:flex;gap:8px;flex-wrap:wrap;margin-top:12px}.mobile-nav{display:none}

.inventory{display:grid;grid-template-columns:repeat(auto-fill,minmax(80px,1fr));gap:10px;margin-top:10px}
.item-card{background:var(--panel2);border:1px solid var(--line);border-radius:12px;padding:8px;text-align:center;font-size:11px;font-weight:bold;color:var(--ink)}
.item-card span{display:block;font-size:20px;margin-bottom:4px}

@media(max-width:760px){.app{display:block;padding-bottom:70px}.sidebar{display:none}.main{padding:16px 12px 24px}.stats{grid-template-columns:repeat(2,minmax(0,1fr));gap:8px}.layout{grid-template-columns:1fr;gap:0}.card{padding:14px}.mobile-nav{display:grid;position:fixed;z-index:4;bottom:0;left:0;right:0;grid-template-columns:repeat(5,1fr);background:rgba(255,255,255,0.95);border-top:1px solid var(--line);padding:6px 4px calc(6px + env(safe-area-inset-bottom));backdrop-filter:blur(12px)}.mobile-nav button{border:0;background:transparent;color:var(--muted);font-size:10px;padding:4px 0;display:grid;gap:2px;justify-items:center;font-weight:bold}.mobile-nav button span{font-size:16px}.mobile-nav button.active{color:var(--pink)}}
</style>
</head>
<body>

<!-- スタート画面 -->
<div id="start-screen">
 <div class="start-card">
  <h1>AFTER THE ENCORE</h1>
  <div class="input-group">
   <label>プレイヤー名</label>
   <input type="text" id="playerNameInput" placeholder="名前を入力">
  </div>
  <button class="start-btn" onclick="startGame()">START</button>
 </div>
</div>

<div class="app">
<aside class="sidebar">
 <div class="brand">AFTER THE ENCORE</div>
 <div class="profile"><strong id="sideName">プレイヤー</strong><small>地下アイドル事務所スタッフ</small></div>
 <nav class="nav" id="nav"><button class="active" data-page="home">⌂ 生活</button><button data-page="work">▤ 仕事</button><button data-page="oshi">♡ 推し活</button><button data-page="shop">🛍️ ショップ</button><button data-page="social">◎ 界隈</button><button data-page="history">≡ ログ</button></nav>
 <div class="side-note">DAY <span id="sideDay">1</span></div>
</aside>
<main class="main">
 <div class="topline"><div><h1 id="pageTitle">生活</h1></div><div class="balance"><small>所持金</small><strong id="moneyTop">¥28,000</strong></div></div>
 <div class="stats">
  <div class="stat"><label>所持金</label><strong id="moneyStat">¥28,000</strong><small id="moneyHint">給料日まで 6日</small></div>
  <div class="stat"><label>推し活満足度</label><strong id="oshiStat">42<span style="font-size:11px;color:var(--muted)">/100</span></strong></div>
  <div class="stat"><label>信用</label><strong id="trustStat">65<span style="font-size:11px;color:var(--muted)">/100</span></strong></div>
  <div class="stat"><label>体力</label><strong id="energyStat">78<span style="font-size:11px;color:var(--muted)">/100</span></strong></div>
 </div>
 <section class="section active" id="page-home">
  <div class="layout"><div class="left-col">
   <div class="card story"><div class="scene" id="sceneLabel">DAY 1</div><h2 id="storyTitle">新しい職場、いつもの推し</h2><p id="storyText">地下アイドル事務所「Lumen Works」で働き始めて一週間。仕事と推し活の毎日はここから。</p><div class="chips"><span class="chip" id="dayChip">DAY 1</span></div></div>
   <div class="card"><div class="card-head"><h2>行動選択</h2></div><div class="actions">
    <button class="action" onclick="act('work')"><span class="symbol">▤</span><span class="copy"><strong>事務所で仕事をする</strong><small>仕事の評価を上げる</small></span><span class="gain">+評価</span></button>
    <button class="action" onclick="act('oshi')"><span class="symbol">♡</span><span class="copy"><strong>推しの情報を追う</strong><small>公式SNSやイベントをチェック</small></span><span class="gain">+満足度</span></button>
    <button class="action" onclick="act('rest')"><span class="symbol">☾</span><span class="copy"><strong>家で休む</strong><small>体力を回復する</small></span><span class="gain">+体力</span></button>
    <button class="action" onclick="act('scroll')"><span class="symbol">◎</span><span class="copy"><strong>SNSを眺める</strong><small>界隈の動きを見る</small></span></button>
   </div></div>
   <div class="card"><div class="card-head"><h2>所持グッズ</h2></div><div class="inventory" id="itemInventory"><p style="font-size:12px;color:var(--muted);margin:0">まだグッズを持っていません</p></div></div>
   <div class="card"><div class="card-head"><h2>最近の出来事</h2><button class="btn secondary" onclick="showPage('history')">ログ一覧</button></div><div class="feed" id="recentFeed"></div></div>
  </div><div class="right-col">
   <div class="card"><div class="card-head"><h2>ステータス</h2></div>
    <div class="barrow"><span>仕事の評価</span><b id="workNum">28 / 100</b></div><div class="bar"><i id="workBar" style="width:28%"></i></div>
    <div class="barrow"><span>推し活満足度</span><b id="oshiNum">42 / 100</b></div><div class="bar"><i id="oshiBar" style="width:42%"></i></div>
    <div class="barrow"><span>評判</span><b id="repNum">55 / 100</b></div><div class="bar green"><i id="repBar" style="width:55%"></i></div>
    <div class="barrow"><span>火種</span><b id="heatNum">8 / 100</b></div><div class="bar gold"><i id="heatBar" style="width:8%"></i></div>
   </div>
   <div class="card"><div class="card-head"><h2>予定</h2></div><div class="event"><div class="dot">♪</div><div><strong>金曜 · 給料日</strong><p>給料が入る日</p></div></div></div>
  </div></div>
 </section>
 <section class="section" id="page-work"><div class="layout"><div><div class="card"><div class="card-head"><h2>仕事</h2></div><div class="choice-list">
  <div class="choice"><strong>公式SNSの告知を作る</strong><p>ライブ情報を整理して投稿する。</p><button class="btn" onclick="act('announce')">告知作成 (-8体力)</button></div>
  <div class="choice"><strong>ライブ現場の準備を手伝う</strong><p>物販リストや現場の確認。</p><button class="btn" onclick="act('venue')">現場準備 (-14体力)</button></div>
  <div class="choice"><strong>メンバーの相談を聞く</strong><p>話を聞く時間を取る。</p><button class="btn" onclick="act('listen')">相談を聞く (-10体力)</button></div>
  <div class="choice"><strong>残業して売上資料を仕上げる</strong><p>資料を完成させる。</p><button class="btn" onclick="act('overtime')">残業 (-20体力)</button></div>
 </div></div></div><div><div class="card"><h2>仕事の状況</h2><div class="barrow"><span>仕事の評価</span><b id="workNum2">28 / 100</b></div><div class="bar"><i id="workBar2" style="width:28%"></i></div></div></div></div></section>
 <section class="section" id="page-oshi"><div class="layout"><div><div class="card"><div class="card-head"><h2>推し活</h2></div><div class="choice-list">
  <div class="choice"><strong>公式情報をチェックする</strong><p>出演情報やリリースを読む。</p><button class="btn" onclick="act('official')">チェックする</button></div>
  <div class="choice"><strong>CDを1枚買う</strong><p>グッズ・作品の購入。</p><button class="btn" onclick="act('cd')">CD購入 (¥1,800)</button></div>
  <div class="choice"><strong>イベントに参加する</strong><p>現場に行く。</p><button class="btn" onclick="act('event')">イベント参加 (¥3,500)</button></div>
  <div class="choice"><strong>お金を貯める</strong><p>今日は使わない。</p><button class="btn" onclick="act('save')">使わない</button></div>
 </div></div></div><div><div class="card"><h2>満足度</h2><div class="barrow"><span>満足度</span><b id="oshiNum2">42 / 100</b></div><div class="bar"><i id="oshiBar2" style="width:42%"></i></div></div></div></div></section>

 <section class="section" id="page-shop"><div class="layout"><div><div class="card"><div class="card-head"><h2>オフィシャルショップ</h2></div><div class="choice-list">
  <div class="choice"><strong>ランダムチェキ</strong><p>何が出るかはお楽しみ！推しのチェキ。</p><button class="btn" onclick="buyItem('チェキ', '📸', 1000, 5)">購入 (¥1,000)</button></div>
  <div class="choice"><strong>アクリルスタンド</strong><p>部屋に飾りたい定番グッズ。</p><button class="btn" onclick="buyItem('アクスタ', '🧍', 2200, 10)">購入 (¥2,200)</button></div>
  <div class="choice"><strong>公式ペンライト</strong><p>ライブの必須アイテム！綺麗に光る。</p><button class="btn" onclick="buyItem('ペンライト', '🪄', 3500, 15)">購入 (¥3,500)</button></div>
  <div class="choice"><strong>限定キーホルダー</strong><p>バッグにつけたいかわいいアクキー。</p><button class="btn" onclick="buyItem('アクキー', '🔑', 1500, 8)">購入 (¥1,500)</button></div>
 </div></div></div><div><div class="card"><h2>お買い物メモ</h2><p style="font-size:12px;color:var(--muted)">グッズを買うと満足度がアップして、ホーム画面にコレクションされるよ！</p></div></div></div></section>

 <section class="section" id="page-social"><div class="layout"><div><div class="card"><div class="card-head"><h2>界隈</h2></div><div class="choice-list">
  <div class="choice"><strong>投稿を眺める</strong><p>現場の感想などをチェック。</p><button class="btn" onclick="act('timeline')">タイムラインを見る</button></div>
  <div class="choice"><strong>チケットの譲渡相談</strong><p>条件確認。</p><button class="btn" onclick="act('ticketSafe')">公式ルール確認</button> <button class="btn secondary" onclick="act('ticketRisk')">そのまま進める</button></div>
  <div class="choice"><strong>撮影ルールの違反を見かけた</strong><p>対応を選ぶ。</p><button class="btn" onclick="act('photoSafe')">ルール確認</button> <button class="btn secondary" onclick="act('photoRisk')">そのまま拡散</button></div>
  <div class="choice"><strong>噂話を聞いた</strong><p>扱いを選ぶ。</p><button class="btn" onclick="act('secretSafe')">流さない</button> <button class="btn secondary" onclick="act('secretRisk')">広める</button></div>
 </div></div></div><div><div class="card"><h2>コンディション</h2><div class="barrow"><span>評判</span><b id="repNum2">55 / 100</b></div><div class="bar green"><i id="repBar2" style="width:55%"></i></div><div class="barrow"><span>火種</span><b id="heatNum2">8 / 100</b></div><div class="bar gold"><i id="heatBar2" style="width:8%"></i></div></div></div></div></section>
 <section class="section" id="page-history"><div class="card"><div class="card-head"><h2>行動ログ</h2></div><div class="log" id="logList"></div><div class="footer-actions"><button class="btn secondary" onclick="saveGame(true)">セーブ</button><button class="btn secondary" onclick="resetGame()">最初からやり直す</button></div></div></section>
 <div class="mobile-nav" id="mobileNav"><button class="active" data-page="home"><span>⌂</span>生活</button><button data-page="work"><span>▤</span>仕事</button><button data-page="oshi"><span>♡</span>推し活</button><button data-page="shop"><span>🛍️</span>ショップ</button><button data-page="social"><span>◎</span>界隈</button></div>
</main></div><div class="toast" id="toast"></div>
<script>
var initial={name:'',day:1,turns:0,money:28000,oshi:42,trust:65,energy:78,work:28,rep:55,heat:8,items:[],logs:[{day:1,time:'09:10',text:'仕事が始まった。'}],events:[]};
var s=loadGame()||JSON.parse(JSON.stringify(initial));
var current='home';
function $(id){return document.getElementById(id);}
function clamp(n){return Math.max(0,Math.min(100,Math.round(n)));}
function yen(n){return '¥'+Math.round(n).toLocaleString('ja-JP');}
function loadGame(){try{return JSON.parse(localStorage.getItem('afterEncoreSave'))}catch(e){return null}}
function saveGame(show){try{localStorage.setItem('afterEncoreSave',JSON.stringify(s));if(show)toast('セーブしました')}catch(e){if(show)toast('セーブ失敗')}}

function startGame(){
 var inputVal=$('playerNameInput').value.trim();
 s.name=inputVal || 'プレイヤー';
 $('start-screen').style.display='none';
 saveGame();
 render();
}

function buyItem(name, icon, price, oshiGain){
 if(!spend(price))return;
 s.oshi=clamp(s.oshi+oshiGain);
 if(!s.items)s.items=[];
 s.items.push({name:name, icon:icon});
 log(name+' を購入した！');
 render();
 saveGame();
 toast(name+' をゲット！');
}

function log(text){s.logs.unshift({day:s.day,time:new Date().toLocaleTimeString('ja-JP',{hour:'2-digit',minute:'2-digit'}),text:text});s.logs=s.logs.slice(0,80);s.events.unshift(text);s.events=s.events.slice(0,3)}
function toast(t){var el=$('toast');el.textContent=t;el.classList.add('show');clearTimeout(window.toastTimer);window.toastTimer=setTimeout(function(){el.classList.remove('show')},2200)}
function spend(amount){if(s.money<amount){toast('お金が足りないよ');return false}s.money-=amount;return true}
function tired(n){if(s.energy<n){toast('体力が足りないよ');return false}s.energy-=n;return true}
function act(type){
 var msg='';
 switch(type){
  case'work':if(!tired(12))return;s.work=clamp(s.work+5);s.trust=clamp(s.trust+2);msg='事務所で告知作成と資料整理を進めた。';break;
  case'oshi':s.oshi=clamp(s.oshi+5);s.energy=clamp(s.energy-4);msg='推しの公式投稿をチェックした。';break;
  case'rest':s.energy=clamp(s.energy+22);msg='家でゆっくり休んだ。';break;
  case'scroll':if(Math.random()<0.5){s.rep=clamp(s.rep+2);msg='タイムラインでファンの感想を見た。'}else{s.energy=clamp(s.energy-5);s.heat=clamp(s.heat+2);msg='タイムラインの議論に時間を取られた。';}break;
  case'announce':if(!tired(8))return;s.work=clamp(s.work+8);s.trust=clamp(s.trust+3);msg='公式告知を丁寧に仕上げた。';break;
  case'venue':if(!tired(14))return;s.work=clamp(s.work+10);s.trust=clamp(s.trust+4);msg='現場準備を完了した。';break;
  case'listen':if(!tired(10))return;s.trust=clamp(s.trust+7);s.work=clamp(s.work+3);msg='メンバーの相談に乗った。';break;
  case'overtime':if(!tired(20))return;s.work=clamp(s.work+12);s.money+=1200;s.energy=clamp(s.energy-4);msg='残業で資料を終わらせた。';break;
  case'official':s.oshi=clamp(s.oshi+4);msg='公式情報をチェックした。';break;
  case'cd':if(!spend(1800))return;s.oshi=clamp(s.oshi+9);msg='CDを1枚購入した。';break;
  case'event':if(!spend(3500))return;if(!tired(12)){s.money+=3500;return}s.oshi=clamp(s.oshi+15);s.rep=clamp(s.rep+2);msg='イベントに参加した。';break;
  case'save':s.trust=clamp(s.trust+1);msg='お金を使わずに残した。';break;
  case'timeline':if(Math.random()<0.5){s.rep=clamp(s.rep+3);msg='タイムラインをチェックした。'}else{s.energy=clamp(s.energy-4);msg='議論を見て少し疲れた。';}break;
  case'ticketSafe':s.rep=clamp(s.rep+3);s.trust=clamp(s.trust+1);msg='チケットの公式規約を確認した。';break;
  case'ticketRisk':s.heat=clamp(s.heat+12);s.rep=clamp(s.rep-5);s.oshi=clamp(s.oshi+3);msg='曖昧なまま譲渡を進めた。';break;
  case'photoSafe':s.rep=clamp(s.rep+2);msg='イベントの撮影ルールを確認した。';break;
  case'photoRisk':s.heat=clamp(s.heat+10);s.rep=clamp(s.rep-6);msg='ルール不透明なまま拡散した。';break;
  case'secretSafe':s.trust=clamp(s.trust+2);s.rep=clamp(s.rep+2);msg='噂話は流さずに留めた。';break;
  case'secretRisk':s.heat=clamp(s.heat+16);s.rep=clamp(s.rep-8);msg='聞いた話を界隈に流した。';break;
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
  if(s.energy<=10){
   s.energy=clamp(s.energy+30);
   s.money=Math.max(0,s.money-600);
   log('疲れて早く休んだ。');
  }else{
   s.energy=clamp(s.energy+6);
   log('一日が終わった。');
  }
  if(s.day%7===0){
   s.money+=18000;
   s.energy=clamp(s.energy+8);
   s.trust=clamp(s.trust+1);
   log('給料日！¥18,000 が入った。');
  }
 }
}
function showPage(page){
 current=page;
 var secs=document.querySelectorAll('.section');
 for(var i=0;i<secs.length;i++){secs[i].classList.toggle('active',secs[i].id==='page-'+page);}
 var btns=document.querySelectorAll('[data-page]');
 for(var j=0;j<btns.length;j++){btns[j].classList.toggle('active',btns[j].dataset.page===page);}
 var titles={home:'生活',work:'仕事',oshi:'推し活',shop:'ショップ',social:'界隈',history:'ログ'};
 $('pageTitle').textContent=titles[page];
}
var navBtns=document.querySelectorAll('[data-page]');
for(var k=0;k<navBtns.length;k++){
 (function(b){
  b.addEventListener('click',function(){showPage(b.dataset.page);});
 })(navBtns[k]);
}
function render(){
 $('moneyTop').textContent=yen(s.money);
 $('moneyStat').textContent=yen(s.money);
 var remDays=7-(s.day%7);
 if(remDays===7)remDays=0;
 $('moneyHint').textContent='給料日まで '+remDays+'日';
 $('oshiStat').innerHTML=s.oshi+'<span style="font-size:11px;color:var(--muted)">/100</span>';
 $('trustStat').innerHTML=s.trust+'<span style="font-size:11px;color:var(--muted)">/100</span>';
 $('energyStat').innerHTML=s.energy+'<span style="font-size:11px;color:var(--muted)">/100</span>';
 $('sideDay').textContent=s.day;
 $('dayChip').textContent='DAY '+s.day;
 $('workNum').textContent=s.work+' / 100';
 $('workNum2').textContent=s.work+' / 100';
 $('oshiNum').textContent=s.oshi+' / 100';
 $('oshiNum2').textContent=s.oshi+' / 100';
 $('repNum').textContent=s.rep+' / 100';
 $('repNum2').textContent=s.rep+' / 100';
 $('heatNum').textContent=s.heat+' / 100';
 $('heatNum2').textContent=s.heat+' / 100';
 var bars=[['workBar',s.work],['workBar2',s.work],['oshiBar',s.oshi],['oshiBar2',s.oshi],['repBar',s.rep],['repBar2',s.rep],['heatBar',s.heat],['heatBar2',s.heat]];
 for(var m=0;m<bars.length;m++){$(bars[m][0]).style.width=bars[m][1]+'%';}
 var recent=s.logs.slice(0,3);
 var html1='';
 for(var n=0;n<recent.length;n++){
  html1+='<div class="event"><div class="dot">'+(n===0?'✦':'·')+'</div><div><strong>DAY '+recent[n].day+' · '+recent[n].time+'</strong><p>'+esc(recent[n].text)+'</p></div></div>';
 }
 $('recentFeed').innerHTML=html1;
 var html2='';
 for(var p=0;p<s.logs.length;p++){
  html2+='<div class="log-item"><time>DAY '+s.logs[p].day+'<br>'+s.logs[p].time+'</time><p>'+esc(s.logs[p].text)+'</p></div>';
 }
 $('logList').innerHTML=html2;

 if(s.items && s.items.length > 0){
  var itemHtml='';
  for(var q=0;q<s.items.length;q++){
   itemHtml+='<div class="item-card"><span>'+s.items[q].icon+'</span>'+esc(s.items[q].name)+'</div>';
  }
  $('itemInventory').innerHTML=itemHtml;
 }else{
  $('itemInventory').innerHTML='<p style="font-size:12px;color:var(--muted);margin:0">まだグッズを持っていません</p>';
 }

 $('sideName').textContent=(s.name||'プレイヤー');
}
function esc(str){return String(str).replace(/[&<>"']/g,function(c){return {'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]})}
function resetGame(){if(confirm('最初からやり直しますか？')){s=JSON.parse(JSON.stringify(initial));saveGame();location.reload();}}
if(s.name){$('start-screen').style.display='none';}
render();
</script>
</body></html>
