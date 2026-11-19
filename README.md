<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>PrepVR – Emergency Preparedness Trainer</title>
<!-- PrepVR: "We cannot predict the unexpected, but we can prepare for it."
     WebXR app built on A-Frame. Works on Meta Quest Browser (Enter VR) and on desktop
     (mouse + keyboard) for testing. -->
<script src="https://aframe.io/releases/1.6.0/aframe.min.js"></script>
<style>
  #info{position:fixed;left:8px;bottom:8px;z-index:5;max-width:420px;padding:8px 10px;border-radius:8px;
        background:rgba(0,0,0,.6);color:#cfe;font:12px/1.4 system-ui,sans-serif}
  #info b{color:#7fe3ff}
</style>

<!-- =====================================================================
     1. ENGINE – pure logic (no DOM / A-Frame). Scenarios are data + rules.
     ===================================================================== -->
<script id="engine">
const Sim = {
  state: 'menu', scenario: null, stepIdx: 0, score: 0, elapsed: 0,
  flags: {}, mistakes: [], seen: {}, listeners: [], result: null,
  ui: { step() {}, feedback() {}, end() {} },

  on(fn) { this.listeners.push(fn); },
  emit(type, data) { this.listeners.forEach(fn => fn(type, data)); },

  start(sc) {
    this.scenario = sc; this.stepIdx = 0; this.score = 0; this.elapsed = 0;
    this.flags = {}; this.mistakes = []; this.seen = {}; this.result = null;
    this.state = 'running';
    if (sc.onStart) sc.onStart(this);
    this.ui.step(this.step(), this);
  },
  step() { return this.scenario.steps[this.stepIdx]; },
  prompt() { const st = this.step(); return typeof st.prompt === 'function' ? st.prompt(this) : st.prompt; },
  accepts(st, name) { return typeof st.accept === 'function' ? st.accept(name, this) : st.accept.includes(name); },

  // Every player interaction arrives here as a named action.
  action(name) {
    if (this.state !== 'running') return false;
    this.lastAction = name;
    const sc = this.scenario, st = this.step();
    if (this.accepts(st, name)) { this.complete(st); return true; }
    const m = sc.mistakes && sc.mistakes[name];
    if (m && (!m.when || m.when(this))) { this.penalize(name, m); return false; }
    const n = sc.neutral && sc.neutral[name];
    if (n) { const msg = n(this); if (msg) this.ui.feedback(msg, 'info'); return false; }
    this.ui.feedback('Not yet — ' + st.hint, 'info');
    return false;
  },
  complete(st) {
    this.score += st.points;
    this.ui.feedback(st.done, 'good');
    const id = st.id;
    this.stepIdx++;
    if (st.after) st.after(this);
    this.emit('done', id);
    if (this.state !== 'running') return;
    if (this.stepIdx >= this.scenario.steps.length) this.finish(true, 'You completed every step.');
    else this.ui.step(this.step(), this);
  },
  penalize(name, m) {
    if (this.seen[name]) { this.ui.feedback(m.msg, 'bad'); return; }   // penalise each mistake once
    this.seen[name] = true;
    this.score = Math.max(0, this.score - m.penalty);
    this.mistakes.push(m.msg);
    this.ui.feedback(m.msg + '  (-' + m.penalty + ')', 'bad');
    this.emit('mistake', name);
    if (m.fatal) this.finish(false, m.msg);
  },
  tick(dt, ctx) {
    if (this.state !== 'running') return;
    this.elapsed += dt;
    if (this.scenario.tick) this.scenario.tick(this, dt, ctx);
    if (this.state === 'running' && this.elapsed > this.scenario.timeLimit)
      this.finish(false, 'Time ran out. In a real emergency, every second counts — practise until the steps are automatic.');
  },
  finish(ok, reason) {
    if (this.state !== 'running') return;
    this.state = 'done';
    const s = this.score;
    const grade = !ok ? 'Did not survive' : s >= 85 ? 'Prepared' : s >= 60 ? 'Almost there' : 'Needs practice';
    this.result = { ok, reason, score: s, grade, mistakes: this.mistakes.slice(), scenario: this.scenario.id };
    this.ui.end(this.result);
    this.emit('end', this.result);
  }
};

