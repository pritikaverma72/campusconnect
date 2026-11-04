import os, sqlite3, secrets, argparse
from datetime import datetime
from functools import wraps
from flask import Flask, request, jsonify, session, render_template_string, send_from_directory
from werkzeug.security import generate_password_hash, check_password_hash
from werkzeug.utils import secure_filename

BASE = os.path.dirname(os.path.abspath(__file__))
DB = os.path.join(BASE, "campusconnect.db")
UPLOADS = os.path.join(BASE, "uploads")
os.makedirs(UPLOADS, exist_ok=True)

app = Flask(__name__)
app.secret_key = os.environ.get("CAMPUSCONNECT_SECRET", secrets.token_hex(32))
app.config["MAX_CONTENT_LENGTH"] = 5 * 1024 * 1024
ALLOWED = {"png", "jpg", "jpeg", "pdf"}

PAGE = r"""<!DOCTYPE html>
<html lang="en"><head><meta charset="UTF-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<title>CampusConnect | Campus Helpdesk</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700;800&family=Manrope:wght@600;700;800&display=swap');
:root{--navy:#172b4d;--blue:#315f9e;--ink:#233047;--muted:#77849a;--line:#e7ecf3;--bg:#f5f7fb;--green:#16865b}
*{box-sizing:border-box}body{margin:0;background:var(--bg);color:var(--ink);font:14px 'DM Sans',sans-serif}button,input,select,textarea{font:inherit}button{cursor:pointer}.hidden{display:none!important}
.auth{min-height:100vh;display:grid;place-items:center;padding:20px;background:linear-gradient(135deg,#edf4fc,#fafbfe)}.authbox{background:white;width:min(430px,100%);padding:34px;border:1px solid var(--line);border-radius:17px;box-shadow:0 18px 50px #19325212}.logo{background:var(--navy);color:white;border-radius:12px;width:45px;height:45px;display:grid;place-items:center;font-weight:800;margin-bottom:20px}.auth h1{font:800 28px Manrope;margin:0 0 7px}.muted{color:var(--muted);line-height:1.6}.tabs{display:flex;border-bottom:1px solid var(--line);margin:22px 0}.tabs button{flex:1;background:none;border:0;padding:12px;color:var(--muted);font-weight:700}.tabs button.active{color:var(--blue);border-bottom:2px solid var(--blue)}label{display:grid;gap:7px;font-size:12px;font-weight:700;margin-bottom:14px}input,select,textarea{padding:12px;border:1px solid #dce3ed;border-radius:8px;width:100%;background:white;color:var(--ink)}textarea{resize:vertical}.btn{background:var(--blue);color:white;border:0;border-radius:8px;padding:12px 17px;font-weight:700;font-size:12px}.btn:hover{background:#244d84}.full{width:100%}.msg{font-size:11px;color:var(--green);margin-top:12px}
.shell{min-height:100vh}.side{position:fixed;inset:0 auto 0 0;width:235px;background:var(--navy);color:white;padding:24px 15px;display:flex;flex-direction:column}.brand{font:800 16px Manrope;padding:4px 9px 35px}.brand span{color:#9dc2f2}.nav{width:100%;border:0;background:none;color:#c5d2e3;text-align:left;padding:13px;border-radius:8px;margin:3px 0;font-size:12px;font-weight:600}.nav:hover,.nav.active{background:#2a496f;color:white}.nav b{display:inline-block;width:25px;font-size:16px}.sidebottom{margin-top:auto;border-top:1px solid #3a506e;padding-top:17px;font-size:11px}.sidebottom button{display:block;background:none;border:0;color:#d2dceb;padding:12px 5px}
.main{margin-left:235px}.top{height:76px;background:white;border-bottom:1px solid var(--line);display:flex;align-items:center;justify-content:space-between;padding:0 35px}.top h2{font:700 18px Manrope;margin:0}.pill{background:#edf3fb;color:var(--blue);padding:6px 9px;border-radius:5px;font-size:9px;font-weight:800}
.content{max-width:1450px;margin:auto;padding:30px 35px}.intro{margin-bottom:22px}.intro h1{font:800 25px Manrope;margin:0 0 7px}.intro p{font-size:12px}.row{display:flex;justify-content:space-between;align-items:center;gap:15px;margin-bottom:22px}.stats{display:grid;grid-template-columns:repeat(4,1fr);gap:14px;margin-bottom:22px}.stat,.panel,.formbox{background:white;border:1px solid var(--line);border-radius:11px}.stat{padding:18px}.stat p{font-size:11px;color:var(--muted);margin:9px 0}.stat strong{font:800 27px Manrope}.panel{overflow:hidden;margin-bottom:20px}.panelhead{padding:18px 20px;border-bottom:1px solid var(--line);display:flex;justify-content:space-between;align-items:center}.panelhead h3,.formbox h3{font:700 14px Manrope;margin:0}.tablewrap{overflow-x:auto}table{width:100%;border-collapse:collapse;min-width:620px}th{text-align:left;background:#fafbfd;color:#8b96a8;font-size:9px;letter-spacing:.8px;padding:14px 17px}td{padding:14px 17px;border-top:1px solid #eff2f6;font-size:11px}.badge{display:inline-block;border-radius:20px;padding:6px 9px;font-size:9px;font-weight:700;background:#fff3df;color:#a86d17}.inprogress{background:#e8f0fc;color:#376cae}.resolved,.closed{background:#e5f5ed;color:#16865b}
.formbox{padding:24px;max-width:850px}.grid{display:grid;grid-template-columns:1fr 1fr;gap:0 17px}.wide{grid-column:1/-1}.actions{display:flex;align-items:center;gap:12px;margin-top:10px}.track{display:flex;gap:10px;max-width:650px;margin-bottom:18px}.result{background:white;border:1px solid var(--line);padding:22px;border-radius:10px;max-width:850px}.timeline{border-left:2px solid #dbe6f4;margin:18px 0 0 5px;padding-left:18px}.timeline p{font-size:11px;color:var(--muted)}.cards{display:grid;grid-template-columns:repeat(2,1fr);gap:14px}.idea{background:white;border:1px solid var(--line);border-radius:10px;padding:18px}.idea h3{font:700 14px Manrope}.idea p{font-size:12px;color:var(--muted);line-height:1.6}.vote{border:1px solid #d5e2f2;background:#f4f8fd;color:var(--blue);padding:8px 12px;border-radius:7px;font-size:11px}
footer{text-align:center;color:#9aa4b2;font-size:10px;padding:25px}.toast{position:fixed;right:20px;bottom:20px;background:#203653;color:white;padding:13px 17px;border-radius:8px;opacity:0;transition:.2s}.toast.show{opacity:1}
@media(max-width:950px){.stats{grid-template-columns:repeat(2,1fr)}.content{padding:22px}.top{padding:0 22px}}
@media(max-width:650px){.side{width:62px;padding:17px 6px}.brand{font-size:0;padding:5px 0 25px}.brand:after{content:'CC';font-size:14px}.nav{text-align:center;font-size:0;padding:14px 4px}.nav b{width:auto;font-size:18px}.sidebottom{font-size:0}.sidebottom button{font-size:0}.main{margin-left:62px}.top{padding:0 12px;height:67px}.content{padding:18px 12px}.row{align-items:flex-start;flex-direction:column}.stats{gap:8px}.stat{padding:12px}.stat strong{font-size:22px}.grid,.cards{grid-template-columns:1fr}.wide{grid-column:auto}.track{flex-direction:column}}
</style></head><body>
<div id="auth" class="auth"><div class="authbox"><div class="logo">CC</div><p style="font-size:10px;letter-spacing:1.5px;color:#8796aa;font-weight:800">YOUR CAMPUS, YOUR VOICE</p><h1>CampusConnect</h1><p class="muted">Report campus issues, follow progress and share ideas.</p>
<div class="tabs"><button id="loginTab" class="active" onclick="authMode('login')">Log in</button><button id="regTab" onclick="authMode('register')">Create account</button></div>
<form id="loginForm"><label>Email<input id="liEmail" type="email" required placeholder="you@college.edu"></label><label>Password<input id="liPass" type="password" required></label><button class="btn full">Log in</button></form>
<form id="regForm" class="hidden"><label>Full name<input id="reName" required></label><label>Email<input id="reEmail" type="email" required></label><label>Department (optional)<input id="reDept"></label><label>Password (minimum 8 characters)<input id="rePass" type="password" minlength="8" required></label><button class="btn full">Create student account</button></form><div id="authMsg" class="msg"></div><p class="muted" style="font-size:10px">Administrator accounts are created separately by the project owner.</p></div></div>
<div id="shell" class="shell hidden"><aside class="side"><div class="brand">Campus<span>Connect</span></div>
<button class="nav active" data-page="dashboard"><b>▦</b> Dashboard</button><button class="nav" data-page="complaints"><b>▤</b> My complaints</button><button class="nav" data-page="report"><b>＋</b> Report an issue</button><button class="nav" data-page="tracking"><b>⌕</b> Track complaint</button><button class="nav" data-page="suggestions"><b>✳</b> Suggestions</button><button class="nav hidden" id="adminNav" data-page="admin"><b>▣</b> Admin management</button>
<div class="sidebottom"><strong id="sideName">Student</strong><br><span id="sideRole">Student account</span><button onclick="logout()">↪ Log out</button></div></aside>
<main class="main"><header class="top"><h2 id="heading">Dashboard</h2><div><span id="topName">Student</span> &nbsp; <span class="pill" id="role">STUDENT</span></div></header><div class="content">
<section id="dashboard" class="view"><div class="row"><div class="intro"><h1 id="welcome">Welcome back</h1><p class="muted">Here is an overview of your campus reports.</p></div><button class="btn" onclick="go('report')">＋ Report an issue</button></div>
<div class="stats"><div class="stat"><p>Total complaints</p><strong id="total">0</strong></div><div class="stat"><p>Awaiting action</p><strong id="pending">0</strong></div><div class="stat"><p>In progress</p><strong id="progress">0</strong></div><div class="stat"><p>Resolved / closed</p><strong id="resolved">0</strong></div></div>
<div class="panel"><div class="panelhead"><h3>Recent complaints</h3><button class="nav" style="width:auto;color:#315f9e" onclick="go('complaints')">View all →</button></div><div class="tablewrap"><table><thead><tr><th>ID</th><th>ISSUE</th><th>CATEGORY</th><th>DATE</th><th>STATUS</th></tr></thead><tbody id="recent"></tbody></table></div></div></section>
<section id="complaints" class="view hidden"><div class="intro"><h1>My complaints</h1><p class="muted">Complaints associated with your account.</p></div><div class="panel"><div class="tablewrap"><table><thead><tr><th>ID</th><th>ISSUE</th><th>CATEGORY</th><th>DATE</th><th>STATUS</th><th></th></tr></thead><tbody id="mine"></tbody></table></div></div></section>
<section id="report" class="view hidden"><div class="intro"><h1>Report an issue</h1><p class="muted">Give the campus team enough detail to understand the problem.</p></div><form id="complaintForm" class="formbox"><h3>Complaint details</h3><br><div class="grid">
<label>Issue title *<input name="title" required maxlength="120" placeholder="e.g. Projector not working"></label><label>Category *<select name="category" required><option value="">Choose category</option><option>Infrastructure</option><option>Technical</option><option>Academic</option><option>Cleanliness</option><option>Facilities</option><option>Safety</option><option>Other</option></select></label>
<label>Location *<input name="location" required placeholder="Building, room or campus area"></label><label>Priority<select name="priority"><option>Normal</option><option>Medium</option><option>High</option><option>Urgent</option></select></label>
<label class="wide">Description *<textarea name="description" required rows="5" maxlength="3000" placeholder="Explain what happened..."></textarea></label><label class="wide">Evidence (optional; PNG/JPG/PDF, max 5 MB)<input name="evidence" type="file" accept=".png,.jpg,.jpeg,.pdf"></label></div><div class="actions"><button class="btn">Submit complaint</button><span id="complaintMsg" class="msg"></span></div></form></section>
<section id="tracking" class="view hidden"><div class="intro"><h1>Track a complaint</h1><p class="muted">Enter the complaint ID received after submission.</p></div><form id="trackForm" class="track"><input id="trackCode" required placeholder="CC-2026-00001"><button class="btn">Track complaint</button></form><div id="trackResult"></div></section>
<section id="suggestions" class="view hidden"><div class="intro"><h1>Campus suggestions</h1><p class="muted">Share a practical idea and support ideas from others.</p></div><form id="suggestionForm" class="formbox"><h3>Share an idea</h3><br><div class="grid"><label>Title<input name="title" required></label><label>Category<select name="category"><option>General</option><option>Facilities</option><option>Technology</option><option>Academic</option><option>Environment</option></select></label><label class="wide">Details<textarea name="description" rows="3" required></textarea></label></div><button class="btn">Submit suggestion</button><span id="suggestionMsg" class="msg"></span></form><br><div id="ideas" class="cards"></div></section>
<section id="admin" class="view hidden"><div class="intro"><h1>Complaint management</h1><p class="muted">Review campus reports and update their status.</p></div><div class="panel"><div class="tablewrap"><table><thead><tr><th>ID / STUDENT</th><th>ISSUE / CATEGORY</th><th>LOCATION</th><th>STATUS</th><th>UPDATE</th></tr></thead><tbody id="adminRows"></tbody></table></div></div></section>
</div><footer>CampusConnect · Raise a concern. Follow its progress. Improve campus life.</footer></main></div><div id="toast" class="toast"></div>
<script>
let me=null;const $=s=>document.querySelector(s),$$=s=>[...document.querySelectorAll(s)];
async function api(url,opt={}){let r=await fetch(url,{credentials:'same-origin',...opt});let d=await r.json();if(!r.ok)throw Error(d.error||'Request failed');return d}
function esc(v=''){return String(v).replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]))}
function toast(t){let e=$('#toast');e.textContent=t;e.classList.add('show');setTimeout(()=>e.classList.remove('show'),2600)}
function badge(s){let c=['Resolved','Closed'].includes(s)?'resolved':s==='In Progress'?'inprogress':'';return `<span class="badge ${c}">${esc(s)}</span>`}
function authMode(m){$('#loginForm').classList.toggle('hidden',m!=='login');$('#regForm').classList.toggle('hidden',m!=='register');$('#loginTab').classList.toggle('active',m==='login');$('#regTab').classList.toggle('active',m==='register');$('#authMsg').textContent=''}
function showApp(){ $('#auth').classList.add('hidden');$('#shell').classList.remove('hidden');$('#sideName').textContent=me.name;$('#topName').textContent=me.name;$('#sideRole').textContent=me.role==='admin'?'Administrator':'Student account';$('#role').textContent=me.role.toUpperCase();$('#adminNav').classList.toggle('hidden',me.role!=='admin');$('#welcome').textContent='Welcome back, '+me.name.split(' ')[0];go('dashboard')}
function go(p){if(p==='admin'&&me.role!=='admin')return toast('Administrator access required');$$('.view').forEach(x=>x.classList.add('hidden'));$('#'+p).classList.remove('hidden');$$('.nav[data-page]').forEach(x=>x.classList.toggle('active',x.dataset.page===p));$('#heading').textContent=({dashboard:'Dashboard',complaints:'My complaints',report:'Report an issue',tracking:'Track complaint',suggestions:'Campus suggestions',admin:'Admin management'})[p];if(p==='dashboard')dashboard();if(p==='complaints')loadMine();if(p==='suggestions')loadIdeas();if(p==='admin')loadAdmin()}
$$('.nav[data-page]').forEach(b=>b.addEventListener('click',()=>go(b.dataset.page)));
$('#loginForm').onsubmit=async e=>{e.preventDefault();try{let d=await api('/api/login',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({email:$('#liEmail').value,password:$('#liPass').value})});me=d.user;showApp()}catch(x){$('#authMsg').textContent=x.message}};
$('#regForm').onsubmit=async e=>{e.preventDefault();try{let d=await api('/api/register',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({name:$('#reName').value,email:$('#reEmail').value,department:$('#reDept').value,password:$('#rePass').value})});me=d.user;showApp();toast('Student account created')}catch(x){$('#authMsg').textContent=x.message}};
async function logout(){await api('/api/logout',{method:'POST'});me=null;$('#shell').classList.add('hidden');$('#auth').classList.remove('hidden');authMode('login')}
async function dashboard(){try{let d=await api('/api/dashboard');$('#total').textContent=d.total;$('#pending').textContent=d.pending;$('#progress').textContent=d.progress;$('#resolved').textContent=d.resolved;$('#recent').innerHTML=d.recent.length?d.recent.map(c=>`<tr><td>${esc(c.code)}</td><td>${esc(c.title)}</td><td>${esc(c.category)}</td><td>${esc(c.date)}</td><td>${badge(c.status)}</td></tr>`).join(''):'<tr><td colspan="5">No complaints submitted yet.</td></tr>'}catch(e){toast(e.message)}}
async function loadMine(){try{let a=await api('/api/complaints');$('#mine').innerHTML=a.length?a.map(c=>`<tr><td>${esc(c.code)}</td><td>${esc(c.title)}</td><td>${esc(c.category)}</td><td>${esc(c.date)}</td><td>${badge(c.status)}</td><td><button class="nav" style="color:#315f9e;width:auto" onclick="track('${esc(c.code)}')">Track</button></td></tr>`).join(''):'<tr><td colspan="6">No complaints yet.</td></tr>'}catch(e){toast(e.message)}}
$('#complaintForm').onsubmit=async e=>{e.preventDefault();try{let d=await api('/api/complaints',{method:'POST',body:new FormData(e.target)});e.target.reset();$('#complaintMsg').textContent='Submitted. Your complaint ID: '+d.code;toast('Complaint submitted: '+d.code);dashboard()}catch(x){$('#complaintMsg').textContent=x.message}};
async function track(code){go('tracking');$('#trackCode').value=code;$('#trackForm').requestSubmit()}
$('#trackForm').onsubmit=async e=>{e.preventDefault();let code=$('#trackCode').value.trim();$('#trackResult').innerHTML='';try{let d=await api('/api/complaints/'+encodeURIComponent(code));let c=d.complaint;$('#trackResult').innerHTML=`<div class="result"><h3>${esc(c.title)} ${badge(c.status)}</h3><p class="muted">ID: ${esc(c.code)} · ${esc(c.category)} · ${esc(c.location)}</p><p>${esc(c.description)}</p>${c.file?`<p><a href="/uploads/${encodeURIComponent(c.file)}" target="_blank">View attachment</a></p>`:''}<h3>Status history</h3><div class="timeline">${d.updates.map(u=>`<div><strong>${esc(u.status)}</strong><p>${esc(u.remarks)} · ${esc(u.date)}</p></div>`).join('')}</div></div>`}catch(x){$('#trackResult').innerHTML=`<div class="result">${esc(x.message)}</div>`}};
$('#suggestionForm').onsubmit=async e=>{e.preventDefault();let f=new FormData(e.target);try{await api('/api/suggestions',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({title:f.get('title'),category:f.get('category'),description:f.get('description')})});e.target.reset();$('#suggestionMsg').textContent='Suggestion submitted';loadIdeas()}catch(x){$('#suggestionMsg').textContent=x.message}};
async function loadIdeas(){try{let a=await api('/api/suggestions');$('#ideas').innerHTML=a.length?a.map(s=>`<article class="idea"><h3>${esc(s.title)}</h3><p>${esc(s.description)}</p><p>${esc(s.category)} · ${esc(s.author)}</p><button class="vote" ${s.voted?'disabled':''} onclick="vote(${s.id})">♡ ${s.votes} votes ${s.voted?'· Voted':'· Vote'}</button></article>`).join(''):'<p class="muted">No suggestions yet.</p>'}catch(e){toast(e.message)}}
async function vote(id){try{await api('/api/suggestions/'+id+'/vote',{method:'POST'});loadIdeas()}catch(e){toast(e.message)}}
async function loadAdmin(){try{let a=await api('/api/complaints');$('#adminRows').innerHTML=a.length?a.map(c=>`<tr><td>${esc(c.code)}<br>${esc(c.student)}</td><td>${esc(c.title)}<br>${esc(c.category)}</td><td>${esc(c.location)}</td><td>${badge(c.status)}</td><td><select id="st${c.id}">${['Submitted','Under Review','Assigned','In Progress','Resolved','Closed'].map(s=>`<option ${s===c.status?'selected':''}>${s}</option>`).join('')}</select><button class="btn" style="padding:8px;margin-top:5px" onclick="updateStatus(${c.id},'${esc(c.code)}')">Save</button></td></tr>`).join(''):'<tr><td colspan="5">No complaints submitted.</td></tr>'}catch(e){toast(e.message)}}
async function updateStatus(id,code){let remarks=prompt('Add a short update for the student (optional):')||'';try{await api('/api/complaints/'+encodeURIComponent(code)+'/status',{method:'PUT',headers:{'Content-Type':'application/json'},body:JSON.stringify({status:$('#st'+id).value,remarks})});toast('Status updated');loadAdmin()}catch(e){toast(e.message)}}
async function start(){try{let d=await api('/api/me');if(d.user){me=d.user;showApp()}}catch(e){}}
start();
</script></body></html>"""


