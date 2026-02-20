<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>8 Slots + WebGazer</title>
  <style>
    body {
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      margin: 0;
      background: #c6ecf3;
      color: #272626;
      height: 100vh;
      overflow: hidden;
    }

    /* ---------- Start screen ---------- */
    .start-screen {
      height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 24px;
      text-align: center;
    }
    .start-card {
      background: rgba(255,255,255,0.75);
      border: 2px solid rgba(215,219,231,0.9);
      border-radius: 18px;
      padding: 28px 22px;
      max-width: 720px;
      width: 100%;
      box-shadow: 0 10px 30px rgba(0,0,0,0.08);
    }
    .start-card h1 {
      margin: 0 0 10px;
      font-size: 34px;
    }
    .start-card p {
      margin: 0;
      font-size: 18px;
      line-height: 1.45;
      color: #333;
    }
    .kbd {
      font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace;
      background: #fff;
      border: 1px solid #d7dbe7;
      border-bottom-width: 2px;
      padding: 1px 6px;
      border-radius: 6px;
      font-size: 0.95em;
    }

    /* ---------- App layout ---------- */
    .app {
      height: 100vh;
      display: none; /* hidden until start */
      flex-direction: column;
    }

    .board {
      flex: 1;
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      grid-template-rows: repeat(2, 1fr);
      gap: 16px;
      padding: 20px;
      box-sizing: border-box;
    }

    .slot {
      background: #fff;
      border: 3px solid #d7dbe7;
      border-radius: 16px;
      padding: 14px;
      box-sizing: border-box;

      display: flex;
      align-items: center;
      justify-content: center;

      font-weight: 700;
      font-size: clamp(18px, 2.6vw, 44px);
      text-align: center;

      user-select: none;
      white-space: pre-wrap;     /* show spaces + newlines */
      overflow: hidden;
    }

    .slot.active {
      border-color: #5b7cfa;
      box-shadow: 0 0 0 6px rgba(91, 124, 250, 0.2);
    }
    .slot.filled {
      border-color: #8ed1a9;
    }

    .controls {
      display: flex;
      gap: 10px;
      padding: 16px 20px 20px;
      box-sizing: border-box;
      align-items: stretch;
    }

    textarea {
      flex: 1;
      resize: none;
      height: 54px;
      font-size: 18px;
      padding: 12px 12px;
      border-radius: 12px;
      border: 2px solid #d7dbe7;
      outline: none;
      background: #fff;
      line-height: 1.25;
    }
    textarea:focus {
      border-color: #5b7cfa;
      box-shadow: 0 0 0 4px rgba(91, 124, 250, 0.12);
    }

    button {
      padding: 12px 16px;
      border-radius: 12px;
      border: 0;
      background: #111;
      color: #fff;
      cursor: pointer;
      font-size: 16px;
      min-width: 110px;
    }
    button:active { transform: translateY(1px); }

    .status {
      padding: 0 20px 18px;
      color: #333;
    }

    /* ---------- Gaze dot overlay ---------- */
    .gaze-dot {
      position: fixed;
      left: -9999px;
      top: -9999px;
      width: 14px;
      height: 14px;
      border-radius: 999px;
      background: rgba(0,0,0,0.75);
      pointer-events: none;
      z-index: 99999;
      transform: translate(-50%, -50%);
    }
  </style>
