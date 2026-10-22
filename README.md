<!doctype html>
<html lang="ja">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no,viewport-fit=cover">
<meta name="theme-color" content="#f7f6f3">
<title>AFTER THE ENCORE</title>
<style>
:root{--bg:#f7f6f3;--card:#ffffff;--text:#2b2b2b;--sub:#767676;--line:#e5e3de;--accent:#c9708f;--accent-hover:#b55d7d;--tint:#faf9f6}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent;touch-action:manipulation}
body{margin:0;background:var(--bg);color:var(--text);font-family:-apple-system,BlinkMacSystemFont,"Hiragino Sans","Yu Gothic",sans-serif;line-height:1.7;letter-spacing:0.02em;user-select:none;-webkit-user-select:none}
button{font:inherit;cursor:pointer;border:none;outline:none}

/* スタート画面 */
#start-screen{position:fixed;top:0;left:0;width:100%;height:100%;background:var(--bg);z-index:100;display:flex;justify-content:center;align-items:center;padding:24px}
.start-card{background:var(--card);padding:48px 32px;border-radius:12px;border:1px solid var(--line);max-width:380px;width:100%;text-align:center}
.start-card h1{font-size:20px;font-weight:400;letter-spacing:0.15em;margin:0 0 8px;color:var(--text)}
.start-card p{font-size:12px;color:var(--sub);margin:0 0 32px}
.start-input{width:100%;padding:12px 16px;border:1px solid var(--line);border-radius:6px;font-size:14px;outline:none;text-align:center;color:var(--text);background:var(--tint);margin-bottom:20px}
.start-input:focus{border-color:var(--accent)}
.start-btn{width:100%;padding:13px;background:var(--text);color:white;border-radius:6px;font-size:13px;letter-spacing:0.1em;transition:background 0.2s}
.start-btn:hover{background:var(--accent)}

/* アプリ全体 */
.app{max-width:640px;margin:0 auto;min-height:100dvh;display:flex;flex-direction:column;padding-bottom:70px}

/* ヘッダー */
header{padding:24px 24px 16px;display:flex;justify-content:space-between;align-items:baseline;border-bottom:1px solid var(--line);background:var(--card)}
.brand{font-size:11px;letter-spacing:0.15em;color:var(--sub);font-weight:600}
.user-status{font-size:13px;color:var(--text);font-weight:500}

/* ステータスバー */
.stats-bar{display:grid;grid-template-columns:repeat(4,1fr);background:var(--card);border-bottom:1px solid var(--line);padding:14px 24px;text-align:center}
.stat-item span{display:block;font-size:10px;color:var(--sub);letter-spacing:0.05em;margin-bottom:2px}
.stat-item strong{font-size:14px;font-weight:500;color:var(--text)}

/* メインエリア */
.container{padding:32px 24px;flex:1}
.section{display:none}.section.active{display:block}

/* シーン・ストーリーカード */
.story-box{background:var(--card);border:1px solid var(--line);border-radius:8px;padding:24px;margin-bottom:24px}
.story-meta{font-size:11px;letter-spacing:0.1em;color:var(--accent);margin-bottom:8px;font-weight:600}
.story-title{font-size:16px;font-weight:500;margin:0 0 12px;color:var(--text)}
.story-text{font-size:13px;color:var(--sub);margin:0}

/* アクションリスト */
.action-list{display:grid;gap:10px}
.action-row{background:var(--card);border:1px solid var(--line);border-radius:8px;padding:16px 20px;display:flex;justify-content:space-between;align-items:center;text-align:left;width:100%;transition:all 0.2s}
.action-row:hover{border-color:var(--accent);background:var(--tint)}
.action-row strong{display:block;font-size:13px;font-weight:500;color:var(--text);margin-bottom:2px}
.action-row small{font-size:11px;color:var(--sub)}
.action-tag{font-size:11px;color:var(--accent);font-weight:500}

/* グッズコレクション */
.collection-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(90px,1fr));gap:10px}
.collection-card{background:var(--card);border:1px solid var(--line);border-radius:6px;padding:14px 10px;text-align:center;font-size:11px;color:var(--sub)}
.collection-card span{font-size:20px;display:block;margin-bottom:6px}