def connect():
    db = sqlite3.connect(DB)
    db.row_factory = sqlite3.Row
    db.execute("PRAGMA foreign_keys=ON")
    return db


def init_db():
    with connect() as db:
        db.executescript("""
        CREATE TABLE IF NOT EXISTS users(
          id INTEGER PRIMARY KEY, name TEXT NOT NULL, email TEXT UNIQUE NOT NULL,
          password TEXT NOT NULL, role TEXT NOT NULL DEFAULT 'student',
          department TEXT DEFAULT '', created TEXT NOT NULL);
        CREATE TABLE IF NOT EXISTS complaints(
          id INTEGER PRIMARY KEY, code TEXT UNIQUE, user_id INTEGER NOT NULL,
          title TEXT NOT NULL, description TEXT NOT NULL, category TEXT NOT NULL,
          location TEXT NOT NULL, priority TEXT NOT NULL, status TEXT NOT NULL,
          file TEXT, created TEXT NOT NULL,
          FOREIGN KEY(user_id) REFERENCES users(id));
        CREATE TABLE IF NOT EXISTS updates(
          id INTEGER PRIMARY KEY, complaint_id INTEGER NOT NULL, user_id INTEGER,
          status TEXT NOT NULL, remarks TEXT DEFAULT '', created TEXT NOT NULL,
          FOREIGN KEY(complaint_id) REFERENCES complaints(id) ON DELETE CASCADE);
        CREATE TABLE IF NOT EXISTS suggestions(
          id INTEGER PRIMARY KEY, user_id INTEGER NOT NULL, title TEXT NOT NULL,
          description TEXT NOT NULL, category TEXT DEFAULT 'General', created TEXT NOT NULL,
          FOREIGN KEY(user_id) REFERENCES users(id));
        CREATE TABLE IF NOT EXISTS votes(
          id INTEGER PRIMARY KEY, suggestion_id INTEGER NOT NULL, user_id INTEGER NOT NULL,
          UNIQUE(suggestion_id,user_id),
          FOREIGN KEY(suggestion_id) REFERENCES suggestions(id) ON DELETE CASCADE,
          FOREIGN KEY(user_id) REFERENCES users(id) ON DELETE CASCADE);
        """)


