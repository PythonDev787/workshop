<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no, maximum-scale=1.0">
  <title>CALAMITY SIMULATOR - VR Disaster Preparedness & Emergency Training</title>
  
  <!-- A-Frame CDN -->
  <script src="https://aframe.io/releases/1.5.0/aframe.min.js"></script>
  <!-- A-Frame Environment Component for rich procedural terrain & sky -->
  <script src="https://cdn.jsdelivr.net/npm/aframe-environment-component@1.3.3/dist/aframe-environment-component.min.js"></script>

  <style>
    :root {
      --bg-dark: #0a0e17;
      --panel-bg: rgba(14, 22, 38, 0.92);
      --panel-border: rgba(0, 229, 255, 0.4);
      --accent-cyan: #00e5ff;
      --accent-orange: #ff9100;
      --accent-red: #ff3d00;
      --accent-green: #00e676;
      --accent-yellow: #ffd600;
      --text-main: #f0f6fc;
      --text-muted: #8b9bb4;
      --font-family: 'Segoe UI', -apple-system, BlinkMacSystemFont, Roboto, sans-serif;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      user-select: none;
      -webkit-user-select: none;
    }

    body, html {
      width: 100%;
      height: 100%;
      overflow: hidden;
      background-color: #000;
      font-family: var(--font-family);
      color: var(--text-main);
    }

    /* 2D HUD & Overlay UI */
    #ui-container {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: 100;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
    }

    .interactive-ui {
      pointer-events: auto;
    }

    /* Top HUD Bar */
    #hud-top {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 14px 24px;
      background: linear-gradient(180deg, rgba(5, 10, 20, 0.85) 0%, rgba(5, 10, 20, 0) 100%);
      text-shadow: 0 2px 4px rgba(0,0,0,0.8);
    }

    .brand-title {
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .brand-badge {
      background: linear-gradient(135deg, var(--accent-red), var(--accent-orange));
      color: #fff;
      font-weight: 900;
      font-size: 11px;
      letter-spacing: 1.5px;
      padding: 4px 8px;
      border-radius: 4px;
      text-transform: uppercase;
      box-shadow: 0 0 12px rgba(255, 61, 0, 0.6);
    }

    .brand-text h1 {
      font-size: 18px;
      font-weight: 800;
      letter-spacing: 2px;
      color: #fff;
      text-transform: uppercase;
    }

    .brand-text p {
      font-size: 11px;
      color: var(--accent-cyan);
      letter-spacing: 1px;
    }

    .hud-stats {
      display: flex;
      gap: 16px;
      align-items: center;
    }

    .stat-pill {
      background: var(--panel-bg);
      border: 1px solid var(--panel-border);
      padding: 6px 14px;
      border-radius: 20px;
      font-size: 12px;
      display: flex;
      align-items: center;
      gap: 8px;
      backdrop-filter: blur(8px);
    }

    .stat-pill span.val {
      font-weight: 700;
      color: var(--accent-cyan);
    }

    /* Objective HUD Banner */
    #hud-objective {
      position: absolute;
      top: 75px;
      left: 50%;
      transform: translateX(-50%);
      background: var(--panel-bg);
      border: 1px solid var(--accent-cyan);
      padding: 10px 24px;
      border-radius: 8px;
      box-shadow: 0 4px 20px rgba(0, 229, 255, 0.25);
      max-width: 600px;
      text-align: center;
      backdrop-filter: blur(10px);
      transition: all 0.3s ease;
      display: none;
    }

    #hud-objective .title {
      font-size: 11px;
      font-weight: 700;
      color: var(--accent-orange);
      text-transform: uppercase;
      letter-spacing: 1.5px;
      margin-bottom: 2px;
    }

    #hud-objective .task {
      font-size: 14px;
      font-weight: 600;
      color: #ffffff;
    }

    /* Warning Toast Banner */
    #emergency-alert-banner {
      position: absolute;
      top: 135px;
      left: 50%;
      transform: translateX(-50%);
      background: rgba(255, 61, 0, 0.9);
      border: 2px solid #ffffff;
      color: #ffffff;
      padding: 12px 30px;
      border-radius: 6px;
      font-size: 16px;
      font-weight: 800;
      letter-spacing: 2px;
      text-transform: uppercase;
      display: none;
      animation: alertPulse 1s infinite alternate;
      box-shadow: 0 0 30px rgba(255, 61, 0, 0.8);
      z-index: 105;
      text-align: center;
    }

    @keyframes alertPulse {
      0% { transform: translateX(-50%) scale(0.98); opacity: 0.85; }
      100% { transform: translateX(-50%) scale(1.03); opacity: 1; }
    }

    /* Bottom HUD Bar & Quick Controls */
    #hud-bottom {
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      padding: 20px 24px;
      background: linear-gradient(0deg, rgba(5, 10, 20, 0.85) 0%, rgba(5, 10, 20, 0) 100%);
    }

    .key-hints {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
      max-width: 70%;
    }

    .key-tag {
      background: rgba(255, 255, 255, 0.08);
      border: 1px solid rgba(255, 255, 255, 0.15);
      border-radius: 4px;
      padding: 3px 8px;
      font-size: 11px;
      color: var(--text-muted);
      display: flex;
      align-items: center;
      gap: 5px;
    }

    .key-tag kbd {
      background: rgba(0, 229, 255, 0.2);
      color: var(--accent-cyan);
      font-weight: 700;
      padding: 1px 5px;
      border-radius: 3px;
      border: 1px solid rgba(0, 229, 255, 0.4);
      font-family: monospace;
    }

    .hud-actions {
      display: flex;
      gap: 10px;
    }

    .btn {
      background: rgba(0, 229, 255, 0.15);
      border: 1px solid var(--accent-cyan);
      color: #fff;
      padding: 8px 16px;
      border-radius: 6px;
      font-size: 13px;
      font-weight: 600;
      letter-spacing: 0.5px;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: 8px;
      transition: all 0.2s ease;
      text-transform: uppercase;
      backdrop-filter: blur(6px);
    }

    .btn:hover {
      background: var(--accent-cyan);
      color: #050d1a;
      box-shadow: 0 0 15px rgba(0, 229, 255, 0.5);
      transform: translateY(-2px);
    }

    .btn:active {
      transform: translateY(0);
    }

    .btn-danger {
      border-color: var(--accent-red);
      background: rgba(255, 61, 0, 0.2);
    }
    .btn-danger:hover {
      background: var(--accent-red);
      color: #fff;
      box-shadow: 0 0 15px rgba(255, 61, 0, 0.6);
    }

    .btn-warning {
      border-color: var(--accent-orange);
      background: rgba(255, 145, 0, 0.2);
    }
    .btn-warning:hover {
      background: var(--accent-orange);
      color: #050d1a;
      box-shadow: 0 0 15px rgba(255, 145, 0, 0.6);
    }

    .btn-success {
      border-color: var(--accent-green);
      background: rgba(0, 230, 118, 0.2);
    }
    .btn-success:hover {
      background: var(--accent-green);
      color: #050d1a;
      box-shadow: 0 0 15px rgba(0, 230, 118, 0.6);
    }

    /* Modal Windows (Menu, Report, Learning, Settings) */
    .modal-overlay {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(4, 8, 16, 0.88);
      backdrop-filter: blur(12px);
      z-index: 200;
      display: flex;
      justify-content: center;
      align-items: center;
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.3s ease;
    }

    .modal-overlay.active {
      opacity: 1;
      pointer-events: auto;
    }

    .modal-card {
      background: var(--panel-bg);
      border: 1px solid var(--panel-border);
      border-radius: 12px;
      width: 90%;
      max-width: 820px;
      max-height: 88vh;
      display: flex;
      flex-direction: column;
      box-shadow: 0 10px 40px rgba(0, 0, 0, 0.8), 0 0 30px rgba(0, 229, 255, 0.15);
      overflow: hidden;
      animation: modalSlide 0.35s cubic-bezier(0.16, 1, 0.3, 1);
    }

    @keyframes modalSlide {
      from { transform: translateY(30px) scale(0.96); opacity: 0; }
      to { transform: translateY(0) scale(1); opacity: 1; }
    }

    .modal-header {
      padding: 18px 24px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.1);
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: rgba(0, 0, 0, 0.3);
    }

    .modal-header h2 {
      font-size: 20px;
      font-weight: 700;
      letter-spacing: 1.5px;
      color: #fff;
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .modal-body {
      padding: 24px;
      overflow-y: auto;
      flex: 1;
    }

    .modal-footer {
      padding: 16px 24px;
      border-top: 1px solid rgba(255, 255, 255, 0.1);
      display: flex;
      justify-content: flex-end;
      gap: 12px;
      background: rgba(0, 0, 0, 0.2);
    }

    /* Disaster Scenario Selection Cards */
    .scenario-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
      gap: 18px;
    }

    .scenario-card {
      background: rgba(255, 255, 255, 0.03);
      border: 1px solid rgba(255, 255, 255, 0.12);
      border-radius: 8px;
      padding: 18px;
      cursor: pointer;
      transition: all 0.25s ease;
      position: relative;
      overflow: hidden;
    }

    .scenario-card::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 4px;
      height: 100%;
      background: var(--accent-cyan);
      opacity: 0;
      transition: opacity 0.25s ease;
    }

    .scenario-card:hover {
      border-color: var(--accent-cyan);
      background: rgba(0, 229, 255, 0.06);
      transform: translateY(-3px);
      box-shadow: 0 8px 24px rgba(0, 0, 0, 0.4);
    }

    .scenario-card:hover::before {
      opacity: 1;
    }

    .scenario-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 8px;
    }

    .scenario-icon {
      font-size: 24px;
    }

    .scenario-difficulty {
      font-size: 10px;
      font-weight: 700;
      padding: 2px 8px;
      border-radius: 10px;
      text-transform: uppercase;
      letter-spacing: 1px;
    }

    .diff-beginner { background: rgba(0, 230, 118, 0.2); color: var(--accent-green); border: 1px solid var(--accent-green); }
    .diff-intermediate { background: rgba(255, 145, 0, 0.2); color: var(--accent-orange); border: 1px solid var(--accent-orange); }
    .diff-advanced { background: rgba(255, 61, 0, 0.2); color: var(--accent-red); border: 1px solid var(--accent-red); }

    .scenario-card h3 {
      font-size: 16px;
      font-weight: 700;
      margin-bottom: 6px;
      color: #fff;
    }

    .scenario-card p {
      font-size: 12px;
      color: var(--text-muted);
      line-height: 1.5;
      margin-bottom: 12px;
    }

    .scenario-meta {
      display: flex;
      justify-content: space-between;
      font-size: 11px;
      color: var(--text-muted);
      border-top: 1px solid rgba(255, 255, 255, 0.08);
      padding-top: 8px;
    }

    /* Decision Popup (Overlay mirror for 2D desktop mode) */
    #decision-overlay {
      position: absolute;
      bottom: 90px;
      left: 50%;
      transform: translateX(-50%);
      background: var(--panel-bg);
      border: 2px solid var(--accent-orange);
      border-radius: 12px;
      padding: 20px 26px;
      width: 90%;
      max-width: 640px;
      box-shadow: 0 0 40px rgba(255, 145, 0, 0.35);
      z-index: 120;
      display: none;
      backdrop-filter: blur(12px);
      animation: modalSlide 0.3s ease;
    }

    #decision-overlay h3 {
      font-size: 13px;
      color: var(--accent-orange);
      text-transform: uppercase;
      letter-spacing: 1.5px;
      margin-bottom: 6px;
    }

    #decision-overlay .prompt-text {
      font-size: 16px;
      font-weight: 600;
      color: #fff;
      margin-bottom: 16px;
      line-height: 1.4;
    }

    .choices-list {
      display: flex;
      flex-direction: column;
      gap: 10px;
    }

    .choice-btn {
      background: rgba(255, 255, 255, 0.06);
      border: 1px solid rgba(255, 255, 255, 0.2);
      border-radius: 6px;
      padding: 12px 16px;
      color: #fff;
      text-align: left;
      font-size: 13.5px;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 12px;
      transition: all 0.2s ease;
    }

    .choice-btn:hover {
      background: rgba(0, 229, 255, 0.2);
      border-color: var(--accent-cyan);
      transform: translateX(4px);
    }

    .choice-btn .choice-key {
      background: rgba(0, 0, 0, 0.4);
      color: var(--accent-cyan);
      font-weight: 700;
      font-size: 12px;
      padding: 3px 8px;
      border-radius: 4px;
      border: 1px solid rgba(0, 229, 255, 0.4);
    }

    /* Decision Feedback Box */
    #feedback-box {
      margin-top: 12px;
      padding: 12px;
      border-radius: 6px;
      font-size: 13px;
      display: none;
      line-height: 1.4;
    }
    #feedback-box.correct {
      background: rgba(0, 230, 118, 0.15);
      border: 1px solid var(--accent-green);
      color: #d7ffec;
    }
    #feedback-box.incorrect {
      background: rgba(255, 61, 0, 0.15);
      border: 1px solid var(--accent-red);
      color: #ffd9d6;
    }

    /* Performance Report Styling */
    .report-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 16px;
      margin-bottom: 20px;
    }

    .score-circle-card {
      background: rgba(0, 0, 0, 0.35);
      border: 1px solid rgba(255, 255, 255, 0.1);
      border-radius: 8px;
      padding: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      text-align: center;
    }

    .score-big {
      font-size: 48px;
      font-weight: 900;
      color: var(--accent-cyan);
      line-height: 1;
      margin: 10px 0;
    }

    .score-grade {
      font-size: 14px;
      font-weight: 700;
      padding: 4px 12px;
      border-radius: 12px;
      letter-spacing: 1px;
    }

    .stats-breakdown {
      display: flex;
      flex-direction: column;
      gap: 10px;
      justify-content: center;
    }

    .stat-row {
      background: rgba(255, 255, 255, 0.04);
      padding: 10px 14px;
      border-radius: 6px;
      display: flex;
      justify-content: space-between;
      font-size: 13px;
    }

    .stat-row span.label {
      color: var(--text-muted);
    }
    .stat-row span.val {
      font-weight: 700;
      color: #fff;
    }

    .lesson-section {
      background: rgba(0, 229, 255, 0.05);
      border-left: 3px solid var(--accent-cyan);
      padding: 14px;
      border-radius: 0 6px 6px 0;
      margin-top: 16px;
      font-size: 13px;
      line-height: 1.5;
    }

    /* Learning Centre Tabs */
    .tabs-nav {
      display: flex;
      gap: 8px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.12);
      margin-bottom: 16px;
      overflow-x: auto;
      padding-bottom: 6px;
    }

    .tab-btn {
      background: transparent;
      border: none;
      color: var(--text-muted);
      padding: 8px 16px;
      font-size: 13px;
      font-weight: 600;
      cursor: pointer;
      border-radius: 4px;
      transition: all 0.2s ease;
      white-space: nowrap;
    }

    .tab-btn.active, .tab-btn:hover {
      color: #fff;
      background: rgba(0, 229, 255, 0.15);
    }

    .tab-content {
      font-size: 13.5px;
      line-height: 1.6;
      color: #d1d5db;
    }

    .tab-content h4 {
      color: var(--accent-cyan);
      margin: 14px 0 6px 0;
      font-size: 15px;
    }

    .tab-content ul {
      margin-left: 20px;
      margin-bottom: 12px;
    }

    .tab-content li {
      margin-bottom: 6px;
    }

    /* Settings Rows */
    .setting-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 12px 0;
      border-bottom: 1px solid rgba(255, 255, 255, 0.08);
    }

    .setting-label {
      font-size: 14px;
      font-weight: 600;
    }
    .setting-desc {
      font-size: 11px;
      color: var(--text-muted);
    }

    select, input[type="range"] {
      background: #0f172a;
      border: 1px solid var(--panel-border);
      color: #fff;
      padding: 6px 12px;
      border-radius: 4px;
      font-size: 13px;
      outline: none;
    }

    /* VR Comfort Vignette Effect */
    #vr-vignette {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: 50;
      box-shadow: inset 0 0 100px 30px rgba(0,0,0,0.85);
      opacity: 0;
      transition: opacity 0.3s ease;
    }

    /* Crosshair for Desktop Mode */
    #desktop-crosshair {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 10px;
      height: 10px;
      pointer-events: none;
      z-index: 90;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    #desktop-crosshair::before, #desktop-crosshair::after {
      content: '';
      position: absolute;
      background: rgba(0, 229, 255, 0.8);
    }
    #desktop-crosshair::before { width: 10px; height: 2px; }
    #desktop-crosshair::after { width: 2px; height: 10px; }

    /* Interactive Raycast Reticle Highlight */
    .crosshair-hover #desktop-crosshair::before,
    .crosshair-hover #desktop-crosshair::after {
      background: var(--accent-orange) !important;
      transform: scale(1.6);
    }

    /* Achievements Grid */
    .achievements-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
      gap: 14px;
    }

    .achieve-card {
      background: rgba(255, 255, 255, 0.03);
      border: 1px solid rgba(255, 255, 255, 0.1);
      border-radius: 8px;
      padding: 14px;
      display: flex;
      gap: 12px;
      align-items: center;
      opacity: 0.5;
      transition: all 0.3s ease;
    }

    .achieve-card.unlocked {
      opacity: 1;
      border-color: var(--accent-yellow);
      background: rgba(255, 214, 0, 0.08);
    }

    .achieve-icon {
      font-size: 26px;
    }

    .achieve-info h4 {
      font-size: 13px;
      color: #fff;
      margin-bottom: 2px;
    }

    .achieve-info p {
      font-size: 11px;
      color: var(--text-muted);
    }

    /* Custom Scrollbars */
    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    ::-webkit-scrollbar-track {
      background: rgba(0, 0, 0, 0.2);
    }
    ::-webkit-scrollbar-thumb {
      background: rgba(0, 229, 255, 0.3);
      border-radius: 3px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: rgba(0, 229, 255, 0.6);
    }
  </style>
