/* ----------------------------- Mock data ----------------------------- */
const PROGRAMS = [
  { name:"Digital Skills", trained:3200, employed:2240, completion:88, placement:70, salaryBefore:14200, salaryAfter:24500, retention6:84, retention12:71, impact:82 },
  { name:"Women Employment", trained:2100, employed:1281, completion:91, placement:61, salaryBefore:11800, salaryAfter:20100, retention6:80, retention12:68, impact:76 },
  { name:"Youth Skill Dev.", trained:4600, employed:2622, completion:79, placement:57, salaryBefore:10500, salaryAfter:18900, retention6:74, retention12:58, impact:68 },
  { name:"Rural Skill Init.", trained:2800, employed:1428, completion:82, placement:51, salaryBefore:9200, salaryAfter:15800, retention6:69, retention12:52, impact:61 },
];
const LOCATIONS = [
  { name:"Bengaluru", rate:74 }, { name:"Pune", rate:68 }, { name:"Hyderabad", rate:66 },
  { name:"Jaipur", rate:54 }, { name:"Bhopal", rate:47 }, { name:"Guwahati", rate:41 },
];
const SKILL_GAP = [
  { skill:"Python", demand:88, possess:60 }, { skill:"SQL", demand:91, possess:55 },
  { skill:"Cloud Computing", demand:84, possess:38 }, { skill:"AI / ML", demand:79, possess:33 },
  { skill:"Cybersecurity", demand:72, possess:34 }, { skill:"Data Analytics", demand:86, possess:57 },
  { skill:"Digital Marketing", demand:63, possess:49 }, { skill:"Communication", demand:90, possess:71 },
];
const EMPLOYMENT_STATUS = [
  { name:"Employed", value:62, color:"green" }, { name:"Seeking work", value:24, color:"amber" },
  { name:"In training", value:9, color:"blue" }, { name:"Inactive", value:5, color:"red" },
];
const OUTCOMES_OVER_TIME = [
  { month:"Jan", rate:51 }, { month:"Feb", rate:53 }, { month:"Mar", rate:55 }, { month:"Apr", rate:54 },
  { month:"May", rate:58 }, { month:"Jun", rate:60 }, { month:"Jul", rate:59 }, { month:"Aug", rate:62 }, { month:"Sep", rate:65 },
];
const FUNNEL = [
  { stage:"Joined Training", count:1000, icon:"🎓" }, { stage:"Completed Training", count:850, icon:"✅" },
  { stage:"Certified", count:700, icon:"📄" }, { stage:"Interviewed", count:500, icon:"👥" },
  { stage:"Employed", count:320, icon:"💼" }, { stage:"Retained – 6 Months", count:270, icon:"⏱" },
  { stage:"Retained – 12 Months", count:214, icon:"📈" },
];
const EMPLOYER_DEMAND = [
  { skill:"Python", demand:"High", available:72, gap:28 }, { skill:"SQL", demand:"Very High", available:61, gap:39 },
  { skill:"Cloud Computing", demand:"High", available:42, gap:58 }, { skill:"Cybersecurity", demand:"Medium", available:35, gap:65 },
  { skill:"AI / ML", demand:"Very High", available:31, gap:69 }, { skill:"Digital Marketing", demand:"Medium", available:58, gap:42 },
];
const CANDIDATES = [
  { id:"C-1042", name:"Ananya Sharma", location:"Bengaluru", education:"B.Tech CSE", program:"Digital Skills", certified:true, status:"Employed", company:"Nimbus Retail", salary:26000, gap:"Cloud", m6:"Retained", m12:"Retained" },
  { id:"C-1043", name:"Rohit Verma", location:"Pune", education:"Diploma - Mech", program:"Youth Skill Dev.", certified:true, status:"Seeking", company:"—", salary:null, gap:"SQL, Cloud", m6:"—", m12:"—" },
  { id:"C-1044", name:"Fatima Khan", location:"Hyderabad", education:"B.Sc IT", program:"Women Employment", certified:true, status:"Employed", company:"Verdant Analytics", salary:22500, gap:"AI/ML", m6:"Retained", m12:"Pending" },
  { id:"C-1045", name:"Suresh Patil", location:"Jaipur", education:"B.A.", program:"Rural Skill Init.", certified:false, status:"In Training", company:"—", salary:null, gap:"SQL, Python, Cloud", m6:"—", m12:"—" },
  { id:"C-1046", name:"Priya Nair", location:"Bengaluru", education:"M.Tech", program:"Digital Skills", certified:true, status:"Employed", company:"Orbit Systems", salary:31000, gap:"—", m6:"Retained", m12:"Retained" },
  { id:"C-1047", name:"Karan Mehta", location:"Guwahati", education:"B.Com", program:"Youth Skill Dev.", certified:true, status:"Employed", company:"Fernhill Media", salary:18500, gap:"Data Analytics", m6:"At Risk", m12:"—" },
  { id:"C-1048", name:"Deepa Iyer", location:"Pune", education:"B.Sc Stats", program:"Women Employment", certified:true, status:"Employed", company:"Lumen Fintech", salary:24800, gap:"Cloud", m6:"Retained", m12:"Retained" },
  { id:"C-1049", name:"Arjun Reddy", location:"Bhopal", education:"Diploma - IT", program:"Rural Skill Init.", certified:false, status:"Seeking", company:"—", salary:null, gap:"SQL, Communication", m6:"—", m12:"—" },
];
const INSIGHTS = [
  { tone:"warn", text:"38% of trained candidates remain unemployed six months after program completion." },
  { tone:"warn", text:"Cloud Computing shows the widest industry skill gap, at 58 percentage points." },
  { tone:"good", text:"Candidates completing advanced-track training show a 24% higher placement rate." },
  { tone:"up", text:"12-month retention improved 15% year-over-year across all initiatives." },
  { tone:"warn", text:"Rural Skill Initiative placement trails the program average by 19 points." },
];
const NAV = [
  { key:"home", label:"Home", icon:"⌂" }, { key:"dashboard", label:"Dashboard", icon:"▦" },
  { key:"skillgap", label:"Skill Gap Analysis", icon:"🎯" }, { key:"outcomes", label:"Employment Outcomes", icon:"⑂" },
  { key:"initiatives", label:"Initiative Impact", icon:"📈" }, { key:"candidates", label:"Candidate Tracking", icon:"👥" },
  { key:"employer", label:"Employer Demand", icon:"🏢" }, { key:"reports", label:"Reports", icon:"📄" },
];