def user():
    if not session.get("uid"):
        return None
    with connect() as db:
        r = db.execute("SELECT id,name,email,role,department FROM users WHERE id=?", (session["uid"],)).fetchone()
        return dict(r) if r else None


def signed(f):
    @wraps(f)
    def w(*a, **k):
        if not user(): return jsonify(error="Please log in first."), 401
        return f(*a, **k)
    return w


def admin(f):
    @wraps(f)
    def w(*a, **k):
        u = user()
        if not u: return jsonify(error="Please log in first."), 401
        if u["role"] != "admin": return jsonify(error="Administrator access required."), 403
        return f(*a, **k)
    return w


def stamp():
    return datetime.now().strftime("%Y-%m-%d %H:%M:%S")


@app.route("/")
def home():
    return render_template_string(PAGE)


@app.route("/api/register", methods=["POST"])
def register():
    d = request.get_json() or {}
    name, email, password = (d.get("name") or "").strip(), (d.get("email") or "").strip().lower(), d.get("password") or ""
    if not name or "@" not in email or len(password) < 8:
        return jsonify(error="Enter a name, valid email and password of at least 8 characters."), 400
    try:
        with connect() as db:
            cur = db.execute("INSERT INTO users(name,email,password,role,department,created) VALUES(?,?,?,'student',?,?)",
                             (name,email,generate_password_hash(password),(d.get("department") or "").strip(),stamp()))
            session["uid"] = cur.lastrowid
    except sqlite3.IntegrityError:
        return jsonify(error="An account with that email already exists."), 409
    return jsonify(user=user()), 201


