# novel-reader
<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<title>📖</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Noto+Serif+TC:wght@300;400;600&display=swap');
:root {
  --bg:#000; --bg2:#0a0a0f; --card:#111118;
  --gold:#c8a96e; --gold2:#e8d4a8;
  --text:#e0d8cc; --dim:#555; --dim2:#2a2a2a; --red:#c0392b;
}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{width:100%;height:100%;overflow:hidden;background:var(--bg);font-family:'Noto Serif TC',-apple-system,serif;color:var(--text)}
.screen{position:fixed;inset:0;display:flex;flex-direction:column;background:var(--bg);transition:transform .3s cubic-bezier(.4,0,.2,1),opacity .3s;z-index:1}
.screen.hidden{transform:translateX(100%);opacity:0;pointer-events:none}
.screen.behind{transform:translateX(-28%);opacity:0;pointer-events:none}

/* HOME */
#s-home{background:radial-gradient(ellipse at 30% 20%,#1a1408 0%,#000 70%)}
.home-top{padding:18px 16px 0;display:flex;justify-content:space-between;align-items:flex-start}
.home-clock{font-size:36px;font-weight:300;letter-spacing:-1px;color:#fff;line-height:1}
.home-date{font-size:10px;color:var(--dim);margin-top:3px;letter-spacing:1px}
.icon-btn{width:34px;height:34px;border-radius:50%;background:rgba(255,255,255,.06);display:flex;align-items:center;justify-content:center;font-size:15px;cursor:pointer;flex-shrink:0}
.icon-btn:active{background:rgba(200,169,110,.2)}
.divider{height:1px;background:linear-gradient(90deg,transparent,rgba(200,169,110,.25),transparent);margin:14px 16px 10px}
.sec-label{font-size:9px;letter-spacing:3px;color:var(--dim);padding:0 16px;margin-bottom:8px}
.continue-btn{margin:0 12px 12px;background:linear-gradient(135deg,#1c1810,#120f08);border:1px solid rgba(200,169,110,.2);border-radius:20px;padding:14px 16px;display:flex;align-items:center;gap:12px;cursor:pointer;transition:all .15s;min-height:68px}
.continue-btn:active{background:rgba(200,169,110,.1);border-color:rgba(200,169,110,.4);transform:scale(.97)}
.ci{font-size:28px;flex-shrink:0}
.cb{flex:1;min-width:0}
.ct{font-size:14px;font-weight:600;color:var(--text);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.cs{font-size:11px;color:var(--gold);margin-top:3px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.ca{font-size:20px;color:var(--gold);flex-shrink:0}
.home-nav{display:grid;grid-template-columns:1fr 1fr;gap:8px;padding:0 12px;margin-top:auto;margin-bottom:16px}
.nav-btn{background:var(--card);border:1px solid var(--dim2);border-radius:20px;padding:14px 10px;display:flex;flex-direction:column;align-items:center;gap:6px;cursor:pointer;transition:all .15s;min-height:72px;justify-content:center}
.nav-btn:active{background:rgba(200,169,110,.1);border-color:var(--gold);transform:scale(.95)}
.ni{font-size:24px}
.nl{font-size:10px;color:var(--dim);letter-spacing:1px}

/* SHARED HEADER */
.shdr{display:flex;align-items:center;padding:16px 14px 12px;gap:10px;flex-shrink:0}
.back-btn{width:32px;height:32px;border-radius:50%;background:rgba(255,255,255,.06);display:flex;align-items:center;justify-content:center;font-size:18px;cursor:pointer;flex-shrink:0;color:var(--gold)}
.back-btn:active{background:rgba(200,169,110,.2)}
.stitle{font-size:14px;font-weight:600;color:var(--text);letter-spacing:1px;flex:1}
.add-btn{width:32px;height:32px;border-radius:50%;background:var(--gold);display:flex;align-items:center;justify-content:center;font-size:20px;font-weight:300;color:#000;cursor:pointer;flex-shrink:0}
.add-btn:active{background:var(--gold2);transform:scale(.9)}

/* BOOKMARKS */
#s-bm{background:var(--bg2)}
.scroll{flex:1;overflow-y:auto;padding:0 12px 20px;-webkit-overflow-scrolling:touch}
.bm-item{background:var(--card);border:1px solid var(--dim2);border-radius:18px;padding:13px 14px;margin-bottom:8px;display:flex;align-items:center;gap:10px;cursor:pointer;transition:all .15s;min-height:62px}
.bm-item:active{background:rgba(200,169,110,.08);border-color:rgba(200,169,110,.3)}
.bm-bar{width:3px;height:38px;border-radius:3px;background:linear-gradient(180deg,var(--gold),transparent);flex-shrink:0}
.bm-info{flex:1;min-width:0}
.bm-name{font-size:13px;color:var(--text);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;font-weight:500}
.bm-ch{font-size:10px;color:var(--gold);margin-top:3px}
.bm-x{width:26px;height:26px;border-radius:50%;background:rgba(192,57,43,.12);display:flex;align-items:center;justify-content:center;font-size:14px;color:rgba(192,57,43,.5);cursor:pointer;flex-shrink:0}
.bm-x:active{background:rgba(192,57,43,.3);color:var(--red)}
.empty{text-align:center;padding:32px 20px;color:var(--dim);font-size:11px;letter-spacing:1px;line-height:2}
.eicon{font-size:30px;display:block;margin-bottom:8px;opacity:.35}

/* ADD */
#s-add{background:var(--bg2)}
.form{flex:1;padding:4px 14px 20px;display:flex;flex-direction:column;gap:12px;overflow-y:auto}
.flabel{font-size:9px;letter-spacing:2px;color:var(--dim);margin-bottom:5px}
.finput{width:100%;background:var(--card);border:1px solid var(--dim2);border-radius:14px;padding:14px;font-size:13px;color:var(--text);font-family:inherit;outline:none;-webkit-appearance:none;transition:border-color .15s}
.finput:focus{border-color:var(--gold)}
.finput::placeholder{color:var(--dim);font-size:12px}
.sbtn{width:100%;background:linear-gradient(135deg,var(--gold),var(--gold2));border:none;border-radius:18px;padding:17px;font-size:15px;font-weight:700;color:#000;cursor:pointer;font-family:inherit;letter-spacing:2px;transition:opacity .15s,transform .15s;margin-top:4px}
.sbtn:active{opacity:.8;transform:scale(.97)}

/* CHAPTER */
#s-ch{background:var(--bg2)}
.chcontent{flex:1;padding:0 14px;display:flex;flex-direction:column;gap:12px;justify-content:center}
.chbookname{text-align:center;font-size:11px;color:var(--dim);letter-spacing:2px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.chdisplay{text-align:center;background:var(--card);border:1px solid var(--dim2);border-radius:22px;padding:20px}
.chlabel{font-size:9px;color:var(--dim);letter-spacing:3px;margin-bottom:6px}
.chnum{font-size:46px;font-weight:300;color:var(--gold);line-height:1;letter-spacing:-2px}
.chunit{font-size:12px;color:var(--dim);margin-top:4px}
.chctrl{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px}
.ccbtn{background:var(--card);border:1px solid var(--dim2);border-radius:18px;padding:14px 8px;display:flex;flex-direction:column;align-items:center;gap:5px;cursor:pointer;transition:all .15s}
.ccbtn:active{background:rgba(200,169,110,.1);border-color:var(--gold);transform:scale(.93)}
.ccicon{font-size:20px}
.cclabel{font-size:9px;color:var(--dim);letter-spacing:1px}
.gobtn{width:100%;background:linear-gradient(135deg,var(--gold),var(--gold2));border:none;border-radius:18px;padding:16px;font-size:14px;font-weight:700;color:#000;cursor:pointer;font-family:inherit;letter-spacing:3px;transition:opacity .15s,transform .15s}
.gobtn:active{opacity:.8;transform:scale(.97)}

/* SETTINGS */
#s-cfg{background:var(--bg2)}
.cfglist{flex:1;padding:0 12px 20px;overflow-y:auto}
.cfgitem{background:var(--card);border:1px solid var(--dim2);border-radius:18px;padding:14px 16px;margin-bottom:8px;display:flex;align-items:center;justify-content:space-between;min-height:56px}
.cfgname{font-size:13px;color:var(--text)}
.cfgsub{font-size:10px;color:var(--dim);margin-top:2px}
.toggle{width:42px;height:25px;border-radius:13px;background:var(--dim2);position:relative;cursor:pointer;transition:background .2s;flex-shrink:0}
.toggle.on{background:var(--gold)}
.toggle::after{content:'';position:absolute;top:3px;left:3px;width:19px;height:19px;border-radius:50%;background:white;transition:transform .2s;box-shadow:0 1px 4px rgba(0,0,0,.4)}
.toggle.on::after{transform:translateX(17px)}
.clearbtn{width:100%;background:rgba(192,57,43,.1);border:1px solid rgba(192,57,43,.25);border-radius:16px;padding:15px;font-size:13px;color:var(--red);cursor:pointer;font-family:inherit;letter-spacing:1px;transition:all .15s;margin-top:4px}
.clearbtn:active{background:rgba(192,57,43,.25);transform:scale(.97)}

/* TOAST */
#toast{position:fixed;bottom:22px;left:50%;transform:translateX(-50%) translateY(10px);background:rgba(200,169,110,.15);border:1px solid rgba(200,169,110,.3);border-radius:20px;padding:8px 20px;font-size:12px;color:var(--gold2);letter-spacing:1px;opacity:0;transition:opacity .25s,transform .25s;pointer-events:none;z-index:999;white-space:nowrap}
#toast.show{opacity:1;transform:translateX(-50%) translateY(0)}
::-webkit-scrollbar{display:none}
</style>
</head>
<body>

<!-- HOME -->
<div class="screen" id="s-home">
  <div class="home-top">
    <div>
      <div class="home-clock" id="clock">--:--</div>
      <div class="home-date" id="datestr"></div>
    </div>
    <div class="icon-btn" onclick="go('s-cfg')">⚙</div>
  </div>
  <div class="divider"></div>
  <div class="sec-label">繼續閱讀</div>
  <div class="continue-btn" onclick="continueReading()">
    <div class="ci">📖</div>
    <div class="cb">
      <div class="ct" id="home-title">尚無進度</div>
      <div class="cs" id="home-sub">新增書籤開始閱讀</div>
    </div>
    <div class="ca">›</div>
  </div>
  <div class="home-nav">
    <div class="nav-btn" onclick="go('s-bm')"><div class="ni">🔖</div><div class="nl">書籤</div></div>
    <div class="nav-btn" onclick="go('s-ch')"><div class="ni">📑</div><div class="nl">章節</div></div>
    <div class="nav-btn" onclick="go('s-add')"><div class="ni">＋</div><div class="nl">新增</div></div>
    <div class="nav-btn" onclick="openUrl()"><div class="ni">🌐</div><div class="nl">開啟</div></div>
  </div>
</div>

<!-- BOOKMARKS -->
<div class="screen hidden" id="s-bm">
  <div class="shdr">
    <div class="back-btn" onclick="back()">‹</div>
    <div class="stitle">書籤</div>
    <div class="add-btn" onclick="go('s-add')">＋</div>
  </div>
  <div class="scroll" id="bm-list"></div>
</div>

<!-- ADD -->
<div class="screen hidden" id="s-add">
  <div class="shdr">
    <div class="back-btn" onclick="back()">‹</div>
    <div class="stitle">新增書籤</div>
  </div>
  <div class="form">
    <div>
      <div class="flabel">書名</div>
      <input class="finput" id="inp-name" type="text" placeholder="例：三體" maxlength="20">
    </div>
    <div>
      <div class="flabel">章節網址</div>
      <input class="finput" id="inp-url" type="url" placeholder="https://czbooks.net/…" inputmode="url">
    </div>
    <button class="sbtn" onclick="saveBm()">儲　存</button>
  </div>
</div>

<!-- CHAPTER -->
<div class="screen hidden" id="s-ch">
  <div class="shdr">
    <div class="back-btn" onclick="back()">‹</div>
    <div class="stitle">章節跳轉</div>
  </div>
  <div class="chcontent">
    <div class="chbookname" id="chbook">請先選擇書籍</div>
    <div class="chdisplay">
      <div class="chlabel">目前章節</div>
      <div class="chnum" id="chdisp">—</div>
      <div class="chunit">章</div>
    </div>
    <div class="chctrl">
      <div class="ccbtn" onclick="adjCh(-10)"><div class="ccicon">«</div><div class="cclabel">−10</div></div>
      <div class="ccbtn" onclick="adjCh(-1)"><div class="ccicon">‹</div><div class="cclabel">上一章</div></div>
      <div class="ccbtn" onclick="adjCh(1)"><div class="ccicon">›</div><div class="cclabel">下一章</div></div>
    </div>
    <button class="gobtn" onclick="goCh()">前　往</button>
  </div>
</div>

<!-- SETTINGS -->
<div class="screen hidden" id="s-cfg">
  <div class="shdr">
    <div class="back-btn" onclick="back()">‹</div>
    <div class="stitle">設定</div>
  </div>
  <div class="cfglist">
    <div class="cfgitem">
      <div><div class="cfgname">深色模式</div><div class="cfgsub">護眼背景</div></div>
      <div class="toggle on" onclick="this.classList.toggle('on')"></div>
    </div>
    <div class="cfgitem">
      <div><div class="cfgname">版本</div><div class="cfgsub">小說閱讀器 v1.0</div></div>
    </div>
    <button class="clearbtn" onclick="clearAll()">清除所有書籤</button>
  </div>
</div>

<div id="toast"></div>

<script>
const KEY='nv3';
function load(){try{return JSON.parse(localStorage.getItem(KEY))||{cur:null,bm:[]}}catch{return{cur:null,bm:[]}}}
function save(){localStorage.setItem(KEY,JSON.stringify(D))}
let D=load();

// Clock
function tick(){
  const n=new Date(),days=['週日','週一','週二','週三','週四','週五','週六'];
  document.getElementById('clock').textContent=String(n.getHours()).padStart(2,'0')+':'+String(n.getMinutes()).padStart(2,'0');
  document.getElementById('datestr').textContent=days[n.getDay()]+' · '+(n.getMonth()+1)+'月'+n.getDate()+'日';
}
tick();setInterval(tick,15000);

// Nav
let hist=['s-home'];
function go(id){
  const c=hist[hist.length-1];
  if(c===id)return;
  document.getElementById(c).classList.add('behind');
  const el=document.getElementById(id);
  el.classList.remove('hidden','behind');
  hist.push(id);
  if(id==='s-bm')renderBm();
  if(id==='s-ch')renderCh();
}
function back(){
  if(hist.length<=1)return;
  const c=hist.pop(),p=hist[hist.length-1];
  document.getElementById(c).classList.add('hidden');
  document.getElementById(p).classList.remove('behind','hidden');
}

// Toast
let tt;
function toast(m){
  const e=document.getElementById('toast');
  e.textContent=m;e.classList.add('show');
  clearTimeout(tt);tt=setTimeout(()=>e.classList.remove('show'),1800);
}

// URL helpers
function parseCh(url){const m=url.match(/[?&]chapterNumber=(\d+)/);return m?parseInt(m[1]):null}
function setCh(url,n){
  if(/[?&]chapterNumber=\d+/.test(url))return url.replace(/([?&]chapterNumber=)\d+/,'$1'+n);
  return url+(url.includes('?')?'&':'?')+'chapterNumber='+n;
}

// Home
function updateHome(){
  const c=D.cur;
  if(c){
    const ch=parseCh(c.url);
    document.getElementById('home-title').textContent=c.name||'繼續閱讀';
    document.getElementById('home-sub').textContent=ch?'第 '+ch+' 章':'點擊繼續';
  }else{
    document.getElementById('home-title').textContent='尚無進度';
    document.getElementById('home-sub').textContent='新增書籤開始閱讀';
  }
}
function continueReading(){if(!D.cur){toast('請先新增書籤');return}window.location.href=D.cur.url}
function openUrl(){if(!D.cur){toast('請先新增書籤');return}window.location.href=D.cur.url}

// Chapter
let tCh=1;
function renderCh(){
  const c=D.cur;
  if(c){document.getElementById('chbook').textContent=c.name||'目前書籍';tCh=parseCh(c.url)||1}
  else{document.getElementById('chbook').textContent='請先選擇書籍';tCh=1}
  document.getElementById('chdisp').textContent=tCh;
}
function adjCh(d){tCh=Math.max(1,tCh+d);document.getElementById('chdisp').textContent=tCh}
function goCh(){
  if(!D.cur){toast('請先新增書籤');return}
  const url=setCh(D.cur.url,tCh);
  D.cur={...D.cur,url};save();updateHome();
  toast('前往第 '+tCh+' 章…');
  setTimeout(()=>{window.location.href=url},700);
}

// Bookmarks
function saveBm(){
  const name=document.getElementById('inp-name').value.trim();
  const url=document.getElementById('inp-url').value.trim();
  if(!url){toast('請輸入網址');return}
  if(!url.startsWith('http')){toast('網址格式錯誤');return}
  const e={id:Date.now(),name:name||('書籤'+(D.bm.length+1)),url};
  D.bm.unshift(e);D.cur={name:e.name,url};save();
  document.getElementById('inp-name').value='';
  document.getElementById('inp-url').value='';
  updateHome();toast('已儲存 ✓');setTimeout(()=>back(),700);
}
function renderBm(){
  const el=document.getElementById('bm-list');
  if(!D.bm.length){el.innerHTML='<div class="empty"><span class="eicon">📚</span>尚無書籤<br>點右上角 ＋ 新增</div>';return}
  el.innerHTML=D.bm.map(b=>{
    const ch=parseCh(b.url);
    return`<div class="bm-item" onclick="openBm(${b.id})">
      <div class="bm-bar"></div>
      <div class="bm-info">
        <div class="bm-name">${esc(b.name)}</div>
        <div class="bm-ch">${ch?'第 '+ch+' 章':'—'}</div>
      </div>
      <div class="bm-x" onclick="event.stopPropagation();delBm(${b.id})">×</div>
    </div>`;
  }).join('');
}
function openBm(id){
  const b=D.bm.find(x=>x.id===id);if(!b)return;
  D.cur={name:b.name,url:b.url};save();updateHome();
  window.location.href=b.url;
}
function delBm(id){
  D.bm=D.bm.filter(x=>x.id!==id);
  if(D.bm.length===0)D.cur=null;
  save();renderBm();updateHome();toast('已刪除');
}
function clearAll(){
  if(!confirm('確定清除所有書籤？'))return;
  D.bm=[];D.cur=null;save();updateHome();toast('已清除');
}
function esc(s){return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;')}

updateHome();
</script>
</body>
</html>