/* ---------- Scenario definitions (rules, scoring, teaching content) ---------- */
const SCENARIOS = {
  fire: {
    id: 'fire', title: 'Apartment Fire Escape', timeLimit: 180,
    blurb: 'Smoke, a hot door and a lift. Can you find the safe way out?',
    start: { x: 0, z: 1.5 },
    lessons: [
      'Stay low: breathable air is near the floor; smoke kills faster than flames.',
      'Back of hand on the door first. A hot door means fire is behind it — find another exit.',
      'Never use lifts in a fire. Use the stairs, then meet at the assembly point and call 112 (fire: 101).'
    ],
    steps: [
      { id: 'crouch', accept: ['crouch'], points: 20,
        prompt: 'FIRE ALARM! Smoke is banking down from the ceiling. Get LOW — crouch now (key C on desktop).',
        hint: 'get low under the smoke first (crouch).',
        done: 'Good — cleaner air is near the floor. Stay low while you move.' },
      { id: 'door1_test', accept: ['door1_test'], points: 15,
        prompt: 'Check the LEFT door for heat before opening it: touch the blue TOUCH pad (back of your hand).',
        hint: 'check the left door for heat with its TOUCH pad.',
        done: 'HOT! Fire is right behind it. Do NOT open it.' },
      { id: 'door2_test', accept: ['door2_test'], points: 15,
        prompt: 'Find another way out. Test the RIGHT door the same way.',
        hint: 'test the right door for heat with its TOUCH pad.',
        done: 'Cool to the touch — it is safer to use.' },
      { id: 'door2_open', accept: ['door2_open'], points: 10,
        prompt: 'Open the right door with the gold knob. Stay low.',
        hint: 'open the right door with its gold knob.',
        done: 'Door open. Head down the corridor (click the floor to move).' },
      { id: 'stairs', accept: ['stairs'], points: 15,
        prompt: 'Move down the corridor (click the floor) and take the STAIRS. Never the lift.',
        hint: 'reach the end of the corridor and take the stairs.',
        done: 'You are out of the smoke. Well done.' },
      { id: 'safe1', accept: (n) => n === 'assembly' || n === 'call112', points: 15,
        prompt: 'You are outside. Do both: go to the ASSEMBLY POINT and CALL 112 on the phone.',
        hint: 'go to the assembly point and call 112.',
        after: s => { s.flags.first = s.lastAction; },
        done: 'Good.' },
      { id: 'safe2', accept: (n, s) => (n === 'assembly' || n === 'call112') && n !== s.flags.first, points: 10,
        prompt: (s) => s.flags.first === 'assembly' ? 'Now call emergency services: touch the phone (112).'
                                                       : 'Now go to the ASSEMBLY POINT and wait for responders.',
        hint: 'finish the remaining safety step.',
        done: 'Everyone accounted for and help is on the way.' }
    ],
    mistakes: {
      door1_open:   { penalty: 25, msg: 'You opened a HOT door — a flashover/backdraft can kill instantly. Always test first.' },
      door2_open:   { penalty: 10, when: s => s.stepIdx < 3, msg: 'Always test a door for heat before opening it.' },
      elevator:     { penalty: 25, msg: 'Never use the lift in a fire — it can stall or open onto the fire floor.' },
      extinguisher: { penalty: 10, msg: 'An extinguisher is only for tiny, early fires. With smoke building, evacuate.' }
    },
    neutral: {
      door1_test: s => s.stepIdx > 1 ? 'That door is still hot — leave it shut.' : null,
      door2_test: s => s.stepIdx > 2 ? null : undefined,
      door2_open: () => null,
      stairs: () => null
    },
    onStart(s) { s.flags.exposure = 0; s.flags.smokeBottom = 2.6; s.flags.first = null; },
    tick(s, dt, ctx) {
      const f = s.flags;
      f.smokeBottom = Math.max(0.6, 2.6 - 0.02 * s.elapsed);
      f.inSmoke = s.stepIdx <= 4;
      if (f.inSmoke) {
        if (ctx.headY > f.smokeBottom) {
          f.exposure += dt;
          if (f.exposure > 4 && !f.warned) { f.warned = true; s.ui.feedback('Smoke is filling your lungs — get lower and move faster!', 'bad'); }
          if (f.exposure > 15) { s.finish(false, 'You breathed in too much smoke. Staying low keeps you under the toxic layer.'); return; }
        } else { f.exposure = Math.max(0, f.exposure - dt * 0.5); if (f.exposure < 1) f.warned = false; }
      }
      if (s.stepIdx === 0) {
        f.crouchT = ctx.crouching ? (f.crouchT || 0) + dt : 0;
        if (f.crouchT >= 1) s.action('crouch');
      }
    }
  },

  quake: {
    id: 'quake', title: 'Earthquake: Drop, Cover, Hold On', timeLimit: 150,
    blurb: 'The room starts shaking. Shelter, hold on, then evacuate safely.',
    start: { x: 0, z: 1.5 },
    lessons: [
      'DROP, COVER, HOLD ON: get down, get under sturdy furniture, and hold until the shaking stops.',
      'Stay away from windows, shelves and heavy objects. Doorways are NOT the safest place.',
      'After shaking: shut off gas, expect aftershocks, use stairs (never lifts), and move to open ground.'
    ],
    steps: [
      { id: 'crouch', accept: ['crouch'], points: 20,
        prompt: 'EARTHQUAKE! DROP — get down now. Crouch (key C on desktop).',
        hint: 'DROP first — get low.',
        done: 'DROP done. Now take cover.' },
      { id: 'shelter', accept: ['shelter'], points: 25,
        prompt: 'COVER — get under the sturdy table: click the green COVER circle.',
        hint: 'take COVER under the table (green circle).',
        done: 'COVER done. Protect your head and neck.' },
      { id: 'hold', accept: ['hold'], points: 25,
        prompt: s => 'HOLD ON — squeeze GRIP (or hold key H) for 5 seconds.  ' + (s.flags.holdT || 0).toFixed(1) + ' / 5.0 s',
        hint: 'hold on: squeeze grip (or hold H) for 5 seconds.',
        after: s => { s.flags.quakeStop = s.elapsed + 4; },
        done: 'Good. Keep holding until the shaking stops.' },
      { id: 'wait', accept: ['quake_end'], points: 0,
        prompt: 'Keep holding on… wait for the shaking to stop.',
        hint: 'wait for the shaking to stop.',
        done: 'The shaking has stopped. Expect aftershocks.' },
      { id: 'gas', accept: ['gas'], points: 15,
        prompt: 'Check for hazards: shut off the GAS VALVE on the left wall.',
        hint: 'shut off the gas valve (left wall) first.',
        done: 'Gas off — this prevents post-quake fires.' },
      { id: 'exit', accept: ['exit'], points: 15,
        prompt: 'Evacuate: use the EXIT / stairs. Avoid the lift.',
        hint: 'evacuate through the EXIT.',
        done: 'Out safely. Move to open ground away from buildings and power lines.' }
    ],
    mistakes: {
      doorway:  { penalty: 20, msg: 'Doorways are not safer in modern buildings, and the door can swing and hit you. Get under sturdy furniture.' },
      window:   { penalty: 25, msg: 'Stay away from windows — glass shatters and flies.' },
      elevator: { penalty: 15, msg: 'Never use lifts after an earthquake — they can stall or fail.' },
      exit:     { penalty: 30, when: s => s.flags.shaking, msg: 'Do not run outside while shaking — most injuries come from falling debris and stumbling.' }
    },
    neutral: { shelter: () => null, gas: () => null, hold: () => null, quake_end: () => null },
    onStart(s) { s.flags.shaking = true; s.flags.quakeStop = null; s.flags.holdT = 0; },
    tick(s, dt, ctx) {
      const f = s.flags;
      if (s.stepIdx === 0) {
        f.crouchT = ctx.crouching ? (f.crouchT || 0) + dt : 0;
        if (f.crouchT >= 1) s.action('crouch');
      }
      if (s.stepIdx === 2) {
        f.holdT = ctx.holding ? f.holdT + dt : 0;
        if (f.holdT >= 5) { f.holdT = 5; s.action('hold'); }
      }
      if (f.shaking && f.quakeStop !== null && s.elapsed >= f.quakeStop) {
        f.shaking = false; f.quakeStop = null; s.action('quake_end');
      }
    }
  }
};
if (typeof module !== 'undefined') module.exports = { Sim, SCENARIOS };
</script>

