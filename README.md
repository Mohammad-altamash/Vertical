<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Vortical</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:wght@300;400;500;600&display=swap');

:root {
  --bg: #07070d;
  --surface: #111118;
  --surface2: #1a1a25;
  --surface3: #22222f;
  --accent: #7c3aed;
  --accent2: #e040fb;
  --accent3: #06b6d4;
  --red: #ff2d55;
  --green: #00e5a0;
  --text: #eeeeff;
  --muted: #55556a;
  --nav-h: 68px;
  --top-h: 56px;
}

*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent;}

body {
  background: var(--bg);
  color: var(--text);
  font-family: 'DM Sans', sans-serif;
  height: 100dvh;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  position: relative;
}

/* ── NOISE TEXTURE OVERLAY ── */
body::before {
  content:'';
  position:fixed;inset:0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E");
  pointer-events:none;z-index:0;opacity:.4;
}

/* ══ TOP BAR ══ */
.topbar {
  height: var(--top-h);
  display:flex;align-items:center;justify-content:space-between;
  padding: 0 18px;
  background: var(--bg);
  position:relative;z-index:50;
  border-bottom: 1px solid #ffffff06;
  flex-shrink:0;
}
.logo {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: 26px;
  letter-spacing: -0.5px;
  background: linear-gradient(110deg, #a855f7, #e040fb, #06b6d4);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
.topbar-right { display:flex;gap:10px;align-items:center; }
.icon-btn {
  background: var(--surface2);
  border: none;
  border-radius: 50%;
  width: 36px; height: 36px;
  display:flex;align-items:center;justify-content:center;
  font-size: 16px;
  cursor: pointer;
  transition: background .15s, transform .1s;
  color: var(--text);
}
.icon-btn:active { transform: scale(.88); background: var(--surface3); }

/* ══ MAIN CONTENT ══ */
.content {
  flex: 1;
  overflow: hidden;
  position: relative;
  z-index: 1;
}
.view { display:none; height:100%; flex-direction:column; overflow:hidden; }
.view.active { display:flex; }

/* ══ BOTTOM NAV ══ */
.bottom-nav {
  height: var(--nav-h);
  background: rgba(7,7,13,0.96);
  backdrop-filter: blur(20px);
  border-top: 1px solid #ffffff08;
  display: flex;
  align-items: center;
  position: relative;
  z-index: 50;
  flex-shrink: 0;
  padding: 0 4px;
}
.nav-item {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 4px;
  cursor: pointer;
  padding: 8px 4px;
  border-radius: 14px;
  transition: background .2s;
  position: relative;
  user-select: none;
}
.nav-item:active { background: var(--surface2); }
.nav-icon {
  font-size: 22px;
  line-height: 1;
  transition: transform .2s;
  filter: grayscale(1) opacity(.5);
}
.nav-label {
  font-size: 10px;
  font-weight: 600;
  letter-spacing: .4px;
  color: var(--muted);
  transition: color .2s;
}
.nav-item.active .nav-icon { filter: none; transform: scale(1.1); }
.nav-item.active .nav-label { color: var(--text); }
/* glowing dot indicator */
.nav-item.active::before {
  content:'';
  position:absolute;
  top: 6px;
  width: 4px; height: 4px;
  border-radius: 50%;
  background: var(--accent2);
  box-shadow: 0 0 8px var(--accent2);
}

/* ══════════════════════════════════════
   1. SHORTS / VORTICAL VIEW
══════════════════════════════════════ */
#view-shorts {
  background: #000;
  position: relative;
}
.shorts-feed {
  flex: 1;
  overflow-y: scroll;
  scroll-snap-type: y mandatory;
  scrollbar-width: none;
}
.shorts-feed::-webkit-scrollbar { display:none; }

.short-slide {
  width: 100%;
  height: 100%;
  scroll-snap-align: start;
  position: relative;
  background: #000;
  display: flex;
  align-items: center;
  justify-content: center;
}
.short-slide video {
  width: 100%; height: 100%;
  object-fit: cover;
}
/* gradient overlays */
.short-slide::before {
  content:'';position:absolute;inset:0;
  background: linear-gradient(to bottom, rgba(0,0,0,.35) 0%, transparent 30%, transparent 55%, rgba(0,0,0,.85) 100%);
  z-index:2;pointer-events:none;
}
.short-bottom {
  position:absolute;bottom:14px;left:14px;right:72px;
  z-index:5;
}
.short-name {
  font-size: 14px;font-weight:600;
  text-shadow: 0 1px 6px rgba(0,0,0,.7);
  margin-bottom:5px;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow:hidden;
}
.short-dur-pill {
  display:inline-flex;align-items:center;gap:4px;
  background: rgba(124,58,237,.7);
  backdrop-filter:blur(6px);
  padding:3px 9px;border-radius:20px;
  font-size:11px;font-weight:600;
}
.short-side {
  position:absolute;right:10px;bottom:14px;
  z-index:5;
  display:flex;flex-direction:column;align-items:center;gap:16px;
}
.side-btn {
  display:flex;flex-direction:column;align-items:center;gap:3px;
  cursor:pointer;
}
.side-btn .sb-ico {
  width:46px;height:46px;
  background:rgba(255,255,255,.1);
  backdrop-filter:blur(10px);
  border-radius:50%;
  display:flex;align-items:center;justify-content:center;
  font-size:20px;
  border:1px solid rgba(255,255,255,.08);
  transition:background .15s,transform .1s;
}
.side-btn:active .sb-ico { transform:scale(.86);background:rgba(255,255,255,.2); }
.side-btn span { font-size:10px;color:rgba(255,255,255,.7);font-weight:500; }

/* progress thin bar */
.short-prog-wrap {
  position:absolute;bottom:0;left:0;right:0;height:2px;
  background:rgba(255,255,255,.12);z-index:6;
}
.short-prog-fill {
  height:100%;
  background: linear-gradient(90deg,var(--accent),var(--accent2));
  width:0%;
}

/* tap pulse */
.tap-pulse {
  position:absolute;top:50%;left:50%;
  transform:translate(-50%,-50%) scale(0);
  width:72px;height:72px;
  background:rgba(255,255,255,.15);
  border-radius:50%;
  display:flex;align-items:center;justify-content:center;
  font-size:30px;
  pointer-events:none;
  z-index:10;
  opacity:0;
  transition:transform .12s,opacity .25s;
}
.tap-pulse.show { transform:translate(-50%,-50%) scale(1);opacity:1; }

/* ══════════════════════════════════════
   2. LONG VIDEO VIEW
══════════════════════════════════════ */
#view-long { background: var(--bg); overflow-y:auto; }

.player-block {
  background:#000;
  position:relative;
  aspect-ratio:16/9;
  width:100%;
  flex-shrink:0;
}
.player-block video { width:100%;height:100%;object-fit:contain;display:block; }

.vid-controls {
  position:absolute;bottom:0;left:0;right:0;
  background:linear-gradient(transparent,rgba(0,0,0,.9));
  padding:6px 12px 10px;
  opacity:0;
  transition:opacity .3s;
}
.player-block.ctrl-show .vid-controls,
.player-block:hover .vid-controls { opacity:1; }

.seek-wrap {
  width:100%;height:4px;
  background:rgba(255,255,255,.2);
  border-radius:4px;
  margin-bottom:8px;
  cursor:pointer;
  position:relative;
}
.seek-fill {
  height:100%;
  background:linear-gradient(90deg,var(--accent),var(--accent2));
  border-radius:4px;
  width:0%;
  pointer-events:none;
  position:relative;
}
.seek-fill::after {
  content:'';position:absolute;right:-6px;top:-4px;
  width:12px;height:12px;
  background:#fff;border-radius:50%;
  box-shadow:0 0 6px rgba(124,58,237,.6);
}
.ctrl-row { display:flex;align-items:center;gap:10px; }
.cb { background:none;border:none;color:#fff;font-size:18px;cursor:pointer;padding:3px;line-height:1;transition:transform .1s; }
.cb:active { transform:scale(.82); }
.ct { font-size:11px;color:rgba(255,255,255,.7);flex:1; }
input[type=range].vs {
  -webkit-appearance:none;width:72px;height:3px;
  background:rgba(255,255,255,.25);border-radius:3px;outline:none;
}
input[type=range].vs::-webkit-slider-thumb {
  -webkit-appearance:none;width:11px;height:11px;
  background:#fff;border-radius:50%;
}

.now-playing-card {
  padding:14px 16px 10px;
  border-bottom:1px solid #ffffff08;
}
.np-title { font-size:16px;font-weight:600;line-height:1.45;margin-bottom:8px; }
.np-meta { display:flex;align-items:center;gap:8px;font-size:12px;color:var(--muted); }
.np-tag {
  padding:3px 10px;border-radius:20px;font-size:11px;font-weight:600;
  background:linear-gradient(110deg,var(--accent),var(--accent2));
}

.section-title {
  padding:14px 16px 6px;
  font-family:'Syne',sans-serif;
  font-size:13px;font-weight:700;
  letter-spacing:.5px;
  color:var(--muted);
  text-transform:uppercase;
}

.vcard {
  display:flex;gap:12px;
  padding:8px 14px;
  cursor:pointer;
  border-radius:12px;
  margin:2px 8px;
  transition:background .15s;
  align-items:center;
}
.vcard:hover,.vcard.vc-active { background:var(--surface); }
.vthumb {
  width:128px;height:72px;
  background:var(--surface2);
  border-radius:8px;
  overflow:hidden;
  position:relative;
  flex-shrink:0;
}
.vthumb video { width:100%;height:100%;object-fit:cover; }
.vthumb-ov {
  position:absolute;inset:0;
  background:rgba(0,0,0,.25);
  display:flex;align-items:center;justify-content:center;
  font-size:20px;
}
.vdur-tag {
  position:absolute;bottom:3px;right:4px;
  background:rgba(0,0,0,.75);
  font-size:10px;padding:1px 5px;
  border-radius:4px;color:#fff;
}
.vcard-info { flex:1;min-width:0; }
.vcard-title {
  font-size:13px;font-weight:500;line-height:1.4;
  display:-webkit-box;-webkit-line-clamp:2;-webkit-box-orient:vertical;overflow:hidden;
}
.vcard-sub { font-size:11px;color:var(--muted);margin-top:3px; }

.eq-bars { display:flex;align-items:flex-end;gap:2px;height:14px;margin-left:auto;flex-shrink:0; }
.eq-bar { width:3px;background:var(--accent2);border-radius:2px;animation:eq .7s ease-in-out infinite alternate; }
.eq-bar:nth-child(2){animation-delay:.15s}
.eq-bar:nth-child(3){animation-delay:.3s}
@keyframes eq{from{height:3px}to{height:14px}}

/* ══════════════════════════════════════
   3. LIBRARY / ADD VIEW
══════════════════════════════════════ */
#view-library {
  background: var(--bg);
  overflow-y:auto;
}
.lib-header {
  padding:20px 18px 10px;
  font-family:'Syne',sans-serif;
  font-size:22px;font-weight:800;
}
.lib-stats-row {
  display:flex;gap:10px;
  padding:0 14px 14px;
  overflow-x:auto;
  scrollbar-width:none;
}
.lib-stats-row::-webkit-scrollbar{display:none;}
.stat-chip {
  background:var(--surface);
  border:1px solid #ffffff0a;
  border-radius:14px;
  padding:12px 14px;
  min-width:120px;
  flex-shrink:0;
}
.sc-val {
  font-family:'Syne',sans-serif;
  font-size:22px;font-weight:700;
  background:linear-gradient(110deg,var(--accent),var(--accent2));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;
}
.sc-lbl { font-size:11px;color:var(--muted);margin-top:2px; }

.add-zone {
  margin:0 14px 14px;
  border:2px dashed var(--surface3);
  border-radius:18px;
  padding:28px 20px;
  display:flex;flex-direction:column;align-items:center;gap:12px;
  cursor:pointer;
  transition:border-color .2s,background .2s;
}
.add-zone:active,.add-zone:hover { border-color:var(--accent);background:rgba(124,58,237,.05); }
.add-zone-icon { font-size:40px; }
.add-zone-title { font-size:16px;font-weight:600; }
.add-zone-sub { font-size:12px;color:var(--muted);text-align:center;line-height:1.5; }

.all-videos-list { padding-bottom:14px; }

/* ══════════════════════════════════════
   4. STATS VIEW
══════════════════════════════════════ */
#view-stats {
  background: var(--bg);
  overflow-y: auto;
}
.stats-header {
  padding:20px 18px 6px;
  font-family:'Syne',sans-serif;
  font-size:22px;font-weight:800;
}
.stats-sub { padding:0 18px 18px;font-size:12px;color:var(--muted); }

