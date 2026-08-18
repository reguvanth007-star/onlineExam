<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ExamHall — Online Examination Portal</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Special+Elite&family=Libre+Baskerville:ital,wght@0,400;0,700;1,400&family=IBM+Plex+Mono:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --paper:#F2EDE1;
    --paper-deep:#E8E1CF;
    --line:#C9BFA6;
    --ink:#1F2A24;
    --pencil:#4B5563;
    --red-pen:#B3261E;
    --green:#2F5233;
    --green-deep:#22401C;
    --gold:#A6822F;
    --white:#FCFAF3;
    --shadow: 0 8px 24px rgba(31,42,36,0.12);
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    background:
      repeating-linear-gradient(transparent, transparent 34px, var(--line) 35px),
      var(--paper);
    background-attachment:local;
    color:var(--ink);
    font-family:'Libre Baskerville', serif;
    min-height:100vh;
    padding:32px 16px 64px;
  }
  .wrap{max-width:880px;margin:0 auto;}
  .mono{font-family:'IBM Plex Mono',monospace;}
  .type{font-family:'Special Elite',cursive;}

  /* ---------- Header / masthead ---------- */
  .masthead{
    display:flex;align-items:baseline;justify-content:space-between;
    border-bottom:3px double var(--ink);
    padding-bottom:10px;margin-bottom:28px;flex-wrap:wrap;gap:8px;
  }
  .masthead h1{
    font-family:'Special Elite',cursive;
    font-size:28px;letter-spacing:1px;margin:0;
  }
  .masthead .sub{
    font-family:'IBM Plex Mono',monospace;
    font-size:11px;letter-spacing:2px;text-transform:uppercase;color:var(--pencil);
  }
  .userchip{
    font-family:'IBM Plex Mono',monospace;font-size:12px;color:var(--green-deep);
    background:var(--white);border:1px solid var(--line);border-radius:3px;
    padding:5px 10px;display:flex;align-items:center;gap:8px;
  }
  .userchip button{
    background:none;border:none;color:var(--red-pen);cursor:pointer;
    font-family:'IBM Plex Mono',monospace;font-size:11px;text-decoration:underline;padding:0;
  }

  /* ---------- Cards ---------- */
  .sheet{
    background:var(--white);
    border:1px solid var(--line);
    box-shadow:var(--shadow);
    border-radius:2px;
    padding:28px;
    margin-bottom:24px;
    position:relative;
  }
  .sheet::before{
    content:"";position:absolute;left:0;top:0;bottom:0;width:6px;
    background:repeating-linear-gradient(180deg, var(--paper-deep) 0 10px, transparent 10px 14px);
    border-right:1px dashed var(--line);
  }

  /* ---------- Buttons ---------- */
  .btn{
    font-family:'IBM Plex Mono',monospace;font-size:13px;font-weight:600;
    letter-spacing:0.5px;text-transform:uppercase;
    background:var(--green);color:var(--white);
    border:none;border-radius:2px;padding:11px 20px;cursor:pointer;
    transition:transform .12s ease, background .15s ease;
  }
  .btn:hover{background:var(--green-deep);transform:translateY(-1px);}
  .btn:active{transform:translateY(0);}
  .btn.secondary{background:transparent;color:var(--green);border:1.5px solid var(--green);}
  .btn.secondary:hover{background:var(--paper-deep);}
  .btn.danger{background:var(--red-pen);}
  .btn.danger:hover{background:#8f1e18;}
  .btn:disabled{opacity:0.45;cursor:not-allowed;transform:none;}
  .btn-row{display:flex;gap:10px;flex-wrap:wrap;}

  input[type=text], input[type=number], textarea, select{
    font-family:'IBM Plex Mono',monospace;font-size:14px;
    padding:9px 10px;border:1px solid var(--line);border-radius:2px;
    background:var(--paper);color:var(--ink);width:100%;
  }
  input:focus, textarea:focus, select:focus{outline:2px solid var(--green);outline-offset:1px;}
  label{font-family:'IBM Plex Mono',monospace;font-size:11px;text-transform:uppercase;letter-spacing:1px;color:var(--pencil);display:block;margin-bottom:4px;}
  .field{margin-bottom:16px;}

  /* ---------- Hall ticket (login) ---------- */
  .ticket{
    max-width:460px;margin:40px auto;background:var(--white);
    border:1.5px solid var(--ink);position:relative;box-shadow:var(--shadow);
    padding:0;overflow:hidden;
  }
  .ticket-head{
    background:var(--green);color:var(--white);padding:16px 22px;
    display:flex;justify-content:space-between;align-items:center;
  }
  .ticket-head .type{font-size:20px;}
  .ticket-head .mono{font-size:10px;letter-spacing:2px;opacity:0.85;}
  .ticket-body{padding:24px 22px 26px;}
  .stamp{
    position:absolute;top:64px;right:24px;
    border:2.5px solid var(--red-pen);color:var(--red-pen);
    font-family:'Special Elite',cursive;font-size:12px;
    padding:5px 10px;transform:rotate(-14deg);border-radius:4px;
    opacity:0.85;letter-spacing:1px;pointer-events:none;
  }
  .perf{
    height:14px;
    background: radial-gradient(circle, var(--paper) 4px, transparent 4.5px) repeat-x;
    background-size:16px 14px;background-position:6px center;
    border-top:1px dashed var(--line);border-bottom:1px dashed var(--line);
  }

  /* ---------- Dashboard exam list ---------- */
  .exam-row{
    display:flex;justify-content:space-between;align-items:center;
    border-bottom:1px solid var(--line);padding:16px 4px;gap:14px;flex-wrap:wrap;
  }
  .exam-row:last-child{border-bottom:none;}
  .exam-title{font-family:'Special Elite',cursive;font-size:17px;margin:0 0 4px;}
  .exam-meta{font-family:'IBM Plex Mono',monospace;font-size:11.5px;color:var(--pencil);letter-spacing:0.5px;}
  .badge{
    font-family:'IBM Plex Mono',monospace;font-size:10.5px;text-transform:uppercase;
    letter-spacing:1px;padding:3px 8px;border-radius:2px;
  }
  .badge.pending{background:var(--paper-deep);color:var(--pencil);border:1px solid var(--line);}
  .badge.done{background:#E6EFE6;color:var(--green-deep);border:1px solid var(--green);}

  h2.section{
    font-family:'Special Elite',cursive;font-size:20px;
    border-bottom:2px solid var(--ink);padding-bottom:8px;margin:0 0 18px;
  }

  /* ---------- Exam taking ---------- */
  .exam-topbar{
    display:flex;justify-content:space-between;align-items:center;
    margin-bottom:20px;flex-wrap:wrap;gap:10px;
  }
  .clock{
    font-family:'IBM Plex Mono',monospace;font-size:22px;font-weight:600;
    background:var(--ink);color:var(--white);padding:8px 16px;border-radius:3px;
    letter-spacing:2px;
  }
  .clock.warn{background:var(--red-pen);}
  .qnav{display:flex;flex-wrap:wrap;gap:7px;margin-bottom:20px;}
  .qnav button{
    width:32px;height:32px;border-radius:50%;border:1.5px solid var(--line);
    background:var(--white);font-family:'IBM Plex Mono',monospace;font-size:12px;cursor:pointer;
  }
  .qnav button.current{border-color:var(--ink);border-width:2px;}
  .qnav button.answered{background:var(--green);color:var(--white);border-color:var(--green);}

  .question-num{font-family:'IBM Plex Mono',monospace;color:var(--gold);font-size:13px;letter-spacing:1px;}
  .question-text{font-size:19px;line-height:1.5;margin:10px 0 22px;}

  .omr-option{
    display:flex;align-items:center;gap:14px;padding:12px 8px;
    border-bottom:1px dashed var(--line);cursor:pointer;
  }
  .omr-option:last-child{border-bottom:none;}
  .bubble{
    width:22px;height:22px;min-width:22px;border-radius:50%;
    border:2px solid var(--pencil);position:relative;flex-shrink:0;
  }
  .bubble::after{
    content:"";position:absolute;inset:3px;border-radius:50%;
    background:var(--ink);transform:scale(0);transition:transform .12s ease;
  }
  .omr-option.selected .bubble::after{transform:scale(1);}
  .omr-option.selected .bubble{border-color:var(--ink);}
  .omr-option .opt-letter{font-family:'IBM Plex Mono',monospace;font-size:12px;color:var(--pencil);width:16px;}
  .omr-option .opt-text{font-size:15.5px;}

  /* ---------- Results ---------- */
  .score-banner{
    display:flex;align-items:center;gap:22px;padding:20px 4px;flex-wrap:wrap;
  }
  .score-circle{
    width:92px;height:92px;border-radius:50%;border:3px solid var(--red-pen);
    display:flex;align-items:center;justify-content:center;flex-direction:column;
    font-family:'Special Elite',cursive;color:var(--red-pen);transform:rotate(-4deg);
  }
  .score-circle .n{font-size:26px;line-height:1;}
  .score-circle .d{font-size:10px;}
  .review-q{border-bottom:1px solid var(--line);padding:16px 4px;}
  .review-q:last-child{border-bottom:none;}
  .review-answer{font-family:'IBM Plex Mono',monospace;font-size:13px;margin-top:6px;}
  .review-answer.correct{color:var(--green-deep);}
  .review-answer.wrong{color:var(--red-pen);text-decoration:line-through;}
  .review-answer.correct-note{color:var(--green-deep);}

  /* ---------- Create exam form ---------- */
  .qblock{border:1px dashed var(--line);padding:16px;margin-bottom:14px;border-radius:2px;position:relative;}
  .qblock .remove-q{
    position:absolute;top:10px;right:10px;background:none;border:none;
    color:var(--red-pen);cursor:pointer;font-family:'IBM Plex Mono',monospace;font-size:11px;
  }
  .opt-grid{display:grid;grid-template-columns:1fr;gap:8px;margin-top:10px;}
  .opt-input-row{display:flex;align-items:center;gap:8px;}
  .opt-input-row input[type=radio]{accent-color:var(--green);width:16px;height:16px;}

  .empty-state{
    text-align:center;padding:40px 20px;color:var(--pencil);font-family:'IBM Plex Mono',monospace;font-size:13px;
  }
  .toast{
    position:fixed;bottom:20px;left:50%;transform:translateX(-50%);
    background:var(--ink);color:var(--white);padding:10px 20px;border-radius:3px;
    font-family:'IBM Plex Mono',monospace;font-size:12.5px;letter-spacing:0.5px;
    box-shadow:var(--shadow);z-index:50;opacity:0;pointer-events:none;transition:opacity .25s ease;
  }
  .toast.show{opacity:1;}

  @media (max-width:520px){
    .masthead h1{font-size:22px;}
    .clock{font-size:18px;padding:7px 12px;}
    .score-circle{width:78px;height:78px;}
  }
</style>
</head>
<body>
<div class="wrap" id="app"></div>
<div class="toast" id="toast"></div>

<script>
/* ============ DATA LAYER ============ */
const SEED_EXAMS = [
  {
    id: "seed-aptitude",
    title: "General Aptitude",
    subject: "Reasoning & Quant",
    duration: 300, // seconds
    seed: true,
    questions: [
      {q:"If a train travels 60 km in 45 minutes, what is its speed in km/h?", opts:["60 km/h","80 km/h","90 km/h","45 km/h"], correct:1},
      {q:"Find the next number: 2, 6, 12, 20, 30, ?", opts:["36","40","42","44"], correct:2},
      {q:"A shopkeeper marks up an item by 25% and then gives a 20% discount. What is the net effect?", opts:["No change","5% profit","5% loss","10% loss"], correct:1},
      {q:"Which of these is NOT a prime number?", opts:["17","23","31","33"], correct:3},
      {q:"If today is Wednesday, what day will it be after 100 days?", opts:["Monday","Tuesday","Friday","Thursday"], correct:2}
    ]
  },
  {
    id: "seed-cs",
    title: "Computer Science Basics",
    subject: "Fundamentals",
    duration: 360,
    seed: true,
    questions: [
      {q:"What does CPU stand for?", opts:["Central Process Unit","Central Processing Unit","Computer Personal Unit","Central Processor Utility"], correct:1},
      {q:"Which data structure uses FIFO (First In First Out)?", opts:["Stack","Queue","Tree","Graph"], correct:1},
      {q:"In binary, what is 1010 in decimal?", opts:["8","9","10","12"], correct:2},
      {q:"Which of these is not a programming language?", opts:["Python","HTML","Java","C++"], correct:1},
      {q:"What is the time complexity of binary search?", opts:["O(n)","O(n log n)","O(log n)","O(1)"], correct:2},
      {q:"Which layer of the OSI model handles routing?", opts:["Physical","Data Link","Network","Transport"], correct:2}
    ]
  },
  {
    id: "seed-english",
    title: "English Grammar",
    subject: "Language",
    duration: 240,
    seed: true,
    questions: [
      {q:"Choose the correctly punctuated sentence.", opts:["Its a nice day.","It's a nice day.","Its' a nice day.","It is' a nice day."], correct:1},
      {q:"Identify the synonym of 'Meticulous'.", opts:["Careless","Thorough","Quick","Vague"], correct:1},
      {q:"Which sentence uses the passive voice?", opts:["She wrote the letter.","The letter was written by her.","She is writing a letter.","She will write a letter."], correct:1},
      {q:"Fill in the blank: Neither of the boys ___ ready.", opts:["is","are","were","have"], correct:0}
    ]
  }
];

const store = {
  async get(key, shared=false){
    try{ const r = await window.storage.get(key, shared); return r ? JSON.parse(r.value) : null; }
    catch(e){ return null; }
  },
  async set(key, value, shared=false){
    try{ await window.storage.set(key, JSON.stringify(value), shared); return true; }
    catch(e){ console.error('storage set failed', e); return false; }
  }
};

let state = {
  user: null,          // {name, roll}
  customExams: [],
  results: {},          // examId -> {score,total,answers,submittedAt}
  screen: 'loading',
  currentExamId: null,
  liveAnswers: {},
  currentQ: 0,
  timeLeft: 0,
  timerHandle: null,
  draftQuestions: []
};

function allExams(){ return [...SEED_EXAMS, ...state.customExams]; }
function getExam(id){ return allExams().find(e=>e.id===id); }

function showToast(msg){
  const t = document.getElementById('toast');
  t.textContent = msg; t.classList.add('show');
  clearTimeout(t._h);
  t._h = setTimeout(()=>t.classList.remove('show'), 2200);
}

/* ============ INIT ============ */
async function init(){
  const user = await store.get('user');
  const customExams = await store.get('customExams');
  const results = await store.get('results');
  state.user = user || null;
  state.customExams = customExams || [];
  state.results = results || {};
  state.screen = state.user ? 'dashboard' : 'login';
  render();
}

/* ============ RENDER ROUTER ============ */
function render(){
  const app = document.getElementById('app');
  app.innerHTML = '';
  app.appendChild(header());
  if(state.screen === 'login') app.appendChild(loginScreen());
  else if(state.screen === 'dashboard') app.appendChild(dashboardScreen());
  else if(state.screen === 'taking') app.appendChild(takingScreen());
  else if(state.screen === 'result') app.appendChild(resultScreen());
  else if(state.screen === 'create') app.appendChild(createScreen());
}

function header(){
  const div = document.createElement('div');
  div.className = 'masthead';
  const left = document.createElement('div');
  left.innerHTML = `<h1 class="type">ExamHall</h1><div class="sub">Online Examination Portal &middot; Est. Session ${new Date().getFullYear()}</div>`;
  div.appendChild(left);
  if(state.user){
    const chip = document.createElement('div');
    chip.className='userchip';
    chip.innerHTML = `<span>${escapeHtml(state.user.name)} &nbsp;|&nbsp; Roll ${state.user.roll}</span>`;
    const logout = document.createElement('button');
    logout.textContent = 'Sign out';
    logout.onclick = async ()=>{
      state.user = null; state.screen='login';
      await store.set('user', null);
      render();
    };
    chip.appendChild(logout);
    div.appendChild(chip);
  }
  return div;
}

function escapeHtml(s){
  const d = document.createElement('div'); d.textContent = s; return d.innerHTML;
}

/* ============ LOGIN ============ */
function loginScreen(){
  const wrap = document.createElement('div');
  wrap.innerHTML = `
    <div class="ticket">
      <div class="ticket-head">
        <span class="type">Admit Card</span>
        <span class="mono">FORM NO. EH-${Math.floor(1000+Math.random()*9000)}</span>
      </div>
      <div class="perf"></div>
      <div class="ticket-body">
        <div class="stamp">VALID</div>
        <div class="field">
          <label>Candidate Name</label>
          <input type="text" id="in-name" placeholder="e.g. Arjun Kumar" autocomplete="off">
        </div>
        <div class="field">
          <label>Roll Number <span class="mono" style="text-transform:none;color:var(--line)">(leave blank to auto-generate)</span></label>
          <input type="text" id="in-roll" placeholder="e.g. EH2026-014" autocomplete="off">
        </div>
        <button class="btn" id="btn-enter" style="width:100%">Enter Examination Hall</button>
      </div>
    </div>
  `;
  setTimeout(()=>{
    document.getElementById('btn-enter').onclick = async ()=>{
      const name = document.getElementById('in-name').value.trim();
      let roll = document.getElementById('in-roll').value.trim();
      if(!name){ showToast('Please enter your name to continue'); return; }
      if(!roll) roll = 'EH' + new Date().getFullYear() + '-' + Math.floor(100+Math.random()*899);
      state.user = {name, roll};
      await store.set('user', state.user);
      state.screen = 'dashboard';
      render();
    };
  });
  return wrap;
}

/* ============ DASHBOARD ============ */
function dashboardScreen(){
  const wrap = document.createElement('div');

  const sheet = document.createElement('div');
  sheet.className = 'sheet';
  const h = document.createElement('h2');
  h.className = 'section'; h.textContent = 'Available Examinations';
  sheet.appendChild(h);

  const exams = allExams();
  if(exams.length === 0){
    sheet.innerHTML += `<div class="empty-state">No examinations scheduled.</div>`;
  } else {
    exams.forEach(exam=>{
      const res = state.results[exam.id];
      const row = document.createElement('div');
      row.className = 'exam-row';
      row.innerHTML = `
        <div>
          <p class="exam-title">${escapeHtml(exam.title)}</p>
          <div class="exam-meta">${escapeHtml(exam.subject)} &middot; ${exam.questions.length} Questions &middot; ${Math.round(exam.duration/60)} min ${res? `&middot; <span class="badge done">Score ${res.score}/${res.total}</span>` : `&middot; <span class="badge pending">Not attempted</span>`}</div>
        </div>
        <div class="btn-row">
          ${res ? `<button class="btn secondary" data-review="${exam.id}">Review</button>` : ''}
          <button class="btn" data-start="${exam.id}">${res? 'Retake' : 'Start Exam'}</button>
        </div>
      `;
      sheet.appendChild(row);
    });
  }
  wrap.appendChild(sheet);

  const createSheet = document.createElement('div');
  createSheet.className = 'sheet';
  createSheet.innerHTML = `
    <h2 class="section">Set a New Examination</h2>
    <p style="color:var(--pencil);font-size:14px;margin-top:-6px;">Build your own timed multiple-choice test — it will appear above for you to take any time.</p>
    <button class="btn secondary" id="btn-create">+ Create Exam</button>
  `;
  wrap.appendChild(createSheet);

  setTimeout(()=>{
    wrap.querySelectorAll('[data-start]').forEach(btn=>{
      btn.onclick = ()=> startExam(btn.getAttribute('data-start'));
    });
    wrap.querySelectorAll('[data-review]').forEach(btn=>{
      btn.onclick = ()=>{ state.currentExamId = btn.getAttribute('data-review'); state.screen='result'; render(); };
    });
    document.getElementById('btn-create').onclick = ()=>{
      state.draftQuestions = [blankDraftQuestion()];
      state.screen = 'create';
      render();
    };
  });

  return wrap;
}

/* ============ TAKE EXAM ============ */
function startExam(examId){
  const exam = getExam(examId);
  state.currentExamId = examId;
  state.liveAnswers = {};
  state.currentQ = 0;
  state.timeLeft = exam.duration;
  state.screen = 'taking';
  render();
  startTimer();
}

function startTimer(){
  clearInterval(state.timerHandle);
  state.timerHandle = setInterval(()=>{
    state.timeLeft--;
    updateClockDisplay();
    if(state.timeLeft <= 0){
      clearInterval(state.timerHandle);
      submitExam(true);
    }
  }, 1000);
}

function updateClockDisplay(){
  const el = document.getElementById('clock-display');
  if(!el) return;
  const m = Math.floor(state.timeLeft/60).toString().padStart(2,'0');
  const s = (state.timeLeft%60).toString().padStart(2,'0');
  el.textContent = `${m}:${s}`;
  el.parentElement.classList.toggle('warn', state.timeLeft <= 30);
}

function takingScreen(){
  const exam = getExam(state.currentExamId);
  const q = exam.questions[state.currentQ];
  const wrap = document.createElement('div');

  const topbar = document.createElement('div');
  topbar.className = 'exam-topbar';
  topbar.innerHTML = `
    <div>
      <p class="exam-title" style="margin-bottom:2px;">${escapeHtml(exam.title)}</p>
      <div class="exam-meta">${escapeHtml(exam.subject)}</div>
    </div>
    <div class="clock"><span id="clock-display" class="mono"></span></div>
  `;
  wrap.appendChild(topbar);

  const nav = document.createElement('div');
  nav.className = 'qnav';
  exam.questions.forEach((_,i)=>{
    const b = document.createElement('button');
    b.textContent = i+1;
    b.className = (i===state.currentQ ? 'current ' : '') + (state.liveAnswers[i] !== undefined ? 'answered' : '');
    b.onclick = ()=>{ state.currentQ = i; render(); startTimer.keepGoing = true; requestAnimationFrame(updateClockDisplay); };
    nav.appendChild(b);
  });
  wrap.appendChild(nav);

  const sheet = document.createElement('div');
  sheet.className = 'sheet';
  sheet.innerHTML = `<div class="question-num mono">QUESTION ${state.currentQ+1} OF ${exam.questions.length}</div><div class="question-text">${escapeHtml(q.q)}</div>`;
  const optWrap = document.createElement('div');
  q.opts.forEach((opt,i)=>{
    const row = document.createElement('div');
    row.className = 'omr-option' + (state.liveAnswers[state.currentQ]===i ? ' selected' : '');
    row.innerHTML = `<span class="opt-letter mono">${String.fromCharCode(65+i)}</span><span class="bubble"></span><span class="opt-text">${escapeHtml(opt)}</span>`;
    row.onclick = ()=>{ state.liveAnswers[state.currentQ] = i; render(); };
    optWrap.appendChild(row);
  });
  sheet.appendChild(optWrap);
  wrap.appendChild(sheet);

  const btnRow = document.createElement('div');
  btnRow.className = 'btn-row';
  btnRow.style.justifyContent = 'space-between';
  const leftBtns = document.createElement('div');
  leftBtns.className = 'btn-row';
  const prevBtn = document.createElement('button');
  prevBtn.className='btn secondary'; prevBtn.textContent='Previous';
  prevBtn.disabled = state.currentQ===0;
  prevBtn.onclick = ()=>{ state.currentQ--; render(); };
  leftBtns.appendChild(prevBtn);
  if(state.currentQ < exam.questions.length-1){
    const nextBtn = document.createElement('button');
    nextBtn.className='btn secondary'; nextBtn.textContent='Next';
    nextBtn.onclick = ()=>{ state.currentQ++; render(); };
    leftBtns.appendChild(nextBtn);
  }
  btnRow.appendChild(leftBtns);
  const submitBtn = document.createElement('button');
  submitBtn.className = 'btn danger';
  submitBtn.textContent = 'Submit Exam';
  submitBtn.onclick = ()=>{
    const answered = Object.keys(state.liveAnswers).length;
    const total = exam.questions.length;
    if(answered < total){
      if(!confirm(`You have answered ${answered} of ${total} questions. Submit anyway?`)) return;
    }
    clearInterval(state.timerHandle);
    submitExam(false);
  };
  btnRow.appendChild(submitBtn);
  wrap.appendChild(btnRow);

  setTimeout(updateClockDisplay);
  return wrap;
}

async function submitExam(autoSubmitted){
  const exam = getExam(state.currentExamId);
  let score = 0;
  exam.questions.forEach((q,i)=>{
    if(state.liveAnswers[i] === q.correct) score++;
  });
  const result = {
    score, total: exam.questions.length,
    answers: {...state.liveAnswers},
    submittedAt: new Date().toISOString(),
    auto: autoSubmitted
  };
  state.results[exam.id] = result;
  await store.set('results', state.results);
  state.screen = 'result';
  render();
  if(autoSubmitted) showToast("Time's up — your exam was submitted automatically.");
}

/* ============ RESULT / REVIEW ============ */
function resultScreen(){
  const exam = getExam(state.currentExamId);
  const res = state.results[exam.id];
  const wrap = document.createElement('div');

  const sheet = document.createElement('div');
  sheet.className = 'sheet';
  sheet.innerHTML = `<h2 class="section">${escapeHtml(exam.title)} — Result</h2>`;
  const banner = document.createElement('div');
  banner.className = 'score-banner';
  const pct = Math.round((res.score/res.total)*100);
  banner.innerHTML = `
    <div class="score-circle"><span class="n">${res.score}/${res.total}</span><span class="d">${pct}%</span></div>
    <div>
      <p style="margin:0 0 4px;font-family:'IBM Plex Mono',monospace;font-size:13px;color:var(--pencil);">Submitted ${new Date(res.submittedAt).toLocaleString()}${res.auto? ' (auto-submitted, time expired)':''}</p>
      <p style="margin:0;font-size:16px;">${pct>=80?'Excellent work.':pct>=50?'Solid attempt — review the misses below.':'Worth another attempt — review the answers below.'}</p>
    </div>
  `;
  sheet.appendChild(banner);
  wrap.appendChild(sheet);

  const reviewSheet = document.createElement('div');
  reviewSheet.className = 'sheet';
  reviewSheet.innerHTML = `<h2 class="section">Answer Review</h2>`;
  exam.questions.forEach((q,i)=>{
    const given = res.answers[i];
    const isCorrect = given === q.correct;
    const div = document.createElement('div');
    div.className = 'review-q';
    div.innerHTML = `
      <div class="question-num mono">QUESTION ${i+1}</div>
      <div class="question-text" style="font-size:16px;margin:6px 0 8px;">${escapeHtml(q.q)}</div>
      <div class="review-answer ${isCorrect? 'correct':'wrong'}">Your answer: ${given!==undefined ? escapeHtml(q.opts[given]) : '(not answered)'}</div>
      ${!isCorrect ? `<div class="review-answer correct-note">Correct answer: ${escapeHtml(q.opts[q.correct])}</div>` : ''}
    `;
    reviewSheet.appendChild(div);
  });
  wrap.appendChild(reviewSheet);

  const btnRow = document.createElement('div');
  btnRow.className = 'btn-row';
  btnRow.innerHTML = `<button class="btn secondary" id="back-dash">Back to Dashboard</button>`;
  wrap.appendChild(btnRow);
  setTimeout(()=>{
    document.getElementById('back-dash').onclick = ()=>{ state.screen='dashboard'; render(); };
  });

  return wrap;
}

/* ============ CREATE EXAM ============ */
function blankDraftQuestion(){
  return { q:'', opts:['','','',''], correct:0 };
}

function createScreen(){
  const wrap = document.createElement('div');
  const sheet = document.createElement('div');
  sheet.className = 'sheet';
  sheet.innerHTML = `<h2 class="section">Set a New Examination</h2>`;

  const metaDiv = document.createElement('div');
  metaDiv.innerHTML = `
    <div class="field"><label>Exam Title</label><input type="text" id="d-title" placeholder="e.g. Data Structures Quiz"></div>
    <div class="field"><label>Subject / Category</label><input type="text" id="d-subject" placeholder="e.g. Computer Science"></div>
    <div class="field"><label>Duration (minutes)</label><input type="number" id="d-duration" value="10" min="1" max="180"></div>
  `;
  sheet.appendChild(metaDiv);
  wrap.appendChild(sheet);

  const qSheet = document.createElement('div');
  qSheet.className = 'sheet';
  qSheet.innerHTML = `<h2 class="section">Questions</h2>`;
  const qContainer = document.createElement('div');
  qContainer.id = 'q-container';
  qSheet.appendChild(qContainer);
  const addBtn = document.createElement('button');
  addBtn.className = 'btn secondary';
  addBtn.textContent = '+ Add Question';
  addBtn.style.marginTop = '6px';
  addBtn.onclick = ()=>{ state.draftQuestions.push(blankDraftQuestion()); renderQuestions(); };
  qSheet.appendChild(addBtn);
  wrap.appendChild(qSheet);

  function renderQuestions(){
    qContainer.innerHTML = '';
    state.draftQuestions.forEach((dq, qi)=>{
      const block = document.createElement('div');
      block.className = 'qblock';
      block.innerHTML = `
        ${state.draftQuestions.length>1? `<button class="remove-q" data-remove="${qi}">Remove</button>`:''}
        <div class="field" style="margin-bottom:10px;">
          <label>Question ${qi+1}</label>
          <input type="text" data-qtext="${qi}" value="${escapeHtml(dq.q)}" placeholder="Enter the question text">
        </div>
        <div class="opt-grid">
          ${dq.opts.map((o,oi)=>`
            <div class="opt-input-row">
              <input type="radio" name="correct-${qi}" data-correct="${qi}-${oi}" ${dq.correct===oi?'checked':''}>
              <input type="text" data-opt="${qi}-${oi}" value="${escapeHtml(o)}" placeholder="Option ${String.fromCharCode(65+oi)}">
            </div>
          `).join('')}
        </div>
      `;
      qContainer.appendChild(block);
    });

    qContainer.querySelectorAll('[data-qtext]').forEach(inp=>{
      inp.oninput = ()=>{ state.draftQuestions[+inp.getAttribute('data-qtext')].q = inp.value; };
    });
    qContainer.querySelectorAll('[data-opt]').forEach(inp=>{
      inp.oninput = ()=>{
        const [qi,oi] = inp.getAttribute('data-opt').split('-').map(Number);
        state.draftQuestions[qi].opts[oi] = inp.value;
      };
    });
    qContainer.querySelectorAll('[data-correct]').forEach(inp=>{
      inp.onchange = ()=>{
        const [qi,oi] = inp.getAttribute('data-correct').split('-').map(Number);
        state.draftQuestions[qi].correct = oi;
      };
    });
    qContainer.querySelectorAll('[data-remove]').forEach(btn=>{
      btn.onclick = ()=>{
        state.draftQuestions.splice(+btn.getAttribute('data-remove'),1);
        renderQuestions();
      };
    });
  }
  renderQuestions();

  const actionRow = document.createElement('div');
  actionRow.className = 'btn-row';
  actionRow.innerHTML = `
    <button class="btn secondary" id="cancel-create">Cancel</button>
    <button class="btn" id="save-exam">Save & Publish Exam</button>
  `;
  wrap.appendChild(actionRow);

  setTimeout(()=>{
    document.getElementById('cancel-create').onclick = ()=>{ state.screen='dashboard'; render(); };
    document.getElementById('save-exam').onclick = async ()=>{
      const title = document.getElementById('d-title').value.trim();
      const subject = document.getElementById('d-subject').value.trim() || 'General';
      const duration = Math.max(1, parseInt(document.getElementById('d-duration').value||'10',10)) * 60;
      if(!title){ showToast('Please give the exam a title'); return; }
      const cleanQs = state.draftQuestions.filter(q=>q.q.trim() && q.opts.every(o=>o.trim()));
      if(cleanQs.length === 0){ showToast('Add at least one complete question with all options filled in'); return; }
      const exam = {
        id: 'custom-' + Date.now(),
        title, subject, duration,
        seed:false,
        questions: cleanQs
      };
      state.customExams.push(exam);
      await store.set('customExams', state.customExams);
      state.screen = 'dashboard';
      render();
      showToast('Exam published — it now appears on the dashboard.');
    };
  });

  return wrap;
}

init();
</script>
</body>
</html>