/* ボトムナビゲーション */
.nav-bar{position:fixed;bottom:0;left:50%;transform:translateX(-50%);width:100%;max-width:640px;background:var(--card);border-top:1px solid var(--line);display:grid;grid-template-columns:repeat(5,1fr);padding:10px 0 calc(10px + env(safe-area-inset-bottom));z-index:20}
.nav-item{background:transparent;color:var(--sub);font-size:10px;letter-spacing:0.05em;display:flex;flex-direction:column;align-items:center;gap:4px;transition:color 0.2s}
.nav-item.active{color:var(--accent)}
.nav-item span{font-size:16px}

/* ログ */
.log-stream{display:grid;gap:8px}
.log-entry{background:var(--card);border:1px solid var(--line);border-radius:6px;padding:12px 16px;font-size:12px}
.log-time{font-size:10px;color:var(--sub);margin-bottom:2px;display:block}

/* トースト */
.toast{position:fixed;top:24px;left:50%;transform:translateX(-50%) translateY(-20px);background:var(--text);color:white;padding:10px 20px;border-radius:4px;font-size:12px;opacity:0;pointer-events:none;transition:all 0.2s;z-index:100}
.toast.show{opacity:1;transform:translateX(-50%) translateY(0)}
</style>
</head>
<body>

<!-- スタート画面 -->
<div id="start-screen">
 <div class="start-card">
  <h1>AFTER THE ENCORE</h1>
  <p>推し活と、生活の記録</p>
  <input type="text" id="playerNameInput" class="start-input" placeholder="名前を入力">
  <button class="start-btn" onclick="startGame()">はじめる</button>
 </div>
</div>