.big-time-card {
  margin:0 14px 14px;
  background:var(--surface);
  border-radius:20px;
  padding:20px;
  border:1px solid #ffffff08;
  position:relative;
  overflow:hidden;
}
.big-time-card::after {
  content:'';
  position:absolute;top:-30px;right:-30px;
  width:130px;height:130px;
  background:radial-gradient(circle,rgba(124,58,237,.2),transparent 70%);
  pointer-events:none;
}
.btc-label { font-size:12px;color:var(--muted);margin-bottom:6px;font-weight:600;text-transform:uppercase;letter-spacing:.6px; }
.btc-val {
  font-family:'Syne',sans-serif;
  font-size:42px;font-weight:800;
  background:linear-gradient(110deg,#a855f7,#e040fb,#06b6d4);
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;
  line-height:1;
}
.btc-sub { font-size:12px;color:var(--muted);margin-top:6px; }

.stats-grid {
  display:grid;grid-template-columns:1fr 1fr;
  gap:10px;margin:0 14px 14px;
}
.sg-card {
  background:var(--surface);
  border-radius:16px;
  padding:16px;
  border:1px solid #ffffff06;
}
.sgc-val {
  font-family:'Syne',sans-serif;
  font-size:24px;font-weight:700;
  margin-bottom:3px;
}
.sgc-lbl { font-size:11px;color:var(--muted); }

.week-bar-chart {
  margin:0 14px 14px;
  background:var(--surface);
  border-radius:20px;
  padding:18px;
  border:1px solid #ffffff06;
}
.wbc-title {
  font-size:13px;font-weight:600;margin-bottom:16px;color:var(--muted);
  text-transform:uppercase;letter-spacing:.5px;
}
.bars-row {
  display:flex;align-items:flex-end;gap:8px;
  height:80px;
}
.day-bar-wrap { flex:1;display:flex;flex-direction:column;align-items:center;gap:4px; }
.day-bar {
  width:100%;
  background:linear-gradient(to top,var(--accent),var(--accent2));
  border-radius:4px 4px 2px 2px;
  min-height:4px;
  transition:height .4s ease;
  position:relative;
}
.day-bar.today { box-shadow:0 0 12px rgba(224,64,251,.4); }
.day-lbl { font-size:9px;color:var(--muted);font-weight:600; }

.storage-card {
  margin:0 14px 14px;
  background:var(--surface);
  border-radius:20px;
  padding:18px;
  border:1px solid #ffffff06;
}
.stor-title { font-size:13px;font-weight:600;color:var(--muted);text-transform:uppercase;letter-spacing:.5px;margin-bottom:14px; }
.stor-row { display:flex;justify-content:space-between;align-items:center;margin-bottom:8px; }
.stor-lbl { font-size:13px; }
.stor-val { font-size:13px;color:var(--muted); }
.stor-bar-bg { background:var(--surface2);border-radius:6px;height:8px;overflow:hidden;margin-bottom:14px; }
.stor-bar-fill {
  height:100%;border-radius:6px;
  background:linear-gradient(90deg,var(--accent),var(--accent2));
  transition:width .6s ease;
}
.stor-types { display:flex;gap:14px; }
.stor-type { display:flex;align-items:center;gap:6px;font-size:11px; }
.st-dot { width:8px;height:8px;border-radius:50%;flex-shrink:0; }

/* ══════════════════════════════════════
   5. PROFILE / SETTINGS VIEW
══════════════════════════════════════ */
#view-profile {
  background: var(--bg);
  overflow-y:auto;
}
.profile-hero {
  padding:28px 18px 18px;
  display:flex;align-items:center;gap:16px;
}
.avatar {
  width:64px;height:64px;
  border-radius:50%;
  background:linear-gradient(135deg,var(--accent),var(--accent2));
  display:flex;align-items:center;justify-content:center;
  font-size:28px;
  flex-shrink:0;
  box-shadow:0 0 20px rgba(124,58,237,.4);
}
.profile-name { font-family:'Syne',sans-serif;font-size:20px;font-weight:800; }
.profile-sub { font-size:12px;color:var(--muted);margin-top:2px; }