@app.route("/api/login", methods=["POST"])
def login():
    d = request.get_json() or {}
    with connect() as db:
        r = db.execute("SELECT * FROM users WHERE email=?", ((d.get("email") or "").strip().lower(),)).fetchone()
    if not r or not check_password_hash(r["password"], d.get("password") or ""):
        return jsonify(error="Incorrect email or password."), 401
    session.clear()
    session["uid"] = r["id"]
    return jsonify(user=user())


@app.route("/api/me")
def me():
    return jsonify(user=user())


@app.route("/api/logout", methods=["POST"])
def logout():
    session.clear()
    return jsonify(message="Logged out")


@app.route("/api/complaints", methods=["POST"])
@signed
def create_complaint():
    u = user()
    title, desc = (request.form.get("title") or "").strip(), (request.form.get("description") or "").strip()
    category, location = (request.form.get("category") or "").strip(), (request.form.get("location") or "").strip()
    priority = request.form.get("priority", "Normal")
    if not all([title,desc,category,location]): return jsonify(error="Complete all required fields."), 400
    if priority not in {"Normal","Medium","High","Urgent"}: return jsonify(error="Invalid priority."), 400
    filename = None
    f = request.files.get("evidence")
    if f and f.filename:
        safe = secure_filename(f.filename)
        ext = safe.rsplit(".",1)[-1].lower() if "." in safe else ""
        if ext not in ALLOWED: return jsonify(error="Only PNG, JPG, JPEG or PDF files are allowed."), 400
        filename = secrets.token_hex(10) + "_" + safe
        f.save(os.path.join(UPLOADS,filename))
    with connect() as db:
        cur = db.execute("""INSERT INTO complaints(user_id,title,description,category,location,priority,status,file,created)
                            VALUES(?,?,?,?,?,?, 'Submitted',?,?)""",
                         (u["id"],title,desc,category,location,priority,filename,stamp()))
        cid = cur.lastrowid
        code = f"CC-{datetime.now().year}-{cid:05d}"
        db.execute("UPDATE complaints SET code=? WHERE id=?", (code,cid))
        db.execute("INSERT INTO updates(complaint_id,user_id,status,remarks,created) VALUES(?,?,'Submitted','Complaint registered successfully.',?)",
                   (cid,u["id"],stamp()))
    return jsonify(message="Complaint submitted",code=code), 201