/* ----------------------------- CSS var reader ----------------------------- */
function cssVar(name){ return getComputedStyle(document.body).getPropertyValue(name).trim(); }

/* ----------------------------- Navigation ----------------------------- */
const navList = document.getElementById("navList");
NAV.forEach(n=>{
  const btn = document.createElement("button");
  btn.innerHTML = `<span class="nav-icon">${n.icon}</span>${n.label}`;
  btn.dataset.key = n.key;
  btn.onclick = ()=> goPage(n.key);
  navList.appendChild(btn);
});

function goPage(key){
  document.querySelectorAll(".page").forEach(p=> p.classList.toggle("active", p.dataset.page===key));
  document.querySelectorAll("#navList button").forEach(b=> b.classList.toggle("active", b.dataset.key===key));
  const label = NAV.find(n=>n.key===key)?.label || "";
  document.getElementById("pageTitle").textContent = label;
  document.getElementById("sidebar").classList.remove("open");
  document.getElementById("overlay").classList.remove("show");
}
goPage("home");

document.getElementById("menuBtn").onclick = ()=>{
  document.getElementById("sidebar").classList.add("open");
  document.getElementById("overlay").classList.add("show");
};
document.getElementById("closeNav").onclick = document.getElementById("overlay").onclick = ()=>{
  document.getElementById("sidebar").classList.remove("open");
  document.getElementById("overlay").classList.remove("show");
};

