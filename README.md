# Ex03 To-Do List using JavaScript
## Date:

## AIM
To create a To-do Application with all features using JavaScript.

## ALGORITHM
### STEP 1
Build the HTML structure (index.html).

### STEP 2
Style the App (style.css).

### STEP 3
Plan the features the To-Do App should have.

### STEP 4
Create a To-do application using Javascript.

### STEP 5
Add functionalities.

### STEP 6
Test the App.

### STEP 7
Open the HTML file in a browser to check layout and functionality.

### STEP 8
Fix styling issues and refine content placement.

### STEP 9
Deploy the website.

### STEP 10
Upload to GitHub Pages for free hosting.

## PROGRAM
```
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>What Matters Today — To-Do</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,400;0,9..144,500;0,9..144,600;1,9..144,500&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root{
    --bg: #EDEAE4;
    --surface: #FBFAF8;
    --ink: #212B24;
    --ink-soft: #5C665F;
    --ink-faint: #9AA39B;
    --moss: #45624A;
    --moss-light: #E3EAE2;
    --amber: #C68A33;
    --coral: #E0664A;
    --sky: #4C7A9E;
    --lilac: #8A6BAE;
    --line: #DAD5C9;
    --line-soft: #E6E2D8;
    --radius: 10px;
    --shadow: 0 1px 2px rgba(33,43,36,0.04), 0 8px 24px -12px rgba(33,43,36,0.10);
  }

  *{ box-sizing: border-box; }

  html{ -webkit-font-smoothing: antialiased; }

  body{
    margin:0;
    min-height:100vh;
    position: relative;
    overflow-x: hidden;
    background: var(--bg);
    font-family: 'Inter', sans-serif;
    color: var(--ink);
    display:flex;
    justify-content:center;
    padding: 64px 24px 80px;
  }

  /* Colourful ambient blobs behind the content */
  .blob{
    position: fixed;
    border-radius: 50%;
    filter: blur(70px);
    opacity: 0.55;
    z-index: 0;
    pointer-events: none;
  }

  .blob-1{
    width: 480px; height: 480px;
    top: -160px; left: -140px;
    background: radial-gradient(circle at 30% 30%, var(--coral), transparent 70%);
    animation: drift1 22s ease-in-out infinite alternate;
  }

  .blob-2{
    width: 520px; height: 520px;
    bottom: -200px; right: -160px;
    background: radial-gradient(circle at 60% 60%, var(--sky), transparent 70%);
    animation: drift2 26s ease-in-out infinite alternate;
  }

  .blob-3{
    width: 380px; height: 380px;
    top: 30%; right: 10%;
    background: radial-gradient(circle at 50% 50%, var(--amber), transparent 70%);
    opacity: 0.4;
    animation: drift3 30s ease-in-out infinite alternate;
  }

  .blob-4{
    width: 340px; height: 340px;
    bottom: 8%; left: 4%;
    background: radial-gradient(circle at 50% 50%, var(--lilac), transparent 70%);
    opacity: 0.35;
    animation: drift1 24s ease-in-out infinite alternate-reverse;
  }

  @keyframes drift1{
    from{ transform: translate(0,0) scale(1); }
    to{ transform: translate(40px, 30px) scale(1.08); }
  }
  @keyframes drift2{
    from{ transform: translate(0,0) scale(1); }
    to{ transform: translate(-50px, -30px) scale(1.1); }
  }
  @keyframes drift3{
    from{ transform: translate(0,0) scale(1); }
    to{ transform: translate(-30px, 40px) scale(0.95); }
  }

  @media (prefers-reduced-motion: reduce){
    .blob{ animation: none !important; }
  }

  .app{
    width:100%;
    max-width: 560px;
    position: relative;
    z-index: 1;
    background: rgba(251,250,248,0.72);
    backdrop-filter: blur(18px);
    -webkit-backdrop-filter: blur(18px);
    border: 1px solid rgba(255,255,255,0.6);
    border-radius: 20px;
    padding: 40px 36px 32px;
    box-shadow: 0 1px 2px rgba(33,43,36,0.04), 0 24px 60px -24px rgba(33,43,36,0.18);
  }

  @media (max-width: 480px){
    .app{ padding: 28px 20px 24px; }
  }

  /* ---------- Hero ---------- */
  .hero{
    margin-bottom: 40px;
  }

  .eyebrow{
    font-family:'JetBrains Mono', monospace;
    font-size: 12px;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    color: var(--moss);
    margin: 0 0 14px;
    display:flex;
    align-items:center;
    gap: 8px;
  }

  .eyebrow::before{
    content:"";
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: var(--amber);
    display:inline-block;
  }

  .hero h1{
    font-family:'Fraunces', serif;
    font-weight: 500;
    font-size: clamp(32px, 5vw, 44px);
    line-height: 1.1;
    letter-spacing: -0.01em;
    margin: 0 0 10px;
  }

  .hero .sub{
    margin:0;
    color: var(--ink-soft);
    font-size: 15px;
  }

  /* ---------- Add form ---------- */
  .add-form{
    position: relative;
    display:flex;
    align-items:center;
    gap: 12px;
    background: var(--surface);
    border: 1px solid var(--line);
    border-radius: var(--radius);
    padding: 4px 4px 4px 20px;
    box-shadow: var(--shadow);
    margin-bottom: 28px;
    transition: border-color .2s ease, box-shadow .2s ease;
  }

  .add-form:focus-within{
    border-color: var(--moss);
    box-shadow: 0 0 0 3px var(--moss-light), var(--shadow);
  }

  .add-form input{
    flex:1;
    border:none;
    outline:none;
    background:transparent;
    font-family:'Inter', sans-serif;
    font-size: 15.5px;
    color: var(--ink);
    padding: 14px 0;
  }

  .add-form input::placeholder{
    color: var(--ink-faint);
  }

  .add-form button{
    flex-shrink:0;
    width: 40px;
    height: 40px;
    border-radius: 8px;
    border:none;
    background: var(--ink);
    color: var(--bg);
    cursor:pointer;
    display:flex;
    align-items:center;
    justify-content:center;
    transition: background .18s ease, transform .12s ease;
  }

  .add-form button:hover{ background: var(--moss); }
  .add-form button:active{ transform: scale(0.92); }

  .add-form button svg{ width:18px; height:18px; }

  /* ---------- Filters ---------- */
  .filters{
    position:relative;
    display:flex;
    gap: 22px;
    margin-bottom: 22px;
    border-bottom: 1px solid var(--line-soft);
    padding-bottom: 0;
  }

  .filter-btn{
    background:none;
    border:none;
    font-family:'Inter', sans-serif;
    font-size: 13.5px;
    font-weight: 500;
    color: var(--ink-faint);
    cursor:pointer;
    padding: 0 2px 12px;
    position: relative;
    transition: color .18s ease;
  }

  .filter-btn.active{ color: var(--ink); }
  .filter-btn:hover{ color: var(--ink); }

  .filter-indicator{
    position:absolute;
    bottom: -1px;
    height: 2px;
    background: var(--moss);
    border-radius: 2px;
    transition: left .25s cubic-bezier(.4,0,.2,1), width .25s cubic-bezier(.4,0,.2,1);
  }

  /* ---------- Task list ---------- */
  .task-list{
    list-style:none;
    margin:0 0 8px;
    padding:0;
    display:flex;
    flex-direction:column;
    gap: 2px;
  }

  .task{
    display:flex;
    align-items:flex-start;
    gap: 14px;
    padding: 14px 6px;
    border-bottom: 1px solid var(--line-soft);
    animation: rise .32s cubic-bezier(.2,.8,.2,1) both;
  }

  .task.removing{
    animation: fade-collapse .28s ease forwards;
  }

  @keyframes rise{
    from{ opacity:0; transform: translateY(6px); }
    to{ opacity:1; transform: translateY(0); }
  }

  @keyframes fade-collapse{
    to{ opacity:0; transform: translateX(8px); max-height:0; padding-top:0; padding-bottom:0; margin:0; }
  }

  .task-check{
    flex-shrink:0;
    width: 22px;
    height: 22px;
    margin-top: 1px;
    border-radius: 50%;
    border: 1.5px solid var(--ink-faint);
    background: transparent;
    cursor:pointer;
    display:flex;
    align-items:center;
    justify-content:center;
    padding:0;
    transition: border-color .2s ease, background .2s ease;
  }

  .task-check:hover{ border-color: var(--moss); }

  .task.done .task-check{
    background: var(--moss);
    border-color: var(--moss);
  }

  .task-check svg{
    width: 12px;
    height: 12px;
    stroke: var(--surface);
    stroke-width: 2.6;
    fill:none;
    stroke-linecap: round;
    stroke-linejoin: round;
    stroke-dasharray: 16;
    stroke-dashoffset: 16;
    transition: stroke-dashoffset .28s ease .04s;
  }

  .task.done .task-check svg{ stroke-dashoffset: 0; }

  .task-text{
    flex:1;
    position: relative;
    font-size: 15.5px;
    line-height: 1.5;
    padding-top: 1px;
    color: var(--ink);
    word-break: break-word;
  }

  .task-text::after{
    content:"";
    position:absolute;
    left:0; top:50%;
    width: 0%;
    height: 1px;
    background: var(--ink-faint);
    transition: width .35s ease;
  }

  .task.done .task-text{ color: var(--ink-faint); }
  .task.done .task-text::after{ width: 100%; }

  .task-delete{
    flex-shrink:0;
    width: 26px;
    height: 26px;
    border:none;
    background:none;
    color: var(--ink-faint);
    cursor:pointer;
    opacity:0;
    display:flex;
    align-items:center;
    justify-content:center;
    border-radius: 6px;
    transition: opacity .15s ease, color .15s ease, background .15s ease;
  }

  .task:hover .task-delete{ opacity:1; }
  .task-delete:hover{ color: #B4432E; background: rgba(180,67,46,0.08); }
  .task-delete svg{ width:15px; height:15px; }

  /* ---------- Empty state ---------- */
  .empty-state{
    display:none;
    text-align:center;
    padding: 48px 20px;
    color: var(--ink-faint);
  }

  .empty-state.visible{ display:block; }

  .empty-state svg{
    width: 34px; height:34px;
    margin-bottom: 14px;
    stroke: var(--ink-faint);
  }

  .empty-state p{
    margin:0;
    font-size: 14.5px;
    font-family: 'Fraunces', serif;
    font-style: italic;
  }

  /* ---------- Footer ---------- */
  .app-footer{ margin-top: 22px; }

  .progress-track{
    width:100%;
    height: 3px;
    background: var(--line-soft);
    border-radius: 3px;
    overflow:hidden;
    margin-bottom: 12px;
  }

  .progress-fill{
    height:100%;
    width:0%;
    background: linear-gradient(90deg, var(--moss), var(--amber));
    border-radius: 3px;
    transition: width .4s cubic-bezier(.4,0,.2,1);
  }

  .footer-row{
    display:flex;
    align-items:center;
    justify-content:space-between;
    font-size: 13px;
    color: var(--ink-faint);
  }

  #clear-completed{
    background:none;
    border:none;
    color: var(--ink-soft);
    font-family:'Inter', sans-serif;
    font-size: 13px;
    cursor:pointer;
    text-decoration: underline;
    text-decoration-color: var(--line);
    text-underline-offset: 3px;
    transition: color .15s ease;
  }

  #clear-completed:hover{ color: var(--ink); text-decoration-color: var(--ink-faint); }

  /* ---------- Focus visibility & motion ---------- */
  button:focus-visible, input:focus-visible{
    outline: 2px solid var(--moss);
    outline-offset: 2px;
  }

  @media (prefers-reduced-motion: reduce){
    *{ animation-duration: 0.001s !important; transition-duration: 0.001s !important; }
  }

  @media (max-width: 480px){
    body{ padding: 40px 16px 60px; }
    .hero h1{ font-size: 30px; }
  }
</style>
</head>
<body>

<div class="blob blob-1"></div>
<div class="blob blob-2"></div>
<div class="blob blob-3"></div>
<div class="blob blob-4"></div>

<div class="app">
  <header class="hero">
    <p class="eyebrow"><span id="today-date">Today</span></p>
    <h1>What matters today</h1>
    <p class="sub" id="counter">No tasks yet — start by adding one below.</p>
  </header>

  <div class="add-form" id="add-form">
    <input type="text" id="task-input" placeholder="Add a task…" autocomplete="off" maxlength="200" />
    <button type="button" id="add-btn" aria-label="Add task">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><line x1="12" y1="5" x2="12" y2="19"/><line x1="5" y1="12" x2="19" y2="12"/></svg>
    </button>
  </div>

  <nav class="filters" id="filters">
    <button class="filter-btn active" data-filter="all">All</button>
    <button class="filter-btn" data-filter="active">Active</button>
    <button class="filter-btn" data-filter="done">Done</button>
    <span class="filter-indicator" id="filter-indicator"></span>
  </nav>

  <ul class="task-list" id="task-list"></ul>

  <div class="empty-state" id="empty-state">
    <svg viewBox="0 0 24 24" fill="none" stroke-width="1.5"><path d="M9 11l3 3L22 4M4 12v6a2 2 0 002 2h12a2 2 0 002-2V7a2 2 0 00-2-2h-6" stroke-linecap="round" stroke-linejoin="round"/></svg>
    <p>Nothing here yet. Add your first task above.</p>
  </div>

  <footer class="app-footer">
    <div class="progress-track"><div class="progress-fill" id="progress-fill"></div></div>
    <div class="footer-row">
      <span id="progress-text">0 of 0 done</span>
      <button id="clear-completed">Clear completed</button>
    </div>
  </footer>
</div>

<script>
(function(){
  // In-memory state (no localStorage available in this environment)
  let tasks = [];
  let idCounter = 1;
  let currentFilter = 'all';

  const addBtn = document.getElementById('add-btn');
  const input = document.getElementById('task-input');
  const list = document.getElementById('task-list');
  const emptyState = document.getElementById('empty-state');
  const counter = document.getElementById('counter');
  const progressFill = document.getElementById('progress-fill');
  const progressText = document.getElementById('progress-text');
  const clearBtn = document.getElementById('clear-completed');
  const filtersNav = document.getElementById('filters');
  const filterIndicator = document.getElementById('filter-indicator');
  const dateEl = document.getElementById('today-date');

  dateEl.textContent = new Date().toLocaleDateString(undefined, { weekday: 'long', month: 'long', day: 'numeric' });

  function checkIcon(){
    return '<svg viewBox="0 0 24 24"><polyline points="20 6 9 17 4 12"/></svg>';
  }

  function trashIcon(){
    return '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="3 6 5 6 21 6"/><path d="M19 6l-1 14a2 2 0 01-2 2H8a2 2 0 01-2-2L5 6"/><path d="M10 11v6M14 11v6"/><path d="M9 6V4a1 1 0 011-1h4a1 1 0 011 1v2"/></svg>';
  }

  function render(){
    list.innerHTML = '';

    const filtered = tasks.filter(t => {
      if(currentFilter === 'active') return !t.done;
      if(currentFilter === 'done') return t.done;
      return true;
    });

    filtered.forEach(task => {
      const li = document.createElement('li');
      li.className = 'task' + (task.done ? ' done' : '');
      li.dataset.id = task.id;
      li.innerHTML = `
        <button class="task-check" aria-label="Toggle task">${checkIcon()}</button>
        <span class="task-text">${escapeHtml(task.text)}</span>
        <button class="task-delete" aria-label="Delete task">${trashIcon()}</button>
      `;
      list.appendChild(li);
    });

    emptyState.classList.toggle('visible', tasks.length === 0);

    const total = tasks.length;
    const done = tasks.filter(t => t.done).length;

    counter.textContent = total === 0
      ? 'No tasks yet — start by adding one below.'
      : `${total} ${total === 1 ? 'task' : 'tasks'} · ${total - done} remaining`;

    progressText.textContent = `${done} of ${total} done`;
    progressFill.style.width = total ? `${(done/total)*100}%` : '0%';
  }

  function escapeHtml(str){
    const div = document.createElement('div');
    div.textContent = str;
    return div.innerHTML;
  }

  function addTask(text){
    tasks.unshift({ id: idCounter++, text: text.trim(), done: false });
    render();
  }

  function handleAdd(){
    const val = input.value.trim();
    if(!val) return;
    addTask(val);
    input.value = '';
    input.focus();
  }

  addBtn.addEventListener('click', handleAdd);

  input.addEventListener('keydown', e => {
    if(e.key === 'Enter'){
      e.preventDefault();
      handleAdd();
    }
  });

  list.addEventListener('click', e => {
    const check = e.target.closest('.task-check');
    const del = e.target.closest('.task-delete');
    const li = e.target.closest('.task');
    if(!li) return;
    const id = Number(li.dataset.id);

    if(check){
      const task = tasks.find(t => t.id === id);
      if(task){ task.done = !task.done; render(); }
    }

    if(del){
      li.classList.add('removing');
      li.addEventListener('animationend', () => {
        tasks = tasks.filter(t => t.id !== id);
        render();
      }, { once:true });
    }
  });

  clearBtn.addEventListener('click', () => {
    tasks = tasks.filter(t => !t.done);
    render();
  });

  function moveIndicator(btn){
    const navRect = filtersNav.getBoundingClientRect();
    const btnRect = btn.getBoundingClientRect();
    filterIndicator.style.left = (btnRect.left - navRect.left) + 'px';
    filterIndicator.style.width = btnRect.width + 'px';
  }

  filtersNav.addEventListener('click', e => {
    const btn = e.target.closest('.filter-btn');
    if(!btn) return;
    document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    currentFilter = btn.dataset.filter;
    moveIndicator(btn);
    render();
  });

  window.addEventListener('resize', () => {
    moveIndicator(document.querySelector('.filter-btn.active'));
  });

  // Seed with a couple of gentle example tasks
  tasks = [
    { id: idCounter++, text: 'Take a breath and plan your day', done: false },
    { id: idCounter++, text: 'Try checking something off', done: true }
  ];

  render();
  requestAnimationFrame(() => moveIndicator(document.querySelector('.filter-btn.active')));
})();
</script>

</body>
</html>
```



## OUTPUT
<img width="1915" height="907" alt="image" src="https://github.com/user-attachments/assets/5e77dfe3-1da8-4d8a-b1b4-470be3ce1b0a" />



## RESULT
The program for creating To-do list using JavaScript is executed successfully.