<!-- =====================================================================
     2. VR LAYER – A-Frame components, world builders, input, HUD, audio
     ===================================================================== -->
<script id="vr">
const World = { rects: [], update: null, onDone: null, onMistake: null };
const Input = { crouchKey: false, holdKey: false, grip: 0 };
const COMFORT = /[?&]comfort=1/.test(location.search);   // add ?comfort=1 to the URL to reduce shaking
let scene, stage, rig, cam, hud, lobbyFloor, ready = false, lastId = 'fire', stand = null, feedT = 0;

/* ---------- tiny helpers ---------- */
function mk(tag, attrs, parent) {
  const e = document.createElement(tag);
  if (attrs) for (const k in attrs) e.setAttribute(k, attrs[k]);
  (parent || stage).appendChild(e);
  const a = attrs && attrs['data-action'];
  if (a && a !== 'teleport') {
    e.addEventListener('mouseenter', () => e.setAttribute('material', 'emissive', '#88ffee'));
    e.addEventListener('mouseleave', () => e.setAttribute('material', 'emissive', '#000000'));
  }
  return e;
}
function text(parent, value, pos, w, color, extra) {
  return mk('a-text', Object.assign({ value, position: pos, width: w, align: 'center', color: color || '#fff', 'wrap-count': Math.round(w * 14) }, extra || {}), parent);
}
// A flat, optionally clickable, labelled panel.
function panel(parent, o) {
  const g = mk('a-entity', { position: o.pos || '0 0 0', rotation: o.rot || '0 0 0' }, parent);
  const at = { width: o.w, height: o.h, material: `color:${o.color || '#333'};opacity:${o.op || 1};transparent:${o.op ? 'true' : 'false'};side:double` };
  if (o.action) { at.class = 'interactive'; at['data-action'] = o.action; }
  const p = mk('a-plane', at, g);
  if (o.label) text(g, o.label, '0 0 0.02', o.w * 0.92, o.tcolor || '#fff', { 'wrap-count': o.wrap || Math.max(8, Math.round(o.w * 12)) });
  return p;
}
function box(parent, pos, size, color, extra) {
  return mk('a-box', Object.assign({ position: pos, width: size[0], height: size[1], depth: size[2], color }, extra || {}), parent);
}
function floorPlane(parent, w, d, pos, color) {
  return mk('a-plane', { rotation: '-90 0 0', width: w, height: d, position: pos, color, class: 'interactive', 'data-action': 'teleport' }, parent);
}
function clearStage() {
  while (stage.firstChild) stage.removeChild(stage.firstChild);
  stage.object3D.position.set(0, 0, 0); stage.object3D.rotation.set(0, 0, 0);
  World.update = null; World.onDone = null; World.onMistake = null; World.rects = [];
}
function clampPoint(x, z) {
  let best = null, bd = Infinity;
  for (const r of World.rects) {
    const cx = Math.min(Math.max(x, r.xMin), r.xMax), cz = Math.min(Math.max(z, r.zMin), r.zMax);
    const d = (cx - x) ** 2 + (cz - z) ** 2;
    if (d < bd) { bd = d; best = [cx, cz]; }
  }
  return best;
}
function teleportTo(x, z) {
  const c = cam.object3D.position;                    // head offset inside the rig
  rig.object3D.position.set(x - c.x, 0, z - c.z);
}
function bestScore(id) { try { return +localStorage.getItem('prepvr_best_' + id) || 0; } catch (e) { return 0; } }
function saveBest(id, s) { try { if (s > bestScore(id)) localStorage.setItem('prepvr_best_' + id, s); } catch (e) {} }