.pref-section {
  margin:0 14px 8px;
  font-family:'Syne',sans-serif;
  font-size:12px;font-weight:700;
  color:var(--muted);
  text-transform:uppercase;letter-spacing:.6px;
  padding:10px 0 4px;
}
.pref-row {
  display:flex;align-items:center;
  padding:14px 18px;
  margin:0 6px;
  border-radius:14px;
  cursor:pointer;
  transition:background .15s;
  gap:14px;
}
.pref-row:hover,.pref-row:active { background:var(--surface); }
.pref-icon { font-size:22px;width:32px;text-align:center; }
.pref-text { flex:1; }
.pref-title { font-size:14px;font-weight:500; }
.pref-desc { font-size:11px;color:var(--muted);margin-top:1px; }
.pref-val { font-size:12px;color:var(--muted); }

/* toggle switch */
.toggle {
  width:44px;height:24px;
  background:var(--surface3);
  border-radius:12px;
  position:relative;
  cursor:pointer;
  transition:background .2s;
  flex-shrink:0;
}
.toggle.on { background:var(--accent); }
.toggle::after {
  content:'';
  position:absolute;
  top:3px;left:3px;
  width:18px;height:18px;
  background:#fff;
  border-radius:50%;
  transition:transform .2s;
}
.toggle.on::after { transform:translateX(20px); }