<div class="app">
 <header>
  <div class="brand">AFTER THE ENCORE</div>
  <div class="user-status"><span id="sideName">プレイヤー</span> / 残高 <strong id="moneyTop" style="color:var(--text);font-weight:500">¥28,000</strong></div>
 </header>

 <div class="stats-bar">
  <div class="stat-item"><span>満足度</span><strong id="oshiStat">42</strong></div>
  <div class="stat-item"><span>信用度</span><strong id="trustStat">65</strong></div>
  <div class="stat-item"><span>体力</span><strong id="energyStat">78</strong></div>
  <div class="stat-item"><span>給料日</span><strong id="dayHint">あと6日</strong></div>
 </div>

 <div class="container">
  <!-- ホーム -->
  <section class="section active" id="page-home">
   <div class="story-box">
    <div class="story-meta">DAY <span id="sideDay">1</span></div>
    <h2 class="story-title" id="storyTitle">新しい職場、いつもの推し</h2>
    <p class="story-text" id="storyText">地下アイドル事務所「Lumen Works」での日々が始まる。仕事と推し活のバランスを取りながら、自分の歩幅で進んでいく。</p>
   </div>

   <div style="margin-bottom:12px;font-size:12px;color:var(--sub);letter-spacing:0.05em">今日の行動</div>
   <div class="action-list">
    <button class="action-row" onclick="act('work')"><div><strong>事務所で仕事をする</strong><small>業務をこなし、評価を高める</small></div><span class="action-tag">+仕事</span></button>
    <button class="action-row" onclick="act('oshi')"><div><strong>推しの情報を追う</strong><small>SNSや最新のリリースをチェック</small></div><span class="action-tag">+満足</span></button>
    <button class="action-row" onclick="act('rest')"><div><strong>家で休息を取る</strong><small>すり減った体力を回復する</small></div><span class="action-tag">+体力</span></button>
    <button class="action-row" onclick="act('scroll')"><div><strong>SNSのタイムラインを見る</strong><small>界隈の空気を眺める</small></div><span class="action-tag">?</span></button>
   </div>

   <div style="margin:28px 0 12px;font-size:12px;color:var(--sub);letter-spacing:0.05em">コレクション</div>
   <div class="collection-grid" id="itemInventory">
    <div style="font-size:12px;color:var(--sub);grid-column:1/-1;padding:12px 0">まだ何も持っていません</div>
   </div>
  </section>

  <!-- 仕事 -->
  <section class="section" id="page-work">
   <div style="margin-bottom:12px;font-size:12px;color:var(--sub)">業務メニュー</div>
   <div class="action-list">
    <button class="action-row" onclick="act('announce')"><div><strong>公式告知の作成</strong><small>ファンに伝わる文章を整える (-8体力)</small></div></button>
    <button class="action-row" onclick="act('venue')"><div><strong>ライブ現場の準備</strong><small>物販や導線の最終確認 (-14体力)</small></div></button>
    <button class="action-row" onclick="act('listen')"><div><strong>メンバーの相談に乗る</strong><small>コンディションに耳を傾ける (-10体力)</small></div></button>
   </div>
  </section>

  <!-- 推し活 -->
  <section class="section" id="page-oshi">
   <div style="margin-bottom:12px;font-size:12px;color:var(--sub)">推し活メニュー</div>
   <div class="action-list">
    <button class="action-row" onclick="act('official')"><div><strong>公式情報を確認する</strong><small>スケジュール帳に書き込む (無料)</small></div></button>
    <button class="action-row" onclick="act('cd')"><div><strong>CDを1枚購入する</strong><small>手元に残る形としての幸せ (¥1,800)</small></div></button>
    <button class="action-row" onclick="act('event')"><div><strong>イベントに参加する</strong><small>限られた時間を共にする (¥3,500)</small></div></button>
   </div>
  </section>

  <!-- ショップ -->
  <section class="section" id="page-shop">
   <div style="margin-bottom:12px;font-size:12px;color:var(--sub)">オフィシャルグッズ</div>
   <div class="action-list">
    <button class="action-row" onclick="buyItem('チェキ', '📷', 1000, 5)"><div><strong>ランダムチェキ</strong><small>何が届くかはお楽しみ</small></div><span class="action-tag">¥1,000</span></button>
    <button class="action-row" onclick="buyItem('アクスタ', '🧍', 2200, 10)"><div><strong>アクリルスタンド</strong><small>デスクに飾る定番アイテム</small></div><span class="action-tag">¥2,200</span></button>
    <button class="action-row" onclick="buyItem('ペンライト', '🪄', 3500, 15)"><div><strong>公式ペンライト</strong><small>会場を染める光</small></div><span class="action-tag">¥3,500</span></button>
   </div>
  </section>

  <!-- ログ -->
  <section class="section" id="page-history">
   <div style="margin-bottom:12px;font-size:12px;color:var(--sub)">これまでの記録</div>
   <div class="log-stream" id="logList"></div>
   <div style="margin-top:24px">
    <button class="action-row" style="justify-content:center;color:#b23b3b" onclick="resetGame()">データをはじめからに戻す</button>
   </div>
  </section>
 </div>

 <nav class="nav-bar">
  <button class="nav-item active" data-page="home"><span>⚪︎</span>ホーム</button>
  <button class="nav-item" data-page="work"><span>■</span>仕事</button>
  <button class="nav-item" data-page="oshi"><span>♡</span>推し活</button>
  <button class="nav-item" data-page="shop"><span>◇</span>ショップ</button>
  <button class="nav-item" data-page="history"><span>≡</span>記録</button>
 </nav>
</div>

<div class="toast" id="toast"></div>

<script>
var initial={name:'',day:1,turns:0,money:28000,oshi:42,trust:65,energy:78,work:28,items:[],logs:[{day:1,time:'09:10',text:'物語が始まった。'}]};
var s=loadGame()||JSON.parse(JSON.stringify(initial));

function $(id){return document.getElementById(id);}
function clamp(n){return Math.max(0,Math.min(100,Math.round(n)));}
function yen(n){return '¥'+Math.round(n).toLocaleString('ja-JP');}
function loadGame(){try{return JSON.parse(localStorage.getItem('afterEncoreSave'))}catch(e){return null}}
function saveGame(){try{localStorage.setItem('afterEncoreSave',JSON.stringify(s))}catch(e){}}

function startGame(){
 var inputVal=$('playerNameInput').value.trim();
 s.name=inputVal || 'プレイヤー';
 $('start-screen').style.display='none';
 saveGame();
 render();
}