/* ---------- audio (simple synthesized cues; no asset files needed) ---------- */
const Snd = {
  ctx: null, osc: [], timer: null,
  init() { try { if (!this.ctx) this.ctx = new (window.AudioContext || window.webkitAudioContext)(); if (this.ctx.state === 'suspended') this.ctx.resume(); } catch (e) {} },
  alarm() {
    this.stop(); if (!this.ctx) return;
    const o = this.ctx.createOscillator(), g = this.ctx.createGain();
    o.type = 'square'; o.frequency.value = 880; g.gain.value = 0; o.connect(g); g.connect(this.ctx.destination); o.start();
    let on = false; this.timer = setInterval(() => { on = !on; g.gain.value = on ? 0.03 : 0; }, 450); this.osc = [o];
  },
  rumble() {
    this.stop(); if (!this.ctx) return;
    const o = this.ctx.createOscillator(), g = this.ctx.createGain();
    o.type = 'sawtooth'; o.frequency.value = 42; g.gain.value = 0.25; o.connect(g); g.connect(this.ctx.destination); o.start(); this.osc = [o];
  },
  stop() { clearInterval(this.timer); this.osc.forEach(o => { try { o.stop(); } catch (e) {} }); this.osc = []; }
};

/* ---------- HUD (head-locked) ---------- */
const HUD = {
  set(id, key, val) { const e = document.getElementById(id); if (e) e.setAttribute(key, val); },
  show(v) { hud.setAttribute('visible', v); document.getElementById('hudStat').setAttribute('visible', v); document.getElementById('hudFeedPanel').setAttribute('visible', v); },
  prompt() {
    if (Sim.state !== 'running') return;
    const n = Sim.stepIdx + 1, N = Sim.scenario.steps.length;
    this.set('hudPrompt', 'value', 'STEP ' + n + '/' + N + ':  ' + Sim.prompt());
  },
  stat() {
    const t = Math.max(0, Math.ceil(Sim.scenario.timeLimit - Sim.elapsed));
    this.set('hudStat', 'value', 'Score ' + Sim.score + '   Time ' + Math.floor(t / 60) + ':' + String(t % 60).padStart(2, '0'));
  },
  feed(msg, type) {
    this.set('hudFeed', 'value', msg);
    this.set('hudFeed', 'color', type === 'good' ? '#7dff9a' : type === 'bad' ? '#ff7b7b' : '#ffe27a');
    this.set('hudFeedPanel', 'visible', true);
    feedT = 6;
  }
};
Sim.ui.step = () => HUD.prompt();
Sim.ui.feedback = (m, t) => HUD.feed(m, t);
Sim.ui.end = (res) => {
  saveBest(res.scenario, res.score);
  HUD.feed(res.ok ? 'Scenario complete!' : 'Scenario failed: ' + res.reason, res.ok ? 'good' : 'bad');
  setTimeout(() => { if (Sim.state === 'done') buildDebrief(res); }, 3000);
};

/* ---------- Menu & Debrief ---------- */
function showMenu() {
  Snd.stop(); clearStage(); HUD.show(false);
  Sim.state = 'menu'; lobbyFloor.setAttribute('visible', true);
  rig.object3D.position.set(0, 0, 0);
  World.rects = [{ xMin: -2.5, xMax: 2.5, zMin: -2, zMax: 2.5 }];
  const g = mk('a-entity', { position: '0 1.6 -2.6' });
  panel(g, { w: 4.2, h: 2.9, color: '#0f1a28', op: 0.92, pos: '0 0 -0.02' });
  text(g, 'PrepVR', '0 1.1 0', 5, '#7fe3ff');
  text(g, 'We cannot predict the unexpected — but we can prepare for it.', '0 0.75 0', 3.6, '#cfe6ff');
  [['fire', -1.0], ['quake', 1.0]].forEach(([id, x]) => {
    const sc = SCENARIOS[id];
    panel(g, { w: 1.8, h: 0.8, color: id === 'fire' ? '#b8431f' : '#7a5a1f', pos: x + ' 0.1 0', label: sc.title, action: 'start_' + id, wrap: 18 });
    text(g, sc.blurb, x + ' -0.55 0', 1.7, '#bcd', { 'wrap-count': 28 });
    text(g, 'Best: ' + bestScore(id) + '/100', x + ' -0.95 0', 1.4, '#7dff9a');
  });
  text(g, 'Aim at a card and press the trigger / click', '0 -1.3 0', 3, '#889');
}
function buildDebrief(res) {
  clearStage(); HUD.show(false); Snd.stop();
  lobbyFloor.setAttribute('visible', true); rig.object3D.position.set(0, 0, 0);
  World.rects = [{ xMin: -2.5, xMax: 2.5, zMin: -2, zMax: 2.5 }];
  const sc = SCENARIOS[res.scenario];
  const g = mk('a-entity', { position: '0 1.6 -2.9' });
  panel(g, { w: 4.8, h: 3.2, color: '#0f1a28', op: 0.94, pos: '0 0 -0.02' });
  text(g, res.ok ? 'SCENARIO COMPLETE' : 'SCENARIO FAILED', '0 1.35 0', 5, res.ok ? '#7dff9a' : '#ff7b7b');
  text(g, 'Score ' + res.score + '/100  ·  ' + res.grade, '0 1.0 0', 4, '#ffe27a');
  if (!res.ok) text(g, res.reason, '0 0.7 0', 4.2, '#ffb0b0', { 'wrap-count': 70 });
  text(g, 'WHAT WENT WRONG', '-1.2 0.4 0', 2, '#7fe3ff', { 'wrap-count': 30 });
  mk('a-text', { value: res.mistakes.length ? res.mistakes.map(m => '• ' + m).join('\n\n') : 'No mistakes — well done!',
    position: '-2.25 0.25 0', width: 2.1, 'wrap-count': 34, align: 'left', anchor: 'left', baseline: 'top', color: '#fff' }, g);
  text(g, 'KEY LESSONS', '1.2 0.4 0', 2, '#7fe3ff', { 'wrap-count': 30 });
  mk('a-text', { value: sc.lessons.map(l => '• ' + l).join('\n\n'),
    position: '0.1 0.25 0', width: 2.1, 'wrap-count': 34, align: 'left', anchor: 'left', baseline: 'top', color: '#fff' }, g);
  panel(g, { w: 1.3, h: 0.45, color: '#2b6cff', pos: '-1 -1.4 0', label: 'Retry', action: 'retry' });
  panel(g, { w: 1.3, h: 0.45, color: '#444', pos: '1 -1.4 0', label: 'Menu', action: 'home' });
}