/* ── EMPTY & TOAST ── */
.empty {
  display:flex;flex-direction:column;align-items:center;
  justify-content:center;gap:12px;
  padding:60px 30px;text-align:center;
  height:100%;
}
.empty-ico { font-size:52px;opacity:.6; }
.empty-ttl { font-size:18px;font-weight:600; }
.empty-txt { font-size:13px;color:var(--muted);line-height:1.6; }
.pick-btn {
  background:linear-gradient(135deg,var(--accent),var(--accent2));
  border:none;color:#fff;
  padding:12px 28px;border-radius:50px;
  font-size:14px;font-weight:600;
  cursor:pointer;
  font-family:'DM Sans',sans-serif;
  transition:transform .15s,box-shadow .15s;
  box-shadow:0 6px 24px rgba(124,58,237,.35);
}
.pick-btn:active { transform:scale(.95); }

.toast {
  position:fixed;
  bottom:82px;left:50%;
  transform:translateX(-50%) translateY(16px);
  background:var(--surface2);
  color:var(--text);
  padding:10px 20px;border-radius:24px;
  font-size:13px;font-weight:500;
  opacity:0;
  transition:opacity .3s,transform .3s;
  z-index:999;
  white-space:nowrap;
  box-shadow:0 4px 20px rgba(0,0,0,.5);
  pointer-events:none;
  border:1px solid #ffffff0a;
}
.toast.show { opacity:1;transform:translateX(-50%) translateY(0); }

#file-input { display:none; }
</style>
</head>
<body>

<!-- TOP BAR -->
<div class="topbar">
  <div class="logo">Vortical</div>
  <div class="topbar-right">
    <button class="icon-btn" onclick="document.getElementById('file-input').click()" title="Add Videos">＋</button>
  </div>
</div>

