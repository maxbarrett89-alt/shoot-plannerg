<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Frame Flow</title>
<style>
  :root {
    --bg: #faf6f3;
    --surface: #ffffff;
    --surface-alt: #fff2e8;
    --border: #e8d9cf;
    --border-strong: #1a1512;
    --text: #181110;
    --text-muted: #5c4a42;
    --text-faint: #8a7a72;
    --orange: #f2611e;
    --orange-dark: #c8460e;
    --red: #d62828;
    --red-dark: #a01c1c;
    --red-bg: #fdeaea;
    --red-border: #e4a8a8;
    --black: #141010;
    --grad: linear-gradient(135deg,#ff7d1f,#d62828);
    --grad-soft: linear-gradient(135deg,#fff2e8,#fde4e0);
  }
  * { box-sizing: border-box; }
  body {
    margin: 0;
    background: var(--bg);
    color: var(--text);
    font-family: system-ui, -apple-system, sans-serif;
    min-height: 100vh;
  }
  #app { min-height: 100vh; padding-bottom: 72px; position: relative; }
  .header {
    background: var(--black);
    padding: 12px 16px;
    text-align: center;
  }
  .header.plan { border-bottom: 3px solid var(--red); }
  .header.shoot { border-bottom: 3px solid var(--orange); }
  .header .eyebrow {
    font-size: 11px; letter-spacing: 4px; color: var(--orange);
    text-transform: uppercase; font-weight: 800;
  }
  .header .title {
    font-size: 20px; font-weight: 900; letter-spacing: 2px; color: #fff;
  }
  .screen { padding: 16px; max-width: 560px; margin: 0 auto; }
  .screen.narrow { max-width: 480px; }

  /* Stepper */
  .stepper { margin-bottom: 14px; }
  .stepper-label {
    font-size: 11px; color: var(--text-muted); text-transform: uppercase;
    letter-spacing: 2px; margin-bottom: 6px; font-weight: 700;
  }
  .stepper-row { display: flex; align-items: center; gap: 6px; flex-wrap: wrap; }
  .stepper-btn {
    padding: 8px 11px; background: #fff; border: 1.5px solid var(--orange);
    border-radius: 8px; color: var(--orange-dark); cursor: pointer;
    font-size: 14px; font-weight: 800; font-family: inherit;
  }
  .stepper-btn:hover { background: var(--surface-alt); }
  .stepper-val {
    padding: 8px 16px; background: var(--black); border: 1.5px solid var(--border-strong);
    border-radius: 8px; color: #fff; font-weight: 900; font-size: 17px;
    min-width: 64px; text-align: center;
  }

  /* Cards */
  .loc-card {
    background: var(--surface); border-radius: 14px; padding: 14px;
    margin-bottom: 14px; border: 1.5px solid var(--border);
    box-shadow: 0 2px 8px rgba(20,16,16,0.05);
  }
  .loc-top { display: flex; gap: 8px; margin-bottom: 10px; align-items: center; }
  input[type="text"], input[type="datetime-local"], textarea {
    background: #fff; border: 1.5px solid var(--border); border-radius: 8px;
    color: var(--text); padding: 9px 11px; font-size: 15px; font-weight: 600;
    font-family: inherit;
  }
  input[type="text"]:focus, textarea:focus, input[type="datetime-local"]:focus {
    outline: 2px solid var(--orange); outline-offset: 1px;
  }
  .loc-name-input { flex: 1; }
  .icon-btn-del {
    background: var(--red-bg); border: 1.5px solid var(--red-border); border-radius: 8px;
    color: var(--red-dark); padding: 9px 13px; cursor: pointer; font-size: 14px; font-weight: 700;
    font-family: inherit;
  }
  .frame-card {
    background: var(--grad-soft); border-radius: 10px; padding: 12px;
    margin-bottom: 8px; border: 1px solid var(--border);
  }
  .frame-top { display: flex; gap: 8px; margin-bottom: 8px; align-items: center; }
  .frame-name-input { flex: 1; padding: 8px 11px; font-size: 14px; }
  .icon-btn-del-sm {
    background: var(--red-bg); border: 1.5px solid var(--red-border); border-radius: 8px;
    color: var(--red-dark); padding: 8px 11px; cursor: pointer; font-size: 13px; font-weight: 700;
    font-family: inherit;
  }
  textarea.poses-input {
    width: 100%; min-height: 70px; resize: vertical; font-size: 13px; font-weight: 500;
  }
  .add-frame-btn, .add-loc-btn {
    background: #fff; border-radius: 8px; padding: 8px 14px; cursor: pointer;
    font-size: 13px; font-weight: 700; font-family: inherit;
  }
  .add-frame-btn { border: 1.5px dashed var(--orange); color: var(--orange-dark); margin-top: 4px; }
  .add-loc-btn {
    width: 100%; border: 1.5px dashed var(--red); color: var(--red-dark);
    border-radius: 10px; padding: 11px; font-size: 14px; margin-bottom: 16px;
  }
  .start-btn {
    width: 100%; background: var(--grad); border: none; border-radius: 12px;
    color: #fff; padding: 16px; font-size: 18px; font-weight: 900; cursor: pointer;
    letter-spacing: 1px; box-shadow: 0 4px 14px rgba(214,40,40,0.3); font-family: inherit;
  }
  .hint { text-align: center; color: var(--text-faint); font-size: 13px; font-weight: 600; }

  /* Shoot screen */
  .dots { display: flex; gap: 4px; margin-bottom: 16px; flex-wrap: wrap; }
  .dot { height: 5px; flex: 1; min-width: 8px; border-radius: 2px; background: var(--border); }
  .dot.past { opacity: 0.35; }
  .loc-bar {
    background: var(--surface); border: 1.5px solid var(--border); border-radius: 12px;
    padding: 10px 14px; margin-bottom: 10px; display: flex; justify-content: space-between;
  }
  .loc-bar .eyebrow2 { font-size: 10px; color: var(--text-faint); text-transform: uppercase; letter-spacing: 2px; font-weight: 700; }
  .loc-bar .locname { color: var(--text); font-weight: 800; font-size: 17px; }
  .loc-bar .right { text-align: right; font-size: 12px; color: var(--text-muted); font-weight: 600; }
  .loc-bar .buffer-tag { color: var(--red-dark); font-size: 10px; font-weight: 800; }

  .frame-box {
    background: var(--surface); border-radius: 16px; padding: 20px; margin-bottom: 12px;
    border: 2px solid var(--border);
  }
  .frame-box.buffer { border-color: var(--red-border); }
  .frame-box .kind { font-size: 10px; text-transform: uppercase; letter-spacing: 2px; margin-bottom: 4px; font-weight: 800; color: var(--orange-dark); }
  .frame-box.buffer .kind { color: var(--red-dark); }
  .frame-box .fname { color: var(--text); font-weight: 800; font-size: 18px; margin-bottom: 20px; }
  .ring-wrap { display: flex; justify-content: center; margin-bottom: 20px; }
  .poses-list .eyebrow2 { font-size: 10px; color: var(--text-faint); text-transform: uppercase; letter-spacing: 2px; margin-bottom: 8px; font-weight: 700; }
  .pose-item {
    background: var(--grad-soft); border: 1px solid var(--border); border-radius: 8px;
    padding: 8px 12px; margin-bottom: 5px; color: var(--text); font-size: 14px; font-weight: 600;
  }

  .controls-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 10px; }
  .play-btn {
    background: var(--grad); border: none; border-radius: 12px; color: #fff;
    padding: 16px; font-size: 20px; font-weight: 900; cursor: pointer;
    box-shadow: 0 4px 12px rgba(214,40,40,0.28); font-family: inherit;
  }
  .pause-btn {
    background: #fff; border: 2px solid var(--orange); border-radius: 12px; color: var(--orange-dark);
    padding: 16px; font-size: 20px; font-weight: 900; cursor: pointer; font-family: inherit;
  }
  .skip-btn {
    background: var(--black); border: 1.5px solid var(--border-strong); border-radius: 12px;
    color: #fff; padding: 16px; font-size: 15px; font-weight: 700; cursor: pointer; font-family: inherit;
  }
  .end-btn {
    width: 100%; background: none; border: none; color: var(--text-faint); font-size: 13px;
    font-weight: 700; cursor: pointer; padding: 8px; font-family: inherit;
  }

  /* Done screen */
  .done-screen { text-align: center; padding: 40px; }
  .done-emoji { font-size: 60px; margin-bottom: 16px; }
  .done-title { color: var(--text); font-size: 22px; font-weight: 900; margin-bottom: 8px; }
  .done-sub { color: var(--text-muted); margin-bottom: 32px; font-weight: 600; }
  .back-btn {
    background: var(--grad); border: none; border-radius: 12px; color: #fff;
    padding: 14px 32px; font-size: 16px; font-weight: 800; cursor: pointer; font-family: inherit;
  }

  /* Schedule screen */
  .add-session-card {
    background: var(--surface); border: 1.5px solid var(--border); border-radius: 14px;
    padding: 16px; margin-bottom: 16px; box-shadow: 0 2px 8px rgba(20,16,16,0.05);
  }
  .add-session-card .eyebrow {
    font-size: 11px; color: var(--text-muted); text-transform: uppercase; letter-spacing: 2px;
    margin-bottom: 12px; font-weight: 700;
  }
  .full-input { width: 100%; margin-bottom: 10px; }
  .add-session-btn {
    width: 100%; background: var(--grad); border: none; border-radius: 10px; color: #fff;
    padding: 12px; font-size: 15px; font-weight: 800; cursor: pointer; margin-top: 4px; font-family: inherit;
  }
  .empty-msg { color: var(--text-faint); text-align: center; padding: 32px; font-weight: 600; }
  .session-row {
    background: var(--surface); border: 1.5px solid var(--border); border-radius: 12px;
    padding: 12px 16px; margin-bottom: 8px; display: flex; justify-content: space-between; align-items: center;
  }
  .session-row .sname { color: var(--text); font-weight: 800; }
  .session-row .sdate { color: var(--text-muted); font-size: 13px; font-weight: 600; }
  .session-del {
    background: var(--red-bg); border: 1.5px solid var(--red-border); border-radius: 8px;
    color: var(--red-dark); padding: 6px 11px; cursor: pointer; font-weight: 700; font-family: inherit;
  }

  /* Bottom nav */
  .bottom-nav {
    position: fixed; bottom: 0; left: 0; right: 0; background: var(--surface);
    border-top: 2px solid var(--border); display: flex;
    box-shadow: 0 -2px 10px rgba(20,16,16,0.06);
  }
  .nav-btn {
    flex: 1; background: none; border: none; cursor: pointer; padding: 10px 0;
    display: flex; flex-direction: column; align-items: center; gap: 3px;
    color: var(--text-faint); font-size: 11px; text-transform: uppercase; letter-spacing: 1px;
    font-weight: 600; font-family: inherit;
  }
  .nav-btn.active { color: var(--red); font-weight: 800; }
  .nav-btn .icon { font-size: 20px; }

  .hidden { display: none !important; }
</style>
</head>
<body>
<div id="app">

  <!-- PLAN + SCHEDULE VIEW -->
  <div id="mainView">
    <div class="header plan">
      <div class="eyebrow">Photographer's</div>
      <div class="title">FRAME FLOW</div>
    </div>

    <!-- PLAN SCREEN -->
    <div id="planScreen" class="screen">
      <div class="stepper" id="totalTimeStepper"></div>
      <div id="locationsContainer"></div>
      <button class="add-loc-btn" id="addLocBtn">+ Add Location</button>
      <button class="start-btn hidden" id="startBtn">▶ START SHOOT</button>
      <div class="hint hidden" id="hintMsg">Add at least one frame to each location to start.</div>
    </div>

    <!-- SCHEDULE SCREEN -->
    <div id="scheduleScreen" class="screen hidden">
      <div class="add-session-card">
        <div class="eyebrow">Add Session</div>
        <input type="text" id="sessionName" class="full-input" placeholder="Session name">
        <input type="datetime-local" id="sessionDt" class="full-input">
        <div class="stepper" id="durationStepper"></div>
        <button class="add-session-btn" id="addSessionBtn">+ Add Session</button>
      </div>
      <div id="sessionsList"></div>
    </div>

    <div class="bottom-nav">
      <button class="nav-btn active" id="navPlan"><span class="icon">✦</span>Plan</button>
      <button class="nav-btn" id="navSchedule"><span class="icon">◷</span>Schedule</button>
    </div>
  </div>

  <!-- SHOOT VIEW -->
  <div id="shootView" class="hidden">
    <div class="header shoot">
      <div class="eyebrow">Shoot Mode</div>
      <div class="title">FRAME FLOW</div>
    </div>
    <div class="screen narrow" id="shootScreenContent"></div>
  </div>

</div>

<script>
// ── State ─────────────────────────────────────────────────────────────────
let totalMin = 0;
let locations = []; // {id, name, minutes, frames:[{id,name,minutes,bufferMin,poses}]}
let sessions = []; // {id, name, dt, dur}
let notified = {};

// Shoot-mode state
let segments = [];
let segIdx = 0;
let segSecs = 0;
let running = false;
let done = false;
let tickInterval = null;

function uid() { return Math.random().toString(36).slice(2, 8); }
function fmt(secs) {
  const m = Math.floor(Math.abs(secs) / 60);
  const s = Math.abs(secs) % 60;
  return `${m}:${s.toString().padStart(2, "0")}`;
}
function beep(freq = 880, ms = 200, vol = 0.5) {
  try {
    const ctx = new (window.AudioContext || window.webkitAudioContext)();
    const o = ctx.createOscillator();
    const g = ctx.createGain();
    o.connect(g); g.connect(ctx.destination);
    o.frequency.value = freq;
    g.gain.value = vol;
    o.start(); o.stop(ctx.currentTime + ms / 1000);
  } catch (e) {}
}
function escapeHtml(str) {
  const d = document.createElement('div');
  d.textContent = str ?? "";
  return d.innerHTML;
}

// ── Stepper builder ──────────────────────────────────────────────────────
// Renders a stepper into container with given value + onChange callback
function renderStepper(container, label, value, min, onChange) {
  container.innerHTML = `
    ${label ? `<div class="stepper-label">${label}</div>` : ""}
    <div class="stepper-row">
      <button class="stepper-btn" data-d="-30">−30</button>
      <button class="stepper-btn" data-d="-10">−10</button>
      <button class="stepper-btn" data-d="-1">−1</button>
      <div class="stepper-val">${value}m</div>
      <button class="stepper-btn" data-d="1">+1</button>
      <button class="stepper-btn" data-d="10">+10</button>
      <button class="stepper-btn" data-d="30">+30</button>
    </div>
  `;
  container.querySelectorAll(".stepper-btn").forEach(btn => {
    btn.addEventListener("click", () => {
      const delta = parseInt(btn.dataset.d, 10);
      const newVal = Math.max(min, value + delta);
      onChange(newVal);
    });
  });
}

// ── Plan Screen Rendering ────────────────────────────────────────────────
function renderPlanScreen() {
  renderStepper(document.getElementById("totalTimeStepper"), "Total Shoot Time", totalMin, 0, (v) => {
    totalMin = v;
    renderPlanScreen();
  });

  const container = document.getElementById("locationsContainer");
  container.innerHTML = "";

  locations.forEach((loc, li) => {
    const locCard = document.createElement("div");
    locCard.className = "loc-card";

    locCard.innerHTML = `
      <div class="loc-top">
        <input type="text" class="loc-name-input" placeholder="Location ${li + 1} name" value="${escapeHtml(loc.name)}">
        <button class="icon-btn-del">✕</button>
      </div>
      <div class="stepper loc-time-stepper"></div>
      <div class="frames-container"></div>
      <button class="add-frame-btn">+ Add Frame</button>
    `;

    // Location name
    locCard.querySelector(".loc-name-input").addEventListener("input", (e) => {
      loc.name = e.target.value;
    });
    // Remove location
    locCard.querySelector(".icon-btn-del").addEventListener("click", () => {
      locations = locations.filter(l => l.id !== loc.id);
      renderPlanScreen();
    });
    // Location time stepper
    renderStepper(locCard.querySelector(".loc-time-stepper"), "Location Time", loc.minutes, 0, (v) => {
      loc.minutes = v;
      renderPlanScreen();
    });

    // Frames
    const framesContainer = locCard.querySelector(".frames-container");
    loc.frames.forEach((fr, fi) => {
      const frameCard = document.createElement("div");
      frameCard.className = "frame-card";
      frameCard.innerHTML = `
        <div class="frame-top">
          <input type="text" class="frame-name-input" placeholder="Frame ${fi + 1} name" value="${escapeHtml(fr.name)}">
          <button class="icon-btn-del-sm">✕</button>
        </div>
        <div class="stepper frame-time-stepper"></div>
        <div class="stepper frame-buffer-stepper"></div>
        <div class="stepper-label">Pose Ideas (one per line)</div>
        <textarea class="poses-input" placeholder="e.g.&#10;Lean on wall&#10;Hands in pockets&#10;Look away">${escapeHtml(fr.poses)}</textarea>
      `;
      frameCard.querySelector(".frame-name-input").addEventListener("input", (e) => {
        fr.name = e.target.value;
      });
      frameCard.querySelector(".icon-btn-del-sm").addEventListener("click", () => {
        loc.frames = loc.frames.filter(f => f.id !== fr.id);
        renderPlanScreen();
      });
      renderStepper(frameCard.querySelector(".frame-time-stepper"), "Frame Time", fr.minutes, 0, (v) => {
        fr.minutes = v;
        renderPlanScreen();
      });
      renderStepper(frameCard.querySelector(".frame-buffer-stepper"), "Buffer After Frame (0 = none)", fr.bufferMin, 0, (v) => {
        fr.bufferMin = v;
        renderPlanScreen();
      });
      frameCard.querySelector(".poses-input").addEventListener("input", (e) => {
        fr.poses = e.target.value;
      });
      framesContainer.appendChild(frameCard);
    });

    locCard.querySelector(".add-frame-btn").addEventListener("click", () => {
      loc.frames.push({ id: uid(), name: "", minutes: 0, bufferMin: 0, poses: "" });
      renderPlanScreen();
    });

    container.appendChild(locCard);
  });

  const canStart = locations.length > 0 && locations.every(l => l.frames.length > 0);
  document.getElementById("startBtn").classList.toggle("hidden", !canStart);
  document.getElementById("hintMsg").classList.toggle("hidden", !(locations.length > 0 && !canStart));
}

document.getElementById("addLocBtn").addEventListener("click", () => {
  locations.push({ id: uid(), name: "", minutes: 0, frames: [] });
  renderPlanScreen();
});

document.getElementById("startBtn").addEventListener("click", () => {
  startShoot();
});

// ── Shoot Mode ────────────────────────────────────────────────────────────
function buildSegments() {
  segments = [];
  locations.forEach((loc, li) => {
    loc.frames.forEach((fr, fi) => {
      segments.push({
        kind: "frame",
        locName: loc.name, locIdx: li, locTotal: locations.length,
        frameName: fr.name, frameIdx: fi, frameTotal: loc.frames.length,
        poses: fr.poses.split("\n").filter(p => p.trim()),
        totalSecs: fr.minutes > 0 ? fr.minutes * 60 : 0
      });
      if (fr.bufferMin > 0) {
        segments.push({
          kind: "buffer",
          locName: loc.name, locIdx: li, locTotal: locations.length,
          frameName: fr.name, frameIdx: fi, frameTotal: loc.frames.length,
          poses: [],
          totalSecs: fr.bufferMin * 60
        });
      }
    });
  });
}

function startShoot() {
  buildSegments();
  segIdx = 0;
  segSecs = segments[0]?.totalSecs ?? 0;
  running = false;
  done = false;
  document.getElementById("mainView").classList.add("hidden");
  document.getElementById("shootView").classList.remove("hidden");
  renderShootScreen();
}

function endShoot() {
  stopTick();
  document.getElementById("shootView").classList.add("hidden");
  document.getElementById("mainView").classList.remove("hidden");
  renderPlanScreen();
}

function stopTick() {
  clearInterval(tickInterval);
  tickInterval = null;
}

function playSeg() {
  if (running) return;
  running = true;
  beep(880, 150);
  startTick();
  renderShootScreen();
}

function pauseSeg() {
  stopTick();
  running = false;
  renderShootScreen();
}

function advanceSeg() {
  stopTick();
  beep(330, 400, 0.6);
  if (navigator.vibrate) navigator.vibrate([200, 100, 200]);
  const next = segIdx + 1;
  if (next >= segments.length) {
    running = false;
    done = true;
    renderShootScreen();
    return;
  }
  segIdx = next;
  segSecs = segments[next].totalSecs;
  running = true;
  renderShootScreen();
  startTick();
  setTimeout(() => { beep(880, 150); beep(1100, 150); }, 600);
}

function startTick() {
  stopTick();
  tickInterval = setInterval(() => {
    segSecs -= 1;
    if (segSecs <= 0) {
      advanceSeg();
    } else {
      updateTimerDisplay();
    }
  }, 1000);
}

function updateTimerDisplay() {
  const seg = segments[segIdx];
  const timerText = document.getElementById("timerText");
  const timerStatus = document.getElementById("timerStatus");
  const ringFg = document.getElementById("ringFg");
  if (!seg || !timerText) return;
  timerText.textContent = fmt(segSecs);
  const pct = seg.totalSecs > 0 ? Math.max(0, (segSecs / seg.totalSecs) * 100) : 0;
  const r = 68;
  const circ = 2 * Math.PI * r;
  const dash = circ * (pct / 100);
  if (ringFg) ringFg.setAttribute("stroke-dasharray", `${dash} ${circ}`);
  if (timerStatus) {
    timerStatus.textContent = running ? "RUNNING" : (segSecs === seg.totalSecs ? "READY" : "PAUSED");
  }
}

function renderShootScreen() {
  const el = document.getElementById("shootScreenContent");

  if (done) {
    el.innerHTML = `
      <div class="done-screen">
        <div class="done-emoji">🎞</div>
        <div class="done-title">Shoot Complete!</div>
        <div class="done-sub">Every frame done. Great work.</div>
        <button class="back-btn" id="backToPlanBtn">Back to Plan</button>
      </div>
    `;
    el.querySelector("#backToPlanBtn").addEventListener("click", endShoot);
    return;
  }

  const seg = segments[segIdx];
  const isBuffer = seg?.kind === "buffer";
  const accentVar = isBuffer ? "var(--red)" : "var(--orange)";
  const size = 160;
  const r = 68;
  const circ = 2 * Math.PI * r;
  const pct = seg && seg.totalSecs > 0 ? Math.max(0, (segSecs / seg.totalSecs) * 100) : 0;
  const dash = circ * (pct / 100);

  const dotsHtml = segments.map((s, i) => {
    let cls = "dot";
    if (i < segIdx) cls += " past";
    return `<div class="${cls}" style="background:${i <= segIdx ? accentVarFor(s, i) : 'var(--border)'}"></div>`;
  }).join("");

  function accentVarFor(s, i) {
    // color for dots up to current: use each segment's own kind color, simplified to current accent
    return i === segIdx ? (isBuffer ? "#d62828" : "#f2611e") : (segments[i].kind === "buffer" ? "#d62828" : "#f2611e");
  }

  const posesHtml = (seg?.poses?.length > 0) ? `
    <div class="poses-list">
      <div class="eyebrow2">Pose Ideas</div>
      ${seg.poses.map(p => `<div class="pose-item">${escapeHtml(p)}</div>`).join("")}
    </div>
  ` : "";

  el.innerHTML = `
    <div class="dots">${dotsHtml}</div>

    <div class="loc-bar">
      <div>
        <div class="eyebrow2">Location ${(seg?.locIdx ?? 0) + 1} / ${seg?.locTotal}</div>
        <div class="locname">${escapeHtml(seg?.locName || "")}</div>
      </div>
      <div class="right">
        Frame ${(seg?.frameIdx ?? 0) + 1} / ${seg?.frameTotal}
        ${isBuffer ? `<div class="buffer-tag">BUFFER</div>` : ""}
      </div>
    </div>

    <div class="frame-box ${isBuffer ? 'buffer' : ''}">
      <div class="kind">${isBuffer ? "Buffer" : "Frame"}</div>
      <div class="fname">${isBuffer ? `Transition after "${escapeHtml(seg?.frameName || "")}"` : escapeHtml(seg?.frameName || "")}</div>

      <div class="ring-wrap">
        <svg width="${size}" height="${size}">
          <circle cx="${size/2}" cy="${size/2}" r="${r}" fill="none" stroke="var(--border)" stroke-width="12"/>
          <circle id="ringFg" cx="${size/2}" cy="${size/2}" r="${r}" fill="none"
            stroke="${isBuffer ? '#d62828' : '#f2611e'}" stroke-width="12"
            stroke-dasharray="${dash} ${circ}" stroke-linecap="round"
            transform="rotate(-90 ${size/2} ${size/2})" style="transition: stroke-dasharray 0.8s linear"/>
          <text id="timerText" x="${size/2}" y="${size/2 - 6}" text-anchor="middle" fill="#181110" font-size="28" font-weight="900" font-family="monospace">${fmt(segSecs)}</text>
          <text id="timerStatus" x="${size/2}" y="${size/2 + 18}" text-anchor="middle" fill="${running ? (isBuffer ? '#d62828' : '#f2611e') : '#8a7a72'}" font-size="11" letter-spacing="2" font-weight="700">${running ? "RUNNING" : (segSecs === seg?.totalSecs ? "READY" : "PAUSED")}</text>
        </svg>
      </div>

      ${posesHtml}
    </div>

    <div class="controls-grid">
      ${running
        ? `<button class="pause-btn" id="pauseBtn">⏸</button>`
        : `<button class="play-btn" id="playBtn">▶</button>`
      }
      <button class="skip-btn" id="skipBtn">Skip →</button>
    </div>

    <button class="end-btn" id="endShootBtn">✕ End Shoot</button>
  `;

  const playBtn = el.querySelector("#playBtn");
  if (playBtn) playBtn.addEventListener("click", playSeg);
  const pauseBtn = el.querySelector("#pauseBtn");
  if (pauseBtn) pauseBtn.addEventListener("click", pauseSeg);
  el.querySelector("#skipBtn").addEventListener("click", advanceSeg);
  el.querySelector("#endShootBtn").addEventListener("click", endShoot);
}

// ── Schedule Screen ───────────────────────────────────────────────────────
let scheduleDuration = 180;

function renderScheduleScreen() {
  renderStepper(document.getElementById("durationStepper"), "Duration", scheduleDuration, 10, (v) => {
    scheduleDuration = v;
    renderScheduleScreen();
  });

  const list = document.getElementById("sessionsList");
  if (sessions.length === 0) {
    list.innerHTML = `<div class="empty-msg">No sessions scheduled yet.</div>`;
    return;
  }
  const sorted = [...sessions].sort((a, b) => new Date(a.dt) - new Date(b.dt));
  list.innerHTML = sorted.map(s => `
    <div class="session-row" data-id="${s.id}">
      <div>
        <div class="sname">${escapeHtml(s.name)}</div>
        <div class="sdate">${new Date(s.dt).toLocaleString([], { month: "short", day: "numeric", hour: "2-digit", minute: "2-digit" })} · ${s.dur} min</div>
      </div>
      <button class="session-del">✕</button>
    </div>
  `).join("");
  list.querySelectorAll(".session-row").forEach(row => {
    row.querySelector(".session-del").addEventListener("click", () => {
      const id = row.dataset.id;
      sessions = sessions.filter(x => x.id !== id);
      renderScheduleScreen();
    });
  });
}

document.getElementById("addSessionBtn").addEventListener("click", () => {
  const nameInput = document.getElementById("sessionName");
  const dtInput = document.getElementById("sessionDt");
  const name = nameInput.value.trim();
  const dt = dtInput.value;
  if (!name || !dt) return;
  sessions.push({ id: uid(), name, dt, dur: scheduleDuration });
  nameInput.value = "";
  dtInput.value = "";
  renderScheduleScreen();
});

// Session notification checker
setInterval(() => {
  const now = Date.now();
  sessions.forEach(s => {
    const start = new Date(s.dt).getTime();
    const end = start + s.dur * 60000;
    if (!notified[s.id + "s"] && now >= start - 300000 && now < start) {
      notified[s.id + "s"] = true;
      beep(660, 300, 0.6); setTimeout(() => beep(660, 300, 0.6), 350);
      alert(`📸 "${s.name}" starts in 5 minutes!`);
    }
    if (!notified[s.id + "e"] && now >= end - 300000 && now < end) {
      notified[s.id + "e"] = true;
      beep(440, 400, 0.6); setTimeout(() => beep(440, 400, 0.6), 450);
      alert(`⏱ "${s.name}" ends in 5 minutes!`);
    }
  });
}, 20000);

// ── Nav ───────────────────────────────────────────────────────────────────
document.getElementById("navPlan").addEventListener("click", () => {
  document.getElementById("planScreen").classList.remove("hidden");
  document.getElementById("scheduleScreen").classList.add("hidden");
  document.getElementById("navPlan").classList.add("active");
  document.getElementById("navSchedule").classList.remove("active");
});
document.getElementById("navSchedule").addEventListener("click", () => {
  document.getElementById("planScreen").classList.add("hidden");
  document.getElementById("scheduleScreen").classList.remove("hidden");
  document.getElementById("navSchedule").classList.add("active");
  document.getElementById("navPlan").classList.remove("active");
});

// ── Init ──────────────────────────────────────────────────────────────────
renderPlanScreen();
renderScheduleScreen();
</script>
</body>
</html>
