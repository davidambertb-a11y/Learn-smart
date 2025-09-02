<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>learn smart — Submit topics & answers</title>
  <meta name="description" content="learn smart — Nigerian university students submit topics via web and WhatsApp; the admin posts clear answers that stay saved." />
  <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><rect rx='18' width='100' height='100' fill='%23007cc3'/><text x='50' y='58' font-size='42' text-anchor='middle' font-family='Poppins' fill='white'>LS</text></svg>">

  <!-- Google font -->
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;800&display=swap" rel="stylesheet">

  <style>
    :root{
      --bg-1: linear-gradient(135deg,#042939,#073b5a);
      --card:#071727;
      --accent:#00d1a6;
      --accent-2:#00a3ff;
      --muted:#9fb0bb;
      --glass: rgba(255,255,255,0.03);
      --radius:14px;
      --maxw:1100px;
      color-scheme: dark;
    }
    html,body{height:100%;}
    body{
      margin:0; padding:28px; font-family:'Poppins',system-ui,-apple-system,Segoe UI,Roboto,'Helvetica Neue',Arial; background:var(--bg-1); color:#e8f7f5;
      display:flex; justify-content:center;
    }
    .wrap{width:100%; max-width:var(--maxw);}

    header{display:flex; align-items:center; gap:16px; margin-bottom:20px; flex-wrap:wrap}
    .logo{
      font-weight:800; font-size:34px; letter-spacing:-0.02em; position:relative; line-height:1;
      color:#fff; font-family:'Poppins',sans-serif;
      text-shadow: 0 6px 22px rgba(0,0,0,0.6), 0 2px 6px rgba(0,163,255,0.12);
    }
    .logo::after{
      content:'learn smart'; position:absolute; left:6px; top:6px; color:var(--accent); z-index:-1; opacity:0.95; filter:blur(2px); transform: translateZ(-6px) rotateX(6deg);
    }

    nav{margin-left:auto; display:flex; gap:8px; flex-wrap:wrap}
    .nav-btn{background:transparent;border:1px solid rgba(255,255,255,0.06); padding:9px 12px;border-radius:10px;color:inherit;text-decoration:none;font-weight:600}
    .nav-btn:hover{transform:translateY(-3px); box-shadow:0 8px 24px rgba(0,0,0,0.35)}
    .whatsapp-btn{background:linear-gradient(90deg,var(--accent),var(--accent-2)); color:#002; padding:9px 12px; border-radius:10px; font-weight:800; text-decoration:none}

    .top-controls{display:flex; gap:12px; margin-bottom:18px; align-items:center; flex-wrap:wrap}
    .searchbar{flex:1; display:flex; gap:8px}
    input.search{flex:1; padding:12px 14px; border-radius:10px; border:1px solid rgba(255,255,255,0.04); background:rgba(255,255,255,0.02); color:inherit}
    select.sort{padding:10px 12px; border-radius:10px; border:1px solid rgba(255,255,255,0.04); background:transparent; color:inherit}
    .btn{background:var(--glass); border:1px solid rgba(255,255,255,0.04); padding:10px 14px; border-radius:10px; cursor:pointer; color:inherit; font-weight:700}

    .grid{display:grid; grid-template-columns:1fr 360px; gap:20px}
    .card{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); border-radius:var(--radius); padding:16px; box-shadow:0 10px 30px rgba(2,6,23,0.6); border:1px solid rgba(255,255,255,0.02)}

    .posts{display:flex;flex-direction:column;gap:12px}
    .topic{padding:12px;border-radius:12px;background:linear-gradient(90deg, rgba(255,255,255,0.01), rgba(255,255,255,0.00)); cursor:default; border-left:4px solid rgba(0,163,255,0.12)}
    .topic h3{margin:0;font-size:18px}
    .meta{font-size:12px;color:var(--muted);margin-top:6px}
    .answer{margin-top:10px;padding:12px;border-radius:10px;background:rgba(0,0,0,0.25); color:#e7fbf7}

    aside .card{position:sticky; top:28px}
    .cta{display:flex; gap:8px; flex-direction:column}
    .big-cta{background:linear-gradient(90deg,var(--accent),var(--accent-2)); color:#002; padding:14px 12px; font-weight:800; border-radius:12px; text-align:center}

    .create-form{display:flex; flex-direction:column; gap:8px}
    .create-form input, .create-form textarea{padding:10px;border-radius:10px;border:1px solid rgba(255,255,255,0.04); background:transparent; color:inherit}
    .row{display:flex; gap:8px}

    footer{margin-top:28px; text-align:center; color:var(--muted); font-size:13px}

    .admin-panel{display:none}
    .hint{color:var(--muted); font-size:13px}

    @media (max-width:980px){
      .grid{grid-template-columns:1fr;}
      aside{order:2}
      header{justify-content:center}
    }
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <div class="logo">learn smart</div>

      <nav>
        <a class="nav-btn" href="#home" data-route>Home</a>
        <a class="nav-btn" href="#search" data-route>Search Topics</a>
        <a class="nav-btn whatsapp-btn" id="submitWhatsApp" href="#" target="_blank">Submit via WhatsApp</a>
        <a class="nav-btn" href="#about" data-route>About</a>
        <a class="nav-btn" href="#contact" data-route>Contact</a>
        <a class="nav-btn" id="adminOpen">Admin</a>
      </nav>
    </header>

    <section class="top-controls">
      <div class="searchbar card" style="min-width:320px;">
        <input class="search" id="q" placeholder='Search topics or answers (e.g., "stoichiometry")'>
        <select class="sort" id="sort">
          <option value="newest">Sort: Newest</option>
          <option value="oldest">Sort: Oldest</option>
          <option value="alpha">Sort: A → Z</option>
        </select>
        <button class="btn" id="searchBtn">Search</button>
      </div>

      <div style="display:flex;gap:10px;align-items:center">
        <div style="text-align:right;font-size:13px;color:var(--muted)">Nigeria time: <span id="nigeriatime">—</span></div>
      </div>
    </section>

    <div class="grid">
      <main>
        <div id="home" class="card">
          <h1 style="margin:0 0 8px 0;font-size:22px">Welcome — learn smart</h1>
          <p style="margin:0 0 12px 0;color:var(--muted)">Students submit topics via WhatsApp or the form below. The admin (you) publishes answers for everyone to learn from.</p>

          <div id="postsWrap">
            <div class="posts" id="postsList">
              <!-- topics will appear here -->
            </div>
            <div id="loading" class="hint" style="margin-top:12px">Loading topics…</div>
            <div id="noTopics" class="hint" style="margin-top:12px;display:none">No topics yet. Students can submit topics using the Submit via WhatsApp button or the form below.</div>
          </div>
        </div>

        <div class="card" style="margin-top:14px" id="submitFormCard">
          <h3 style="margin-top:0">Submit Topic (students)</h3>
          <p class="hint">Students may fill this form or message on WhatsApp: <strong>+2347083701096</strong></p>
          <form id="studentForm" class="create-form">
            <input id="sname" placeholder="Your name (optional)" />
            <input id="scontact" placeholder="WhatsApp number (optional)" />
            <input id="stopic" placeholder="Short topic title (e.g., 'Redox balancing')" required />
            <textarea id="sdetail" rows="4" placeholder="Describe the question or what you need help with..." required></textarea>
            <div class="row">
              <button class="btn" type="button" id="sendTopic">Submit Topic</button>
              <button class="btn" type="button" id="clearStudent">Clear</button>
            </div>
          </form>
        </div>

        <div id="about" class="card" style="margin-top:14px">
          <h2>About learn smart</h2>
          <p style="color:var(--muted)">learn smart is a free educational posting board for Nigerian university students. Students send topic requests via WhatsApp or the site form; the admin researches and posts clear, audio-friendly answers here so every student can benefit. Open to all courses and departments.</p>
        </div>

        <div id="terms" class="card" style="margin-top:14px">
          <h3>Terms & Conduct</h3>
          <ol style="color:var(--muted)">
            <li>Students submit topics only via WhatsApp or the site form. The site owner is the sole publisher.</li>
            <li>Respectful language only. Abusive or illegal content will not be published.</li>
            <li>Published answers are educational. Verify critical exam instructions with your lecturer.</li>
          </ol>
        </div>

        <div id="contact" class="card" style="margin-top:14px">
          <h3>Contact</h3>
          <p style="color:var(--muted)">To submit a topic via WhatsApp: <strong>+2347083701096</strong></p>
          <a class="btn" id="contactWhatsApp" href="#" target="_blank">Message on WhatsApp</a>
        </div>

      </main>

      <aside>
        <div class="card">
          <h4 style="margin-top:0">Quick Actions</h4>
          <div class="cta">
            <a class="big-cta" id="quickSubmit" href="#" target="_blank">Submit Topic (WhatsApp)</a>
            <button class="btn" id="openAdminPanelBtn">Open Admin Panel</button>
            <button class="btn" id="refreshBtn">Refresh topics</button>
          </div>
        </div>

        <div class="card" style="margin-top:12px">
          <h4 style="margin-top:0">Search Tips</h4>
          <p style="color:var(--muted)">Try keywords like "stoichiometry", "integration", or "DNA replication". Results include both questions and published answers.</p>
        </div>

        <div class="card" style="margin-top:12px">
          <h4 style="margin-top:0">Admin</h4>
          <p class="hint">Admin user: <strong>davidambertb@gmail.com</strong></p>
          <button class="btn" id="adminLoginBtn">Sign in as Admin</button>
        </div>
      </aside>
    </div>

    <footer>
      <div class="card" style="display:inline-block;padding:10px 14px">© <strong>learn smart</strong> — For Nigerian university students. Hosted by you.</div>
    </footer>
  </div>

  <!-- Admin modal/panel (hidden by default) -->
  <div id="adminModal" style="position:fixed;left:0;top:0;right:0;bottom:0;background:rgba(2,6,23,0.6);display:none;align-items:center;justify-content:center;padding:20px;z-index:9999">
    <div style="width:100%;max-width:920px;background:linear-gradient(180deg,#041821,#062b3a);border-radius:12px;padding:18px;color:#eaf9f6;box-shadow:0 18px 40px rgba(0,0,0,0.6)">
      <div style="display:flex;justify-content:space-between;align-items:center">
        <h3 style="margin:0">Admin Panel</h3>
        <div>
          <button class="btn" id="adminSignOut" style="margin-right:8px;display:none">Sign out</button>
          <button class="btn" id="closeAdmin">Close</button>
        </div>
      </div>

      <!-- Login area -->
      <div id="adminLoginUI" style="margin-top:12px">
        <p class="hint">Sign in as admin to view submitted topics and publish answers. (Email: <strong>davidambertb@gmail.com</strong>)</p>
        <input id="adminEmail" placeholder="Email" value="davidambertb@gmail.com" />
        <input id="adminPassword" placeholder="Password" type="password" />
        <div style="display:flex;gap:8px;margin-top:8px">
          <button class="btn" id="doSignIn">Sign in</button>
          <button class="btn" id="doCreateAdmin">Create admin account</button>
        </div>
        <p class="hint" style="margin-top:8px">If you prefer, create the admin user in Firebase Console instead. Creating here will also create the user in Firebase (only do this if you understand).</p>
        <div id="adminMsg" class="hint" style="margin-top:8px"></div>
      </div>

      <!-- Admin workspace -->
      <div id="adminWorkspace" style="display:none;margin-top:12px">
        <h4>Pending & All Topics</h4>
        <div style="display:flex;gap:12px;flex-wrap:wrap;">
          <div style="flex:1 1 420px;min-width:280px">
            <div id="adminTopics" style="max-height:420px;overflow:auto;padding:8px;border-radius:10px;background:rgba(255,255,255,0.02)"></div>
          </div>
          <div style="flex:1 1 420px;min-width:260px">
            <h4 style="margin:6px 0">Selected topic</h4>
            <div id="selTopic" style="padding:8px;border-radius:10px;background:rgba(0,0,0,0.18);min-height:150px"></div>

            <h4 style="margin:10px 0 6px 0">Write / Edit Answer</h4>
            <textarea id="adminAnswerText" rows="8" placeholder="Type the answer here..."></textarea>
            <div style="display:flex;gap:8px;margin-top:8px">
              <button class="btn" id="publishAnswerBtn">Publish Answer</button>
              <button class="btn" id="markAnsweredBtn">Mark as answered (without editing)</button>
            </div>
            <div id="adminStatus" class="hint" style="margin-top:10px"></div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Firebase + app script (module) -->
  <script type="module">
    // ----- FIREBASE CONFIG (from your paste) -----
    import { initializeApp } from "https://www.gstatic.com/firebasejs/12.2.1/firebase-app.js";
    import { getAnalytics } from "https://www.gstatic.com/firebasejs/12.2.1/firebase-analytics.js";
    import {
      getFirestore, collection, addDoc, doc, onSnapshot, query, orderBy, getDocs, updateDoc, serverTimestamp, limit
    } from "https://www.gstatic.com/firebasejs/12.2.1/firebase-firestore.js";
    import {
      getAuth, signInWithEmailAndPassword, createUserWithEmailAndPassword, signOut, onAuthStateChanged
    } from "https://www.gstatic.com/firebasejs/12.2.1/firebase-auth.js";

    const firebaseConfig = {
      apiKey: "AIzaSyCjNN3-ar92LXYHRUm4Aoze6b95W6D8blU",
      authDomain: "learn-smart-f1833.firebaseapp.com",
      projectId: "learn-smart-f1833",
      storageBucket: "learn-smart-f1833.firebasestorage.app",
      messagingSenderId: "459907839429",
      appId: "1:459907839429:web:4a908af852923f02e207ac",
      measurementId: "G-2T6XZKWPYJ"
    };

    const app = initializeApp(firebaseConfig);
    try{ getAnalytics(app); }catch(e){ /* analytics optional */ }
    const db = getFirestore(app);
    const auth = getAuth(app);

    // ----- UI refs -----
    const postsList = document.getElementById('postsList');
    const loading = document.getElementById('loading');
    const noTopics = document.getElementById('noTopics');
    const qInput = document.getElementById('q');
    const sortEl = document.getElementById('sort');
    const searchBtn = document.getElementById('searchBtn');
    const sendTopicBtn = document.getElementById('sendTopic');
    const studentForm = document.getElementById('studentForm');
    const submitWhatsApp = document.getElementById('submitWhatsApp');
    const contactWhatsApp = document.getElementById('contactWhatsApp');
    const quickSubmit = document.getElementById('quickSubmit');
    const phone = '+2347083701096';

    // WhatsApp links
    const waText = encodeURIComponent('Hello, I would like to submit a topic for Learn Smart. My name: [your name]. My question: [briefly type the topic].');
    const waHref = `https://wa.me/${phone.replace(/\\D/g,'')}?text=${waText}`;
    submitWhatsApp.href = waHref;
    contactWhatsApp.href = waHref;
    quickSubmit.href = waHref;
    document.getElementById('submitWhatsApp').target = '_blank';
    document.getElementById('contactWhatsApp').target = '_blank';
    quickSubmit.target = '_blank';

    // Nigeria time
    function nowNigeria(){ try{return new Intl.DateTimeFormat('en-NG',{dateStyle:'medium',timeStyle:'short',timeZone:'Africa/Lagos'}).format(new Date());}catch(e){return new Date().toLocaleString()} }
    document.getElementById('nigeriatime').textContent = nowNigeria();
    setInterval(()=>document.getElementById('nigeriatime').textContent = nowNigeria(),60000);

    // ----- Firestore: real-time listener for topics (most recent 200) -----
    const topicsColRef = collection(db, 'topics');
    const topQuery = query(topicsColRef, orderBy('createdAt','desc'), limit(200));
    let allTopics = []; // local cache

    // onSnapshot updates in real-time
    onSnapshot(topQuery, snapshot => {
      allTopics = [];
      snapshot.forEach(docSnap => {
        const d = docSnap.data(); d.id = docSnap.id;
        // Convert timestamps to JS Date if present
        if(d.createdAt && d.createdAt.toDate) d.createdAt = d.createdAt.toDate();
        if(d.answeredAt && d.answeredAt.toDate) d.answeredAt = d.answeredAt.toDate();
        allTopics.push(d);
      });
      renderList();
    }, err=>{
      console.error('Firestore listen error', err);
      loading.textContent = 'Unable to load topics (check Firestore rules / internet).';
    });

    // ----- Render topics list (client-side search/filter) -----
    function renderList(filterQ){
      postsList.innerHTML = '';
      loading.style.display = 'none';
      const q = (filterQ ?? qInput.value || '').trim().toLowerCase();
      let filtered = allTopics.slice();

      if(q) {
        filtered = filtered.filter(t => (
          (t.title||'').toLowerCase().includes(q) ||
          (t.question||'').toLowerCase().includes(q) ||
          (t.answer||'').toLowerCase().includes(q)
        ));
      }

      const sortVal = sortEl.value;
      if(sortVal==='alpha') filtered.sort((a,b)=> (a.title||'').localeCompare(b.title||''));
      if(sortVal==='newest') filtered.sort((a,b)=> new Date(b.createdAt || 0) - new Date(a.createdAt || 0));
      if(sortVal==='oldest') filtered.sort((a,b)=> new Date(a.createdAt || 0) - new Date(b.createdAt || 0));

      if(filtered.length === 0){
        noTopics.style.display = 'block';
        return;
      } else noTopics.style.display = 'none';

      filtered.forEach(t => {
        const el = document.createElement('div'); el.className = 'topic';
        const created = t.createdAt ? new Date(t.createdAt).toLocaleString('en-NG') : '';
        el.innerHTML = `
          <div style="display:flex;justify-content:space-between;align-items:center">
            <div style="flex:1">
              <h3>${escapeHtml(t.title || '(no title)')}</h3>
              <div class="meta">Submitted by ${escapeHtml(t.submitterName||'Anonymous')} • ${created}</div>
            </div>
            <div style="margin-left:12px; text-align:right">
              ${t.answered ? '<div style="background:linear-gradient(90deg,#00d1a6,#00a3ff);color:#002;padding:6px 8px;border-radius:8px;font-weight:800">Answered</div>' : '<div style="background:rgba(255,255,255,0.03);color:var(--muted);padding:6px 8px;border-radius:8px">Pending</div>'}
            </div>
          </div>
          <div style="margin-top:8px;color:var(--muted)">${escapeHtml(t.question || '')}</div>
          ${t.answer ? `<div class="answer"><strong>Answer:</strong><div style="margin-top:6px">${escapeHtml(t.answer)}</div><div class="meta" style="margin-top:6px">By ${escapeHtml(t.answerAuthor||'learn smart')} • ${t.answeredAt ? new Date(t.answeredAt).toLocaleString('en-NG') : ''}</div></div>` : ''}
          <div style="margin-top:8px;display:flex;gap:8px">
            <button class="btn" onclick="copyTopicLink('${t.id}')">Copy Link</button>
            <button class="btn" onclick="openInWhatsApp('${t.id}')">Share on WhatsApp</button>
          </div>
        `;
        postsList.appendChild(el);
      });
    }

    // Helpers for copying link / sharing
    window.copyTopicLink = function(id){
      const url = location.origin + location.pathname + '#topic-' + id;
      navigator.clipboard.writeText(url).then(()=> alert('Link copied to clipboard')).catch(()=> alert('Copy failed'));
    }
    window.openInWhatsApp = function(id){
      const t = allTopics.find(x=>x.id===id);
      const txt = encodeURIComponent(`Check this Learn Smart topic: ${t.title || 'Topic'}\n${location.origin + location.pathname + '#topic-'+id}`);
      window.open(`https://wa.me/${phone.replace(/\\D/g,'')}?text=${txt}`, '_blank');
    }

    // search and sort events
    document.getElementById('sort').addEventListener('change', ()=> renderList());
    document.getElementById('searchBtn').addEventListener('click', ()=> renderList(qInput.value));

    // quick refresh
    document.getElementById('refreshBtn').addEventListener('click', ()=> renderList());

    // Clear student form
    document.getElementById('clearStudent').addEventListener('click', ()=> {
      document.getElementById('sname').value=''; document.getElementById('scontact').value=''; document.getElementById('stopic').value=''; document.getElementById('sdetail').value='';
    });

    // ----- Submit topic (students) -----
    document.getElementById('sendTopic').addEventListener('click', async ()=>{
      const name = document.getElementById('sname').value.trim();
      const contact = document.getElementById('scontact').value.trim();
      const title = document.getElementById('stopic').value.trim();
      const question = document.getElementById('sdetail').value.trim();
      if(!title || !question){ alert('Please provide a short title and some details.'); return; }
      try{
        const docRef = await addDoc(topicsColRef, {
          title, question, submitterName: name||'Anonymous', submitterContact: contact||null,
          answered: false, createdAt: serverTimestamp()
        });
        alert('Topic submitted. The admin will respond when possible. Thank you!');
        document.getElementById('sname').value=''; document.getElementById('scontact').value=''; document.getElementById('stopic').value=''; document.getElementById('sdetail').value='';
      }catch(e){
        console.error(e);
        alert('Unable to submit topic. Check your internet connection and Firestore rules.');
      }
    });

    // ----- Admin UI logic -----
    const adminModal = document.getElementById('adminModal');
    const adminOpen = document.getElementById('adminOpen');
    const adminLoginBtn = document.getElementById('adminLoginBtn');
    const adminLoginUI = document.getElementById('adminLoginUI');
    const adminWorkspace = document.getElementById('adminWorkspace');
    const adminEmailEl = document.getElementById('adminEmail');
    const adminPasswordEl = document.getElementById('adminPassword');
    const doSignInBtn = document.getElementById('doSignIn');
    const doCreateAdminBtn = document.getElementById('doCreateAdmin');
    const adminMsg = document.getElementById('adminMsg');
    const adminTopicsDiv = document.getElementById('adminTopics');
    const selTopicDiv = document.getElementById('selTopic');
    const adminAnswerText = document.getElementById('adminAnswerText');
    const publishAnswerBtn = document.getElementById('publishAnswerBtn');
    const markAnsweredBtn = document.getElementById('markAnsweredBtn');
    const adminSignOutBtn = document.getElementById('adminSignOut');
    const closeAdminBtn = document.getElementById('closeAdmin');
    const openAdminPanelBtn = document.getElementById('openAdminPanelBtn');

    // open modal
    function openAdmin(){
      adminModal.style.display = 'flex';
      adminMsg.textContent = '';
    }
    function closeAdmin(){ adminModal.style.display='none'; }
    adminOpen.addEventListener('click', openAdmin);
    openAdminPanelBtn.addEventListener('click', openAdmin);
    closeAdminBtn.addEventListener('click', closeAdmin);

    // Auth state
    let currentUser = null;
    onAuthStateChanged(auth, user => {
      currentUser = user;
      if(user){
        // only allow if email matches admin email
        adminLoginUI.style.display = 'none';
        adminWorkspace.style.display = 'block';
        adminSignOutBtn.style.display = 'inline-block';
        loadAdminTopics();
      }else{
        adminLoginUI.style.display = 'block';
        adminWorkspace.style.display = 'none';
        adminSignOutBtn.style.display = 'none';
      }
    });

    doSignInBtn.addEventListener('click', async ()=>{
      const email = adminEmailEl.value.trim();
      const pw = adminPasswordEl.value;
      if(!email || !pw){ adminMsg.textContent = 'Please provide email and password.'; return; }
      try{
        await signInWithEmailAndPassword(auth, email, pw);
        adminMsg.textContent = 'Signed in.';
      }catch(err){
        console.error(err);
        if(err.code === 'auth/user-not-found'){
          adminMsg.textContent = 'No admin user found. You can create the admin account (button below) or create it in Firebase Console.';
        } else if(err.code === 'auth/wrong-password'){
          adminMsg.textContent = 'Wrong password.';
        } else {
          adminMsg.textContent = 'Sign in failed: ' + err.message;
        }
      }
    });

    doCreateAdminBtn.addEventListener('click', async ()=>{
      const email = adminEmailEl.value.trim();
      const pw = adminPasswordEl.value;
      if(!email || !pw){ adminMsg.textContent = 'Please provide email and password to create account.'; return; }
      const ok = confirm('Create admin account with this email and password in Firebase? Only do this if you understand. You can also create account in Firebase Console.');
      if(!ok) return;
      try{
        await createUserWithEmailAndPassword(auth, email, pw);
        adminMsg.textContent = 'Admin account created and signed in.';
      }catch(err){
        console.error(err); adminMsg.textContent = 'Creation failed: ' + err.message;
      }
    });

    adminSignOutBtn.addEventListener('click', async ()=>{
      await signOut(auth);
      adminMsg.textContent = 'Signed out.';
    });

    // Admin topics list loader
    let adminSelectedTopic = null;
    async function loadAdminTopics(){
      // Use the local cache allTopics
      renderAdminList();
    }

    function renderAdminList(){
      adminTopicsDiv.innerHTML = '';
      const list = allTopics.slice(); // newest first already from snapshot
      if(list.length===0){
        adminTopicsDiv.innerHTML = '<div class="hint">No topics yet.</div>'; return;
      }
      list.forEach(t=>{
        const node = document.createElement('div');
        node.style.padding='8px'; node.style.borderRadius='8px'; node.style.marginBottom='8px'; node.style.background='rgba(255,255,255,0.02)';
        node.innerHTML = `<strong>${escapeHtml(t.title)}</strong><div class="meta">${escapeHtml(t.submitterName||'Anonymous')} • ${t.createdAt ? new Date(t.createdAt).toLocaleString('en-NG') : ''}</div>`;
        node.onclick = ()=> selectTopicForAdmin(t);
        adminTopicsDiv.appendChild(node);
      });
    }

    function selectTopicForAdmin(t){
      adminSelectedTopic = t;
      selTopicDiv.innerHTML = `<h4 style="margin:6px 0">${escapeHtml(t.title)}</h4><div class="meta">Submitted by ${escapeHtml(t.submitterName||'Anonymous')} • ${t.createdAt ? new Date(t.createdAt).toLocaleString('en-NG') : ''}</div><div style="margin-top:8px;color:var(--muted)">${escapeHtml(t.question)}</div>`;
      adminAnswerText.value = t.answer || '';
    }

    publishAnswerBtn.addEventListener('click', async ()=>{
      if(!currentUser){ adminStatus('You must be signed in as admin to publish.'); return; }
      if(!adminSelectedTopic){ adminStatus('Select a topic on the left to answer.'); return; }
      const txt = adminAnswerText.value.trim();
      if(!txt){ adminStatus('Please write an answer first.'); return; }
      try{
        const docRef = doc(db, 'topics', adminSelectedTopic.id);
        await updateDoc(docRef, {
          answer: txt,
          answerAuthor: currentUser.email || 'admin',
          answered: true,
          answeredAt: serverTimestamp()
        });
        adminStatus('Answer published.');
      }catch(err){
        console.error(err); adminStatus('Failed to publish: ' + err.message);
      }
    });

    markAnsweredBtn.addEventListener('click', async ()=>{
      if(!currentUser){ adminStatus('You must be signed in as admin to publish.'); return; }
      if(!adminSelectedTopic){ adminStatus('Select a topic on the left to mark answered.'); return; }
      try{
        const docRef = doc(db, 'topics', adminSelectedTopic.id);
        await updateDoc(docRef, {
          answered: true,
          answerAuthor: currentUser.email||'admin',
          answeredAt: serverTimestamp()
        });
        adminStatus('Marked as answered.');
      }catch(err){ adminStatus('Failed: ' + err.message); }
    });

    function adminStatus(msg){ document.getElementById('adminStatus').textContent = msg; setTimeout(()=>document.getElementById('adminStatus').textContent='',4000); }

    // allow closing modal by clicking outside
    adminModal.addEventListener('click', (e)=>{ if(e.target === adminModal) closeAdmin(); });

    // ----- handle deep link to topic via hash like #topic-<id> -----
    function handleHash(){
      const h = location.hash || '';
      if(h.startsWith('#topic-')) {
        const id = h.replace('#topic-','');
        // find in cache
        const t = allTopics.find(x=>x.id===id);
        if(t){
          window.scrollTo({top:0,behavior:'smooth'});
          // open a quick modal-like view by selecting top post area
          alert('Topic: ' + (t.title||'') + '\\n\\n' + (t.question||'') + (t.answer ? '\\n\\nAnswer:\\n'+t.answer : '\\n\\n(Not yet answered)'));
        } else {
          alert('Topic not found (it may be new or removed).');
        }
      }
    }
    window.addEventListener('hashchange', handleHash);

    // ----- small helpers -----
    function escapeHtml(str){ return (str||'').replace(/[&<>\"']/g, s=>({\"&\":\"&amp;\",\"<\":\"&lt;\",\">\":\"&gt;\",\"\\\"\":\"&quot;\",\"'\":\"&#39;\"}[s])); }

    // initial render and attempts
    setTimeout(()=>{ renderList(); },800);

    // Expose some debugging helpers to the page (for copying links)
    window._ls_debug = { allTopics };

    // Good to remind about rules
    console.log('learn smart client running. Make sure Firestore rules allow read/write for your testing phase (or adjust rules for production).');

  </script>
</body>
</html>