<!-- CONTENT -->
<div class="content">

  <!-- ① SHORTS -->
  <div class="view active" id="view-shorts">
    <div class="shorts-feed" id="shorts-feed">
      <div class="empty" id="shorts-empty">
        <div class="empty-ico">⚡</div>
        <div class="empty-ttl">Koi Shorts Nahi</div>
        <div class="empty-txt">1 min se kam ki vertical videos yahan scroll hongi. Neeche Library se ya + se add karein.</div>
        <button class="pick-btn" onclick="document.getElementById('file-input').click()">Videos Add Karein</button>
      </div>
    </div>
  </div>

  <!-- ② LONG VIDEO -->
  <div class="view" id="view-long">
    <div id="long-player-section" style="display:none;flex-shrink:0;">
      <div class="player-block" id="player-block">
        <video id="long-vid" playsinline></video>
        <div class="vid-controls" id="vid-controls">
          <div class="seek-wrap" id="seek-wrap">
            <div class="seek-fill" id="seek-fill"></div>
          </div>
          <div class="ctrl-row">
            <button class="cb" id="lp-btn" onclick="toggleLong()">▶</button>
            <button class="cb" onclick="skipL(-10)">⏪</button>
            <button class="cb" onclick="skipL(10)">⏩</button>
            <span class="ct" id="lp-time">0:00 / 0:00</span>
            <input type="range" class="vs" min="0" max="1" step="0.05" value="1"
              oninput="document.getElementById('long-vid').volume=this.value">
            <button class="cb" id="mute-btn" onclick="toggleMute()" style="font-size:15px">🔊</button>
            <button class="cb" onclick="toggleFS()" style="font-size:13px">⛶</button>
          </div>
        </div>
      </div>
    </div>
    <div style="flex:1;overflow-y:auto;" id="long-scroll">
      <div class="empty" id="long-empty">
        <div class="empty-ico">🎬</div>
        <div class="empty-ttl">Koi Long Video Nahi</div>
        <div class="empty-txt">1 min se zyada ki videos yahan aayengi. Library se add karein.</div>
        <button class="pick-btn" onclick="document.getElementById('file-input').click()">Videos Add Karein</button>
      </div>
      <div id="now-playing-wrap" style="display:none;">
        <div class="now-playing-card">
          <div class="np-title" id="np-title">—</div>
          <div class="np-meta">
            <span class="np-tag">🎬 Long</span>
            <span id="np-dur" style="color:var(--muted);font-size:12px;">—</span>
          </div>
        </div>
      </div>
      <div class="section-title" id="playlist-hdr" style="display:none;">UP NEXT</div>
      <div id="long-cards"></div>
    </div>
  </div>

  <!-- ③ LIBRARY -->
  <div class="view" id="view-library">
    <div class="lib-header">Library</div>
    <div class="lib-stats-row" id="lib-stats-row">
      <div class="stat-chip"><div class="sc-val" id="lsc-total">0</div><div class="sc-lbl">Total Videos</div></div>
      <div class="stat-chip"><div class="sc-val" id="lsc-shorts">0</div><div class="sc-lbl">Shorts ⚡</div></div>
      <div class="stat-chip"><div class="sc-val" id="lsc-longs">0</div><div class="sc-lbl">Long 🎬</div></div>
      <div class="stat-chip"><div class="sc-val" id="lsc-size">0 MB</div><div class="sc-lbl">Storage Used</div></div>
    </div>

    <div class="add-zone" onclick="document.getElementById('file-input').click()">
      <div class="add-zone-icon">📂</div>
      <div class="add-zone-title">Videos Add Karein</div>
      <div class="add-zone-sub">Phone ki gallery se multiple videos ek saath choose karein. Short aur Long automatically classify honge.</div>
    </div>

    <div class="section-title">All Videos</div>
    <div id="lib-all-videos" class="all-videos-list">
      <div class="empty" id="lib-empty" style="padding:30px 20px;">
        <div class="empty-ico" style="font-size:36px;">📭</div>
        <div class="empty-txt">Abhi koi video nahi. Upar se add karein.</div>
      </div>
    </div>
  </div>

  <!-- ④ STATS -->
  <div class="view" id="view-stats">
    <div class="stats-header">Watch Stats</div>
    <div class="stats-sub">Aaj ka aur weekly screen time</div>

    <div class="big-time-card">
      <div class="btc-label">Aaj Total Watch Time</div>
      <div class="btc-val" id="stat-today-val">0m 0s</div>
      <div class="btc-sub" id="stat-today-sub">Abhi tak koi video nahi dekha</div>
    </div>

    <div class="stats-grid">
      <div class="sg-card">
        <div class="sgc-val" id="sg-shorts-time" style="background:linear-gradient(110deg,var(--accent),var(--accent2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;">0m</div>
        <div class="sgc-lbl">Shorts Time ⚡</div>
      </div>
      <div class="sg-card">
        <div class="sgc-val" id="sg-long-time" style="background:linear-gradient(110deg,var(--accent3),var(--green));-webkit-background-clip:text;-webkit-text-fill-color:transparent;">0m</div>
        <div class="sgc-lbl">Long Time 🎬</div>
      </div>
      <div class="sg-card">
        <div class="sgc-val" id="sg-videos-watched" style="background:linear-gradient(110deg,var(--red),var(--accent2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;">0</div>
        <div class="sgc-lbl">Videos Dekhe</div>
      </div>
      <div class="sg-card">
        <div class="sgc-val" id="sg-streak" style="background:linear-gradient(110deg,var(--green),var(--accent3));-webkit-background-clip:text;-webkit-text-fill-color:transparent;">0🔥</div>
        <div class="sgc-lbl">Day Streak</div>
      </div>
    </div>

    <div class="week-bar-chart">
      <div class="wbc-title">Is Hafte (Minutes)</div>
      <div class="bars-row" id="week-bars"></div>
    </div>

    <div class="storage-card">
      <div class="stor-title">Storage Usage</div>
      <div class="stor-row">
        <span class="stor-lbl">Used</span>
        <span class="stor-val" id="stor-used-lbl">0 MB</span>
      </div>
      <div class="stor-bar-bg">
        <div class="stor-bar-fill" id="stor-bar" style="width:0%"></div>
      </div>
      <div class="stor-types">
        <div class="stor-type"><div class="st-dot" style="background:var(--accent)"></div><span id="stor-shorts-sz">Shorts: 0 MB</span></div>
        <div class="stor-type"><div class="st-dot" style="background:var(--accent3)"></div><span id="stor-long-sz">Long: 0 MB</span></div>
      </div>
    </div>
  </div>

  <!-- ⑤ PROFILE -->
  <div class="view" id="view-profile">
    <div class="profile-hero">
      <div class="avatar">👤</div>
      <div>
        <div class="profile-name">Mera Profile</div>
        <div class="profile-sub" id="prof-sub">0 videos • Vortical User</div>
      </div>
    </div>

    <div class="pref-section">Playback</div>

    <div class="pref-row" onclick="togglePref('autoplay')">
      <div class="pref-icon">▶️</div>
      <div class="pref-text">
        <div class="pref-title">Auto Play</div>
        <div class="pref-desc">Next video automatically chalao</div>
      </div>
      <div class="toggle on" id="toggle-autoplay"></div>
    </div>
    <div class="pref-row" onclick="togglePref('loop')">
      <div class="pref-icon">🔁</div>
      <div class="pref-text">
        <div class="pref-title">Loop Shorts</div>
        <div class="pref-desc">Short videos loop hote rahein</div>
      </div>
      <div class="toggle on" id="toggle-loop"></div>
    </div>
    <div class="pref-row" onclick="togglePref('mute')">
      <div class="pref-icon">🔇</div>
      <div class="pref-text">
        <div class="pref-title">Mute on Start</div>
        <div class="pref-desc">Videos muted se start hon</div>
      </div>
      <div class="toggle" id="toggle-mute"></div>
    </div>

    <div class="pref-section">Data</div>

    <div class="pref-row" onclick="resetStats()">
      <div class="pref-icon">🗑️</div>
      <div class="pref-text">
        <div class="pref-title">Stats Reset Karein</div>
        <div class="pref-desc">Watch history aur time data clear ho jaayega</div>
      </div>
      <span class="pref-val">›</span>
    </div>
    <div class="pref-row" onclick="removeAllVideos()">
      <div class="pref-icon">📭</div>
      <div class="pref-text">
        <div class="pref-title">Sab Videos Hatao</div>
        <div class="pref-desc">Saari videos list se hatao</div>
      </div>
      <span class="pref-val">›</span>
    </div>

    <div class="pref-section">About</div>
    <div class="pref-row">
      <div class="pref-icon">⚡</div>
      <div class="pref-text">
        <div class="pref-title">Vortical v1.0</div>
        <div class="pref-desc">Offline Video Player • Short & Long</div>
      </div>
    </div>
  </div>

</div><!-- /content -->

<!-- BOTTOM NAV -->
<nav class="bottom-nav">
  <div class="nav-item active" id="nav-shorts" onclick="goTo('shorts')">
    <div class="nav-icon">⚡</div>
    <div class="nav-label">Shorts</div>
  </div>
  <div class="nav-item" id="nav-long" onclick="goTo('long')">
    <div class="nav-icon">🎬</div>
    <div class="nav-label">Long</div>
  </div>
  <div class="nav-item" id="nav-library" onclick="goTo('library')">
    <div class="nav-icon">📂</div>
    <div class="nav-label">Library</div>
  </div>
  <div class="nav-item" id="nav-stats" onclick="goTo('stats')">
    <div class="nav-icon">📊</div>
    <div class="nav-label">Stats</div>
  </div>
  <div class="nav-item" id="nav-profile" onclick="goTo('profile')">
    <div class="nav-icon">👤</div>
    <div class="nav-label">Profile</div>
  </div>