function toast(t){var el=$('toast');el.textContent=t;el.classList.add('show');clearTimeout(window.toastTimer);window.toastTimer=setTimeout(function(){el.classList.remove('show')},2000)}
function spend(amount){if(s.money<amount){toast('資金が足りません');return false}s.money-=amount;return true}
function tired(n){if(s.energy<n){toast('体力が限界です。休息を取ってください');return false}s.energy-=n;return true}

function buyItem(name, icon, price, oshiGain){
 if(!spend(price))return;
 s.oshi=clamp(s.oshi+oshiGain);
 if(!s.items)s.items=[];
 s.items.push({name:name, icon:icon});
 log(name+'を手に入れた。');
 render();
 saveGame();
 toast(name+'を購入しました');
}

function act(type){
 var msg='';
 var isLucky = Math.random() < 0.2;

 switch(type){
  case'work':if(!tired(12))return;var g=isLucky?10:5;s.work=clamp(s.work+g);msg=isLucky?'丁寧な仕事ぶりが評価された。':'業務を堅実にこなした。';break;
  case'oshi':var og=isLucky?10:5;s.oshi=clamp(s.oshi+og);s.energy=clamp(s.energy-4);msg=isLucky?'心動かされる瞬間に出会えた。':'推しの気配を感じて心が満たされた。';break;
  case'rest':s.energy=clamp(s.energy+25);msg='静かな部屋でしっかりと休息を取った。';break;
  case'scroll':if(Math.random()<0.5){s.oshi=clamp(s.oshi+3);msg='タイムラインで温かい言葉を見つけた。'}else{s.energy=clamp(s.energy-5);msg='情報の波に飲まれ、少し消耗した。'}break;
  case'announce':if(!tired(8))return;s.work=clamp(s.work+8);msg='公式告知の文章を丁寧に整えた。';break;
  case'venue':if(!tired(14))return;s.work=clamp(s.work+12);msg='ライブの準備を入念に進めた。';break;
  case'listen':if(!tired(10))return;s.trust=clamp(s.trust+8);msg='メンバーの言葉に静かに耳を傾けた。';break;
  case'official':s.oshi=clamp(s.oshi+4);msg='スケジュールの確認を済ませた。';break;
  case'cd':if(!spend(1800))return;s.oshi=clamp(s.oshi+10);msg='届いたパッケージを開封した。';break;
  case'event':if(!spend(3500))return;if(!tired(12)){s.money+=3500;return}s.oshi=clamp(s.oshi+18);msg='忘れられない時間過ごした。';break;
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
 s.logs=s.logs.slice(0,50);
}

function showPage(page){
 var secs=document.querySelectorAll('.section');
 for(var i=0;i<secs.length;i++){secs[i].classList.toggle('active',secs[i].id==='page-'+page);}
 var btns=document.querySelectorAll('.nav-item');
 for(var j=0;j<btns.length;j++){btns[j].classList.toggle('active',btns[j].dataset.page===page);}
}

var navBtns=document.querySelectorAll('.nav-item');
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
 $('dayHint').textContent='あと'+remDays+'日';

 var html='';
 for(var p=0;p<s.logs.length;p++){
  html+='<div class="log-entry"><span class="log-time">DAY '+s.logs[p].day+' / '+s.logs[p].time+'</span>'+s.logs[p].text+'</div>';
 }
 $('logList').innerHTML=html;

 if(s.items && s.items.length>0){
  var itemHtml='';
  for(var q=0;q<s.items.length;q++){
   itemHtml+='<div class="collection-card"><span>'+s.items[q].icon+'</span>'+s.items[q].name+'</div>';
  }
  $('itemInventory').innerHTML=itemHtml;
 }else{
  $('itemInventory').innerHTML='<div style="font-size:12px;color:var(--sub);grid-column:1/-1;padding:12px 0">まだ何も持っていません</div>';
 }
}

function resetGame(){if(confirm('データをリセットしますか？')){s=JSON.parse(JSON.stringify(initial));saveGame();location.reload();}}
if(s.name){$('start-screen').style.display='none';}
render();
</script>
</body>
</html>