/* ----------------------------- Theme toggle ----------------------------- */
const themeToggle = document.getElementById("themeToggle");
themeToggle.onclick = ()=>{
  const isDark = document.body.getAttribute("data-theme") === "dark";
  document.body.setAttribute("data-theme", isDark ? "light" : "dark");
  themeToggle.textContent = isDark ? "☾" : "☀";
  renderAllCharts();
};

/* ----------------------------- Populate selects ----------------------------- */
function fillSelect(el, items, prefix){
  el.innerHTML = "";
  const allOpt = document.createElement("option"); allOpt.textContent = prefix; el.appendChild(allOpt);
  items.forEach(i=>{ const o = document.createElement("option"); o.textContent = i; el.appendChild(o); });
}
fillSelect(document.getElementById("filterLocation"), LOCATIONS.map(l=>l.name), "All");
fillSelect(document.getElementById("filterProgram1"), PROGRAMS.map(p=>p.name), "All");
fillSelect(document.getElementById("filterProgram2"), PROGRAMS.map(p=>p.name), "All");
fillSelect(document.getElementById("repLocation"), LOCATIONS.map(l=>l.name), "All locations");
fillSelect(document.getElementById("repProgram"), PROGRAMS.map(p=>p.name), "All programs");

/* ----------------------------- Insights ----------------------------- */
const toneMap = { warn:{icon:"⚠",accent:"amber"}, good:{icon:"✔",accent:"green"}, up:{icon:"📈",accent:"blue"} };
document.getElementById("insightsList").innerHTML = INSIGHTS.map(ins=>{
  const {icon,accent} = toneMap[ins.tone];
  return `<div class="insight-item"><div class="insight-icon" style="background:var(--${accent}Soft); color:var(--${accent});">${icon}</div><span>${ins.text}</span></div>`;
}).join("");

/* ----------------------------- Skill gap bars ----------------------------- */
document.getElementById("skillBars").innerHTML = SKILL_GAP.map(s=>`
  <div class="skill-row">
    <div class="skill-row-top"><span class="name">${s.skill}</span><span class="meta">${s.possess}% possess · ${s.demand}% demand</span></div>
    <div class="bar-wrap">
      <div class="bar-bg" style="width:${s.demand}%;"></div>
      <div class="bar-fg" style="width:${s.possess}%;"></div>
    </div>
  </div>`).join("");

/* ----------------------------- Funnel ----------------------------- */
function renderFunnel(){
  const max = FUNNEL[0].count;
  document.getElementById("funnelCard").innerHTML = FUNNEL.map((f,i)=>{
    const pct = Math.round((f.count/max)*100);
    const prevPct = i>0 ? Math.round((FUNNEL[i-1].count/max)*100) : null;
    const drop = prevPct ? prevPct-pct : 0;
    return `<div class="funnel-row">
      <div class="funnel-icon">${f.icon}</div>
      <div class="funnel-body">
        <div class="funnel-top"><span style="font-weight:500;">${f.stage}</span><span style="color:var(--inkSoft);">${f.count.toLocaleString()} ${drop>0?`<span style="color:var(--red);">· −${drop}%</span>`:""}</span></div>
        <div class="funnel-track"><div class="funnel-fill" style="width:${pct}%;"></div></div>
      </div>
    </div>`;
  }).join("");
}
renderFunnel();