/* ---------- Scenario world: FIRE ---------- */
function buildFire() {
  const W = mk('a-entity', {});
  floorPlane(W, 8, 9, '0 0 -0.5', '#6b5a48');
  floorPlane(W, 5, 7, '0 0 -8.5', '#4b525c');
  const wall = (pos, size, c) => box(W, pos, size, c || '#d9d2c5');
  wall('-3.25 1.5 -5', [1.5, 3, 0.1]); wall('0 1.5 -5', [3, 3, 0.1]); wall('3.25 1.5 -5', [1.5, 3, 0.1]);
  wall('-2 2.55 -5', [1, 0.9, 0.1]); wall('2 2.55 -5', [1, 0.9, 0.1]);
  wall('-4 1.5 -0.5', [0.1, 3, 9]); wall('4 1.5 -0.5', [0.1, 3, 9]); wall('0 1.5 4', [8, 3, 0.1]);
  mk('a-plane', { rotation: '90 0 0', width: 8, height: 9, position: '0 3 -0.5', color: '#cfcfcf' }, W);
  wall('-2.5 1.5 -8.5', [0.1, 3, 7], '#b9b3a6'); wall('2.5 1.5 -8.5', [0.1, 3, 7], '#b9b3a6'); wall('0 1.5 -12', [5, 3, 0.1], '#b9b3a6');
  mk('a-plane', { rotation: '90 0 0', width: 5, height: 7, position: '0 3 -8.5', color: '#bbb' }, W);

  // furniture + fire (sofa corner)
  box(W, '2.8 0.3 1', [1.8, 0.6, 0.9], '#5b3b5b'); box(W, '0.8 0.2 1.2', [1.0, 0.4, 0.6], '#6e5236');
  box(W, '-3.9 1.4 1', [0.1, 0.8, 1.4], '#111');
  for (let i = 0; i < 6; i++) {
    mk('a-cone', { 'radius-bottom': 0.25, 'radius-top': 0.02, height: 0.9, position: (2.2 + Math.random() * 1.2) + ' 0.95 ' + (0.6 + Math.random() * 0.8),
      material: 'color:#ff6a00;emissive:#ff4000;emissiveIntensity:1',
      animation: 'property:scale;from:1 0.8 1;to:1.25 1.5 1.25;dir:alternate;loop:true;dur:' + (250 + i * 70) + ';easing:easeInOutSine' }, W);
  }
  mk('a-entity', { light: 'type:point;color:#ff6a1a;intensity:1.3;distance:8', position: '2.5 1.3 1' }, W);

  // extinguisher (a trap: tempting but wrong here)
  mk('a-cylinder', { radius: 0.1, height: 0.5, position: '-3.7 0.9 -4.8', color: '#d22', class: 'interactive', 'data-action': 'extinguisher' }, W);
  text(W, 'EXTINGUISHER', '-3.7 1.3 -4.8', 0.8, '#fff');

  // doors: pivot at hinge; panel offset 0.5
  const doors = {};
  [['door1', -2.5], ['door2', 1.5]].forEach(([id, hx]) => {
    const pivot = mk('a-entity', { position: hx + ' 0 -5' }, W);
    box(pivot, '0.5 1.05 0', [1, 2.1, 0.08], '#7a4b2a');
    panel(pivot, { w: 0.55, h: 0.22, color: '#2b6cff', pos: '0.5 1.55 0.05', label: 'TOUCH', action: id + '_test' });
    mk('a-sphere', { radius: 0.05, position: '0.88 1.0 0.08', color: '#e5b93c', class: 'interactive', 'data-action': id + '_open' }, pivot);
    doors[id] = pivot;
  });
  box(W, '-2 0.03 -4.95', [1, 0.05, 0.02], '#ff6a00', { material: 'color:#ff6a00;emissive:#ff4000;emissiveIntensity:1' }); // glow under hot door
  panel(W, { w: 0.8, h: 0.3, color: '#1f9d4a', pos: '2 2.45 -4.93', label: 'EXIT' });

  // burst of flames if the hot door is opened
  const burst = mk('a-entity', { visible: false, position: '-2 0 -5' }, W);
  for (let i = 0; i < 8; i++) mk('a-cone', { 'radius-bottom': 0.3, 'radius-top': 0.02, height: 1.4, position: (Math.random() - 0.5) * 1.2 + ' 1 ' + Math.random() * 0.8,
    material: 'color:#ff7a00;emissive:#ff4000;emissiveIntensity:1', animation: 'property:scale;from:1 0.8 1;to:1.4 1.7 1.4;dir:alternate;loop:true;dur:' + (200 + i * 40) }, burst);

  // corridor end: stairs vs lift
  panel(W, { w: 1.4, h: 0.7, color: '#1f9d4a', pos: '-1.4 1.5 -11.93', label: 'STAIRS', action: 'stairs' });
  panel(W, { w: 0.5, h: 0.7, color: '#777', pos: '1.5 1.4 -11.93', label: 'LIFT', action: 'elevator' });

  // smoke layer (descends over time)
  const smoke = mk('a-box', { width: 8, depth: 17, height: 1, position: '0 2.5 -4.5',
    material: 'color:#2b2b2b;opacity:0.62;transparent:true;side:double;depthWrite:false' }, W);

  World.rects = [{ xMin: -3.6, xMax: 3.6, zMin: -4.5, zMax: 3.6 }];
  World.update = () => {
    const b = Sim.flags.smokeBottom != null ? Sim.flags.smokeBottom : 2.6, h = 3.2 - b;
    smoke.object3D.position.y = b + h / 2; smoke.object3D.scale.y = h;
    smoke.object3D.visible = Sim.flags.inSmoke !== false;
  };
  World.onDone = id => {
    if (id === 'door2_open') {
      doors.door2.setAttribute('animation__open', 'property:rotation;to:0 90 0;dur:1200;easing:easeOutQuad');
      World.rects.push({ xMin: -2.2, xMax: 2.2, zMin: -11.4, zMax: -4.5 });
    }
    if (id === 'stairs') { buildOutside(); }
  };
  World.onMistake = name => {
    if (name === 'door1_open') { burst.setAttribute('visible', true); doors.door1.setAttribute('animation__open', 'property:rotation;to:0 40 0;dur:600'); }
  };
  Snd.alarm();
}
function buildOutside() {
  const O = mk('a-entity', {});
  floorPlane(O, 16, 12, '0 0 -20', '#2f6b3a');
  mk('a-cylinder', { radius: 1.2, height: 0.04, position: '0 0.02 -21', color: '#2b9bff', class: 'interactive', 'data-action': 'assembly' }, O);
  text(O, 'ASSEMBLY POINT', '0 1.6 -21', 2.4, '#ffe27a');
  panel(O, { w: 0.5, h: 0.8, color: '#222', pos: '2.4 1.2 -18', rot: '0 -20 0', label: 'CALL 112', action: 'call112', wrap: 6 });
  mk('a-sky', { color: '#6aa9dd' }, O);
  World.rects = [{ xMin: -7.5, xMax: 7.5, zMin: -25.5, zMax: -14.5 }];
  teleportTo(0, -15.5);
}