</nav>

<div class="toast" id="toast"></div>
<input type="file" id="file-input" accept="video/*" multiple>

<script>
/* ═══════════════════════════════════════════
   STATE
═══════════════════════════════════════════ */
const state = {
  shorts: [],   // {url, name, duration, size}
  longs: [],
  currentLong: -1,
  prefs: { autoplay: true, loop: true, mute: false },
  stats: loadStats(),
  watchTimers: {},   // active timers per video
};

function loadStats() {
  try {
    const s = localStorage.getItem('vortical_stats');
    if (s) return JSON.parse(s);
  } catch(e) {}
  return { todayShorts:0, todayLong:0, videosWatched:0, streak:0,
           lastDay:'', weekData:[0,0,0,0,0,0,0] };
}
function saveStats() {
  const today = new Date().toDateString();
  if (state.stats.lastDay !== today) {
    // new day
    state.stats.weekData.push(Math.floor((state.stats.todayShorts+state.stats.todayLong)/60));
    state.stats.weekData = state.stats.weekData.slice(-7);
    state.stats.todayShorts = 0;
    state.stats.todayLong = 0;
    state.stats.lastDay = today;
    state.stats.streak = (state.stats.streak||0) + 1;
  }
  try { localStorage.setItem('vortical_stats', JSON.stringify(state.stats)); } catch(e) {}
}

/* ═══════════════════════════════════════════
   NAV
═══════════════════════════════════════════ */
function goTo(tab) {
  ['shorts','long','library','stats','profile'].forEach(t => {
    document.getElementById('view-'+t).classList.toggle('active', t===tab);
    document.getElementById('nav-'+t).classList.toggle('active', t===tab);
  });
  if (tab === 'stats') refreshStats();
  if (tab === 'library') refreshLibrary();
  if (tab === 'profile') refreshProfile();
}

/* ═══════════════════════════════════════════
   FILE INPUT
═══════════════════════════════════════════ */
document.getElementById('file-input').addEventListener('change', async function() {
  const files = Array.from(this.files);
  if (!files.length) return;
  let added = 0;
  for (const f of files) {
    const url = URL.createObjectURL(f);
    const dur = await getVideoDuration(url);
    const entry = { url, name: f.name.replace(/\.[^.]+$/,''), duration: dur, size: f.size, file: f };
    if (dur < 60) state.shorts.push(entry);
    else state.longs.push(entry);
    added++;
  }
  renderShorts();
  renderLongs();
  refreshLibrary();
  showToast(`${added} video${added>1?'s':''} add ho gaye ✓`);
  this.value = '';
});

function getVideoDuration(url) {
  return new Promise(res => {
    const v = document.createElement('video');
    v.src = url; v.preload = 'metadata';
    v.onloadedmetadata = () => res(v.duration);
    v.onerror = () => res(0);
  });
}
function fmt(s) {
  if (!isFinite(s)||s<=0) return '0:00';
  const m=Math.floor(s/60), sc=Math.floor(s%60);
  return `${m}:${sc.toString().padStart(2,'0')}`;
}
function fmtMB(bytes) { return (bytes/1048576).toFixed(1)+' MB'; }
function fmtMin(sec) { const m=Math.floor(sec/60),s=Math.floor(sec%60); return m>0?`${m}m ${s}s`:`${s}s`; }

/* ═══════════════════════════════════════════
   SHORTS RENDER
═══════════════════════════════════════════ */
function renderShorts() {
  const feed = document.getElementById('shorts-feed');
  feed.querySelectorAll('.short-slide').forEach(e=>e.remove());
  document.getElementById('shorts-empty').style.display = state.shorts.length ? 'none' : 'flex';

  state.shorts.forEach((s, i) => {
    const div = document.createElement('div');
    div.className = 'short-slide';
    div.style.height = `calc(100dvh - ${getComputedStyle(document.documentElement).getPropertyValue('--top-h').trim()} - ${getComputedStyle(document.documentElement).getPropertyValue('--nav-h').trim()})`;
    div.dataset.i = i;
    div.innerHTML = `
      <video class="sv" src="${s.url}" ${state.prefs.loop?'loop':''} playsinline
        ${state.prefs.mute?'muted':''}></video>
      <div class="tap-pulse" id="tp-${i}"></div>
      <div class="short-bottom">
        <div class="short-name">${s.name}</div>
        <span class="short-dur-pill">⚡ ${fmt(s.duration)}</span>
      </div>
      <div class="short-side">
        <div class="side-btn" onclick="deleteShort(${i})">
          <div class="sb-ico">🗑</div><span>Hatao</span>
        </div>
      </div>
      <div class="short-prog-wrap"><div class="short-prog-fill" id="sp-${i}"></div></div>
    `;
    const vid = div.querySelector('.sv');

    // tap play/pause
    div.addEventListener('click', e => {
      if (e.target.closest('.short-side')) return;
      const tp = document.getElementById(`tp-${i}`);
      if (vid.paused) {
        vid.play().catch(()=>{});
        tp.textContent='▶'; tp.classList.add('show');
      } else {
        vid.pause();
        tp.textContent='⏸'; tp.classList.add('show');
      }
      setTimeout(()=>tp.classList.remove('show'), 600);
    });

    // progress
    vid.addEventListener('timeupdate', () => {
      const pct = vid.duration ? vid.currentTime/vid.duration*100 : 0;
      const el = document.getElementById(`sp-${i}`);
      if (el) el.style.width = pct+'%';
    });

    // watch time tracking
    let watchStart = null;
    vid.addEventListener('play', () => { watchStart = Date.now(); });
    vid.addEventListener('pause', () => {
      if (watchStart) {
        const secs = (Date.now()-watchStart)/1000;
        state.stats.todayShorts += secs;
        state.stats.videosWatched++;
        saveStats();
        watchStart = null;
      }
    });
    vid.addEventListener('ended', () => {
      if (watchStart) {
        const secs = (Date.now()-watchStart)/1000;
        state.stats.todayShorts += secs;
        state.stats.videosWatched++;
        saveStats();
        watchStart = null;
      }
    });

    feed.appendChild(div);
  });

  // IntersectionObserver auto-play
  const io = new IntersectionObserver(entries => {
    entries.forEach(en => {
      const vid = en.target.querySelector('.sv');
      if (!vid) return;
      if (en.isIntersecting) {
        document.querySelectorAll('.sv').forEach(v=>{ if(v!==vid){v.pause();v.currentTime=0;} });
        vid.play().catch(()=>{});
      } else {
        vid.pause();
      }
    });
  }, { threshold: 0.65 });

  feed.querySelectorAll('.short-slide').forEach(el => io.observe(el));
  if (state.shorts.length) setTimeout(()=>feed.querySelectorAll('.sv')[0]?.play().catch(()=>{}), 100);
}