@app.route("/api/complaints")
@signed
def complaints():
    u = user()
    sql = """SELECT c.*,u.name AS student FROM complaints c JOIN users u ON u.id=c.user_id"""
    args = []
    if u["role"] != "admin":
        sql += " WHERE c.user_id=?"; args.append(u["id"])
    sql += " ORDER BY c.id DESC"
    with connect() as db: rows = db.execute(sql,args).fetchall()
    return jsonify([{"id":r["id"],"code":r["code"],"title":r["title"],"description":r["description"],
                     "category":r["category"],"location":r["location"],"priority":r["priority"],
                     "status":r["status"],"file":r["file"],"date":r["created"],"student":r["student"]} for r in rows])


@app.route("/api/complaints/<code>")
@signed
def track(code):
    u = user()
    with connect() as db:
        c = db.execute("SELECT c.*,u.name student FROM complaints c JOIN users u ON u.id=c.user_id WHERE c.code=?", (code.upper(),)).fetchone()
        if not c: return jsonify(error="Complaint not found."), 404
        if u["role"] != "admin" and c["user_id"] != u["id"]: return jsonify(error="You can only view your own complaints."), 403
        ups = db.execute("SELECT status,remarks,created FROM updates WHERE complaint_id=? ORDER BY id", (c["id"],)).fetchall()
    return jsonify(complaint={"code":c["code"],"title":c["title"],"description":c["description"],"category":c["category"],
                              "location":c["location"],"priority":c["priority"],"status":c["status"],"file":c["file"]},
                   updates=[{"status":r["status"],"remarks":r["remarks"],"date":r["created"]} for r in ups])


