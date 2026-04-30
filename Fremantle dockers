<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Freo Dockers — History</title>
<style>
  :root{--accent:#4b2e83;--bg:#f7f7fb;--card:#fff}
  body{font-family:system-ui,-apple-system,Segoe UI,Roboto,"Helvetica Neue",Arial;margin:0;background:var(--bg);color:#111}
  header{background:linear-gradient(90deg,#24124b, var(--accent));color:#fff;padding:24px 20px}
  header h1{margin:0;font-size:1.6rem}
  .container{max-width:900px;margin:20px auto;padding:0 16px}
  .controls{display:flex;gap:8px;flex-wrap:wrap;align-items:center;margin-bottom:12px}
  .search{flex:1;min-width:180px}
  input,select,button{padding:8px 10px;font-size:0.95rem;border-radius:8px;border:1px solid #ddd}
  .timeline{display:grid;grid-template-columns:1fr;gap:12px}
  .card{background:var(--card);border-radius:10px;padding:12px;box-shadow:0 6px 18px rgba(20,10,60,0.06);display:flex;gap:12px;align-items:flex-start}
  .thumb{width:110px;height:70px;background:#eee;border-radius:8px;overflow:hidden;flex-shrink:0}
  .thumb img{width:100%;height:100%;object-fit:cover;display:block}
  .meta{font-size:0.85rem;color:#555;margin-bottom:6px}
  .title{font-weight:600;margin:0 0 6px 0}
  .desc{margin:0;color:#222;line-height:1.3}
  .empty{padding:24px;text-align:center;color:#666}
  footer{max-width:900px;margin:18px auto;padding:10px 16px;color:#666;font-size:0.9rem}
  @media (min-width:760px){ .timeline{grid-template-columns:1fr 1fr} }
</style>
</head>
<body>
<header>
  <div class="container">
    <h1>Fremantle Dockers — Key Moments & History</h1>
    <div style="margin-top:8px;color:rgba(255,255,255,0.9)">Interactive timeline with search, filter, and sort</div>
  </div>
</header>

<main class="container">
  <div class="controls">
    <input id="q" class="search" placeholder="Search events, players, or years" />
    <select id="filter">
      <option value="all">All eras</option>
      <option value="origins">Origins & formation</option>
      <option value="early">Early AFL years</option>
      <option value="modern">Modern era</option>
      <option value="milestones">Milestones</option>
    </select>
    <select id="sort">
      <option value="asc">Oldest → Newest</option>
      <option value="desc">Newest → Oldest</option>
    </select>
    <button id="clear">Clear</button>
  </div>

  <section id="timeline" class="timeline" aria-live="polite"></section>
  <div id="empty" class="empty" hidden>No events found — try different search terms.</div>
</main>

<footer>
  Timeline data is illustrative. Add or edit events in the JavaScript data array.
</footer>

<script>
const events = [
  { year: 1994, title: "Fremantle Football Club formed", era: "origins",
    img: "https://upload.wikimedia.org/wikipedia/commons/6/6b/Fremantle_Dockers_logo.svg",
    desc: "The Fremantle Football Club is founded and admitted to the AFL for the 1995 season." },
  { year: 1995, title: "AFL debut season", era: "early",
    img: "https://upload.wikimedia.org/wikipedia/commons/6/6b/Fremantle_Dockers_logo.svg",
    desc: "Fremantle plays its first AFL matches; the club establishes its identity and maroon/purple colours." },
  { year: 1997, title: "First finals appearance", era: "early",
    img: "https://upload.wikimedia.org/wikipedia/commons/5/57/1997_AFL_finals_logo.png",
    desc: "Fremantle reaches its first finals series." },
  { year: 2013, title: "First Grand Final appearance", era: "modern",
    img: "https://upload.wikimedia.org/wikipedia/commons/6/6b/Fremantle_Dockers_logo.svg",
    desc: "Fremantle reaches its first AFL Grand Final (lost to Hawthorn)." },
  { year: 2015, title: "Nat Fyfe Brownlow Medal", era: "modern",
    img: "https://upload.wikimedia.org/wikipedia/commons/1/12/Brownlow_Medal.png",
    desc: "Nat Fyfe wins the Brownlow Medal as the AFL's best and fairest." },
  { year: 2023, title: "Recent rebuild & draft focus", era: "modern",
    img: "https://upload.wikimedia.org/wikipedia/commons/6/6b/Fremantle_Dockers_logo.svg",
    desc: "The club focuses on youth and recruiting through the draft as part of a rebuild." }
];

// Utility: render timeline
const timelineEl = document.getElementById('timeline');
const emptyEl = document.getElementById('empty');
const qEl = document.getElementById('q');
const filterEl = document.getElementById('filter');
const sortEl = document.getElementById('sort');
const clearBtn = document.getElementById('clear');

function render(list){
  timelineEl.innerHTML = '';
  if(!list.length){ emptyEl.hidden = false; return }
  emptyEl.hidden = true;
  list.forEach(ev => {
    const card = document.createElement('article');
    card.className = 'card';
    card.innerHTML = `
      <div class="thumb"><img loading="lazy" src="${ev.img}" alt=""></div>
      <div>
        <div class="meta"><strong>${ev.year}</strong> — <span>${capitalize(ev.era)}</span></div>
        <h3 class="title">${ev.title}</h3>
        <p class="desc">${ev.desc}</p>
      </div>
    `;
    timelineEl.appendChild(card);
  });
}

function capitalize(s){ return s[0]?.toUpperCase()+s.slice(1) }

function applyFilters(){
  const q = qEl.value.trim().toLowerCase();
  const era = filterEl.value;
  const sort = sortEl.value;
  let results = events.filter(ev => {
    const matchesQ = !q || [ev.title, ev.desc, String(ev.year)].join(' ').toLowerCase().includes(q);
    const matchesEra = era === 'all' || ev.era === era;
    return matchesQ && matchesEra;
  });
  results.sort((a,b)=> sort==='asc' ? a.year - b.year : b.year - a.year);
  render(results);
}

// Initial render
applyFilters();

// Event listeners
[qEl, filterEl, sortEl].forEach(el => el.addEventListener('input', applyFilters));
clearBtn.addEventListener('click', ()=>{
  qEl.value=''; filterEl.value='all'; sortEl.value='asc'; applyFilters();
});
</script>