function deleteShort(i) {
  state.shorts.splice(i,1);
  renderShorts();
  refreshLibrary();
  showToast('Short delete ho gaya');
}

/* ═══════════════════════════════════════════
   LONG VIDEO RENDER
═══════════════════════════════════════════ */
function renderLongs() {
  const cards = document.getElementById('long-cards');
  cards.innerHTML = '';
  document.getElementById('long-empty').style.display = state.longs.length ? 'none' : 'flex';
  document.getElementById('playlist-hdr').style.display = state.longs.length ? 'block' : 'none';

  state.longs.forEach((v, i) => {
    const c = document.createElement('div');
    c.className = 'vcard' + (i===state.currentLong?' vc-active':'');
    c.id = `lc-${i}`;
    c.onclick = () => playLong(i);
    c.innerHTML = `
      <div class="vthumb">
        <video src="${v.url}" preload="metadata" muted></video>
        <div class="vthumb-ov">${i===state.currentLong?'':'▶'}</div>
        <span class="vdur-tag">${fmt(v.duration)}</span>
      </div>
      <div class="vcard-info">
        <div class="vcard-title">${v.name}</div>
        <div class="vcard-sub">${fmt(v.duration)} • Local</div>
      </div>
      ${i===state.currentLong?`<div class="eq-bars"><div class="eq-bar"></div><div class="eq-bar"></div><div class="eq-bar"></div></div>`:''}
    `;
    cards.appendChild(c);
  });
}

let longWatchStart = null;
const longVid = document.getElementById('long-vid');

function playLong(i) {
  const v = state.longs[i]; if (!v) return;
  state.currentLong = i;
  document.getElementById('long-player-section').style.display = 'block';
  document.getElementById('now-playing-wrap').style.display = 'block';
  longVid.src = v.url;
  longVid.play().catch(()=>{});
  document.getElementById('lp-btn').textContent = '⏸';
  document.getElementById('np-title').textContent = v.name;
  document.getElementById('np-dur').textContent = fmt(v.duration);
  renderLongs();
  document.getElementById('long-scroll').scrollTo({top:0,behavior:'smooth'});
}

longVid.addEventListener('timeupdate', () => {
  const pct = longVid.duration ? longVid.currentTime/longVid.duration*100 : 0;
  document.getElementById('seek-fill').style.width = pct+'%';
  document.getElementById('lp-time').textContent = `${fmt(longVid.currentTime)} / ${fmt(longVid.duration)}`;
});
longVid.addEventListener('play', () => { longWatchStart = Date.now(); });
longVid.addEventListener('pause', () => {
  if (longWatchStart) {
    state.stats.todayLong += (Date.now()-longWatchStart)/1000;
    saveStats(); longWatchStart = null;
  }
});
longVid.addEventListener('ended', () => {
  if (longWatchStart) {
    state.stats.todayLong += (Date.now()-longWatchStart)/1000;
    state.stats.videosWatched++;
    saveStats(); longWatchStart = null;
  }
  document.getElementById('lp-btn').textContent = '▶';
  if (state.prefs.autoplay && state.currentLong < state.longs.length-1) playLong(state.currentLong+1);
});

const pb = document.getElementById('player-block');
pb.addEventListener('click', e => {
  if (e.target.closest('.vid-controls')) return;
  pb.classList.add('ctrl-show');
  clearTimeout(pb._t);
  pb._t = setTimeout(()=>pb.classList.remove('ctrl-show'), 2500);
});

document.getElementById('seek-wrap').addEventListener('click', e => {
  if (!longVid.duration) return;
  const r = e.currentTarget.getBoundingClientRect();
  longVid.currentTime = ((e.clientX-r.left)/r.width)*longVid.duration;
});

function toggleLong() {
  if (longVid.paused) { longVid.play(); document.getElementById('lp-btn').textContent='⏸'; }
  else { longVid.pause(); document.getElementById('lp-btn').textContent='▶'; }
}
function skipL(s) { longVid.currentTime = Math.max(0, Math.min((longVid.duration||0), longVid.currentTime+s)); }
function toggleMute() {
  longVid.muted = !longVid.muted;
  document.getElementById('mute-btn').textContent = longVid.muted ? '🔇' : '🔊';
}
function toggleFS() {
  if (!document.fullscreenElement) pb.requestFullscreen?.();
  else document.exitFullscreen?.();
}