/* ----------------------------- Initiatives ----------------------------- */
const initColors = ["blue","purple","green","amber"];
function impactRingSVG(value, colorVar){
  const r=26, c=2*Math.PI*r, off = c - (value/100)*c;
  return `<svg width="64" height="64" viewBox="0 0 64 64">
    <circle cx="32" cy="32" r="${r}" fill="none" stroke="var(--surfaceAlt)" stroke-width="7"/>
    <circle cx="32" cy="32" r="${r}" fill="none" stroke="var(--${colorVar})" stroke-width="7" stroke-dasharray="${c}" stroke-dashoffset="${off}" stroke-linecap="round" transform="rotate(-90 32 32)"/>
    <text x="32" y="36" text-anchor="middle" font-size="14" font-weight="600" fill="var(--ink)" font-family="Manrope, sans-serif">${value}</text>
  </svg>`;
}
document.getElementById("initiativeCards").innerHTML = PROGRAMS.map((p,i)=>`
  <div class="card">
    <div class="init-card-top">
      <div><h3>${p.name}</h3><span>${p.trained.toLocaleString()} candidates trained</span></div>
      ${impactRingSVG(p.impact, initColors[i])}
    </div>
    <div class="init-metrics">
      <div class="init-metric"><div class="val">${p.completion}%</div><div class="lbl">Completion</div></div>
      <div class="init-metric"><div class="val">${p.placement}%</div><div class="lbl">Placement</div></div>
      <div class="init-metric"><div class="val">${p.retention12}%</div><div class="lbl">Retention 12mo</div></div>
    </div>
    <div class="init-salary"><span>Avg. salary post-training</span><b>₹${p.salaryAfter.toLocaleString()}/mo</b></div>
  </div>`).join("");

/* ----------------------------- Candidates table ----------------------------- */
function statusPillClass(s){ return s==="Employed"?"pill-green":s==="Seeking"?"pill-amber":"pill-blue"; }

function renderCandidates(){
  const q = document.getElementById("candidateSearch").value.toLowerCase();
  const statusF = document.getElementById("filterStatus").value;
  const programF = document.getElementById("filterProgram2").value;
  const filtered = CANDIDATES.filter(c=>
    (statusF==="All" || c.status===statusF) &&
    (programF==="All" || c.program===programF) &&
    (c.name.toLowerCase().includes(q) || c.id.toLowerCase().includes(q))
  );
  const tbody = document.getElementById("candidateTable");
  if(filtered.length===0){
    tbody.innerHTML = `<tr><td colspan="6" class="empty-row">No candidates match these filters.</td></tr>`;
    return;
  }
  tbody.innerHTML = filtered.map(c=>`
    <tr class="row-clickable" onclick='openDrawer("${c.id}")'>
      <td style="font-weight:500;">${c.name}</td>
      <td style="color:var(--inkSoft);">📍 ${c.location}</td>
      <td style="color:var(--inkSoft);">${c.program}</td>
      <td><span class="pill ${statusPillClass(c.status)}">${c.status}</span></td>
      <td style="color:var(--inkSoft);">${c.company}</td>
      <td>${c.salary ? "₹"+c.salary.toLocaleString() : "—"}</td>
    </tr>`).join("");
}
document.getElementById("candidateSearch").addEventListener("input", renderCandidates);
document.getElementById("filterStatus").addEventListener("change", renderCandidates);
document.getElementById("filterProgram2").addEventListener("change", renderCandidates);
renderCandidates();

/* ----------------------------- Candidate drawer ----------------------------- */
function openDrawer(id){
  const c = CANDIDATES.find(x=>x.id===id);
  if(!c) return;
  document.getElementById("drawerName").textContent = c.name;
  document.getElementById("drawerMeta").textContent = `${c.id} · ${c.location}`;
  document.getElementById("drawerTags").innerHTML = `<span class="pill ${statusPillClass(c.status)}">${c.status}</span><span class="pill pill-purple">${c.program}</span>`;
  const fields = [["Education",c.education],["Company",c.company],["Salary", c.salary ? "₹"+c.salary.toLocaleString()+"/mo" : "—"],["Certified", c.certified?"Yes":"No"],["Skill gap",c.gap]];
  document.getElementById("drawerGrid").innerHTML = fields.map(([l,v])=>`<div><div class="lbl">${l}</div><div class="val">${v}</div></div>`).join("");

  const steps = ["Joined","Completed","Certified","Interviewed","Employed","6-Month","12-Month"];
  const reached = c.status==="Employed" ? (c.m12==="Retained"?7:c.m6==="Retained"?6:5) : c.certified?3:2;
  document.getElementById("drawerTimeline").innerHTML = steps.map((s,i)=>`
    <div class="timeline-step">
      <div class="timeline-dotcol">
        <div class="timeline-dot ${i<reached?'reached':''}"></div>
        ${i<steps.length-1 ? `<div class="timeline-line ${i<reached-1?'reached':''}"></div>` : ""}
      </div>
      <div class="timeline-label ${i<reached?'reached':''}">${s}</div>
    </div>`).join("");

  document.getElementById("drawerOverlay").classList.add("show");
}
document.getElementById("drawerClose").onclick =
document.getElementById("drawerOverlay").onclick = ()=> document.getElementById("drawerOverlay").classList.remove("show");