@app.route("/api/complaints/<code>/status", methods=["PUT"])
@admin
def status(code):
    d = request.get_json() or {}; new = d.get("status")
    allowed = {"Submitted","Under Review","Assigned","In Progress","Resolved","Closed"}
    if new not in allowed: return jsonify(error="Invalid status."), 400
    with connect() as db:
        c = db.execute("SELECT id FROM complaints WHERE code=?", (code.upper(),)).fetchone()
        if not c: return jsonify(error="Complaint not found."), 404
        db.execute("UPDATE complaints SET status=? WHERE id=?", (new,c["id"]))
        db.execute("INSERT INTO updates(complaint_id,user_id,status,remarks,created) VALUES(?,?,?,?,?)",
                   (c["id"],user()["id"],new,(d.get("remarks") or "").strip(),stamp()))
    return jsonify(message="Status updated")


@app.route("/api/dashboard")
@signed
def dashboard():
    u = user()
    clause = "" if u["role"] == "admin" else " WHERE user_id=?"
    args = () if u["role"] == "admin" else (u["id"],)
    with connect() as db:
        total = db.execute("SELECT COUNT(*) FROM complaints"+clause,args).fetchone()[0]
        pending = db.execute("SELECT COUNT(*) FROM complaints"+clause+(" AND" if clause else " WHERE")+" status IN ('Submitted','Under Review','Assigned')",args).fetchone()[0]
        progress = db.execute("SELECT COUNT(*) FROM complaints"+clause+(" AND" if clause else " WHERE")+" status='In Progress'",args).fetchone()[0]
        resolved = db.execute("SELECT COUNT(*) FROM complaints"+clause+(" AND" if clause else " WHERE")+" status IN ('Resolved','Closed')",args).fetchone()[0]
        sql = "SELECT c.*,u.name student FROM complaints c JOIN users u ON u.id=c.user_id"
        if u["role"] != "admin": sql += " WHERE c.user_id=?"
        sql += " ORDER BY c.id DESC LIMIT 5"
        rows = db.execute(sql,args).fetchall()
    recent = [{"code":r["code"],"title":r["title"],"category":r["category"],"status":r["status"],"date":r["created"]} for r in rows]
    return jsonify(total=total,pending=pending,progress=progress,resolved=resolved,recent=recent)


