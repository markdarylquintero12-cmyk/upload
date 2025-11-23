<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>DALTON — Student Support</title>

<style>
  :root{
    --bg:#f5f7fb;
    --card:#ffffff;
    --primary:#2563eb;
    --accent:#7c3aed;
    --muted:#6b7280;
    --success:#10b981;
    --danger:#ef4444;
    --radius:14px;
    --glass: rgba(255,255,255,0.6);
  }
  *{box-sizing:border-box}
  body{
    margin:0;
    font-family:Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    background: linear-gradient(180deg,var(--bg),#eef2ff 60%);
    color:#0f172a;
    -webkit-font-smoothing:antialiased;
  }

  /* center layout */
  .wrap { max-width:980px; margin:28px auto; padding:20px; }

  /* pages */
  .page{ display:none; }
  .page.active{ display:block; }

  /* card */
  .card{
    background:var(--card);
    border-radius:var(--radius);
    padding:18px;
    box-shadow: 0 6px 18px rgba(15,23,42,0.08);
    margin-bottom:18px;
  }

  /* login */
  .login-grid{ display:grid; grid-template-columns:1fr 1fr; gap:16px; align-items:start; }
  .full { grid-column:1/-1; }

  label{ font-weight:600; color:#0f172a; display:block; margin-bottom:6px; font-size:14px;}
  input[type="text"]{ width:100%; padding:10px 12px; border-radius:10px; border:1px solid #e6eef8; background:#fbfdff; }
  .role-row{ display:flex; gap:10px; }
  .btn{ background:var(--primary); color:#fff; border:none; padding:10px 14px; border-radius:10px; cursor:pointer; font-weight:600; }
  .btn.secondary{ background:#fff; color:var(--primary); border:1px solid #dbeafe; }
  .btn.ghost{ background:transparent; color:var(--muted); border:1px dashed rgba(15,23,42,0.06); }

  .emoji-grid{ display:flex; flex-wrap:wrap; gap:10px; }
  .emoji-btn{ font-size:26px; cursor:pointer; padding:8px; border-radius:10px; border:1px solid transparent; background:transparent; }
  .emoji-btn.selected{ box-shadow:0 4px 14px rgba(37,99,235,0.12); border:1px solid rgba(37,99,235,0.12); background:linear-gradient(180deg, rgba(37,99,235,0.03), rgba(124,58,237,0.02)); }

  h1.site-title{ margin:0 0 10px 0; font-size:22px; letter-spacing:0.2px; color:var(--primary); }

  /* header on feed */
  .header{
    display:flex; justify-content:space-between; align-items:center; gap:12px; margin-bottom:12px;
  }
  .profile{
    display:flex; gap:10px; align-items:center;
  }
  .avatar{ width:48px; height:48px; border-radius:12px; display:flex; align-items:center; justify-content:center; font-size:22px; background:linear-gradient(180deg,#fff,#fff); box-shadow:0 8px 24px rgba(2,6,23,0.06);}
  .welcome{ font-weight:700; font-size:15px; }
  .meta{ font-size:13px; color:var(--muted); }

  .controls{ display:flex; gap:8px; align-items:center; }

  /* feed */
  .feed{
    display:grid; grid-template-columns: 1fr 340px; gap:18px;
  }
  .main-col{ }
  .side-col{ }

  .post{
    border-radius:12px; padding:14px; background:linear-gradient(180deg,#ffffff,#fbfdff); border:1px solid #eef2ff; margin-bottom:12px;
  }
  .post-head{ display:flex; gap:12px; align-items:center; }
  .post-username{ font-weight:700; font-size:15px; }
  .post-role{ font-size:12px; color:var(--muted); margin-left:6px; }
  .post-time{ margin-left:auto; font-size:12px; color:var(--muted); }

  .post-body{ margin-top:10px; font-size:14px; color:#0f172a; line-height:1.4; }
  .post-emotion{ display:inline-block; margin-top:8px; font-size:20px; }

  .comment-block{ margin-top:12px; padding:10px; border-radius:10px; background:#f1f5f9; border:1px solid rgba(2,6,23,0.03); }
  .comment-block b{ display:block; margin-bottom:6px; }

  .teacher-comment{ background:#fff8f6; border:1px solid rgba(239,68,68,0.06); }

  .post-actions{ display:flex; gap:8px; margin-top:10px; }
  .small-btn{ padding:8px 10px; border-radius:10px; border:none; cursor:pointer; font-weight:600; font-size:13px; }
  .small-btn.ghost{ background:transparent; border:1px solid rgba(15,23,42,0.06); color:var(--muted); }
  .small-btn.primary{ background:var(--primary); color:#fff; }

  /* compose card (side) */
  .compose-card textarea{ width:100%; min-height:100px; padding:10px; border-radius:8px; border:1px solid #e6eef8; resize:vertical; font-size:14px; background:#fbfdff; }
  .compose-footer{ display:flex; gap:8px; align-items:center; justify-content:space-between; margin-top:8px; }

  /* teacher comment input */
  .teacher-input{ margin-top:8px; display:flex; gap:8px; align-items:center; }
  .teacher-input input{ flex:1; padding:8px 10px; border-radius:8px; border:1px solid #e6eef8; }

  /* filters */
  .filters{ display:flex; gap:8px; margin-bottom:12px; align-items:center; }
  .chip{ padding:8px 10px; border-radius:999px; border:1px solid transparent; background:transparent; cursor:pointer; font-weight:600; color:var(--muted);}
  .chip.active{ background:linear-gradient(90deg,#eef2ff,#f8f3ff); border:1px solid rgba(37,99,235,0.06); color:var(--primary); }

  /* responsive */
  @media (max-width:880px){
    .feed{ grid-template-columns: 1fr; }
    .avatar{ width:44px; height:44px; }
    .login-grid{ grid-template-columns:1fr; }
  }
</style>
</head>
<body>

<div class="wrap">

  <!-- LOGIN PAGE -->
  <div id="page-login" class="page active">
    <div class="card">
      <h1 class="site-title">DALTON — Student Support & Counseling</h1>
      <p class="meta">A safe space for students to share feelings. Teachers can counsel — AI gives supportive replies.</p>
    </div>

    <div class="card">
      <div class="login-grid">
        <div>
          <label for="username">Username</label>
          <input id="username" type="text" placeholder="e.g. juan.dela.cruz" />

          <div style="height:8px"></div>
          <label>Choose Role</label>
          <div class="role-row">
            <button class="btn" id="role-student">Student</button>
            <button class="btn secondary" id="role-teacher">Teacher</button>
          </div>

          <div style="height:8px"></div>
          <label>Select Avatar (choose one)</label>
          <div class="emoji-grid" id="avatar-options">
            <!-- avatar options injected by JS -->
          </div>

          <div style="height:10px"></div>
          <button class="btn" id="enter-btn">Enter DALTON</button>
        </div>

        <div>
          <label>Why DALTON?</label>
          <p style="color:var(--muted); margin-top:6px;">
            Share feelings, get supportive messages from an AI counselor and receive guidance from your teachers.
            Your posts are shown on the feed; teachers can respond with counseling messages.
          </p>

          <div style="height:12px"></div>
          <label>Tips</label>
          <ul style="color:var(--muted); margin:6px 0 0 18px;">
            <li>Be honest and kind — our AI will offer encouragement.</li>
            <li>Teachers: add constructive, supportive responses.</li>
            <li>Your username helps teachers identify you privately.</li>
          </ul>
        </div>
      </div>
    </div>

    <div class="card full">
      <small style="color:var(--muted)">
        This is a front-end prototype with local storage. If you want login persistence across devices or privacy features, I can add server-side storage later.
      </small>
    </div>
  </div>

  <!-- FEED PAGE -->
  <div id="page-feed" class="page">
    <div class="card header">
      <div class="profile">
        <div class="avatar" id="hdr-avatar">🙂</div>
        <div>
          <div class="welcome" id="hdr-welcome">Welcome</div>
          <div class="meta" id="hdr-role">Role</div>
        </div>
      </div>

      <div class="controls">
        <div style="text-align:right;">
          <small class="meta" id="time-now"></small><br>
          <button class="btn ghost" id="logout-btn">Logout</button>
        </div>
      </div>
    </div>

    <div class="feed">
      <div class="main-col">
        <div class="card">
          <div style="display:flex; justify-content:space-between; align-items:center; gap:10px;">
            <div>
              <h3 style="margin:0">Feed</h3>
              <div class="meta" style="margin-top:6px">See posts from students. AI will respond automatically. Teachers can add counseling comments.</div>
            </div>

            <div style="display:flex; gap:8px; align-items:center;">
              <button class="chip active" data-filter="all">All</button>
              <button class="chip" data-filter="students">Students</button>
              <button class="chip" data-filter="mine">Mine</button>
              <button class="btn" id="compose-open">Compose</button>
            </div>
          </div>
        </div>

        <div id="posts-list"></div>
      </div>

      <div class="side-col">
        <div class="card compose-card">
          <h4 style="margin:0 0 8px 0">Quick Compose</h4>
          <small class="meta">Write a short message and choose emotion below — post will appear on the feed.</small>

          <div style="height:8px"></div>
          <textarea id="quick-text" placeholder="I feel..."></textarea>

          <div class="compose-footer">
            <div class="emoji-grid" id="quick-emotions" style="gap:6px">
              <!-- emotions injected by JS -->
            </div>
            <button class="btn" id="quick-post">Post</button>
          </div>
        </div>

        <div class="card" style="margin-top:12px;">
          <h4 style="margin:0 0 6px 0">Teacher Panel</h4>
          <div class="meta">Only visible actions to teachers: add counseling response to posts.</div>
          <div style="height:10px"></div>
          <div id="teacher-notes" class="meta">No new notes.</div>
        </div>

        <div class="card" style="margin-top:12px;">
          <h4 style="margin:0 0 6px 0">About DALTON</h4>
          <small class="meta">
            Built as a supportive classroom tool. Posts are stored locally on your browser.
          </small>
        </div>
      </div>
    </div>
  </div>

  <!-- COMPOSE PAGE (full editor) -->
  <div id="page-compose" class="page">
    <div class="card">
      <div style="display:flex; justify-content:space-between; align-items:center;">
        <div>
          <h2 style="margin:0">Compose Complaint</h2>
          <div class="meta">Select an emotion that best fits how you feel, write your message, then Post.</div>
        </div>
        <div>
          <button class="btn ghost" id="compose-back">Back</button>
        </div>
      </div>
    </div>

    <div class="card">
      <label><b>Emotion</b></label>
      <div class="emoji-grid" id="compose-emotions"></div>

      <div style="height:10px"></div>
      <label><b>Your Message</b></label>
      <textarea id="compose-text" placeholder="Write what's on your mind..."></textarea>

      <div style="height:10px"></div>
      <div style="display:flex; gap:8px; justify-content:flex-end;">
        <button class="btn secondary" id="compose-clear">Clear</button>
        <button class="btn" id="compose-post">Post Complaint</button>
      </div>
    </div>
  </div>
</div>

<script>
/* -------------------------
   Data & Utilities
   ------------------------- */
const AVATARS = ['😀','😊','😎','🧑‍🎓','🧑‍🏫','😅','😔','😢','🤍','🤝','🌟','🔥','🦋','🌈'];
const EMOTIONS = [
  {code:'😔', label:'Sad / Down'},
  {code:'😡', label:'Angry / Annoyed'},
  {code:'😢', label:'Very Sad / Crying'},
  {code:'😞', label:'Disappointed'},
  {code:'🤯', label:'Overwhelmed'},
  {code:'🙂', label:'Okay / Fine'},
  {code:'😌', label:'Relieved / Calm'}
];

const STORAGE_KEY = 'dalton_posts_v1';

/* load / save posts (localStorage) */
function loadPosts() {
  try {
    const raw = localStorage.getItem(STORAGE_KEY);
    return raw ? JSON.parse(raw) : [];
  } catch(e) { return []; }
}
function savePosts(posts) {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(posts));
}

/* fetch UI elements */
const pageLogin = document.getElementById('page-login');
const pageFeed = document.getElementById('page-feed');
const pageCompose = document.getElementById('page-compose');

const avatarOptions = document.getElementById('avatar-options');
const composeEmotions = document.getElementById('compose-emotions');
const quickEmotions = document.getElementById('quick-emotions');

const usernameInput = document.getElementById('username');

/* runtime state */
let SESSION = { username:'', role:'', avatar:'' };
let posts = loadPosts();
let selectedAvatar = '';
let selectedRole = '';
let composeSelectedEmotion = '';
let quickSelectedEmotion = '';

/* -------------------------
   Render initial pickers
   ------------------------- */
function renderAvatarOptions(){
  avatarOptions.innerHTML = '';
  AVATARS.forEach(a=>{
    const btn = document.createElement('button');
    btn.className = 'emoji-btn';
    btn.innerText = a;
    btn.title = a;
    btn.onclick = ()=> {
      document.querySelectorAll('#avatar-options .emoji-btn').forEach(x=>x.classList.remove('selected'));
      btn.classList.add('selected');
      selectedAvatar = a;
    };
    avatarOptions.appendChild(btn);
  });
}

function renderComposeEmotions(){
  composeEmotions.innerHTML = '';
  EMOTIONS.forEach(e=>{
    const btn = document.createElement('button');
    btn.className = 'emoji-btn';
    btn.innerText = e.code;
    btn.title = e.label;
    btn.onclick = ()=> {
      document.querySelectorAll('#compose-emotions .emoji-btn').forEach(x=>x.classList.remove('selected'));
      btn.classList.add('selected');
      composeSelectedEmotion = e.code;
    };
    composeEmotions.appendChild(btn);
  });
}

function renderQuickEmotions(){
  quickEmotions.innerHTML = '';
  EMOTIONS.forEach(e=>{
    const btn = document.createElement('button');
    btn.className = 'emoji-btn';
    btn.innerText = e.code;
    btn.title = e.label;
    btn.onclick = ()=> {
      document.querySelectorAll('#quick-emotions .emoji-btn').forEach(x=>x.classList.remove('selected'));
      btn.classList.add('selected');
      quickSelectedEmotion = e.code;
    };
    quickEmotions.appendChild(btn);
  });
}

/* -------------------------
   Page helpers
   ------------------------- */
function showPage(id){
  pageLogin.classList.remove('active');
  pageFeed.classList.remove('active');
  pageCompose.classList.remove('active');
  document.getElementById('page-' + id).classList.add('active');
  // update header time
  document.getElementById('time-now').innerText = (new Date()).toLocaleString();
}

/* -------------------------
   Role selection + login
   ------------------------- */
document.getElementById('role-student').addEventListener('click', ()=>{
  selectedRole = 'Student';
  document.getElementById('role-student').classList.add('btn');
  document.getElementById('role-teacher').classList.remove('btn');
  document.getElementById('role-teacher').classList.add('btn','secondary');
});
document.getElementById('role-teacher').addEventListener('click', ()=>{
  selectedRole = 'Teacher';
  document.getElementById('role-teacher').classList.remove('secondary');
  document.getElementById('role-teacher').classList.add('btn');
  document.getElementById('role-student').classList.remove('btn');
  document.getElementById('role-student').classList.add('btn','secondary');
});

document.getElementById('enter-btn').addEventListener('click', ()=>{
  const name = usernameInput.value.trim();
  if(!name){ alert('Please enter your username.'); usernameInput.focus(); return; }
  if(!selectedRole){ alert('Please choose a role (Student or Teacher).'); return; }
  if(!selectedAvatar){ alert('Please pick an avatar'); return; }

  SESSION.username = name;
  SESSION.role = selectedRole;
  SESSION.avatar = selectedAvatar;

  // show feed
  renderHeader();
  showPage('feed');
  renderPosts();
  updateTeacherNotes();
});

/* logout */
document.getElementById('logout-btn').addEventListener('click', ()=>{
  // clear session and go back
  SESSION = { username:'', role:'', avatar:'' };
  selectedAvatar = ''; selectedRole = '';
  usernameInput.value = '';
  document.querySelectorAll('#avatar-options .emoji-btn').forEach(x=>x.classList.remove('selected'));
  document.querySelectorAll('#role-student,#role-teacher').forEach(x=>x.classList.remove('btn'));
  document.getElementById('role-student').classList.add('btn');
  document.getElementById('role-teacher').classList.add('btn','secondary');
  showPage('login');
});

/* -------------------------
   Header & info
   ------------------------- */
function renderHeader(){
  document.getElementById('hdr-avatar').innerText = SESSION.avatar || '🙂';
  document.getElementById('hdr-welcome').innerText = `Hi, ${SESSION.username}`;
  document.getElementById('hdr-role').innerText = `${SESSION.role}`;
}

/* -------------------------
   Posting logic
   ------------------------- */
function generateAIResponse(emotion, text){
  // simple mapping + small contextualization
  const map = {
    "😔":"I’m sorry you’re feeling down. It helps to talk about it — you’re not alone, and this feeling will pass.",
    "😡":"It’s okay to feel angry. Try to breathe deeply, name the cause, and consider small steps you can take to feel better.",
    "😢":"Crying is okay. Allow yourself to feel, and reach out to someone you trust if you can.",
    "😞":"Disappointment hurts. See what you can learn from the situation and remember progress is step-by-step.",
    "🤯":"When everything feels overwhelming, focus on one small task. You’re doing your best — that matters.",
    "🙂":"Thanks for sharing. Keep checking in with yourself and remember small wins count.",
    "😌":"You sound a bit relieved. Keep doing what helps you stay calm and grounded."
  };
  const base = map[emotion] || "Thanks for sharing — I'm here to listen.";
  // add short tailored line if message contains certain words
  const lower = (text||'').toLowerCase();
  if(lower.includes('friends') || lower.includes('peer')) return base + " If it's about friends, consider speaking honestly with them or a teacher you trust.";
  if(lower.includes('grade') || lower.includes('exam') || lower.includes('fail')) return base + " Try breaking your study into small steps and ask your teacher for guidance.";
  return base;
}

function addPost({username, role, avatar, emotion, text}) {
  const now = new Date().toISOString();
  const ai = generateAIResponse(emotion, text);
  const item = { id:Date.now(), username, role, avatar, emotion, text, ai, teacherComment:'', createdAt: now };
  posts.unshift(item);
  savePosts(posts);
  renderPosts();
}

function updateTeacherNotes(){
  if(SESSION.role === 'Teacher'){
    document.getElementById('teacher-notes').innerText = 'You can add counseling replies on any post. Please be kind and constructive.';
  } else {
    document.getElementById('teacher-notes').innerText = 'Students: post honestly. Teachers: switch role to add responses.';
  }
}

/* compose open / back */
document.getElementById('compose-open').addEventListener('click', ()=>{
  showPage('compose');
  // reset compose selections
  composeSelectedEmotion = '';
  document.querySelectorAll('#compose-emotions .emoji-btn').forEach(x=>x.classList.remove('selected'));
  document.getElementById('compose-text').value = '';
});
document.getElementById('compose-back').addEventListener('click', ()=> showPage('feed'));

/* quick compose */
document.getElementById('quick-post').addEventListener('click', ()=>{
  const txt = document.getElementById('quick-text').value.trim();
  if(!SESSION.username){ alert('Please login first.'); return; }
  if(!txt){ alert('Write a short message first.'); return; }
  if(!quickSelectedEmotion){ alert('Please choose an emotion for your post.'); return; }
  addPost({ username:SESSION.username, role:SESSION.role, avatar:SESSION.avatar, emotion:quickSelectedEmotion, text:txt });
  document.getElementById('quick-text').value = '';
  quickSelectedEmotion = '';
  document.querySelectorAll('#quick-emotions .emoji-btn').forEach(x=>x.classList.remove('selected'));
  showPage('feed');
});

/* full compose post */
document.getElementById('compose-post').addEventListener('click', ()=>{
  const txt = document.getElementById('compose-text').value.trim();
  if(!SESSION.username){ alert('Please login first.'); return; }
  if(!txt){ alert('Write a message first.'); return; }
  if(!composeSelectedEmotion){ alert('Choose an emotion before posting.'); return; }
  addPost({ username:SESSION.username, role:SESSION.role, avatar:SESSION.avatar, emotion:composeSelectedEmotion, text:txt });
  document.getElementById('compose-text').value = '';
  composeSelectedEmotion = '';
  document.querySelectorAll('#compose-emotions .emoji-btn').forEach(x=>x.classList.remove('selected'));
  showPage('feed');
});

/* clear compose */
document.getElementById('compose-clear').addEventListener('click', ()=>{
  document.getElementById('compose-text').value = '';
  composeSelectedEmotion = '';
  document.querySelectorAll('#compose-emotions .emoji-btn').forEach(x=>x.classList.remove('selected'));
});

/* -------------------------
   Render posts to DOM
   ------------------------- */
function renderPosts(filter='all'){
  const container = document.getElementById('posts-list');
  container.innerHTML = '';

  // filter chips
  document.querySelectorAll('.chip').forEach(c=> c.classList.toggle('active', c.dataset.filter === filter));

  let visible = posts.slice(); // copy
  if(filter === 'students') visible = visible.filter(p => p.role.toLowerCase() === 'student');
  if(filter === 'mine') visible = visible.filter(p => p.username === SESSION.username);

  if(!visible.length){
    container.innerHTML = `<div class="card"><div class="meta">No posts yet.</div></div>`;
    return;
  }

  visible.forEach(p=>{
    const div = document.createElement('div');
    div.className = 'post card';
    div.innerHTML = `
      <div class="post-head">
        <div style="display:flex; gap:10px; align-items:center;">
          <div class="avatar" style="width:46px;height:46px;border-radius:10px;">${p.avatar}</div>
          <div>
            <div class="post-username">${escapeHtml(p.username)} <span class="post-role">· ${escapeHtml(p.role)}</span></div>
            <div class="meta" style="font-size:12px;">${new Date(p.createdAt).toLocaleString()}</div>
          </div>
        </div>
        <div class="post-time">${p.emotion}</div>
      </div>

      <div class="post-body">${escapeHtml(p.text)}</div>

      <div class="comment-block" style="margin-top:12px;">
        <b>🤖 AI Counseling</b>
        <div>${escapeHtml(p.ai)}</div>
      </div>

      <div class="comment-block teacher-comment" style="margin-top:10px;">
        <b>👨‍🏫 Teacher Counseling</b>
        <div id="teacher-comment-${p.id}">${p.teacherComment ? escapeHtml(p.teacherComment) : '<span style="color:var(--muted)">No teacher comment yet.</span>'}</div>

        <div class="post-actions">
          ${SESSION.role === 'Teacher' ? `<button class="small-btn ghost" data-action="add-comment" data-id="${p.id}">Add/Update Comment</button>` : ''}
          ${SESSION.username === p.username ? `<button class="small-btn ghost" data-action="delete" data-id="${p.id}">Delete</button>` : ''}
          <button class="small-btn ghost" data-action="share" data-id="${p.id}">Copy link</button>
        </div>
      </div>
    `;
    container.appendChild(div);
  });

  // attach action handlers
  container.querySelectorAll('[data-action]').forEach(btn=>{
    btn.addEventListener('click', (e)=>{
      const id = Number(btn.dataset.id);
      const action = btn.dataset.action;
      if(action==='add-comment'){
        const text = prompt('Enter your counseling message for this student (teacher note):', getPostById(id).teacherComment || '');
        if(text !== null){
          updateTeacherComment(id, text);
        }
      } else if(action==='delete'){
        if(confirm('Delete this post? This cannot be undone.')){
          deletePostById(id);
        }
      } else if(action==='share'){
        const url = location.href.split('#')[0] + `#post-${id}`;
        navigator.clipboard?.writeText(url).then(()=> alert('Post link copied to clipboard!')).catch(()=> alert('Copied: ' + url));
      }
    });
  });
}

/* helper: find post */
function getPostById(id){
  return posts.find(p=>p.id===id);
}
function updateTeacherComment(id, text){
  const p = getPostById(id);
  if(!p) return;
  p.teacherComment = text;
  savePosts(posts);
  renderPosts(currentFilter());
}
function deletePostById(id){
  posts = posts.filter(p=>p.id!==id);
  savePosts(posts);
  renderPosts(currentFilter());
}

/* filter chips */
document.querySelectorAll('.chip').forEach(chip=>{
  chip.addEventListener('click', ()=>{
    const f = chip.dataset.filter;
    renderPosts(f);
  });
});

/* keep track of last filter */
let lastFilter = 'all';
function currentFilter(){ return lastFilter; }
(function bindChipTracking(){
  document.querySelectorAll('.chip').forEach(c=>{
    c.addEventListener('click', ()=> lastFilter = c.dataset.filter);
  });
})();

/* -------------------------
   Utilities
   ------------------------- */
function escapeHtml(s){
  if(!s && s!==0) return '';
  return String(s).replaceAll('&','&amp;').replaceAll('<','&lt;').replaceAll('>','&gt;');
}

/* -------------------------
   Init
   ------------------------- */
renderAvatarOptions();
renderComposeEmotions();
renderQuickEmotions();
renderPosts('all');

/* set initial role UI */
document.getElementById('role-student').classList.add('btn');
document.getElementById('role-teacher').classList.add('btn','secondary');

/* set up quick open compose */
document.getElementById('compose-open').addEventListener('click', ()=> {
  // open compose handled earlier
});

/* small keyboard shortcut: Ctrl+K to open compose */
document.addEventListener('keydown', (e)=>{
  if((e.ctrlKey||e.metaKey) && e.key.toLowerCase()==='k'){
    if(pageFeed.classList.contains('active')) showPage('compose');
    e.preventDefault();
  }
});

/* show anchor post if present (share links) */
window.addEventListener('hashchange', ()=>{
  const h = location.hash;
  if(h.startsWith('#post-')){
    const id = Number(h.replace('#post-',''));
    const p = getPostById(id);
    if(p) {
      alert(`Post by ${p.username} on ${new Date(p.createdAt).toLocaleString()}:\n\n${p.text}`);
    }
  }
});

/* accessibility: Enter key on username to focus avatar */
usernameInput.addEventListener('keydown', (e)=>{
  if(e.key==='Enter') {
    e.preventDefault();
    const first = document.querySelector('#avatar-options .emoji-btn');
    if(first) first.focus();
  }
});

</script>
</body>
</html>