/* ---------- Scenario world: EARTHQUAKE ---------- */
function buildQuake() {
  const W = mk('a-entity', {});
  floorPlane(W, 8, 8, '0 0 0', '#7a6650');
  const wall = (pos, size) => box(W, pos, size, '#d8d2c8');
  wall('0 1.5 -4', [8, 3, 0.1]); wall('-4 1.5 0', [0.1, 3, 8]); wall('4 1.5 0', [0.1, 3, 8]); wall('0 1.5 4', [8, 3, 0.1]);
  mk('a-plane', { rotation: '90 0 0', width: 8, height: 8, position: '0 3 0', color: '#ccc' }, W);

  // window (hazard)
  box(W, '-2 1.6 -3.96', [1.5, 1.1, 0.06], '#444');
  panel(W, { w: 1.4, h: 1.0, color: '#8fd3ff', op: 0.5, pos: '-2 1.6 -3.92', label: 'WINDOW', action: 'window', tcolor: '#0b3a55' });
  // doorway myth (hazard)
  panel(W, { w: 1.0, h: 2.1, color: '#2a2a2a', pos: '3.93 1.05 -1.5', rot: '0 -90 0', label: 'DOORWAY', action: 'doorway' });
  // gas valve (hazard to remove)
  panel(W, { w: 0.5, h: 0.5, color: '#c22', pos: '-3.93 1.3 1.5', rot: '0 90 0', label: 'GAS VALVE', action: 'gas', wrap: 8 });
  // exit + lift
  panel(W, { w: 1.0, h: 2.1, color: '#1f9d4a', pos: '1.5 1.05 3.93', rot: '0 180 0', label: 'EXIT / STAIRS', action: 'exit', wrap: 8 });
  panel(W, { w: 0.4, h: 0.5, color: '#777', pos: '-0.4 1.2 3.93', rot: '0 180 0', label: 'LIFT', action: 'elevator' });

  // sturdy table + cover marker
  box(W, '0 0.75 -1.5', [1.8, 0.08, 1.0], '#8b5a2b');
  [[-0.8, -1.95], [0.8, -1.95], [-0.8, -1.05], [0.8, -1.05]].forEach(p => box(W, p[0] + ' 0.37 ' + p[1], [0.08, 0.75, 0.08], '#8b5a2b'));
  mk('a-circle', { rotation: '-90 0 0', radius: 0.6, position: '0 0.02 -1.5', color: '#2ecc71', opacity: 0.6, class: 'interactive', 'data-action': 'shelter',
    animation: 'property:scale;from:1 1 1;to:1.15 1.15 1;dir:alternate;loop:true;dur:700' }, W);
  mk('a-text', { value: 'COVER', rotation: '-90 0 0', position: '0 0.04 -1.5', width: 1.6, align: 'center', color: '#fff' }, W);

  // sofa, bookshelf with books that fall
  box(W, '-2.6 0.3 1', [1.8, 0.6, 0.9], '#3b5b7a');
  box(W, '3.5 1.0 -3', [0.5, 2, 1.5], '#5a3a1a');
  for (let i = 0; i < 4; i++) {
    mk('a-box', { width: 0.3, height: 0.25, depth: 0.2, color: ['#c33', '#36c', '#3a3', '#cc3'][i], position: '3.4 ' + (1.7 + (i % 2) * 0.3) + ' ' + (-3.4 + i * 0.35),
      animation__fall: 'property:position;to:3.0 0.13 ' + (-2.6 + i * 0.35) + ';dur:900;delay:' + (800 + i * 450) + ';easing:easeInQuad' }, W);
  }
  // swinging ceiling lamp
  const lamp = mk('a-entity', { position: '0 3 0', animation__sway: 'property:rotation;from:-8 0 -8;to:8 0 8;dir:alternate;loop:true;dur:500;easing:easeInOutSine' }, W);
  mk('a-cylinder', { radius: 0.01, height: 0.5, position: '0 -0.25 0', color: '#222' }, lamp);
  mk('a-sphere', { radius: 0.18, position: '0 -0.55 0', material: 'color:#fff7c0;emissive:#fff7c0;emissiveIntensity:0.8' }, lamp);

  World.rects = [{ xMin: -3.6, xMax: 3.6, zMin: -3.6, zMax: 3.6 }];
  World.update = () => { if (!Sim.flags.shaking && lamp.hasAttribute('animation__sway')) { lamp.removeAttribute('animation__sway'); lamp.object3D.rotation.set(0, 0, 0); } };
  World.onDone = id => { if (id === 'shelter') teleportTo(0, -1.5); };
  Snd.rumble();
}