/* ═══════════════════════════════════════════
   LIBRARY
═══════════════════════════════════════════ */
function refreshLibrary() {
  const all = [...state.shorts, ...state.longs];
  const totalSize = all.reduce((a,v)=>a+(v.size||0),0);
  const shortSize = state.shorts.reduce((a,v)=>a+(v.size||0),0);
  const longSize  = state.longs.reduce((a,v)=>a+(v.size||0),0);

  document.getElementById('lsc-total').textContent = all.length;
  document.getElementById('lsc-shorts').textContent = state.shorts.length;
  document.getElementById('lsc-longs').textContent = state.longs.length;
  document.getElementById('lsc-size').textContent = fmtMB(totalSize);

  const container = document.getElementById('lib-all-videos');
  container.querySelectorAll('.vcard').forEach(e=>e.remove());
  document.getElementById('lib-empty').style.display = all.length ? 'none' : 'flex';

  all.forEach((v, i) => {
    const isShort = v.duration < 60;
    const c = document.createElement('div');
    c.className = 'vcard';
    c.onclick = () => { isShort ? goTo('shorts') : playLong(state.longs.indexOf(v)); if(!isShort) goTo('long'); };
    c.innerHTML = `
      <div class="vthumb">
        <video src="${v.url}" preload="metadata" muted></video>
        <div class="vthumb-ov">${isShort?'⚡':'▶'}</div>
        <span class="vdur-tag">${fmt(v.duration)}</span>
      </div>
      <div class="vcard-info">
        <div class="vcard-title">${v.name}</div>
        <div class="vcard-sub">
          <span style="background:${isShort?'rgba(124,58,237,.25)':'rgba(6,182,212,.2)'};padding:1px 7px;border-radius:8px;font-size:10px;margin-right:5px;">${isShort?'⚡ Short':'🎬 Long'}</span>
          ${fmt(v.duration)} • ${fmtMB(v.size||0)}
        </div>
      </div>
    `;
    container.appendChild(c);
  });
}

/* ═══════════════════════════════════════════
   STATS
═══════════════════════════════════════════ */
function refreshStats() {
  saveStats();
  const total = state.stats.todayShorts + state.stats.todayLong;
  document.getElementById('stat-today-val').textContent = fmtMin(total);
  document.getElementById('stat-today-sub').textContent = total > 0
    ? `Shorts: ${fmtMin(state.stats.todayShorts)} • Long: ${fmtMin(state.stats.todayLong)}`
    : 'Abhi tak koi video nahi dekha';
  document.getElementById('sg-shorts-time').textContent = fmtMin(state.stats.todayShorts);
  document.getElementById('sg-long-time').textContent = fmtMin(state.stats.todayLong);
  document.getElementById('sg-videos-watched').textContent = state.stats.videosWatched;
  document.getElementById('sg-streak').textContent = (state.stats.streak||0)+'🔥';

  // week bars
  const days = ['Su','Mo','Tu','We','Th','Fr','Sa'];
  const today = new Date().getDay();
  const data = state.stats.weekData;
  const maxVal = Math.max(...data, 1);
  const barsEl = document.getElementById('week-bars');
  barsEl.innerHTML = '';
  data.forEach((val, di) => {
    const heightPct = (val/maxVal)*72;
    const isToday = di === (data.length-1);
    const dayIdx = (today - (data.length-1-di) + 7) % 7;
    const w = document.createElement('div');
    w.className = 'day-bar-wrap';
    w.innerHTML = `
      <div class="day-bar${isToday?' today':''}" style="height:${Math.max(4,heightPct)}px"></div>
      <div class="day-lbl">${days[dayIdx]}</div>
    `;
    barsEl.appendChild(w);
  });

  // storage
  const all = [...state.shorts, ...state.longs];
  const totalSize = all.reduce((a,v)=>a+(v.size||0),0);
  const shortSize = state.shorts.reduce((a,v)=>a+(v.size||0),0);
  const longSize  = state.longs.reduce((a,v)=>a+(v.size||0),0);
  const maxStorage = 5*1024*1024*1024; // 5GB estimate
  document.getElementById('stor-used-lbl').textContent = fmtMB(totalSize);
  document.getElementById('stor-bar').style.width = Math.min(100,(totalSize/maxStorage*100))+'%';
  document.getElementById('stor-shorts-sz').textContent = 'Shorts: '+fmtMB(shortSize);
  document.getElementById('stor-long-sz').textContent = 'Long: '+fmtMB(longSize);
}

/* ═══════════════════════════════════════════
   PROFILE
═══════════════════════════════════════════ */
function refreshProfile() {
  const total = state.shorts.length + state.longs.length;
  document.getElementById('prof-sub').textContent = `${total} videos • Vortical User`;
  ['autoplay','loop','mute'].forEach(k => {
    const el = document.getElementById('toggle-'+k);
    el.classList.toggle('on', state.prefs[k]);
  });
}
function togglePref(k) {
  state.prefs[k] = !state.prefs[k];
  document.getElementById('toggle-'+k).classList.toggle('on', state.prefs[k]);
  // apply loop to existing short videos
  if (k==='loop') document.querySelectorAll('.sv').forEach(v=>{ v.loop=state.prefs.loop; });
  showToast(k + (state.prefs[k]?' on':' off'));
}
function resetStats() {
  state.stats = { todayShorts:0, todayLong:0, videosWatched:0, streak:0, lastDay:'', weekData:[0,0,0,0,0,0,0] };
  saveStats();
  showToast('Stats reset ho gaye ✓');
}
function removeAllVideos() {
  if (!confirm('Sab videos hatao?')) return;
  state.shorts.length = 0;
  state.longs.length = 0;
  state.currentLong = -1;
  renderShorts();
  renderLongs();
  refreshLibrary();
  showToast('Sab videos hat gaye');
}

/* ═══════════════════════════════════════════
   TOAST
═══════════════════════════════════════════ */
let _tt;
function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg; t.classList.add('show');
  clearTimeout(_tt); _tt = setTimeout(()=>t.classList.remove('show'), 2300);
}

// init
refreshLibrary();
refreshStats();
</script>
</body>
</html>