@app.route("/api/suggestions", methods=["POST"])
@signed
def add_idea():
    d = request.get_json() or {}
    if not (d.get("title") or "").strip() or not (d.get("description") or "").strip():
        return jsonify(error="Title and description are required."), 400
    with connect() as db:
        db.execute("INSERT INTO suggestions(user_id,title,description,category,created) VALUES(?,?,?,?,?)",
                   (user()["id"],d["title"].strip(),d["description"].strip(),d.get("category","General"),stamp()))
    return jsonify(message="Suggestion added"), 201


@app.route("/api/suggestions")
@signed
def ideas():
    uid = user()["id"]
    with connect() as db:
        rows = db.execute("""SELECT s.*,u.name author,COUNT(v.id) votes,
          MAX(CASE WHEN v.user_id=? THEN 1 ELSE 0 END) voted
          FROM suggestions s JOIN users u ON u.id=s.user_id
          LEFT JOIN votes v ON v.suggestion_id=s.id GROUP BY s.id ORDER BY votes DESC,s.id DESC""",(uid,)).fetchall()
    return jsonify([{"id":r["id"],"title":r["title"],"description":r["description"],"category":r["category"],
                     "author":r["author"],"votes":r["votes"],"voted":bool(r["voted"])} for r in rows])


@app.route("/api/suggestions/<int:sid>/vote", methods=["POST"])
@signed
def vote(sid):
    try:
        with connect() as db:
            db.execute("INSERT INTO votes(suggestion_id,user_id) VALUES(?,?)",(sid,user()["id"]))
    except sqlite3.IntegrityError:
        return jsonify(error="You have already voted for this suggestion."), 409
    return jsonify(message="Vote recorded")