/* ----------------------------- Employer demand table ----------------------------- */
function demandPillClass(d){ return d==="Very High"?"pill-red":d==="High"?"pill-amber":"pill-blue"; }
document.getElementById("employerTable").innerHTML = EMPLOYER_DEMAND.map(r=>`
  <tr>
    <td style="font-weight:500;">${r.skill}</td>
    <td><span class="pill ${demandPillClass(r.demand)}">${r.demand}</span></td>
    <td style="color:var(--inkSoft);">${r.available}%</td>
    <td style="color:var(--red); font-weight:500;">${r.gap}%</td>
  </tr>`).join("");

/* ----------------------------- Reports ----------------------------- */
document.getElementById("generateReportBtn").onclick = ()=>{
  const range = document.getElementById("repRange").value;
  const location = document.getElementById("repLocation").value;
  const program = document.getElementById("repProgram").value;
  const status = document.getElementById("repStatus").value;
  document.getElementById("reportTitle").textContent = `Summary — ${range}, ${location}, ${program}, ${status}`;
  const items = [
    ["Training participation","12,700 candidates enrolled across 4 programs"],
    ["Employment outcomes","58% employed within the selected filters"],
    ["Skill gaps","Cloud Computing and AI/ML remain the widest gaps"],
    ["Salary outcomes","Average salary rose from ₹11,400 to ₹19,800/mo"],
    ["Retention","71% retained at 12 months for top-performing programs"],
    ["Overall impact","Blended impact score of 72/100 across all initiatives"],
  ];
  document.getElementById("reportGrid").innerHTML = items.map(([l,v])=>`<div class="report-item"><div class="lbl">${l}</div><div class="val">${v}</div></div>`).join("");
  document.getElementById("reportSummary").style.display = "block";
};

/* ----------------------------- Charts (Chart.js) ----------------------------- */
let chartInstances = [];
function destroyCharts(){ chartInstances.forEach(c=>c.destroy()); chartInstances = []; }

function baseGridColor(){ return cssVar("--border"); }
function baseTextColor(){ return cssVar("--inkSoft"); }

function makeBar(id, labels, dataset, color, horizontal=false, label=""){
  const ctx = document.getElementById(id);
  if(!ctx) return;
  const chart = new Chart(ctx, {
    type: "bar",
    data: { labels, datasets: [{ label, data: dataset, backgroundColor: color, borderRadius: 6, maxBarThickness: 40 }] },
    options: {
      indexAxis: horizontal ? "y" : "x",
      plugins: { legend: { display: false } },
      scales: {
        x: { grid: { color: baseGridColor(), display: !horizontal }, ticks: { color: baseTextColor(), font:{size:11} } },
        y: { grid: { color: baseGridColor(), display: horizontal }, ticks: { color: baseTextColor(), font:{size:11} } },
      }
    }
  });
  chartInstances.push(chart);
  return chart;
}