</head>
<body>

  <!-- VR Comfort Vignette overlay -->
  <div id="vr-vignette"></div>

  <!-- Desktop First-Person Crosshair -->
  <div id="desktop-crosshair"></div>

  <!-- 2D Screen Overlay HUD System -->
  <div id="ui-container">
    <!-- Top HUD: Branding, Session Status, Health/Safety -->
    <div id="hud-top">
      <div class="brand-title">
        <div class="brand-badge">SimVR 2.0</div>
        <div class="brand-text">
          <h1>CALAMITY SIMULATOR</h1>
          <p>"Prepare for the Unexpected."</p>
        </div>
      </div>

      <div class="hud-stats">
        <div class="stat-pill" id="hud-scenario-name">
          <span>SCENARIO:</span>
          <span class="val" id="hud-cur-scenario">COMMAND CENTER</span>
        </div>
        <div class="stat-pill">
          <span>SAFETY SCORE:</span>
          <span class="val" id="hud-cur-score">100%</span>
        </div>
        <div class="stat-pill">
          <span>TIME:</span>
          <span class="val" id="hud-cur-time">00:00</span>
        </div>
      </div>
    </div>

    <!-- Active Objective Card -->
    <div id="hud-objective">
      <div class="title" id="obj-title">PRIMARY OBJECTIVE</div>
      <div class="task" id="obj-task">Welcome Trainee. Select an emergency scenario to begin preparedness drills.</div>
    </div>

    <!-- Flashing Emergency Alert -->
    <div id="emergency-alert-banner">
      ⚠️ EMERGENCY ALARM DETECTED ⚠️
    </div>

    <!-- Bottom HUD: Keybind reminders & Quick Action Buttons -->
    <div id="hud-bottom">
      <div class="key-hints">
        <div class="key-tag"><kbd>W</kbd><kbd>A</kbd><kbd>S</kbd><kbd>D</kbd> Move</div>
        <div class="key-tag"><kbd>Mouse</kbd> Look</div>
        <div class="key-tag"><kbd>E</kbd> or <kbd>Left Click</kbd> Interact / Trigger</div>
        <div class="key-tag"><kbd>ESC</kbd> Menu / Pause</div>
        <div class="key-tag"><kbd>F</kbd> Fullscreen</div>
        <div class="key-tag"><kbd>Quest 3S</kbd> Laser Ray + Trigger / Thumbsticks</div>
      </div>

      <div class="hud-actions interactive-ui">
        <button class="btn" id="btn-quick-menu" onclick="App.openModal('main-menu-modal')">
          📋 Menu
        </button>
        <button class="btn btn-warning" id="btn-quick-learn" onclick="App.openModal('learning-modal')">
          📖 Learning
        </button>
        <button class="btn" id="btn-quick-settings" onclick="App.openModal('settings-modal')">
          ⚙️ Settings
        </button>
        <button class="btn btn-danger" id="btn-quick-abort" onclick="App.returnToCommandCenter()" style="display:none;">
          ⏹️ Exit Scenario
        </button>
      </div>
    </div>
  </div>

  <!-- 2D Mirror for Decision Making (Desktop Fallback / Enhanced readability) -->
  <div id="decision-overlay" class="interactive-ui">
    <h3 id="dec-header">EMERGENCY PROTOCOL DECISION</h3>
    <div class="prompt-text" id="dec-prompt">An active earthquake is occurring! What is your immediate action?</div>
    <div class="choices-list" id="dec-choices">
      <!-- Injected dynamically -->
    </div>
    <div id="feedback-box"></div>
    <div style="margin-top:14px; text-align:right;">
      <button class="btn btn-success" id="dec-continue-btn" style="display:none;" onclick="App.continueAfterDecision()">
        Proceed ➔
      </button>
    </div>
  </div>

  <!-- MAIN MENU MODAL -->
  <div class="modal-overlay active" id="main-menu-modal">
    <div class="modal-card">
      <div class="modal-header">
        <h2>🛡️ CALAMITY SIMULATOR - CRISIS TRAINING CENTER</h2>
        <span style="font-size:12px; color:var(--accent-cyan); font-weight:700;">WEBXR & META QUEST 3S READY</span>
      </div>
      <div class="modal-body">
        <p style="color:var(--text-muted); font-size:13.5px; margin-bottom:18px; line-height:1.5;">
          Life is unpredictable, and emergencies can strike anytime without warning. Our VR simulation trains you to make informed decisions under pressure, identify hazards, and respond with confidence rather than panic.
        </p>

        <h3 style="font-size:14px; color:var(--accent-orange); text-transform:uppercase; letter-spacing:1px; margin-bottom:12px;">
          Select Training Drill:
        </h3>

        <div class="scenario-grid">
          <!-- Scenario 1 -->
          <div class="scenario-card" onclick="App.startScenario('earthquake')">
            <div class="scenario-header">
              <span class="scenario-icon">🏚️</span>
              <span class="scenario-difficulty diff-beginner">Beginner</span>
            </div>
            <h3>1. Severe Earthquake</h3>
            <p>Indoor classroom/office scenario. Practice immediate "Drop, Cover, and Hold On", avoid shattering window glass, and execute post-tremor building evacuation.</p>
            <div class="scenario-meta">
              <span>Time: ~3 mins</span>
              <span>Objectives: 4 Tasks</span>
            </div>
          </div>

          <!-- Scenario 2 -->
          <div class="scenario-card" onclick="App.startScenario('flood')">
            <div class="scenario-header">
              <span class="scenario-icon">🌊</span>
              <span class="scenario-difficulty diff-intermediate">Intermediate</span>
            </div>
            <h3>2. Flash Flood & Inundation</h3>
            <p>Suburban residential street scenario. Rapidly rising floodwaters, downed power lines, and electrical hazards. Navigate to designated higher ground safely.</p>
            <div class="scenario-meta">
              <span>Time: ~3.5 mins</span>
              <span>Objectives: 4 Tasks</span>
            </div>
          </div>

          <!-- Scenario 3 -->
          <div class="scenario-card" onclick="App.startScenario('fire')">
            <div class="scenario-header">
              <span class="scenario-icon">🔥</span>
              <span class="scenario-difficulty diff-intermediate">Intermediate</span>
            </div>
            <h3>3. Indoor Structure Fire</h3>
            <p>Office complex fire scenario. Heavy smoke layer, sounding alarms, hot door handles, and blocked elevators. Crawl low and reach safe exterior muster point.</p>
            <div class="scenario-meta">
              <span>Time: ~3.5 mins</span>
              <span>Objectives: 5 Tasks</span>
            </div>
          </div>

          <!-- Scenario 4 -->
          <div class="scenario-card" onclick="App.startScenario('cyclone')">
            <div class="scenario-header">
              <span class="scenario-icon">🌪️</span>
              <span class="scenario-difficulty diff-advanced">Advanced</span>
            </div>
            <h3>4. Cyclone & Severe Gale</h3>
            <p>Destructive high-velocity cyclone. Extreme winds, airborne debris, failing windows. Secure emergency battery radio and shelter inside an interior windowless room.</p>
            <div class="scenario-meta">
              <span>Time: ~4 mins</span>
              <span>Objectives: 4 Tasks</span>
            </div>
          </div>
        </div>
      </div>
      <div class="modal-footer">
        <button class="btn" onclick="App.openModal('instructions-modal')">🎮 Controls & Guide</button>
        <button class="btn" onclick="App.openModal('achievements-modal')">🏆 Achievements</button>
        <button class="btn" onclick="App.openModal('learning-modal')">📚 Learning Centre</button>
        <button class="btn" onclick="App.openModal('settings-modal')">⚙️ Settings</button>
        <button class="btn btn-success" onclick="App.closeAllModals()">Enter Simulation ➔</button>
      </div>
    </div>
  </div>

  <!-- INSTRUCTIONS & CONTROLS MODAL -->
  <div class="modal-overlay" id="instructions-modal">
    <div class="modal-card">
      <div class="modal-header">
        <h2>🎮 TRAINING INSTRUCTIONS & DUAL CONTROLS</h2>
      </div>
      <div class="modal-body">
        <div style="display:grid; grid-template-columns:1fr 1fr; gap:20px;">
          <div>
            <h4 style="color:var(--accent-cyan); margin-bottom:10px;">🥽 Meta Quest 3S / WebXR Controls</h4>
            <ul style="list-style:none; line-height:1.9; font-size:13px;">
              <li>🔘 <strong>Right Trigger:</strong> Select, click, raycast buttons</li>
              <li>🔘 <strong>Left / Right Thumbsticks:</strong> Smooth movement & 45° snap turns</li>
              <li>🔘 <strong>A Button:</strong> Confirm / Interact with targeted objects</li>
              <li>🔘 <strong>B Button:</strong> Back / Toggle Pause Menu</li>
              <li>🔘 <strong>Grip Buttons:</strong> Grab emergency equipment (radios, extinguishers)</li>
              <li>🔘 <strong>Y Button:</strong> Show in-game emergency checklist</li>
            </ul>
          </div>
          <div>
            <h4 style="color:var(--accent-orange); margin-bottom:10px;">🖥️ Windows Desktop Controls</h4>
            <ul style="list-style:none; line-height:1.9; font-size:13px;">
              <li>⌨️ <strong>W / A / S / D:</strong> Walk Forward, Left, Backward, Right</li>
              <li>🖱️ <strong>Mouse:</strong> Look around (360° first-person view)</li>
              <li>🖱️ <strong>Left Click / E:</strong> Interact with 3D objects & pick up tools</li>
              <li>⌨️ <strong>Spacebar:</strong> Step over minor obstacles / Jump</li>
              <li>⌨️ <strong>ESC:</strong> Toggle Main Menu & Pause</li>
              <li>⌨️ <strong>F:</strong> Toggle Fullscreen Mode</li>
              <li>⌨️ <strong>H:</strong> Toggle Help Overlay</li>
            </ul>
          </div>
        </div>

        <div class="lesson-section" style="margin-top:20px;">
          <strong>Pro-Tip for VR Trainees:</strong> Point your controller laser at the interactive 3D holographic consoles in the environment or use the floating decision menus. If you feel motion sensitivity, adjust the snap-turn angle and comfort vignette in the Settings panel.
        </div>
      </div>
      <div class="modal-footer">
        <button class="btn" onclick="App.openModal('main-menu-modal')">Back to Menu</button>
        <button class="btn btn-success" onclick="App.closeAllModals()">Ready to Train</button>
      </div>
    </div>
  </div>

  <!-- LEARNING CENTRE MODAL -->
  <div class="modal-overlay" id="learning-modal">
    <div class="modal-card">
      <div class="modal-header">
        <h2>📚 DISASTER PREPAREDNESS LEARNING ACADEMY</h2>
      </div>
      <div class="modal-body">
        <div class="tabs-nav">
          <button class="tab-btn active" onclick="App.switchLearnTab('tab-earthquake')">🏚️ Earthquake</button>
          <button class="tab-btn" onclick="App.switchLearnTab('tab-flood')">🌊 Flood</button>
          <button class="tab-btn" onclick="App.switchLearnTab('tab-fire')">🔥 Fire Safety</button>
          <button class="tab-btn" onclick="App.switchLearnTab('tab-storm')">🌪️ Cyclone / Storm</button>
          <button class="tab-btn" onclick="App.switchLearnTab('tab-kit')">🎒 72-Hour Survival Kit</button>
        </div>

        <div id="tab-earthquake" class="tab-content">
          <h4>The Golden Rule: DROP, COVER, AND HOLD ON</h4>
          <p>Earthquakes strike with zero notice. Studies across seismic regions prove that running outside during tremors leads to severe injuries from falling facade bricks, glass, and roof tiles.</p>
          <ul>
            <li><strong>DROP:</strong> Drop onto your hands and knees immediately so you aren't knocked down.</li>
            <li><strong>COVER:</strong> Crawl under a sturdy table or desk. Cover your head and neck with your arms if no shelter is available.</li>
            <li><strong>HOLD ON:</strong> Hold onto your shelter until the violent shaking ceases. Be prepared for it to shift.</li>
            <li><strong>STAY AWAY FROM WINDOWS:</strong> Glass shatters outward and inward with high projectile velocity.</li>
            <li><strong>NEVER USE ELEVATORS:</strong> Seismic safety sensors or power grid cutoffs will trap you between floors.</li>
          </ul>
        </div>

        <div id="tab-flood" class="tab-content" style="display:none;">
          <h4>Turn Around, Don't Drown!</h4>
          <p>Flash floods are among the deadliest natural disasters. Just 15 cm (6 inches) of swiftly moving water can knock an adult off their feet; 30 cm (12 inches) can sweep away a car.</p>
          <ul>
            <li><strong>Seek Higher Ground:</strong> Immediately move to second stories, roofs, or designated elevated terrain.</li>
            <li><strong>Avoid Standing Water:</strong> Flood water often conceals open manholes, sharp debris, raw sewage, and deadly energized electric cables.</li>
            <li><strong>Disconnect Utilities:</strong> If safe to do so before evacuating, switch off the main electrical breaker and gas lines to prevent fires.</li>
            <li><strong>Never Drive Through Floods:</strong> The roadbed beneath the murky water may be completely washed away.</li>
          </ul>
        </div>

        <div id="tab-fire" class="tab-content" style="display:none;">
          <h4>Smoke Inhalation & Evacuation Tactics</h4>
          <p>In structural fires, toxic smoke, carbon monoxide, and superheated gases kill far more people than direct flames.</p>
          <ul>
            <li><strong>Get Low and Go:</strong> Toxic smoke rises to the ceiling, leaving a cleaner, cooler layer of breathable air 30–60 cm above the floor. Crawl underneath smoke.</li>
            <li><strong>Test Doors Before Opening:</strong> Touch the door handle or frame with the back of your hand. If hot, fire is on the other side—do not open it!</li>
            <li><strong>Use Fire Extinguishers (PASS Method):</strong> Pull pin, Aim nozzle at base of flame, Squeeze trigger, Sweep side-to-side.</li>
            <li><strong>Never Return Inside:</strong> Once evacuated to the external assembly muster zone, remain there. Never re-enter for pets or belongings.</li>
          </ul>
        </div>

        <div id="tab-storm" class="tab-content" style="display:none;">
          <h4>Severe Tropical Cyclone & Gale Defense</h4>
          <p>Extreme winds exceed 150 km/h, turning everyday items like patio chairs, tree limbs, and corrugated iron into lethal missiles.</p>
          <ul>
            <li><strong>Shelter in an Interior Room:</strong> Choose a small, windowless interior room (hallway, closet, or bathroom on the lowest floor).</li>
            <li><strong>Put as Many Walls Between You and the Outside:</strong> Exterior walls take direct impact from debris.</li>
            <li><strong>Beware the "Eye of the Storm":</strong> A sudden calm period does not mean the cyclone is over; the other eyewall will strike shortly from the reverse direction.</li>
            <li><strong>Monitor Battery-Operated Radio:</strong> Cellular cell towers often collapse; analog emergency broadcasts are the most resilient source of guidance.</li>
          </ul>
        </div>

        <div id="tab-kit" class="tab-content" style="display:none;">
          <h4>Essential 72-Hour Go-Bag Checklist</h4>
          <p>Every household should maintain a packed emergency kit capable of supporting life for at least three days:</p>
          <ul>
            <li>💧 <strong>Water:</strong> 4 liters per person per day (drinking and sanitation).</li>
            <li>🥫 <strong>Food:</strong> Non-perishable, ready-to-eat canned goods and energy bars.</li>
            <li>🔦 <strong>Lighting:</strong> LED Flashlight, hand-crank lantern, extra batteries.</li>
            <li>📻 <strong>Communication:</strong> Battery-powered or crank AM/FM NOAA emergency radio.</li>
            <li>🩹 <strong>First Aid Kit:</strong> Antiseptic wipes, sterile bandages, tourniquet, prescription medications.</li>
            <li>📑 <strong>Important Documents:</strong> Waterproof pouch containing passports, insurance, and emergency cash.</li>
          </ul>
        </div>
      </div>
      <div class="modal-footer">
        <button class="btn" onclick="App.openModal('main-menu-modal')">Back to Menu</button>
        <button class="btn btn-success" onclick="App.closeAllModals()">Understood</button>
      </div>
    </div>
  </div>

  <!-- ACHIEVEMENTS MODAL -->
  <div class="modal-overlay" id="achievements-modal">
    <div class="modal-card">
      <div class="modal-header">
        <h2>🏆 DISASTER DRILL ACHIEVEMENTS</h2>
      </div>
      <div class="modal-body">
        <p style="color:var(--text-muted); font-size:13px; margin-bottom:16px;">
          Demonstrate proficiency across crisis scenarios to unlock emergency responder credentials.
        </p>
        <div class="achievements-grid" id="achievements-list">
          <!-- Dynamically populated -->
        </div>
      </div>
      <div class="modal-footer">
        <button class="btn" onclick="App.openModal('main-menu-modal')">Back to Menu</button>
      </div>
    </div>
  </div>

  <!-- SETTINGS MODAL -->
  <div class="modal-overlay" id="settings-modal">
    <div class="modal-card">
      <div class="modal-header">
        <h2>⚙️ SIMULATOR & COMFORT SETTINGS</h2>
      </div>
      <div class="modal-body">
        <div class="setting-item">
          <div>
            <div class="setting-label">Master Sound Effects Volume</div>
            <div class="setting-desc">Adjust synthesized sirens, thunder, rumble & alerts</div>
          </div>
          <input type="range" id="setting-sfx-vol" min="0" max="100" value="80" onchange="App.updateSettings()">
        </div>

        <div class="setting-item">
          <div>
            <div class="setting-label">VR Snap Turning Angle</div>
            <div class="setting-desc">Comfort rotation angle for VR thumbsticks</div>
          </div>
          <select id="setting-snap-turn" onchange="App.updateSettings()">
            <option value="30">30 Degrees (Gentle)</option>
            <option value="45" selected>45 Degrees (Standard)</option>
            <option value="90">90 Degrees (Fast)</option>
            <option value="smooth">Smooth Continuous Turn</option>
          </select>
        </div>

        <div class="setting-item">
          <div>
            <div class="setting-label">VR Motion Comfort Vignette</div>
            <div class="setting-desc">Darkens field of view periphery during movement to prevent nausea</div>
          </div>
          <select id="setting-vignette" onchange="App.updateSettings()">
            <option value="enabled" selected>Enabled (Recommended)</option>
            <option value="disabled">Disabled</option>
          </select>
        </div>

        <div class="setting-item">
          <div>
            <div class="setting-label">Desktop Movement Speed</div>
            <div class="setting-desc">Adjust keyboard walking velocity</div>
          </div>
          <select id="setting-move-speed" onchange="App.updateSettings()">
            <option value="0.12">Slow / Cautious</option>
            <option value="0.18" selected>Standard Pace</option>
            <option value="0.25">Brisk Sprint</option>
          </select>
        </div>

        <div class="setting-item">
          <div>
            <div class="setting-label">Emergency Subtitles & Guidance HUD</div>
            <div class="setting-desc">Visual text indicators for all audio cues</div>
          </div>
          <select id="setting-subtitles" onchange="App.updateSettings()">
            <option value="on" selected>Always Display (Default)</option>
            <option value="off">Off (Hardcore)</option>
          </select>
        </div>

        <div style="margin-top:20px;">
          <button class="btn btn-danger" onclick="App.resetProgress()">⚠️ Reset All Trainee Progress & Scores</button>
        </div>
      </div>
      <div class="modal-footer">
        <button class="btn btn-success" onclick="App.closeAllModals()">Save & Close</button>
      </div>
    </div>
  </div>

  <!-- POST-SCENARIO ASSESSMENT REPORT MODAL -->
  <div class="modal-overlay" id="assessment-modal">
    <div class="modal-card">
      <div class="modal-header">
        <h2>📊 TRAINEE EMERGENCY RESPONSE ASSESSMENT</h2>
        <span class="brand-badge" id="report-scenario-badge">EARTHQUAKE</span>
      </div>
      <div class="modal-body">
        <div class="report-grid">
          <div class="score-circle-card">
            <span style="font-size:12px; font-weight:700; color:var(--text-muted); text-transform:uppercase;">Preparedness Rating</span>
            <div class="score-big" id="report-score-val">95%</div>
            <div class="score-grade diff-beginner" id="report-grade-badge">GRADE: S (EXEMPLARY)</div>
          </div>

          <div class="stats-breakdown">
            <div class="stat-row">
              <span class="label">Time Elapsed:</span>
              <span class="val" id="report-time-val">01:42</span>
            </div>
            <div class="stat-row">
              <span class="label">Critical Decisions Passed:</span>
              <span class="val" id="report-decisions-val">3 / 3</span>
            </div>
            <div class="stat-row">
              <span class="label">Hazards Avoided:</span>
              <span class="val" id="report-hazards-val">4 / 4</span>
            </div>
            <div class="stat-row">
              <span class="label">Evacuation Safety Compliance:</span>
              <span class="val" id="report-compliance-val">100%</span>
            </div>
          </div>
        </div>

        <h4 style="font-size:14px; color:var(--accent-cyan); margin-bottom:8px;">Instructor Evaluation & Feedback</h4>
        <div class="lesson-section" id="report-feedback-text">
          Excellent situational awareness. You identified the sturdy desk immediately during the violent shaking phase, protected your vital head/neck regions, avoided the shattering glass windows, and safely evacuated without taking the elevator.
        </div>

        <div style="margin-top:14px; font-size:12px; color:var(--text-muted);">
          <strong>Recommended Follow-up:</strong> Review your home family communication plan and verify smoke detector battery reserves.
        </div>
      </div>
      <div class="modal-footer">
        <button class="btn" onclick="App.restartCurrentScenario()">🔄 Retry Scenario</button>
        <button class="btn btn-success" onclick="App.returnToCommandCenter()">Command Center ➔</button>
      </div>
    </div>
  </div>

  <!-- A-FRAME 3D SCENE -->
  <a-scene
    id="main-scene"
    renderer="antialias: true; colorManagement: true; physicallyCorrectLights: false; highRefreshRate: true;"
    fog="type: linear; color: #0a0f1d; near: 8; far: 45;"
    vr-mode-ui="enabled: true">

    <!-- ASSET MANAGEMENT (Procedural and Fallbacks) -->
    <a-assets timeout="4000">
      <img id="grid-texture" src="data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='100' height='100' viewBox='0 0 100 100'><rect width='100' height='100' fill='%23111827'/><path d='M 100 0 L 0 0 0 100' fill='none' stroke='%231f2937' stroke-width='2'/></svg>">
    </a-assets>

    <!-- PLAYER RIG & CAMERA CONTROLLER -->
    <a-entity id="rig" position="0 0 0">
      <!-- Main Head & Desktop Look Camera -->
      <a-camera
        id="camera"
        position="0 1.6 0"
        look-controls="pointerLockEnabled: false"
        wasd-controls="acceleration: 25; fly: false;">
        
        <!-- Desktop Cursor Raycaster -->
        <a-cursor
          id="desktop-cursor"
          raycaster="objects: .clickable; far: 15;"
          fuse="false"
          cursor="rayOrigin: mouse"
          material="color: #00e5ff; shader: flat; opacity: 0.6"
          geometry="primitive: ring; radiusInner: 0.003; radiusOuter: 0.006"
          position="0 0 -0.8">
        </a-cursor>

        <!-- Dynamic In-VR HUD Plane attached to camera for immersive VR viewing -->
        <a-entity id="vr-floating-hud" position="0 -0.4 -1" visible="false">
          <a-plane width="1.2" height="0.25" color="#0a0f1d" opacity="0.85" material="transparent: true">
            <a-text id="vr-hud-text" value="CALAMITY SIMULATOR | VR HUD" align="center" color="#00e5ff" width="1.8" position="0 0 0.01"></a-text>
          </a-plane>
        </a-entity>
      </a-camera>

      <!-- Meta Quest 3S VR Left Controller -->
      <a-entity
        id="left-controller"
        oculus-touch-controls="hand: left"
        laser-controls="hand: left"
        raycaster="objects: .clickable; far: 12; lineColor: #00e5ff; lineOpacity: 0.7;"
        thumbstick-controls>
      </a-entity>

      <!-- Meta Quest 3S VR Right Controller -->
      <a-entity
        id="right-controller"
        oculus-touch-controls="hand: right"
        laser-controls="hand: right"
        raycaster="objects: .clickable; far: 12; lineColor: #ff9100; lineOpacity: 0.7;"
        thumbstick-controls>
      </a-entity>
    </a-entity>

    <!-- DYNAMIC LIGHTING -->
    <a-entity id="ambient-light" light="type: ambient; color: #8ab4f8; intensity: 0.65;"></a-entity>
    <a-entity id="directional-light" light="type: directional; color: #ffffff; intensity: 0.85; castShadow: false;" position="5 15 8"></a-entity>
    <a-entity id="strobe-light" light="type: point; color: #ff3d00; intensity: 0; distance: 20;" position="0 3 0"></a-entity>

    <!-- ========================================== -->
    <!-- ENVIRONMENT 0: COMMAND CENTER (MAIN HUB)    -->
    <!-- ========================================== -->
    <a-entity id="env-hub" position="0 0 0">
      <!-- Futuristic circular operations floor -->
      <a-cylinder position="0 0.05 0" radius="10" height="0.1" color="#0d1527" material="roughness: 0.8; metalness: 0.2"></a-cylinder>
      <a-ring position="0 0.11 0" rotation="-90 0 0" radius-inner="9.5" radius-outer="10" color="#00e5ff" material="shader: flat; opacity: 0.8"></a-ring>
      <a-ring position="0 0.11 0" rotation="-90 0 0" radius-inner="4.5" radius-outer="4.7" color="#ff9100" material="shader: flat; opacity: 0.6"></a-ring>

      <!-- Grid terrain floor base -->
      <a-plane position="0 0 0" rotation="-90 0 0" width="80" height="80" color="#080c14" material="roughness: 0.9"></a-plane>

      <!-- Command Center Holographic Consoles (Clickable in 3D & VR) -->
      <a-entity position="0 1.2 -3.5">
        <!-- Center Main Title Hologram -->
        <a-plane width="3.5" height="1.6" color="#040b17" opacity="0.9" material="transparent: true" class="clickable">
          <a-text value="CALAMITY SIMULATOR" align="center" color="#00e5ff" width="5.5" position="0 0.45 0.02" font="kelsonsans"></a-text>
          <a-text value="Select a Disaster Scenario to Begin Preparedness Drill" align="center" color="#ffffff" width="2.4" position="0 0.18 0.02"></a-text>
          
          <!-- Quick Interactive Buttons on the 3D Panel for VR Laser Interaction -->
          <a-entity position="-1.1 -0.3 0.03">
            <a-box class="clickable" onclick="App.startScenario('earthquake')" width="0.7" height="0.32" depth="0.04" color="#ff9100">
              <a-text value="1. EARTHQUAKE" align="center" color="#000" width="1.6" position="0 0 0.03"></a-text>
            </a-box>
          </a-entity>

          <a-entity position="-0.35 -0.3 0.03">
            <a-box class="clickable" onclick="App.startScenario('flood')" width="0.7" height="0.32" depth="0.04" color="#00e5ff">
              <a-text value="2. FLOOD" align="center" color="#000" width="1.6" position="0 0 0.03"></a-text>
            </a-box>
          </a-entity>

          <a-entity position="0.4 -0.3 0.03">
            <a-box class="clickable" onclick="App.startScenario('fire')" width="0.7" height="0.32" depth="0.04" color="#ff3d00">
              <a-text value="3. FIRE" align="center" color="#fff" width="1.6" position="0 0 0.03"></a-text>
            </a-box>
          </a-entity>

          <a-entity position="1.15 -0.3 0.03">
            <a-box class="clickable" onclick="App.startScenario('cyclone')" width="0.7" height="0.32" depth="0.04" color="#ffd600">
              <a-text value="4. CYCLONE" align="center" color="#000" width="1.6" position="0 0 0.03"></a-text>
            </a-box>
          </a-entity>
        </a-plane>

        <!-- Hologram Pedestal Base -->
        <a-cylinder position="0 -1.15 0" radius="0.3" height="1.1" color="#162238" material="metalness: 0.5"></a-cylinder>
      </a-entity>

      <!-- Decorative Pillars & Architectural Canopy -->
      <a-cylinder position="-6 3 -4" radius="0.4" height="6" color="#1a263c"></a-cylinder>
      <a-cylinder position="6 3 -4" radius="0.4" height="6" color="#1a263c"></a-cylinder>
      <a-box position="0 5.8 -4" width="13" height="0.4" depth="1.2" color="#111c2e"></a-box>
      <a-text value="CRISIS RESPONSE OPERATIONS DIVISION" align="center" color="#00e5ff" width="6" position="0 5.8 -3.3"></a-text>
    </a-entity>

    <!-- ========================================== -->
    <!-- ENVIRONMENT 1: EARTHQUAKE (INDOOR ROOM)    -->
    <!-- ========================================== -->
    <a-entity id="env-earthquake" position="0 0 0" visible="false">
      <!-- Classroom / Office Room Structure -->
      <!-- Floor -->
      <a-plane position="0 0.01 -2" rotation="-90 0 0" width="14" height="12" color="#64748b" material="roughness: 0.9"></a-plane>
      <!-- Ceiling -->
      <a-plane id="eq-ceiling" position="0 3.6 -2" rotation="90 0 0" width="14" height="12" color="#cbd5e1"></a-plane>
      <!-- Back Wall with Blackboard -->
      <a-box position="0 1.8 -7.9" width="14" height="3.6" depth="0.2" color="#e2e8f0">
        <a-box position="0 0.2 0.15" width="6" height="1.8" depth="0.04" color="#1e293b">
          <a-text value="SAFETY DRILL: EARTHQUAKE SAFETY" align="center" color="#f8fafc" width="4.5" position="0 0.5 0.03"></a-text>
          <a-text value="1. Drop onto your knees\n2. Cover head & neck under table\n3. Hold On to legs until shaking stops" align="center" color="#94a3b8" width="3" position="0 -0.1 0.03"></a-text>
        </a-box>
      </a-box>
      <!-- Left Wall with Large Windows (HAZARD) -->
      <a-box position="-6.9 1.8 -2" rotation="0 90 0" width="12" height="3.6" depth="0.2" color="#e2e8f0">
        <!-- Windows -->
        <a-box id="eq-window" class="clickable" onclick="App.onObjectInteracted('eq-window')" position="0 0.4 0.15" width="7" height="1.8" depth="0.05" color="#38bdf8" material="opacity: 0.45; transparent: true">
          <a-text value="⚠️ HAZARD: Shatterable Glass Window" align="center" color="#ff3d00" width="3" position="0 -0.6 0.04"></a-text>
        </a-box>
      </a-box>
      <!-- Right Wall with Bookshelf & Exit Door -->
      <a-box position="6.9 1.8 -2" rotation="0 -90 0" width="12" height="3.6" depth="0.2" color="#e2e8f0">
        <!-- Exit Door -->
        <a-box id="eq-exit-door" class="clickable" onclick="App.onObjectInteracted('eq-exit-door')" position="2 -0.3 0.15" width="1.2" height="2.2" depth="0.08" color="#15803d">
          <a-text value="EMERGENCY EXIT" align="center" color="#fff" width="1.8" position="0 0.7 0.06"></a-text>
        </a-box>
      </a-box>

      <!-- Furniture Items -->
      <!-- Sturdy Desk (Safe Shelter Target) -->
      <a-entity id="eq-sturdy-desk" position="0 0 -3" class="clickable" onclick="App.onObjectInteracted('eq-desk')">
        <!-- Table Top -->
        <a-box position="0 0.75 0" width="2" height="0.1" depth="1.2" color="#b45309"></a-box>
        <!-- 4 Table Legs -->
        <a-cylinder position="-0.9 0.35 -0.5" radius="0.04" height="0.7" color="#334155"></a-cylinder>
        <a-cylinder position="0.9 0.35 -0.5" radius="0.04" height="0.7" color="#334155"></a-cylinder>
        <a-cylinder position="-0.9 0.35 0.5" radius="0.04" height="0.7" color="#334155"></a-cylinder>
        <a-cylinder position="0.9 0.35 0.5" radius="0.04" height="0.7" color="#334155"></a-cylinder>
        <!-- Marker Text -->
        <a-text value="▼ SAFE COVER: Heavy Oak Desk (Click to Drop, Cover, Hold)" align="center" color="#00e676" width="3.5" position="0 1.15 0"></a-text>
      </a-entity>

      <!-- Falling Bookshelf & Books (Reacting during shaking) -->
      <a-entity id="eq-bookshelf" position="-5 0 -5">
        <a-box position="0 1.2 0" width="1.2" height="2.4" depth="0.5" color="#78350f"></a-box>
        <!-- Shelf tiers -->
        <a-box id="eq-book-1" position="0 1.6 0.1" width="0.9" height="0.25" depth="0.3" color="#dc2626"></a-box>
        <a-box id="eq-book-2" position="0 1.1 0.1" width="0.8" height="0.25" depth="0.3" color="#2563eb"></a-box>
      </a-entity>

      <!-- Hanging Overhead Light (Swinging during quake) -->
      <a-entity id="eq-hanging-light" position="0 3.5 -3">
        <a-cylinder position="0 -0.5 0" radius="0.02" height="1" color="#475569"></a-cylinder>
        <a-box position="0 -1.05 0" width="1.5" height="0.1" depth="0.3" color="#f8fafc">
          <a-entity light="type: point; color: #fffbeb; intensity: 0.8; distance: 6;"></a-entity>
        </a-box>
      </a-entity>
    </a-entity>

    <!-- ========================================== -->
    <!-- ENVIRONMENT 2: FLOOD (SUBURBAN STREET)     -->
    <!-- ========================================== -->
    <a-entity id="env-flood" position="0 0 0" visible="false">
      <!-- Street Roadway -->
      <a-plane position="0 0.02 -5" rotation="-90 0 0" width="12" height="30" color="#334155" material="roughness: 0.9"></a-plane>
      <!-- Sidewalks -->
      <a-box position="-6.5 0.15 -5" width="2" height="0.3" depth="30" color="#94a3b8"></a-box>
      <a-box position="6.5 0.15 -5" width="2" height="0.3" depth="30" color="#94a3b8"></a-box>

      <!-- Suburban Houses -->
      <a-entity position="-10 0 -3">
        <a-box position="0 2 0" width="5" height="4" depth="6" color="#f1f5f9"></a-box>
        <a-cone position="0 4.8 0" radius-bottom="4.2" radius-top="0.2" height="1.8" color="#991b1b"></a-cone>
      </a-entity>
      <a-entity position="10 0 -4">
        <a-box position="0 2 0" width="5" height="4" depth="6" color="#fef3c7"></a-box>
        <a-cone position="0 4.8 0" radius-bottom="4.2" radius-top="0.2" height="1.8" color="#1e3a8a"></a-cone>
      </a-entity>

      <!-- DANGER: Downed Electric Power Pole & Transformer with Sparks -->
      <a-entity id="flood-hazard-pole" position="-3 0 -6" class="clickable" onclick="App.onObjectInteracted('flood-hazard')">
        <a-cylinder position="0 1.2 0" rotation="0 0 65" radius="0.12" height="3.8" color="#713f12"></a-cylinder>
        <a-box position="1.4 0.3 0" width="0.5" height="0.5" depth="0.5" color="#475569"></a-box>
        <!-- Spark glow effect -->
        <a-sphere id="flood-spark" position="1.4 0.4 0" radius="0.15" color="#00e5ff" material="shader: flat; opacity: 0.9">
          <a-entity light="type: point; color: #00e5ff; intensity: 1.2; distance: 4;"></a-entity>
        </a-sphere>
        <a-text value="⚡ EXTREME HAZARD: Submerged High-Voltage Wire!" align="center" color="#ff3d00" width="3" position="0 1.9 0"></a-text>
      </a-entity>

      <!-- Rising Water Level Plane -->
      <a-plane
        id="flood-water-mesh"
        position="0 0.1 -5"
        rotation="-90 0 0"
        width="30"
        height="35"
        color="#0284c7"
        material="roughness: 0.1; metalness: 0.7; opacity: 0.7; transparent: true">
      </a-plane>

      <!-- Safe High Ground Elevation (Mound / Hilltop Refuge) -->
      <a-entity id="flood-high-ground" position="0 0 -16" class="clickable" onclick="App.onObjectInteracted('flood-safe-hill')">
        <a-box position="0 1.5 0" width="8" height="3" depth="6" color="#166534"></a-box>
        <a-box position="0 3.05 0" width="6" height="0.1" depth="4" color="#22c55e"></a-box>
        <!-- Sandbags around high ground -->
        <a-cylinder position="-2.5 3.2 -1.5" rotation="0 0 90" radius="0.18" height="1.2" color="#d97706"></a-cylinder>
        <a-cylinder position="2.5 3.2 -1.5" rotation="0 0 90" radius="0.18" height="1.2" color="#d97706"></a-cylinder>
        <a-text value="▲ HIGHER GROUND: Emergency Sandbagged Relief Summit" align="center" color="#ffffff" width="4" position="0 4.2 0"></a-text>
      </a-entity>
    </a-entity>

    <!-- ========================================== -->
    <!-- ENVIRONMENT 3: FIRE EMERGENCY (OFFICE/CORRIDOR) -->
    <!-- ========================================== -->
    <a-entity id="env-fire" position="0 0 0" visible="false">
      <!-- Corridor Floor -->
      <a-plane position="0 0.01 -6" rotation="-90 0 0" width="5" height="22" color="#475569"></a-plane>
      <!-- Corridor Ceiling with Smoke Plume -->
      <a-plane position="0 3.2 -6" rotation="90 0 0" width="5" height="22" color="#1e293b"></a-plane>
      <a-plane id="fire-smoke-ceiling" position="0 2.7 -6" rotation="90 0 0" width="4.9" height="21.8" color="#0f172a" material="opacity: 0.85; transparent: true"></a-plane>

      <!-- Corridor Walls -->
      <a-box position="-2.5 1.6 -6" width="0.2" height="3.2" depth="22" color="#cbd5e1"></a-box>
      <a-box position="2.5 1.6 -6" width="0.2" height="3.2" depth="22" color="#cbd5e1"></a-box>

      <!-- Fire Alarm Pull Station -->
      <a-box id="fire-pull-station" class="clickable" onclick="App.onObjectInteracted('fire-alarm-pull')" position="-2.35 1.4 -2" width="0.1" height="0.25" depth="0.2" color="#dc2626">
        <a-text value="FIRE ALARM" align="center" color="#fff" width="1" position="0.08 0 0" rotation="0 90 0"></a-text>
      </a-box>

      <!-- Elevator (FATAL HAZARD DURING FIRE) -->
      <a-entity id="fire-elevator" position="-2.35 1.4 -5" class="clickable" onclick="App.onObjectInteracted('fire-elevator')">
        <a-box width="0.1" height="2.4" depth="1.8" color="#64748b"></a-box>
        <a-box position="0.06 0 0" width="0.02" height="2.2" depth="1.6" color="#334155"></a-box>
        <a-text value="❌ ELEVATOR (DO NOT USE IN FIRE)" align="center" color="#ff3d00" width="2" position="0.1 1.4 0" rotation="0 90 0"></a-text>
      </a-entity>

      <!-- Fire Extinguisher on wall (Interactable Item) -->
      <a-entity id="fire-extinguisher" position="2.35 1.2 -3" class="clickable" onclick="App.onObjectInteracted('fire-extinguisher')">
        <a-cylinder radius="0.1" height="0.55" color="#dc2626"></a-cylinder>
        <a-cylinder position="0 0.3 0" radius="0.04" height="0.15" color="#1e293b"></a-cylinder>
        <a-text value="🧯 ABC Fire Extinguisher (Click to grab)" align="center" color="#00e5ff" width="2.2" position="-0.1 0.5 0" rotation="0 -90 0"></a-text>
      </a-entity>

      <!-- Closed Doorway with Heat Signature -->
      <a-entity id="fire-hot-door" position="0 1.2 -11" class="clickable" onclick="App.onObjectInteracted('fire-door-test')">
        <a-box width="1.6" height="2.4" depth="0.1" color="#78350f"></a-box>
        <a-sphere id="fire-door-handle" position="0.6 0 0.08" radius="0.06" color="#f97316"></a-sphere>
        <a-text value="🚪 Office Door (Feel handle with back of hand)" align="center" color="#ffd600" width="2.5" position="0 1.4 0.1"></a-text>
      </a-entity>

      <!-- Safe Exterior Emergency Fire Stairs (Evacuation Route) -->
      <a-entity id="fire-safe-exit" position="0 1.2 -16" class="clickable" onclick="App.onObjectInteracted('fire-exit-stairs')">
        <a-box width="2" height="2.6" depth="0.1" color="#15803d"></a-box>
        <a-text value="🟩 EMERGENCY STAIRWELL (Safe Route to Assembly Point)" align="center" color="#ffffff" width="3" position="0 0 0.15"></a-text>
      </a-entity>
    </a-entity>

    <!-- ========================================== -->
    <!-- ENVIRONMENT 4: CYCLONE / SEVERE STORM      -->
    <!-- ========================================== -->
    <a-entity id="env-cyclone" position="0 0 0" visible="false">
      <!-- Dark Wet Yard Ground -->
      <a-plane position="0 0.01 -5" rotation="-90 0 0" width="35" height="35" color="#1e293b" material="roughness: 0.95"></a-plane>

      <!-- Cyclone Storm Rain / Debris Volume Simulation -->
      <a-entity id="storm-debris-group"></a-entity>

      <!-- Battered Residence Exterior -->
      <a-entity position="0 0 -6">
        <!-- House Shell -->
        <a-box position="0 2 0" width="9" height="4" depth="7" color="#475569"></a-box>
        <a-cone position="0 4.8 0" radius-bottom="6.8" radius-top="0.2" height="1.8" color="#334155"></a-cone>

        <!-- Large Exposed Patio Window (DANGER: Shatter risk from wind) -->
        <a-box id="cyclone-window-hazard" class="clickable" onclick="App.onObjectInteracted('cyclone-window')" position="-2.4 1.8 3.55" width="2.2" height="1.8" depth="0.05" color="#94a3b8" material="opacity: 0.5; transparent: true">
          <a-text value="⚠️ HAZARD: Unshuttered Window Facing Gale Winds" align="center" color="#ff3d00" width="2.6" position="0 1.1 0.04"></a-text>
        </a-box>

        <!-- Emergency Battery-Powered Radio inside Front Entryway -->
        <a-entity id="cyclone-radio-item" position="0 1 2.5" class="clickable" onclick="App.onObjectInteracted('cyclone-radio')">
          <a-box width="0.4" height="0.25" depth="0.15" color="#ca8a04"></a-box>
          <a-cylinder position="0.15 0.25 0" radius="0.01" height="0.3" color="#e2e8f0"></a-cylinder>
          <a-text value="📻 Emergency NOAA/Analog Weather Radio" align="center" color="#00e5ff" width="2" position="0 0.45 0"></a-text>
        </a-entity>

        <!-- Reinforced Interior Safe Room (Closet / Hallway without Windows) -->
        <a-entity id="cyclone-safe-room" position="2.2 1.2 0" class="clickable" onclick="App.onObjectInteracted('cyclone-safe-bunker')">
          <a-box width="2" height="2.4" depth="2" color="#0f172a"></a-box>
          <a-text value="🛡️ REINFORCED INTERIOR ROOM\n(Windowless Storm Sanctuary)" align="center" color="#22c55e" width="2.6" position="0 1.5 1.05"></a-text>
        </a-entity>
      </a-entity>

      <!-- Trees that sway in fierce winds -->
      <a-entity id="cyclone-tree-1" position="-6 0 -3">
        <a-cylinder position="0 1.5 0" radius="0.25" height="3" color="#451a03"></a-cylinder>
        <a-cone position="0 3.8 0" radius-bottom="1.6" radius-top="0.1" height="2.8" color="#14532d"></a-cone>
      </a-entity>
      <a-entity id="cyclone-tree-2" position="6 0 -2">
        <a-cylinder position="0 1.5 0" radius="0.25" height="3" color="#451a03"></a-cylinder>
        <a-cone position="0 3.8 0" radius-bottom="1.6" radius-top="0.1" height="2.8" color="#14532d"></a-cone>
      </a-entity>
    </a-entity>

  </a-scene>

  <!-- ======================================================== -->
  <!-- JAVASCRIPT GAME ENGINE, AUDIO SYNTH, & STATE CONTROLLER -->
  <!-- ======================================================== -->
  <script>
    /**
     * CALAMITY SIMULATOR - High Fidelity WebXR & Desktop Emergency Trainer
     * Self-contained JavaScript Game Architecture
     */

    // --- PROCEDURAL WEB AUDIO SYNTHESIZER ---
    // Generates realistic earthquake rumbles, fire alarms, thunder, sirens, and UI SFX without external audio files!
    const AudioEngine = {
      ctx: null,
      sfxVolume: 0.8,

      init() {
        if (!this.ctx) {
          const AudioContext = window.AudioContext || window.webkitAudioContext;
          this.ctx = new AudioContext();
        }
        if (this.ctx.state === 'suspended') {
          this.ctx.resume();
        }
      },

      playUiClick() {
        this.init();
        const osc = this.ctx.createOscillator();
        const gain = this.ctx.createGain();
        osc.type = 'sine';
        osc.frequency.setValueAtTime(800, this.ctx.currentTime);
        osc.frequency.exponentialRampToValueAtTime(1400, this.ctx.currentTime + 0.08);
        gain.gain.setValueAtTime(0.15 * this.sfxVolume, this.ctx.currentTime);
        gain.gain.exponentialRampToValueAtTime(0.001, this.ctx.currentTime + 0.08);
        osc.connect(gain);
        gain.connect(this.ctx.destination);
        osc.start();
        osc.stop(this.ctx.currentTime + 0.08);
      },

      playSuccessTone() {
        this.init();
        const now = this.ctx.currentTime;
        [523.25, 659.25, 783.99, 1046.50].forEach((freq, i) => {
          const osc = this.ctx.createOscillator();
          const gain = this.ctx.createGain();
          osc.type = 'triangle';
          osc.frequency.setValueAtTime(freq, now + (i * 0.08));
          gain.gain.setValueAtTime(0.2 * this.sfxVolume, now + (i * 0.08));
          gain.gain.exponentialRampToValueAtTime(0.001, now + (i * 0.08) + 0.25);
          osc.connect(gain);
          gain.connect(this.ctx.destination);
          osc.start(now + (i * 0.08));
          osc.stop(now + (i * 0.08) + 0.25);
        });
      },

      playWarningBuzzer() {
        this.init();
        const now = this.ctx.currentTime;
        const osc = this.ctx.createOscillator();
        const gain = this.ctx.createGain();
        osc.type = 'sawtooth';
        osc.frequency.setValueAtTime(180, now);
        osc.frequency.setValueAtTime(140, now + 0.15);
        gain.gain.setValueAtTime(0.25 * this.sfxVolume, now);
        gain.gain.exponentialRampToValueAtTime(0.001, now + 0.35);
        osc.connect(gain);
        gain.connect(this.ctx.destination);
        osc.start(now);
        osc.stop(now + 0.35);
      },

      // Earthquake deep tectonic low frequency rumble
      startEarthquakeRumble() {
        this.init();
        if (this.eqOsc) return;
        const now = this.ctx.currentTime;
        this.eqOsc = this.ctx.createOscillator();
        this.eqGain = this.ctx.createGain();
        this.eqOsc.type = 'sawtooth';
        this.eqOsc.frequency.setValueAtTime(45, now);
        
        // Lowpass filter to muffle into subterranean rumble
        const filter = this.ctx.createBiquadFilter();
        filter.type = 'lowpass';
        filter.frequency.setValueAtTime(90, now);

        this.eqGain.gain.setValueAtTime(0.01, now);
        this.eqGain.gain.linearRampToValueAtTime(0.4 * this.sfxVolume, now + 2);

        this.eqOsc.connect(filter);
        filter.connect(this.eqGain);
        this.eqGain.connect(this.ctx.destination);
        this.eqOsc.start(now);
      },

      stopEarthquakeRumble() {
        if (this.eqGain && this.eqOsc) {
          const now = this.ctx.currentTime;
          this.eqGain.gain.linearRampToValueAtTime(0.001, now + 1.5);
          setTimeout(() => {
            if (this.eqOsc) {
              this.eqOsc.stop();
              this.eqOsc.disconnect();
              this.eqOsc = null;
            }
          }, 1600);
        }
      },

      // Pulsing industrial fire alarm klaxon
      startFireAlarm() {
        this.init();
        if (this.alarmInterval) return;
        let toggle = false;
        this.alarmInterval = setInterval(() => {
          const now = this.ctx.currentTime;
          const osc = this.ctx.createOscillator();
          const gain = this.ctx.createGain();
          osc.type = 'square';
          osc.frequency.setValueAtTime(toggle ? 950 : 750, now);
          gain.gain.setValueAtTime(0.2 * this.sfxVolume, now);
          gain.gain.exponentialRampToValueAtTime(0.01, now + 0.35);
          osc.connect(gain);
          gain.connect(this.ctx.destination);
          osc.start(now);
          osc.stop(now + 0.35);
          toggle = !toggle;
        }, 500);
      },

      stopFireAlarm() {
        if (this.alarmInterval) {
          clearInterval(this.alarmInterval);
          this.alarmInterval = null;
        }
      },

      // Severe hurricane howling wind synth
      startWindHowl() {
        this.init();
        if (this.windNode) return;
        // White noise generator
        const bufferSize = this.ctx.sampleRate * 2;
        const buffer = this.ctx.createBuffer(1, bufferSize, this.ctx.sampleRate);
        const output = buffer.getChannelData(0);
        for (let i = 0; i < bufferSize; i++) {
          output[i] = Math.random() * 2 - 1;
        }
        this.windNode = this.ctx.createBufferSource();
        this.windNode.buffer = buffer;
        this.windNode.loop = true;

        const filter = this.ctx.createBiquadFilter();
        filter.type = 'bandpass';
        filter.frequency.setValueAtTime(450, this.ctx.currentTime);
        filter.Q.setValueAtTime(4.0, this.ctx.currentTime);

        this.windGain = this.ctx.createGain();
        this.windGain.gain.setValueAtTime(0.01, this.ctx.currentTime);
        this.windGain.gain.linearRampToValueAtTime(0.3 * this.sfxVolume, this.ctx.currentTime + 3);

        this.windNode.connect(filter);
        filter.connect(this.windGain);
        this.windGain.connect(this.ctx.destination);
        this.windNode.start();
      },

      stopWindHowl() {
        if (this.windGain && this.windNode) {
          const now = this.ctx.currentTime;
          this.windGain.gain.linearRampToValueAtTime(0.001, now + 1);
          setTimeout(() => {
            if (this.windNode) {
              this.windNode.stop();
              this.windNode.disconnect();
              this.windNode = null;
            }
          }, 1100);
        }
      },

      // Thunderclap boom
      playThunder() {
        this.init();
        const now = this.ctx.currentTime;
        const osc = this.ctx.createOscillator();
        const gain = this.ctx.createGain();
        osc.type = 'triangle';
        osc.frequency.setValueAtTime(80, now);
        osc.frequency.exponentialRampToValueAtTime(25, now + 1.5);
        gain.gain.setValueAtTime(0.4 * this.sfxVolume, now);
        gain.gain.exponentialRampToValueAtTime(0.001, now + 1.8);
        osc.connect(gain);
        gain.connect(this.ctx.destination);
        osc.start(now);
        osc.stop(now + 1.8);
      }
    };

    // --- MAIN SIMULATOR APPLICATION CONTROLLER ---
    const App = {
      // Game State
      currentScenario: null, // 'hub', 'earthquake', 'flood', 'fire', 'cyclone'
      currentDifficulty: 'beginner',
      elapsedSeconds: 0,
      timerInterval: null,
      safetyScore: 100,
      decisionsMade: 0,
      correctDecisions: 0,
      hazardsEncountered: 0,
      tasksCompleted: 0,
      totalScenarioTasks: 4,
      scenarioStep: 0,
      activeDecisionPending: false,

      // Achievements Data
      achievements: [
        { id: 'first_step', name: 'Ready Responder', desc: 'Commenced your first disaster simulation drill', icon: '🎖️', unlocked: false },
        { id: 'eq_master', name: 'Seismic Survivor', desc: 'Successfully performed Drop, Cover, and Hold in the Earthquake', icon: '🏚️', unlocked: false },
        { id: 'flood_master', name: 'High Ground Pioneer', desc: 'Avoided electrical flood currents and reached elevated safety', icon: '🌊', unlocked: false },
        { id: 'fire_master', name: 'Smoke Navigator', desc: 'Tested door heat and safely exited without taking elevators', icon: '🔥', unlocked: false },
        { id: 'storm_master', name: 'Cyclone Sentinel', desc: 'Secured emergency radio and fortified the windowless room', icon: '🌪️', unlocked: false },
        { id: 'flawless_score', name: 'Crisis Commander', desc: 'Completed any emergency drill with a 100% safety score', icon: '⭐', unlocked: false }
      ],

      // Scenario Definitions & Step-by-step logic
      scenariosData: {
        earthquake: {
          title: 'SEVERE EARTHQUAKE',
          badge: 'EARTHQUAKE',
          envId: 'env-earthquake',
          initialPos: { x: 0, y: 1.6, z: 1 },
          steps: [
            {
              objective: 'Classroom is calm. Review environment and identify potential earthquake shelters.',
              instruction: 'Look around the room using your mouse or VR headset.',
              triggerAfter: 3500,
              action: () => App.triggerEarthquakeEvent()
            }
          ]
        },
        flood: {
          title: 'FLASH FLOOD & INUNDATION',
          badge: 'FLOOD',
          envId: 'env-flood',
          initialPos: { x: 0, y: 1.6, z: 5 },
          steps: [
            {
              objective: 'Torrential downpour has triggered flash flood warnings. Assess street hazards.',
              instruction: 'Notice rising floodwaters and spot downed utility lines.',
              triggerAfter: 3000,
              action: () => App.triggerFloodEvent()
            }
          ]
        },
        fire: {
          title: 'INDOOR STRUCTURE FIRE',
          badge: 'FIRE',
          envId: 'env-fire',
          initialPos: { x: 0, y: 1.6, z: 2 },
          steps: [
            {
              objective: 'A commercial fire alarm has been triggered. Locate nearest safe egress path.',
              instruction: 'Smoke is beginning to accumulate near the ceiling.',
              triggerAfter: 2500,
              action: () => App.triggerFireEvent()
            }
          ]
        },
        cyclone: {
          title: 'CYCLONE & SEVERE GALE',
          badge: 'CYCLONE',
          envId: 'env-cyclone',
          initialPos: { x: 0, y: 1.6, z: 3 },
          steps: [
            {
              objective: 'Category 4 Cyclone winds approaching residential area. Secure shelter.',
              instruction: 'Look for the emergency radio and reinforce structural safety.',
              triggerAfter: 3000,
              action: () => App.triggerCycloneEvent()
            }
          ]
        }
      },

      init() {
        console.log("Initializing CALAMITY SIMULATOR WebXR/Desktop engine...");
        this.loadSavedData();
        this.renderAchievements();
        this.setupEventListeners();
        this.detectVR();
        this.startHudTimer();
      },

      loadSavedData() {
        try {
          const saved = localStorage.getItem('calamity_sim_achievements');
          if (saved) {
            const parsed = JSON.parse(saved);
            this.achievements.forEach(a => {
              if (parsed[a.id]) a.unlocked = true;
            });
          }
        } catch (e) {
          console.warn("Storage not accessible:", e);
        }
      },

      saveAchievements() {
        try {
          const data = {};
          this.achievements.forEach(a => { data[a.id] = a.unlocked; });
          localStorage.setItem('calamity_sim_achievements', JSON.stringify(data));
        } catch (e) {}
      },

      unlockAchievement(id) {
        const ach = this.achievements.find(a => a.id === id);
        if (ach && !ach.unlocked) {
          ach.unlocked = true;
          this.saveAchievements();
          this.renderAchievements();
          this.showEmergencyAlert(`🏆 ACHIEVEMENT UNLOCKED: ${ach.name}!`, 3500);
          AudioEngine.playSuccessTone();
        }
      },

      detectVR() {
        const scene = document.querySelector('a-scene');
        if (scene) {
          scene.addEventListener('enter-vr', () => {
            console.log("Entered VR mode! Enabling laser controllers & VR floating HUD.");
            document.getElementById('vr-vignette').style.display = 'block';
            document.getElementById('vr-floating-hud').setAttribute('visible', 'true');
            // Hide 2D crosshair in VR
            document.getElementById('desktop-crosshair').style.display = 'none';
          });
          scene.addEventListener('exit-vr', () => {
            console.log("Exited VR mode.");
            document.getElementById('vr-floating-hud').setAttribute('visible', 'false');
            document.getElementById('desktop-crosshair').style.display = 'flex';
          });
        }
      },

      setupEventListeners() {
        // Desktop keyboard controls
        window.addEventListener('keydown', (e) => {
          if (e.key === 'Escape') {
            this.toggleMenu();
          } else if (e.key === 'f' || e.key === 'F') {
            this.toggleFullscreen();
          } else if (e.key === 'h' || e.key === 'H') {
            this.openModal('instructions-modal');
          } else if (e.key === 'e' || e.key === 'E') {
            // Trigger raycast interaction in desktop center view
            this.triggerCenterDesktopInteraction();
          }
        });

        // Controller Raycaster crosshair hover styling
        const cursor = document.getElementById('desktop-cursor');
        if (cursor) {
          cursor.addEventListener('raycaster-intersected', () => {
            document.body.classList.add('crosshair-hover');
          });
          cursor.addEventListener('raycaster-intersected-cleared', () => {
            document.body.classList.remove('crosshair-hover');
          });
        }

        // WebXR VR Touch Controller Button Listeners (Quest 3S)
        const setupControllerListeners = (controllerId) => {
          const el = document.getElementById(controllerId);
          if (!el) return;
          el.addEventListener('triggerdown', () => AudioEngine.playUiClick());
          el.addEventListener('abuttondown', () => this.onVrAButtonPressed());
          el.addEventListener('bbuttondown', () => this.toggleMenu());
          el.addEventListener('xbuttondown', () => this.openModal('learning-modal'));
          el.addEventListener('ybuttondown', () => this.openModal('instructions-modal'));
        };

        setupControllerListeners('left-controller');
        setupControllerListeners('right-controller');
      },

      startHudTimer() {
        if (this.timerInterval) clearInterval(this.timerInterval);
        this.timerInterval = setInterval(() => {
          if (this.currentScenario && this.currentScenario !== 'hub') {
            this.elapsedSeconds++;
            const mins = String(Math.floor(this.elapsedSeconds / 60)).padStart(2, '0');
            const secs = String(this.elapsedSeconds % 60).padStart(2, '0');
            document.getElementById('hud-cur-time').textContent = `${mins}:${secs}`;
          }
        }, 1000);
      },

      showEmergencyAlert(text, duration = 3000) {
        const el = document.getElementById('emergency-alert-banner');
        el.textContent = text;
        el.style.display = 'block';
        if (this.alertTimeout) clearTimeout(this.alertTimeout);
        this.alertTimeout = setTimeout(() => {
          el.style.display = 'none';
        }, duration);
      },

      setObjective(title, task) {
        document.getElementById('obj-title').textContent = title;
        document.getElementById('obj-task').textContent = task;
        document.getElementById('hud-objective').style.display = 'block';
        
        // Also mirror to VR floating HUD
        const vrText = document.getElementById('vr-hud-text');
        if (vrText) {
          vrText.setAttribute('value', `${title}: ${task}`);
        }
      },

      updateSafetyScore(change) {
        this.safetyScore = Math.max(0, Math.min(100, this.safetyScore + change));
        const el = document.getElementById('hud-cur-score');
        el.textContent = `${this.safetyScore}%`;
        if (this.safetyScore < 60) {
          el.style.color = 'var(--accent-red)';
        } else if (this.safetyScore < 85) {
          el.style.color = 'var(--accent-orange)';
        } else {
          el.style.color = 'var(--accent-cyan)';
        }
      },

      // Navigation & Modal Handling
      openModal(modalId) {
        AudioEngine.playUiClick();
        document.querySelectorAll('.modal-overlay').forEach(m => m.classList.remove('active'));
        const target = document.getElementById(modalId);
        if (target) target.classList.add('active');
      },

      closeAllModals() {
        AudioEngine.playUiClick();
        document.querySelectorAll('.modal-overlay').forEach(m => m.classList.remove('active'));
      },

      toggleMenu() {
        const menu = document.getElementById('main-menu-modal');
        if (menu.classList.contains('active')) {
          this.closeAllModals();
        } else {
          this.openModal('main-menu-modal');
        }
      },

      toggleFullscreen() {
        if (!document.fullscreenElement) {
          document.documentElement.requestFullscreen().catch(() => {});
        } else {
          document.exitFullscreen().catch(() => {});
        }
      },

      // SCENARIO STARTING & SWITCHING
      startScenario(scenarioKey) {
        AudioEngine.playUiClick();
        this.unlockAchievement('first_step');
        this.closeAllModals();
        this.currentScenario = scenarioKey;
        this.elapsedSeconds = 0;
        this.safetyScore = 100;
        this.decisionsMade = 0;
        this.correctDecisions = 0;
        this.hazardsEncountered = 0;
        this.tasksCompleted = 0;
        this.scenarioStep = 0;
        this.updateSafetyScore(0);

        // Update Top HUD
        const data = this.scenariosData[scenarioKey];
        document.getElementById('hud-cur-scenario').textContent = data.title;
        document.getElementById('btn-quick-abort').style.display = 'inline-flex';

        // Hide all 3D environment models and show the chosen one
        ['env-hub', 'env-earthquake', 'env-flood', 'env-fire', 'env-cyclone'].forEach(id => {
          const el = document.getElementById(id);
          if (el) el.setAttribute('visible', 'false');
        });

        const activeEnv = document.getElementById(data.envId);
        if (activeEnv) activeEnv.setAttribute('visible', 'true');

        // Reset Player Rig Position
        const rig = document.getElementById('rig');
        if (rig && data.initialPos) {
          rig.setAttribute('position', `${data.initialPos.x} ${data.initialPos.y} ${data.initialPos.z}`);
        }

        // Reset ambient fog / sky color to match scenario
        const scene = document.querySelector('a-scene');
        if (scenarioKey === 'earthquake') {
          scene.setAttribute('fog', 'color: #1e293b; near: 6; far: 30;');
        } else if (scenarioKey === 'flood') {
          scene.setAttribute('fog', 'color: #334155; near: 8; far: 40;');
        } else if (scenarioKey === 'fire') {
          scene.setAttribute('fog', 'color: #1f120e; near: 2; far: 18;');
        } else if (scenarioKey === 'cyclone') {
          scene.setAttribute('fog', 'color: #0f172a; near: 4; far: 25;');
        }

        // Set initial objective and trigger timed scenario events
        this.setObjective(`STEP 1: ${data.title}`, data.steps[0].objective);
        if (data.steps[0].action) {
          setTimeout(() => data.steps[0].action(), data.steps[0].triggerAfter || 2000);
        }
      },

      returnToCommandCenter() {
        AudioEngine.playUiClick();
        this.stopAllScenarioSimulations();
        this.currentScenario = 'hub';
        document.getElementById('hud-cur-scenario').textContent = 'COMMAND CENTER';
        document.getElementById('btn-quick-abort').style.display = 'none';
        document.getElementById('hud-objective').style.display = 'none';

        ['env-earthquake', 'env-flood', 'env-fire', 'env-cyclone'].forEach(id => {
          const el = document.getElementById(id);
          if (el) el.setAttribute('visible', 'false');
        });
        document.getElementById('env-hub').setAttribute('visible', 'true');

        // Reset Rig Position to Hub
        const rig = document.getElementById('rig');
        if (rig) rig.setAttribute('position', '0 0 0');

        const scene = document.querySelector('a-scene');
        scene.setAttribute('fog', 'color: #0a0f1d; near: 8; far: 45;');
        this.closeAllModals();
      },

      stopAllScenarioSimulations() {
        AudioEngine.stopEarthquakeRumble();
        AudioEngine.stopFireAlarm();
        AudioEngine.stopWindHowl();
        if (this.quakeAnimInterval) clearInterval(this.quakeAnimInterval);
        if (this.floodInterval) clearInterval(this.floodInterval);
        this.hideDecisionModal();
      },

      // ==========================================
      // SCENARIO 1: EARTHQUAKE SIMULATION LOGIC
      // ==========================================
      triggerEarthquakeEvent() {
        if (this.currentScenario !== 'earthquake') return;
        this.showEmergencyAlert('⚠️ SEISMIC DETECTED: SEVERE EARTHQUAKE IN PROGRESS! ⚠️', 5000);
        AudioEngine.startEarthquakeRumble();

        // Environmental Shaking Animation Loop
        const desk = document.getElementById('eq-sturdy-desk');
        const hangingLight = document.getElementById('eq-hanging-light');
        const book1 = document.getElementById('eq-book-1');
        const book2 = document.getElementById('eq-book-2');
        let shakeCount = 0;

        this.quakeAnimInterval = setInterval(() => {
          shakeCount++;
          const offsetX = (Math.random() - 0.5) * 0.12;
          const offsetZ = (Math.random() - 0.5) * 0.12;

          // Shake camera rig subtly (avoiding severe VR sickness by keeping offset gentle)
          const rig = document.getElementById('rig');
          if (rig) {
            rig.setAttribute('position', `${offsetX * 0.5} 0 ${1 + offsetZ * 0.5}`);
          }

          // Swing light fixture
          if (hangingLight) {
            hangingLight.setAttribute('rotation', `${Math.sin(shakeCount * 0.5) * 15} 0 ${Math.cos(shakeCount * 0.4) * 12}`);
          }

          // Books tumble off shelf
          if (shakeCount > 15 && book1) {
            book1.setAttribute('position', `0.3 0.2 0.8`);
            book1.setAttribute('rotation', `45 30 15`);
          }
          if (shakeCount > 25 && book2) {
            book2.setAttribute('position', `-0.2 0.1 0.7`);
            book2.setAttribute('rotation', `-30 40 -10`);
          }
        }, 60);

        this.setObjective('CRITICAL DECISION', 'Earthquake violently shaking room! Choose your immediate action:');

        // Present Decision Point
        setTimeout(() => {
          this.presentDecision({
            title: 'SEISMIC EMERGENCY PROTOCOL',
            prompt: 'Violent shaking has commenced. Ceiling debris and books are falling! What is your immediate safe action?',
            choices: [
              {
                text: 'A. Sprint toward the exterior window to call for rescue outside.',
                correct: false,
                feedback: 'INCORRECT: Exterior windows easily shatter during tremors, spraying lethal glass shards. Never run towards windows!'
              },
              {
                text: 'B. DROP to hands and knees, take COVER under the sturdy desk, and HOLD ON.',
                correct: true,
                feedback: 'EXCELLENT: "Drop, Cover, and Hold On" protects your head, neck, and vital organs from falling fixtures and collapsing ceiling tiles.'
              },
              {
                text: 'C. Run into the hallway and jump into the building elevator to escape.',
                correct: false,
                feedback: 'FATAL MISTAKE: Never use elevators during earthquakes! Seismic cutoff relays and electrical failure will trap you inside shaft walls.'
              }
            ],
            onComplete: (wasCorrect) => {
              if (wasCorrect) {
                this.tasksCompleted += 2;
                this.unlockAchievement('eq_master');
                this.setObjective('STEP 2: WAIT FOR TREMORS TO STOP', 'Tremors subsiding. Prepare to evacuate calmly through designated exit door.');
                setTimeout(() => {
                  AudioEngine.stopEarthquakeRumble();
                  clearInterval(this.quakeAnimInterval);
                  this.showEmergencyAlert('Shaking has stopped. Inspect exit route.', 4000);
                  this.setObjective('STEP 3: EVACUATION', 'Click the GREEN EMERGENCY EXIT door to safely exit the building.');
                }, 4000);
              } else {
                this.updateSafetyScore(-25);
              }
            }
          });
        }, 2000);
      },

      // ==========================================
      // SCENARIO 2: FLOOD SIMULATION LOGIC
      // ==========================================
      triggerFloodEvent() {
        if (this.currentScenario !== 'flood') return;
        this.showEmergencyAlert('🌊 FLASH FLOOD ADVISORY: RISING WATER LEVEL! 🌊', 5000);
        
        // Water rise animation
        const water = document.getElementById('flood-water-mesh');
        let waterHeight = 0.1;
        this.floodInterval = setInterval(() => {
          if (waterHeight < 1.4) {
            waterHeight += 0.015;
            if (water) water.setAttribute('position', `0 ${waterHeight} -5`);
          }
        }, 120);

        this.presentDecision({
          title: 'RAPID FLOOD NAVIGATION',
          prompt: 'Brown floodwaters are inundating the street, and a downed power transformer is sparking nearby. How should you navigate?',
          choices: [
            {
              text: 'A. Wade directly through the knee-deep water on the road to reach your parked car.',
              correct: false,
              feedback: 'CRITICAL HAZARD: Just 15 cm of moving floodwater knocks an adult down. Submerged downed power lines electrocute floodwaters with zero warning.'
            },
            {
              text: 'B. Stay clear of flooded streets and power lines; proceed immediately to HIGHER GROUND.',
              correct: true,
              feedback: 'CORRECT: Always move to elevated terrain or upper structures away from submerged utility lines. "Turn Around, Don\'t Drown".'
            },
            {
              text: 'C. Try to pick up the downed wire with a wet stick to clear the walkway.',
              correct: false,
              feedback: 'EXTREME RISK: High voltage will arc through wet objects and water film directly into your body, causing fatal electrocution.'
            }
          ],
          onComplete: (wasCorrect) => {
            if (wasCorrect) {
              this.tasksCompleted += 2;
              this.unlockAchievement('flood_master');
              this.setObjective('STEP 2: REACH ELEVATION', 'Advance toward the sandbagged High Ground Summit to complete evacuation.');
            } else {
              this.updateSafetyScore(-30);
            }
          }
        });
      },

      // ==========================================
      // SCENARIO 3: FIRE SIMULATION LOGIC
      // ==========================================
      triggerFireEvent() {
        if (this.currentScenario !== 'fire') return;
        this.showEmergencyAlert('🔥 EVACUATE: COMMERCIAL FIRE ALARM SOUNDING! 🔥', 5000);
        AudioEngine.startFireAlarm();

        // Strobe lighting pulse
        const strobe = document.getElementById('strobe-light');
        let strobeOn = false;
        this.strobeInterval = setInterval(() => {
          strobeOn = !strobeOn;
          if (strobe) strobe.setAttribute('light', `type: point; color: #ff3d00; intensity: ${strobeOn ? 2.5 : 0.2}; distance: 20;`);
        }, 400);

        this.presentDecision({
          title: 'SMOKE EGRESS PROTOCOL',
          prompt: 'Thick, toxic black smoke is accumulating near the ceiling. What is your proper movement posture and exit plan?',
          choices: [
            {
              text: 'A. Stand upright and run quickly into the elevator to descend 4 floors.',
              correct: false,
              feedback: 'DEADLY DECISION: Elevator shafts act like chimneys during fires, filling with lethal gas. Power cuts will strand you in superheated shafts.'
            },
            {
              text: 'B. CRAWL LOW under the smoke layer, test door handles with the back of hand, use STAIRS.',
              correct: true,
              feedback: 'PERFECT: Clean air remains lowest to the floor (30–60 cm). Testing door heat prevents opening rooms consumed by backdraft flames.'
            },
            {
              text: 'C. Hide inside a restroom stall and close your eyes.',
              correct: false,
              feedback: 'INCORRECT: Restrooms quickly fill with toxic carbon monoxide. Active evacuation along designated fire exit routes is required.'
            }
          ],
          onComplete: (wasCorrect) => {
            if (wasCorrect) {
              this.tasksCompleted += 2;
              this.unlockAchievement('fire_master');
              this.setObjective('STEP 2: SAFELY EVACUATE', 'Proceed to the safe emergency stairwell. Test the door handle first!');
            } else {
              this.updateSafetyScore(-25);
            }
          }
        });
      },

      // ==========================================
      // SCENARIO 4: CYCLONE SIMULATION LOGIC
      // ==========================================
      triggerCycloneEvent() {
        if (this.currentScenario !== 'cyclone') return;
        this.showEmergencyAlert('🌪️ CATEGORY 4 CYCLONE: DESTRUCTIVE GALE FORCE WINDS! 🌪️', 5000);
        AudioEngine.startWindHowl();
        AudioEngine.playThunder();

        // Tree bending animation
        const tree1 = document.getElementById('cyclone-tree-1');
        const tree2 = document.getElementById('cyclone-tree-2');
        let sway = 0;
        this.windAnim = setInterval(() => {
          sway += 0.2;
          const angle = Math.sin(sway) * 14 - 15;
          if (tree1) tree1.setAttribute('rotation', `0 0 ${angle}`);
          if (tree2) tree2.setAttribute('rotation', `0 0 ${angle * 0.8}`);
        }, 50);

        this.presentDecision({
          title: 'CYCLONE SHELTER SELECTION',
          prompt: '160 km/h winds are throwing airborne debris against exterior walls. Where should you take refuge inside the home?',
          choices: [
            {
              text: 'A. In the large patio living room next to the picture window to watch for falling branches.',
              correct: false,
              feedback: 'HAZARDOUS: Picture windows implode inward under storm pressures and projectile impacts, creating lethal flying glass shards.'
            },
            {
              text: 'B. In an interior windowless room (hallway/closet) with an emergency battery radio.',
              correct: true,
              feedback: 'OUTSTANDING: Windowless interior rooms provide the highest structural reinforcement with multiple perimeter walls deflecting debris.'
            },
            {
              text: 'C. In the outdoor metal shed in the backyard.',
              correct: false,
              feedback: 'EXTREME PERIL: Backyard sheds and carports are unanchored and frequently become airborne in Category 3+ cyclones.'
            }
          ],
          onComplete: (wasCorrect) => {
            if (wasCorrect) {
              this.tasksCompleted += 2;
              this.unlockAchievement('storm_master');
              this.setObjective('STEP 2: SECURE BARRICADE', 'Grab the yellow Emergency Weather Radio and enter the Interior Safe Room.');
            } else {
              this.updateSafetyScore(-20);
            }
          }
        });
      },

      // ==========================================
      // INTERACTIVE DECISION DISPLAY & FEEDBACK
      // ==========================================
      presentDecision(data) {
        this.activeDecisionPending = true;
        this.decisionsMade++;

        const overlay = document.getElementById('decision-overlay');
        const header = document.getElementById('dec-header');
        const promptEl = document.getElementById('dec-prompt');
        const choicesEl = document.getElementById('dec-choices');
        const feedbackEl = document.getElementById('feedback-box');
        const contBtn = document.getElementById('dec-continue-btn');

        header.textContent = data.title;
        promptEl.textContent = data.prompt;
        choicesEl.innerHTML = '';
        feedbackEl.style.display = 'none';
        contBtn.style.display = 'none';

        data.choices.forEach((choice, index) => {
          const btn = document.createElement('button');
          btn.className = 'choice-btn';
          const keyLetter = String.fromCharCode(65 + index);
          btn.innerHTML = `<span class="choice-key">${keyLetter}</span> <span>${choice.text}</span>`;
          btn.onclick = () => {
            if (!this.activeDecisionPending) return;
            this.handleChoiceSelected(choice, data);
          };
          choicesEl.appendChild(btn);
        });

        overlay.style.display = 'block';
      },

      handleChoiceSelected(choice, data) {
        this.activeDecisionPending = false;
        const feedbackEl = document.getElementById('feedback-box');
        const contBtn = document.getElementById('dec-continue-btn');

        feedbackEl.textContent = choice.feedback;
        feedbackEl.className = choice.correct ? 'correct' : 'incorrect';
        feedbackEl.style.display = 'block';
        contBtn.style.display = 'inline-block';

        if (choice.correct) {
          AudioEngine.playSuccessTone();
          this.correctDecisions++;
        } else {
          AudioEngine.playWarningBuzzer();
        }

        this.pendingDecisionCallback = () => {
          if (data.onComplete) data.onComplete(choice.correct);
        };
      },

      continueAfterDecision() {
        AudioEngine.playUiClick();
        this.hideDecisionModal();
        if (this.pendingDecisionCallback) {
          this.pendingDecisionCallback();
          this.pendingDecisionCallback = null;
        }
      },

      hideDecisionModal() {
        document.getElementById('decision-overlay').style.display = 'none';
        this.activeDecisionPending = false;
      },

      // ==========================================
      // 3D OBJECT INTERACTION HANDLER
      // ==========================================
      onObjectInteracted(objectId) {
        AudioEngine.playUiClick();
        console.log("3D Interactive Object clicked:", objectId);

        if (objectId === 'eq-desk') {
          this.showEmergencyAlert('✅ SECURE COVER: Under sturdy oak desk in Drop, Cover, Hold position.', 4000);
          AudioEngine.playSuccessTone();
          this.tasksCompleted++;
          this.updateSafetyScore(10);
        } else if (objectId === 'eq-window') {
          this.showEmergencyAlert('⚠️ WARNING: Stay back from window! Shatter risk!', 3500);
          AudioEngine.playWarningBuzzer();
          this.updateSafetyScore(-15);
          this.hazardsEncountered++;
        } else if (objectId === 'eq-exit-door') {
          this.completeScenario('earthquake');
        } else if (objectId === 'flood-hazard') {
          this.showEmergencyAlert('⚡ DANGER: High voltage current detected in water! Step back!', 4000);
          AudioEngine.playWarningBuzzer();
          this.updateSafetyScore(-25);
          this.hazardsEncountered++;
        } else if (objectId === 'flood-safe-hill') {
          this.completeScenario('flood');
        } else if (objectId === 'fire-alarm-pull') {
          this.showEmergencyAlert('🔔 Fire Alarm pulled! Building evacuation alert transmitted.', 3500);
          this.tasksCompleted++;
        } else if (objectId === 'fire-elevator') {
          this.showEmergencyAlert('❌ DO NOT ENTER ELEVATOR! Shaft smoke will suffocate occupants!', 4000);
          AudioEngine.playWarningBuzzer();
          this.updateSafetyScore(-30);
          this.hazardsEncountered++;
        } else if (objectId === 'fire-door-test') {
          this.showEmergencyAlert('🌡️ Door handle checked with back of hand: Handle is COOL. Safe to crack open.', 4000);
          AudioEngine.playSuccessTone();
          this.tasksCompleted++;
        } else if (objectId === 'fire-extinguisher') {
          this.showEmergencyAlert('🧯 ABC Dry Chemical Extinguisher acquired for egress clearing.', 3500);
          AudioEngine.playSuccessTone();
          this.tasksCompleted++;
        } else if (objectId === 'fire-exit-stairs') {
          this.completeScenario('fire');
        } else if (objectId === 'cyclone-window') {
          this.showEmergencyAlert('⚠️ Move away from exterior patio window! Gale winds will shatter it!', 4000);
          AudioEngine.playWarningBuzzer();
          this.updateSafetyScore(-20);
          this.hazardsEncountered++;
        } else if (objectId === 'cyclone-radio') {
          this.showEmergencyAlert('📻 Battery radio secured! Receiving national emergency weather broadcasts.', 3500);
          AudioEngine.playSuccessTone();
          this.tasksCompleted++;
        } else if (objectId === 'cyclone-safe-bunker') {
          this.completeScenario('cyclone');
        }
      },

      triggerCenterDesktopInteraction() {
        // Find clickable entities via raycaster intersection
        const cursor = document.getElementById('desktop-cursor');
        if (cursor && cursor.components && cursor.components.raycaster) {
          const intersectedEls = cursor.components.raycaster.intersectedEls;
          if (intersectedEls && intersectedEls.length > 0) {
            intersectedEls[0].click();
          }
        }
      },

      onVrAButtonPressed() {
        // VR Controller A button pressed
        this.triggerCenterDesktopInteraction();
      },

      // ==========================================
      // SCENARIO COMPLETION & ASSESSMENT REPORT
      // ==========================================
      completeScenario(scenarioKey) {
        this.stopAllScenarioSimulations();
        AudioEngine.playSuccessTone();

        if (this.safetyScore >= 100) {
          this.unlockAchievement('flawless_score');
        }

        // Build Evaluation Metrics
        const mins = String(Math.floor(this.elapsedSeconds / 60)).padStart(2, '0');
        const secs = String(this.elapsedSeconds % 60).padStart(2, '0');
        const timeStr = `${mins}:${secs}`;

        let grade = 'GRADE: S (EXEMPLARY)';
        let gradeClass = 'diff-beginner';
        if (this.safetyScore < 60) {
          grade = 'GRADE: F (UNSAFE - RETRAIN)';
          gradeClass = 'diff-advanced';
        } else if (this.safetyScore < 75) {
          grade = 'GRADE: C (MARGINAL)';
          gradeClass = 'diff-intermediate';
        } else if (this.safetyScore < 90) {
          grade = 'GRADE: B (PROFICIENT)';
          gradeClass = 'diff-intermediate';
        } else if (this.safetyScore < 100) {
          grade = 'GRADE: A (EXCELLENT)';
          gradeClass = 'diff-beginner';
        }

        // Populate Assessment Modal
        document.getElementById('report-scenario-badge').textContent = scenarioKey.toUpperCase();
        document.getElementById('report-score-val').textContent = `${this.safetyScore}%`;
        const gradeBadge = document.getElementById('report-grade-badge');
        gradeBadge.textContent = grade;
        gradeBadge.className = `score-grade ${gradeClass}`;

        document.getElementById('report-time-val').textContent = timeStr;
        document.getElementById('report-decisions-val').textContent = `${this.correctDecisions} / ${Math.max(1, this.decisionsMade)}`;
        document.getElementById('report-hazards-val').textContent = `${Math.max(0, 4 - this.hazardsEncountered)} / 4`;
        document.getElementById('report-compliance-val').textContent = `${Math.min(100, Math.round((this.safetyScore + (this.correctDecisions * 15)) / 1.15))}%`;

        // Narrative feedback per scenario
        const feedbackEl = document.getElementById('report-feedback-text');
        if (scenarioKey === 'earthquake') {
          feedbackEl.innerHTML = `<strong>Earthquake Drill Evaluation:</strong> You demonstrated proper adherence to the <em>Drop, Cover, and Hold On</em> protocol under simulated tremor stresses. You recognized that running outdoors during shaking is the primary cause of flying debris casualties, stayed clear of shattering window panes, and avoided elevator shafts.`;
        } else if (scenarioKey === 'flood') {
          feedbackEl.innerHTML = `<strong>Flash Flood Drill Evaluation:</strong> Critical hazard recognition observed. You adhered to the "Turn Around, Don't Drown" safety doctrine, correctly identified lethal electrical potentials around submerged utility poles, and spearheaded evacuation directly to higher ground.`;
        } else if (scenarioKey === 'fire') {
          feedbackEl.innerHTML = `<strong>Structure Fire Drill Evaluation:</strong> Outstanding smoke evasion discipline. You stayed low to preserve respiratory safety against superheated air, utilized proper tactile back-of-hand testing for door thermal signatures, and exited via exterior fire stairs without attempting elevator transit.`;
        } else if (scenarioKey === 'cyclone') {
          feedbackEl.innerHTML = `<strong>Severe Cyclone Drill Evaluation:</strong> Excellent structural awareness. You avoided vulnerable exterior glazing facing destructive gale forces, secured vital analog broadcast reception tools, and established shelter inside a reinforced windowless core.`;
        }

        this.openModal('assessment-modal');
      },

      restartCurrentScenario() {
        if (this.currentScenario && this.currentScenario !== 'hub') {
          this.startScenario(this.currentScenario);
        } else {
          this.startScenario('earthquake');
        }
      },

      // ==========================================
      // LEARNING CENTRE & ACHIEVEMENTS UI RENDERING
      // ==========================================
      switchLearnTab(tabId) {
        AudioEngine.playUiClick();
        document.querySelectorAll('.tab-content').forEach(c => c.style.display = 'none');
        document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
        const target = document.getElementById(tabId);
        if (target) target.style.display = 'block';
        if (event && event.currentTarget) event.currentTarget.classList.add('active');
      },

      renderAchievements() {
        const container = document.getElementById('achievements-list');
        if (!container) return;
        container.innerHTML = '';
        this.achievements.forEach(ach => {
          const card = document.createElement('div');
          card.className = `achieve-card ${ach.unlocked ? 'unlocked' : ''}`;
          card.innerHTML = `
            <div class="achieve-icon">${ach.icon}</div>
            <div class="achieve-info">
              <h4>${ach.name}</h4>
              <p>${ach.desc}</p>
            </div>
          `;
          container.appendChild(card);
        });
      },

      updateSettings() {
        const sfxVol = document.getElementById('setting-sfx-vol').value;
        AudioEngine.sfxVolume = sfxVol / 100;

        const snapTurn = document.getElementById('setting-snap-turn').value;
        const vignette = document.getElementById('setting-vignette').value;
        const moveSpeed = document.getElementById('setting-move-speed').value;

        // Apply movement speed to camera wasd-controls
        const cam = document.getElementById('camera');
        if (cam) {
          cam.setAttribute('wasd-controls', `acceleration: ${moveSpeed * 150}; fly: false;`);
        }

        // Apply vignette preference
        const vigEl = document.getElementById('vr-vignette');
        if (vigEl) {
          vigEl.style.opacity = (vignette === 'enabled') ? '0.6' : '0';
        }

        console.log(`Settings updated: SFX=${sfxVol}%, Snap=${snapTurn}, Vignette=${vignette}, Speed=${moveSpeed}`);
      },

      resetProgress() {
        if (confirm("Are you sure you want to reset all trainee achievements and scores?")) {
          localStorage.removeItem('calamity_sim_achievements');
          this.achievements.forEach(a => a.unlocked = false);
          this.renderAchievements();
          this.safetyScore = 100;
          this.updateSafetyScore(0);
          this.showEmergencyAlert('Progress and drill records reset.', 3000);
        }
      }
    };

    // Boot the application on page load
    window.addEventListener('DOMContentLoaded', () => {
      App.init();
    });
  </script>
</body>
</html>