</head>
<body>

  <!-- Start screen -->
  <div class="start-screen" id="startScreen">
    <div class="start-card">
      <h1>Press Enter to Start</h1>
      <p>
        First press of <span class="kbd">Enter</span> opens the 8 slots and starts WebGazer (camera permission).<br/>
        Type a line (spaces allowed), then press <span class="kbd">Enter</span> to place it.<br/>
        Use <span class="kbd">Shift</span> + <span class="kbd">Enter</span> for a new line (optional).
      </p>
    </div>
  </div>

  <!-- App -->
  <div class="app" id="app">
    <div class="board" id="board" aria-label="8 slots">
      <div class="slot" data-i="0">—</div>
      <div class="slot" data-i="1">—</div>
      <div class="slot" data-i="2">—</div>
      <div class="slot" data-i="3">—</div>
      <div class="slot" data-i="4">—</div>
      <div class="slot" data-i="5">—</div>
      <div class="slot" data-i="6">—</div>
      <div class="slot" data-i="7">—</div>
    </div>

    <div class="controls">
      <textarea id="lineInput" placeholder="Type slot 1 text and press Enter…" disabled></textarea>
      <button id="resetBtn" type="button">Reset</button>
    </div>

    <div class="status" id="status">Waiting…</div>
  </div>

  <div class="gaze-dot" id="gazeDot" aria-hidden="true"></div>

  <!-- WebGazer library (served by Brown) -->
  <!-- Docs show including webgazer.js and calling webgazer.begin(). -->
  <script src="https://webgazer.cs.brown.edu/webgazer.js" type="text/javascript"></script> <!-- :contentReference[oaicite:2]{index=2} -->

  <script>
    const startScreen = document.getElementById("startScreen");
    const app = document.getElementById("app");
    const input = document.getElementById("lineInput");
    const statusEl = document.getElementById("status");
    const resetBtn = document.getElementById("resetBtn");
    const slots = Array.from(document.querySelectorAll(".slot"));
    const gazeDot = document.getElementById("gazeDot");

    let started = false;
    let index = 0;
    const lines = Array(8).fill("");

    let webgazerStarted = false;

    function setActiveSlot(i) {
      slots.forEach((s, idx) => {
        s.classList.toggle("active", started && idx === i && i < 8);
      });
    }

    function render() {
      slots.forEach((s, i) => {
        s.textContent = lines[i] ? lines[i] : "—";
        s.classList.toggle("filled", Boolean(lines[i]));
      });

      if (!started) return;

      if (index < 8) {
        statusEl.textContent = `Slot ${index + 1} of 8`;
        input.placeholder = `Type slot ${index + 1} text and press Enter…`;
        input.disabled = false;
      } else {
        statusEl.textContent = "Done! All 8 slots filled.";
        input.placeholder = "Completed";
        input.disabled = true;
      }

      setActiveSlot(index);
    }

    async function startWebgazer() {
      if (webgazerStarted) return;

      if (!window.webgazer) {
        statusEl.textContent = "WebGazer failed to load. Check your connection / script tag.";
        return;
      }

      try {
        // Optional: hide built-in overlays, and show a prediction point if you want.
        // (API listed in WebGazer wiki for prediction points.) :contentReference[oaicite:3]{index=3}
        webgazer
          .showVideoPreview(false)
          .showFaceOverlay(false)
          .showFaceFeedbackBox(false)
          .showPredictionPoints(false); // we use our own dot

        // Listener: move our dot to the predicted gaze coordinates. :contentReference[oaicite:4]{index=4}
        webgazer.setGazeListener((data) => {
          if (!data) return;
          gazeDot.style.left = data.x + "px";
          gazeDot.style.top = data.y + "px";
        });

        // Begin: requests camera permission and starts predictions. :contentReference[oaicite:5]{index=5}
        await webgazer.begin();

        webgazerStarted = true;
        statusEl.textContent = `Slot ${index + 1} of 8 (WebGazer running)`;
      } catch (err) {
        console.error(err);
        statusEl.textContent = "Could not start WebGazer (camera permission denied or unavailable).";
      }
    }

    function stopWebgazer() {
      if (!window.webgazer) return;
      try { webgazer.pause(); } catch (_) {}
      try { webgazer.end(); } catch (_) {}
      webgazerStarted = false;

      // hide dot
      gazeDot.style.left = "-9999px";
      gazeDot.style.top = "-9999px";
    }

    function start() {
      if (started) return;
      started = true;

      // hide start, show app
      startScreen.style.display = "none";
      app.style.display = "flex";

      index = 0;
      input.disabled = false;
      input.value = "";
      input.focus();
      render();

      // start WebGazer on start
      startWebgazer();
    }

    function addLine(raw) {
      // spaces allowed; just reject empty/all-whitespace
      const text = raw.replace(/\r\n/g, "\n").trim();
      if (!text) return false;

      lines[index] = text;
      index += 1;
      input.value = "";
      render();
      if (index < 8) input.focus();
      return true;
    }

    function resetAll() {
      // stop tracking + reset UI
      stopWebgazer();

      started = false;
      index = 0;
      for (let i = 0; i < 8; i++) lines[i] = "";

      // show start, hide app
      startScreen.style.display = "flex";
      app.style.display = "none";

      input.value = "";
      input.disabled = true;
      statusEl.textContent = "Waiting…";
      slots.forEach(s => {
        s.textContent = "—";
        s.classList.remove("filled", "active");
      });
    }

    // First Enter starts the app (only when not started)
    document.addEventListener("keydown", (e) => {
      if (!started && e.key === "Enter") {
        e.preventDefault();
        start();
      }
    });

    // In textarea:
    // - Enter commits line
    // - Shift+Enter inserts newline
    input.addEventListener("keydown", (e) => {
      if (e.key !== "Enter") return;

      if (e.shiftKey) return; // allow newline
      e.preventDefault();

      if (index >= 8) return;

      const ok = addLine(input.value);
      if (!ok) statusEl.textContent = "Please type something (spaces are fine).";
    });

    resetBtn.addEventListener("click", resetAll);

    // initial state
    resetAll();
  </script>
</body>
</html>