function renderAllCharts(){
  destroyCharts();

  makeBar("chartByProgram", PROGRAMS.map(p=>p.name), PROGRAMS.map(p=>p.placement), cssVar("--blue"));
  makeBar("chartByLocation", LOCATIONS.map(l=>l.name), LOCATIONS.map(l=>l.rate), cssVar("--purple"), true);

  const ctxSalary = document.getElementById("chartSalary");
  if(ctxSalary){
    const c = new Chart(ctxSalary, {
      type:"bar",
      data:{ labels: PROGRAMS.map(p=>p.name), datasets:[
        { label:"Before training (₹/mo)", data: PROGRAMS.map(p=>p.salaryBefore), backgroundColor: cssVar("--inkSoft"), borderRadius:6, maxBarThickness:26 },
        { label:"After training (₹/mo)", data: PROGRAMS.map(p=>p.salaryAfter), backgroundColor: cssVar("--green"), borderRadius:6, maxBarThickness:26 },
      ]},
      options:{ plugins:{ legend:{ position:"bottom", labels:{ color: baseTextColor(), font:{size:12} } } },
        scales:{ x:{ grid:{color:baseGridColor()}, ticks:{color:baseTextColor(), font:{size:11}} }, y:{ grid:{color:baseGridColor()}, ticks:{color:baseTextColor(), font:{size:11}} } } }
    });
    chartInstances.push(c);
  }

  const ctxStatus = document.getElementById("chartStatus");
  if(ctxStatus){
    const c = new Chart(ctxStatus, {
      type:"doughnut",
      data:{ labels: EMPLOYMENT_STATUS.map(s=>s.name), datasets:[{ data: EMPLOYMENT_STATUS.map(s=>s.value), backgroundColor: EMPLOYMENT_STATUS.map(s=>cssVar("--"+s.color)), borderWidth:0 }] },
      options:{ cutout:"58%", plugins:{ legend:{ position:"bottom", labels:{ color: baseTextColor(), font:{size:12} } } } }
    });
    chartInstances.push(c);
  }

  const demandSorted = [...SKILL_GAP].sort((a,b)=>b.demand-a.demand);
  makeBar("chartDemand", demandSorted.map(s=>s.skill), demandSorted.map(s=>s.demand), cssVar("--blue"));
  makeBar("chartDemand2", demandSorted.map(s=>s.skill), demandSorted.map(s=>s.demand), cssVar("--blue"));

  const gapSorted = [...SKILL_GAP].map(s=>({...s, gap:s.demand-s.possess})).sort((a,b)=>b.gap-a.gap);
  makeBar("chartGap1", gapSorted.map(s=>s.skill), gapSorted.map(s=>s.gap), cssVar("--amber"));
  makeBar("chartGap2", gapSorted.map(s=>s.skill), gapSorted.map(s=>s.gap), cssVar("--amber"));
  makeBar("chartGap3", EMPLOYER_DEMAND.map(s=>s.skill), EMPLOYER_DEMAND.map(s=>s.gap), cssVar("--amber"));

  const ctxTrend = document.getElementById("chartTrend");
  if(ctxTrend){
    const c = new Chart(ctxTrend, {
      type:"line",
      data:{ labels: OUTCOMES_OVER_TIME.map(o=>o.month), datasets:[{ label:"Employment rate", data: OUTCOMES_OVER_TIME.map(o=>o.rate), borderColor: cssVar("--blue"), backgroundColor: cssVar("--blue"), tension:0.35, pointRadius:3 }] },
      options:{ plugins:{ legend:{ display:false } },
        scales:{ x:{ grid:{color:baseGridColor()}, ticks:{color:baseTextColor(), font:{size:11}} },
                 y:{ min:40, max:70, grid:{color:baseGridColor()}, ticks:{color:baseTextColor(), font:{size:11}} } } }
    });
    chartInstances.push(c);
  }

  makeBar("chartImpact", PROGRAMS.map(p=>p.name), PROGRAMS.map(p=>p.impact), cssVar("--purple"));
}
renderAllCharts();