/* ---------- Flow control ---------- */
function startScenario(id) {
  const sc = SCENARIOS[id]; lastId = id;
  clearStage(); Snd.stop();
  lobbyFloor.setAttribute('visible', false);
  rig.object3D.position.set(sc.start.x, 0, sc.start.z);
  cam.object3D.position.x = 0; cam.object3D.position.z = 0;
  try { const lc = cam.components['look-controls']; lc.yawObject.rotation.y = 0; lc.pitchObject.rotation.x = 0; } catch (e) {}
  Input.crouchKey = false; stand = null;
  if (id === 'fire') buildFire(); else buildQuake();
  Sim.start(sc);
  HUD.show(true); HUD.prompt(); HUD.stat();
  HUD.feed(sc.title + ' — stay calm and act.', 'info');
}
function onAction(name, e) {
  Snd.init();
  if (name === 'teleport') {
    if (Sim.state !== 'running' || !e.detail || !e.detail.intersection) return;
    const p = e.detail.intersection.point, c = clampPoint(p.x, p.z);
    if (c) teleportTo(c[0], c[1]);
    return;
  }
  if (name.startsWith('start_')) return startScenario(name.slice(6));
  if (name === 'retry') return startScenario(lastId);
  if (name === 'home') return showMenu();
  Sim.action(name);
}