@app.route("/uploads/<path:filename>")
@signed
def uploaded_file(filename):
    # Demo access control: production apps should verify the file belongs to a complaint
    # the current user is allowed to view.
    return send_from_directory(UPLOADS, filename)


@app.errorhandler(413)
def too_large(_):
    return jsonify(error="File exceeds the 5 MB limit."), 413


def make_admin(email, name, password):
    if len(password) < 8: raise ValueError("Password must be at least 8 characters.")
    with connect() as db:
        existing = db.execute("SELECT id FROM users WHERE email=?",(email.lower(),)).fetchone()
        if existing:
            db.execute("UPDATE users SET role='admin' WHERE id=?",(existing["id"],))
            print("Existing account promoted to administrator.")
        else:
            db.execute("INSERT INTO users(name,email,password,role,department,created) VALUES(?,?,?,'admin','Administration',?)",
                       (name,email.lower(),generate_password_hash(password),stamp()))
            print("Administrator account created.")


if __name__ == "__main__":
    parser = argparse.ArgumentParser()
    parser.add_argument("--create-admin", action="store_true")
    parser.add_argument("--admin-email")
    parser.add_argument("--admin-name", default="Campus Administrator")
    args = parser.parse_args()
    init_db()
    if args.create_admin:
        email = args.admin_email or input("Admin email: ").strip()
        password = input("Admin password (at least 8 characters): ")
        make_admin(email,args.admin_name,password)
    else:
        app.run(host="127.0.0.1",port=5000,debug=True)