/* ---------- A-Frame component: per-frame simulation loop ---------- */
AFRAME.registerComponent('sim-loop', {
  init() {
    this.v = new THREE.Vector3(); this.acc = 0;
    window.addEventListener('keydown', e => { if (e.repeat) return; const k = e.key.toLowerCase(); if (k === 'c') Input.crouchKey = !Input.crouchKey; if (k === 'h') Input.holdKey = true; });
    window.addEventListener('keyup', e => { if (e.key.toLowerCase() === 'h') Input.holdKey = false; });
  },
  tick(t, dtms) {
    if (!ready) return;
    const dt = Math.min(dtms / 1000, 0.1), o = cam.object3D;
    if (!this.el.is('vr-mode')) {                                    // desktop crouch emulation
      const target = Input.crouchKey ? 0.9 : 1.6;
      o.position.y += (target - o.position.y) * Math.min(1, dt * 8);
    }
    o.getWorldPosition(this.v);
    const headY = this.v.y;
    if (Sim.state === 'running') {
      if (stand === null) stand = headY > 1.0 ? headY : 1.6;
      if (headY > 1.2 && headY > stand) stand = headY;
      const crouching = headY < Math.min(1.1, stand * 0.68);
      Sim.tick(dt, { headY, crouching, holding: Input.holdKey || Input.grip > 0 });
    }
    if (World.rects.length) {                                         // keep player inside the allowed area
      const c = clampPoint(this.v.x, this.v.z);
      if (c) { rig.object3D.position.x += c[0] - this.v.x; rig.object3D.position.z += c[1] - this.v.z; }
    }
    if (World.update) World.update(dt);
    // earthquake: shake the environment (not the camera)
    const s = stage.object3D, shaking = Sim.state === 'running' && Sim.flags.shaking;
    if (shaking) {
      const a = COMFORT ? 0.01 : 0.035;
      s.position.set((Math.random() - 0.5) * 2 * a, (Math.random() - 0.5) * a, (Math.random() - 0.5) * 2 * a);
      s.rotation.z = (Math.random() - 0.5) * a * 0.4;
    } else if (s.position.lengthSq() > 0) { s.position.set(0, 0, 0); s.rotation.set(0, 0, 0); }
    if (Sim.state === 'running' && Sim.scenario.id === 'quake' && !Sim.flags.shaking) Snd.stop();
    // HUD refresh ~4x/sec
    this.acc += dt;
    if (this.acc > 0.25 && Sim.state === 'running') { this.acc = 0; HUD.prompt(); HUD.stat(); }
    if (feedT > 0) { feedT -= dt; if (feedT <= 0) HUD.set('hudFeedPanel', 'visible', false); }
  }
});

function init() {
  scene = document.querySelector('a-scene'); stage = document.getElementById('stage');
  rig = document.getElementById('rig'); cam = document.getElementById('cam'); hud = document.getElementById('hud');
  lobbyFloor = document.getElementById('lobbyFloor');
  scene.addEventListener('click', e => {
    let t = e.target;
    while (t && t !== scene && !(t.dataset && t.dataset.action)) t = t.parentNode;
    if (t && t.dataset && t.dataset.action) onAction(t.dataset.action, e);
  });
  ['lhand', 'rhand'].forEach(id => {
    const h = document.getElementById(id);
    h.addEventListener('gripdown', () => { Input.grip++; });
    h.addEventListener('gripup', () => { Input.grip = Math.max(0, Input.grip - 1); });
  });
  Sim.on((type, d) => {
    if (type === 'done' && World.onDone) World.onDone(d);
    if (type === 'mistake' && World.onMistake) World.onMistake(d);
  });
  ready = true; showMenu();
}
document.addEventListener('DOMContentLoaded', () => {
  const s = document.querySelector('a-scene');
  if (s.hasLoaded) init(); else s.addEventListener('loaded', init);
});
</script>
</head>

<body>
<div id="info"><b>PrepVR</b> — Desktop: click to interact · <b>WASD</b> move · <b>C</b> crouch · <b>H</b> hold on (earthquake).
  VR headset: aim + trigger to interact, click the floor to move, physically crouch, grip to hold on.</div>

<a-scene sim-loop renderer="colorManagement: true" webxr="optionalFeatures: local-floor, bounded-floor" vr-mode-ui="enabled: true" background="color: #0b0f14">
  <a-entity light="type: ambient; color: #ffffff; intensity: 0.7"></a-entity>
  <a-entity light="type: directional; color: #ffffff; intensity: 0.7" position="-1 4 2"></a-entity>
  <a-entity id="lobbyFloor"><a-plane rotation="-90 0 0" width="30" height="30" color="#131c28"></a-plane></a-entity>

  <a-entity id="rig" position="0 0 0">
    <a-entity id="cam" camera look-controls wasd-controls="acceleration: 25" position="0 1.6 0">
      <!-- head-locked HUD -->
      <a-entity id="hud" position="0 -0.34 -1.1" visible="false">
        <a-plane width="1.35" height="0.26" material="color:#000;opacity:0.6;transparent:true" position="0 0 -0.002"></a-plane>
        <a-text id="hudPrompt" value="" align="center" width="1.25" wrap-count="52" color="#ffffff"></a-text>
      </a-entity>
      <a-entity id="hudFeedPanel" position="0 0.3 -1.1" visible="false">
        <a-plane width="1.35" height="0.26" material="color:#000;opacity:0.6;transparent:true" position="0 0 -0.002"></a-plane>
        <a-text id="hudFeed" value="" align="center" width="1.25" wrap-count="52" color="#ffe27a"></a-text>
      </a-entity>
      <a-text id="hudStat" value="" position="-0.62 0.46 -1.1" width="0.8" color="#9fe" visible="false"></a-text>
    </a-entity>
    <a-entity id="lhand" laser-controls="hand: left" raycaster="objects: .interactive; far: 40"></a-entity>
    <a-entity id="rhand" laser-controls="hand: right" raycaster="objects: .interactive; far: 40"></a-entity>
  </a-entity>

  <!-- mouse pointer for desktop testing -->
  <a-entity cursor="rayOrigin: mouse" raycaster="objects: .interactive; far: 40"></a-entity>

  <!-- everything scenario-specific is created/destroyed inside #stage -->
  <a-entity id="stage"></a-entity>
</a-scene>
</body>
</html>
