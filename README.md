<!DOCTYPE html>
<html lang="en" data-theme="light">
<head>
<!--
═══════════════════════════════════════════════════════════════════════════
  ClearSight Eye Care — Clinical Exam Portal
  Single-file, zero-dependency static web app
═══════════════════════════════════════════════════════════════════════════

  📦 DEPLOYMENT — 3 WAYS TO GO LIVE IN UNDER 2 MINUTES
  ───────────────────────────────────────────────────────

  ── OPTION 1 · GITHUB PAGES (free, recommended) ──────────────────────────
     1. Create a new GitHub repo (don't add a README).
     2. Rename this file to exactly:  index.html
     3. Upload it to the repo root (or use git):
            git init
            git add index.html
            git commit -m "Deploy ClearSight portal"
            git branch -M main
            git remote add origin https://github.com/<you>/<repo>.git
            git push -u origin main
     4. Repo → Settings → Pages → Source: "Deploy from a branch"
        Branch: main · Folder: / (root) → Save
     5. Wait ~60 seconds. Your app is live at:
            https://<you>.github.io/<repo>/

  ── OPTION 2 · NETLIFY DROP (no account needed) ──────────────────────────
     1. Rename this file to:  index.html
     2. Open https://app.netlify.com/drop
     3. Drag the file onto the page. Done — instant URL.

  ── OPTION 3 · VERCEL ────────────────────────────────────────────────────
     1. Rename to:  index.html
     2. Push to GitHub, then:
            https://vercel.com/new  →  Import repo
            Framework: Other · Build: (empty) · Output: .  →  Deploy

  ── OPTION 4 · LOCAL PREVIEW ─────────────────────────────────────────────
     Just double-click the file. It opens in your browser.
     Or serve it:   python3 -m http.server 8080

  ─────────────────────────────────────────────────────────────────────────

  🖼️ REPLACING PLACEHOLDER IMAGES
  ────────────────────────────────
     Every <img> uses https://placehold.co as a temporary source.
     To use real clinical images:
       1. Create  assets/images/  next to this file.
       2. Save your images there (e.g., fundus-od.jpg, snellen.png).
       3. Find/replace  https://placehold.co/...  with  assets/images/...
       4. Also update the matching  data-caption  attribute on each <img>.

  🎨 CHANGING THE COLOR THEME
  ───────────────────────────
     All colors live in the  :root { }  block inside <style> below.
     Change --primary, --secondary, --hero-from, --hero-to to rebrand
     the entire interface. Dark mode uses [data-theme="dark"] { }.

  👤 CHANGING THE PATIENT
  ───────────────────────
     Search for "Emily Carter" — replace in:
       · <h1 id="patientName">
       · the four .qstat values
       · the .snapshot rail card
       · the finalize section (#fin-patient, #fin-id)
       · the patient history timeline

  ⌨️ KEYBOARD SHORTCUTS
  ─────────────────────
     Alt+1 … Alt+6   jump between exam steps
     Esc             close image lightbox
     Tab / Shift+Tab  move through controls
     Arrow keys      navigate the tab bar

  ⚠️ CLINICAL DISCLAIMER
  ─────────────────────
     Demonstration interface only. Not a certified medical device.
     Do NOT deploy with real Protected Health Information (PHI)
     without adding authentication, encryption, audit logging,
     and appropriate regulatory clearance (HIPAA / GDPR / MDR).

  📄 LICENSE
  ──────────
     MIT — free to use, modify, and redistribute. See:
     https://opensource.org/licenses/MIT

═══════════════════════════════════════════════════════════════════════════
-->
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="description" content="ClearSight Eye Care — accessible clinical eye exam portal for optometrists. Single-file static web app.">
<meta name="theme-color" content="#0b5e8a">
<title>ClearSight Eye Care · Clinical Exam Portal</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>👁</text></svg>">
<style>
/* ============================================================
   1. DESIGN TOKENS
   ============================================================ */
:root{
  --font:'Inter',system-ui,-apple-system,"Segoe UI",Roboto,sans-serif;
  --container:1280px;
  --gutter:24px;
  --topbar-h:68px;
  --radius-lg:16px;
  --radius:12px;
  --radius-sm:8px;
  --space:24px;
  --space-sm:16px;
  --space-xs:8px;
  --ring:0 0 0 3px rgba(255,143,0,.55);
  --bg:#f3f8fb;
  --surface:#ffffff;
  --surface-2:#f8fbfd;
  --text:#14202b;
  --text-muted:#55697c;
  --border:#dce8f1;
  --border-strong:#c3d5e2;
  --primary:#0b5e8a;
  --primary-soft:#e6f2f8;
  --primary-soft-2:#d3e9f4;
  --secondary:#127f8f;
  --btn-bg:#0b5e8a;
  --btn-bg-hover:#084a6d;
  --btn-text:#ffffff;
  --success:#2e7d32;
  --success-soft:#e8f5e9;
  --warning:#9a6100;
  --warning-soft:#fff4e0;
  --danger:#b3261e;
  --danger-soft:#fdecea;
  --shadow-sm:0 1px 2px rgba(16,42,67,.06),0 1px 3px rgba(16,42,67,.05);
  --shadow:0 4px 16px rgba(16,42,67,.08);
  --shadow-lg:0 14px 36px rgba(16,42,67,.14);
  --hero-from:#0b5e8a;
  --hero-to:#0a4a6e;
}
[data-theme="dark"]{
  --bg:#0d1620;--surface:#152332;--surface-2:#1a2b3c;
  --text:#e9f2f8;--text-muted:#a2b7c8;
  --border:#24384b;--border-strong:#35526b;
  --primary:#7ccbf0;--primary-soft:#14344a;--primary-soft-2:#1b4661;
  --secondary:#4dd0c4;
  --btn-bg:#7ccbf0;--btn-bg-hover:#9ad8f5;--btn-text:#062330;
  --success:#7fda8b;--success-soft:#16341d;
  --warning:#ffc46b;--warning-soft:#3a2c14;
  --danger:#ff9d97;--danger-soft:#3a1b1b;
  --shadow-sm:0 1px 2px rgba(0,0,0,.4);
  --shadow:0 6px 20px rgba(0,0,0,.4);
  --shadow-lg:0 16px 40px rgba(0,0,0,.5);
  --hero-from:#0e3350;--hero-to:#0a2438;
}

/* ============================================================
   2. RESET & BASE
   ============================================================ */
*,*::before,*::after{box-sizing:border-box}
html{scroll-behavior:smooth;-webkit-text-size-adjust:100%}
body{margin:0;font-family:var(--font);font-size:15px;line-height:1.55;color:var(--text);background:var(--bg);-webkit-font-smoothing:antialiased}
h1,h2,h3,h4,p,figure,ul,ol{margin:0}
ul,ol{padding:0;list-style:none}
img{max-width:100%;display:block}
button{font:inherit;color:inherit;cursor:pointer}
a{color:inherit;text-decoration:none}
input,select,textarea{font:inherit;color:inherit}
:focus-visible{outline:none;box-shadow:var(--ring);border-radius:var(--radius-sm)}

/* ============================================================
   3. UTILITIES
   ============================================================ */
.container{width:100%;max-width:var(--container);margin-inline:auto;padding-inline:var(--gutter)}
.sr-only{position:absolute;width:1px;height:1px;padding:0;margin:-1px;overflow:hidden;clip:rect(0,0,0,0);white-space:nowrap;border:0}
.skip-link{position:absolute;left:var(--gutter);top:-60px;z-index:1000;background:var(--surface);color:var(--primary);font-weight:700;padding:12px 20px;border-radius:var(--radius-sm);box-shadow:var(--shadow-lg);border:2px solid var(--primary);transition:top .2s}
.skip-link:focus{top:12px}
.stack{display:flex;flex-direction:column;gap:var(--space)}
.grid{display:grid;gap:var(--space)}

/* ============================================================
   4. TOP BAR
   ============================================================ */
.topbar{position:sticky;top:0;z-index:90;height:var(--topbar-h);background:color-mix(in srgb,var(--surface) 92%,transparent);backdrop-filter:saturate(180%) blur(12px);border-bottom:1px solid var(--border)}
.topbar-inner{height:100%;display:grid;grid-template-columns:auto minmax(0,1fr) auto;align-items:center;gap:var(--space)}
.brand{display:inline-flex;align-items:center;gap:10px;font-weight:800;font-size:1.12rem;color:var(--primary);letter-spacing:-.02em;min-height:44px}
.brand-mark{width:40px;height:40px;border-radius:11px;background:linear-gradient(135deg,var(--hero-from),var(--hero-to));color:#fff;display:grid;place-items:center;font-size:1.15rem;box-shadow:var(--shadow-sm)}
.brand-sub{font-weight:500;color:var(--text-muted);font-size:.9rem}
.search-field{position:relative;max-width:420px;width:100%}
.search-field input{width:100%;height:44px;padding:0 16px 0 44px;border:1.5px solid var(--border);border-radius:var(--radius);background:var(--surface-2);transition:border-color .15s,background .15s}
.search-field input:focus-visible{border-color:var(--primary)}
.search-field .search-icon{position:absolute;left:14px;top:50%;transform:translateY(-50%);color:var(--text-muted);pointer-events:none;font-size:1rem}
.topbar-actions{display:flex;align-items:center;gap:10px}
.autosave{display:inline-flex;align-items:center;gap:8px;font-size:.8rem;font-weight:600;color:var(--text-muted);padding:6px 12px;border-radius:999px;background:var(--surface-2);border:1px solid var(--border);min-height:36px}
.autosave .dot{width:8px;height:8px;border-radius:50%;background:var(--success);flex:0 0 auto}
.autosave.is-saving .dot{background:var(--warning);animation:pulse 1s infinite}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.35}}
.icon-btn{width:44px;height:44px;display:grid;place-items:center;border:1.5px solid var(--border);border-radius:var(--radius);background:var(--surface);font-size:1.05rem;transition:.15s}
.icon-btn:hover{background:var(--primary-soft);border-color:var(--primary)}
.doctor-chip{display:inline-flex;align-items:center;gap:10px;padding:5px 14px 5px 5px;border-radius:999px;border:1.5px solid var(--border);background:var(--surface);min-height:44px}
.doctor-chip img{width:32px;height:32px;border-radius:50%;object-fit:cover}
.doctor-chip .who{line-height:1.1}
.doctor-chip .who strong{display:block;font-size:.82rem}
.doctor-chip .who span{font-size:.72rem;color:var(--text-muted)}

/* ============================================================
   5. PATIENT HERO
   ============================================================ */
.patient-hero{background:linear-gradient(135deg,var(--hero-from),var(--hero-to));color:#fff;padding-block:22px 60px;position:relative;overflow:hidden}
.patient-hero::after{content:"";position:absolute;right:-120px;top:-140px;width:440px;height:440px;border-radius:50%;background:radial-gradient(circle,rgba(27,154,170,.35),transparent 70%);pointer-events:none}
.patient-hero .container{position:relative;z-index:1}
.breadcrumbs{display:flex;align-items:center;gap:8px;flex-wrap:wrap;font-size:.8rem;color:rgba(255,255,255,.72);margin-bottom:18px}
.breadcrumbs a{color:rgba(255,255,255,.9);text-decoration:underline;text-underline-offset:3px}
.breadcrumbs .sep{opacity:.55}
.breadcrumbs [aria-current="page"]{color:#fff;font-weight:600}
.patient-head{display:grid;grid-template-columns:minmax(0,1fr) auto;align-items:center;gap:var(--space)}
.patient-identity{display:flex;align-items:center;gap:18px;min-width:0}
.patient-avatar{width:76px;height:76px;border-radius:50%;flex:0 0 auto;border:3px solid rgba(255,255,255,.32);box-shadow:0 6px 18px rgba(0,0,0,.22);object-fit:cover;background:#fff}
.patient-identity h1{font-size:clamp(1.35rem,2.4vw,1.75rem);font-weight:800;letter-spacing:-.02em;line-height:1.15}
.patient-identity .meta{display:flex;flex-wrap:wrap;gap:6px 18px;margin-top:6px;font-size:.85rem;color:rgba(255,255,255,.86)}
.patient-actions{display:flex;flex-wrap:wrap;gap:10px}
.chip{display:inline-flex;align-items:center;gap:7px;padding:7px 14px;border-radius:999px;font-size:.8rem;font-weight:600;background:rgba(255,255,255,.14);border:1px solid rgba(255,255,255,.22);color:#fff;white-space:nowrap;backdrop-filter:blur(6px)}
.chip strong{font-weight:800}

.btn{display:inline-flex;align-items:center;justify-content:center;gap:8px;min-height:44px;padding:0 20px;border-radius:var(--radius);font-weight:600;font-size:.9rem;border:1.5px solid transparent;transition:.15s ease;white-space:nowrap}
.btn-primary{background:var(--btn-bg);color:var(--btn-text);box-shadow:var(--shadow-sm)}
.btn-primary:hover{background:var(--btn-bg-hover)}
.btn-secondary{background:var(--surface);color:var(--primary);border-color:var(--border-strong)}
.btn-secondary:hover{background:var(--primary-soft);border-color:var(--primary)}
.btn-ghost{background:rgba(255,255,255,.1);color:#fff;border-color:rgba(255,255,255,.35)}
.btn-ghost:hover{background:rgba(255,255,255,.2)}
.btn-sm{min-height:36px;padding:0 14px;font-size:.82rem;border-radius:var(--radius-sm)}

/* ============================================================
   6. QUICK STATS
   ============================================================ */
.quick-stats-wrap{margin-top:-38px;position:relative;z-index:10}
.quick-stats{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:0;background:var(--surface);border:1px solid var(--border);border-radius:var(--radius-lg);box-shadow:var(--shadow-lg);overflow:hidden}
.qstat{padding:18px 22px;border-right:1px solid var(--border);display:flex;flex-direction:column;justify-content:center;gap:3px;min-width:0}
.qstat:last-child{border-right:0}
.qstat .k{font-size:.7rem;font-weight:700;letter-spacing:.08em;text-transform:uppercase;color:var(--text-muted)}
.qstat .v{font-size:1.18rem;font-weight:800;color:var(--primary);letter-spacing:-.01em}
.qstat .v small{font-size:.72rem;font-weight:600;color:var(--text-muted);margin-left:3px}
.qstat .v.is-danger{color:var(--danger)}

/* ============================================================
   7. LAYOUT
   ============================================================ */
.page-main{padding-block:28px 56px}
.layout{display:grid;grid-template-columns:minmax(0,1fr) 340px;gap:var(--space);align-items:start}

/* ============================================================
   8. TAB BAR
   ============================================================ */
.tabbar-wrap{position:sticky;top:calc(var(--topbar-h) + 10px);z-index:60;margin-bottom:var(--space)}
.tabbar{display:grid;grid-template-columns:repeat(6,minmax(0,1fr));gap:6px;background:var(--surface);border:1px solid var(--border);border-radius:var(--radius-lg);padding:8px;box-shadow:var(--shadow)}
.tab{display:flex;flex-direction:column;align-items:center;justify-content:center;gap:5px;min-height:78px;padding:10px 6px;background:transparent;border:1.5px solid transparent;border-radius:var(--radius);text-align:center;transition:.16s ease;position:relative}
.tab:hover{background:var(--primary-soft)}
.tab .tab-ico{width:34px;height:34px;border-radius:10px;display:grid;place-items:center;background:var(--primary-soft);font-size:1.05rem;transition:.16s}
.tab .tab-label{font-size:.76rem;font-weight:700;letter-spacing:.01em;color:var(--text-muted);line-height:1.15}
.tab[aria-selected="true"]{background:var(--primary);border-color:var(--primary);box-shadow:var(--shadow-sm)}
.tab[aria-selected="true"] .tab-ico{background:rgba(255,255,255,.2)}
.tab[aria-selected="true"] .tab-label{color:var(--btn-text)}
[data-theme="dark"] .tab[aria-selected="true"] .tab-label{color:var(--btn-text)}
.tab .tab-dot{position:absolute;top:8px;right:8px;width:7px;height:7px;border-radius:50%;background:var(--border-strong);opacity:.9}
.tab.is-visited .tab-dot{background:var(--success)}
.tabbar-meta{display:flex;align-items:center;justify-content:space-between;gap:12px;padding:10px 4px 0;font-size:.76rem;color:var(--text-muted)}
.progress{display:flex;align-items:center;gap:10px;min-width:0;flex:1 1 auto}
.progress-track{flex:1 1 auto;max-width:220px;height:7px;border-radius:999px;background:var(--primary-soft);overflow:hidden}
.progress-fill{height:100%;width:0;border-radius:999px;background:linear-gradient(90deg,var(--primary),var(--secondary));transition:width .35s ease}
.kbd-hint{display:inline-flex;align-items:center;gap:5px;flex:0 0 auto}
kbd{font-family:var(--font);font-size:.68rem;font-weight:700;padding:2px 6px;border-radius:5px;border:1px solid var(--border-strong);background:var(--surface);box-shadow:0 1px 0 var(--border-strong)}

/* ============================================================
   9. PANELS & FORMS
   ============================================================ */
.panel{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius-lg);padding:var(--space);box-shadow:var(--shadow-sm)}
.panel[hidden]{display:none !important}
.panel-head{display:flex;align-items:flex-start;justify-content:space-between;gap:16px;padding-bottom:16px;margin-bottom:20px;border-bottom:1px solid var(--border)}
.panel-head h3{font-size:1.18rem;font-weight:800;color:var(--primary);letter-spacing:-.01em}
.panel-head p{font-size:.84rem;color:var(--text-muted);margin-top:2px}
.field-grid{display:grid;gap:16px 20px}
.cols-2{grid-template-columns:repeat(2,minmax(0,1fr))}
.cols-3{grid-template-columns:repeat(3,minmax(0,1fr))}
.field{display:flex;flex-direction:column;gap:6px;min-width:0}
.field label{font-size:.82rem;font-weight:700;color:var(--text)}
.field .hint{font-size:.74rem;color:var(--text-muted)}
.control{width:100%;height:44px;padding:0 14px;border:1.5px solid var(--border);border-radius:var(--radius-sm);background:var(--surface);transition:.15s;font-size:.92rem}
.control:focus-visible{border-color:var(--primary)}
.control:disabled,.control[readonly]{background:var(--surface-2);color:var(--text-muted);cursor:not-allowed}
textarea.control{height:auto;min-height:86px;padding:12px 14px;resize:vertical;line-height:1.5}
select.control{appearance:none;background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='14' height='14' viewBox='0 0 24 24' fill='none' stroke='%2355697c' stroke-width='2.5' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpolyline points='6 9 12 15 18 9'/%3E%3C/svg%3E");background-repeat:no-repeat;background-position:right 14px center;padding-right:40px}
[data-theme="dark"] select.control{background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='14' height='14' viewBox='0 0 24 24' fill='none' stroke='%23a2b7c8' stroke-width='2.5' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpolyline points='6 9 12 15 18 9'/%3E%3C/svg%3E")}
.field.has-error .control{border-color:var(--danger);background:var(--danger-soft)}
.error-msg{display:flex;align-items:center;gap:6px;font-size:.78rem;font-weight:600;color:var(--danger)}
.error-msg[hidden]{display:none}
.split{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:var(--space);align-items:start}
.split-wide{grid-template-columns:minmax(0,1.5fr) minmax(0,1fr)}
.media-frame{margin-top:20px;border:1px solid var(--border);border-radius:var(--radius);overflow:hidden;background:var(--surface-2)}
.media-frame img{width:100%;aspect-ratio:16/6;object-fit:cover;cursor:zoom-in;transition:transform .3s}
.media-frame img:hover{transform:scale(1.015)}
.media-frame figcaption{padding:10px 16px;font-size:.78rem;color:var(--text-muted);background:var(--surface);border-top:1px solid var(--border);font-weight:500}
.badge{display:inline-flex;align-items:center;gap:5px;padding:4px 11px;border-radius:999px;font-size:.72rem;font-weight:800;letter-spacing:.02em;white-space:nowrap}
.badge-success{background:var(--success-soft);color:var(--success)}
.badge-warning{background:var(--warning-soft);color:var(--warning)}
.badge-danger{background:var(--danger-soft);color:var(--danger)}
.badge-info{background:var(--primary-soft);color:var(--primary)}

/* ============================================================
   10. RIGHT RAIL
   ============================================================ */
.rail{position:sticky;top:calc(var(--topbar-h) + 10px);display:flex;flex-direction:column;gap:var(--space-sm)}
.rail-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius-lg);padding:20px;box-shadow:var(--shadow-sm)}
.rail-card h3{font-size:.74rem;font-weight:800;letter-spacing:.08em;text-transform:uppercase;color:var(--text-muted);margin-bottom:14px}
.snapshot{display:flex;align-items:center;gap:12px}
.snapshot img{width:52px;height:52px;border-radius:50%;object-fit:cover;border:2px solid var(--primary-soft)}
.snapshot .nm{font-weight:800;font-size:.95rem}
.snapshot .id{font-size:.76rem;color:var(--text-muted)}
.snapshot-list{margin-top:14px;display:flex;flex-direction:column;gap:0}
.snapshot-list li{display:flex;align-items:center;justify-content:space-between;gap:10px;padding:9px 0;border-bottom:1px dashed var(--border);font-size:.82rem}
.snapshot-list li:last-child{border-bottom:0;padding-bottom:0}
.snapshot-list .k{color:var(--text-muted);font-weight:500}
.snapshot-list .v{font-weight:700;text-align:right}
.spark{width:100%;height:auto;display:block;margin-top:4px}
.spark-legend{display:flex;justify-content:space-between;font-size:.72rem;color:var(--text-muted);margin-top:8px}
.spark-meta{display:flex;align-items:center;justify-content:space-between;gap:10px;margin-top:12px;font-size:.8rem}
.spark-meta .latest{font-weight:800;color:var(--primary);font-size:1rem}
.checklist{display:flex;flex-direction:column;gap:2px}
.checklist li{display:flex;align-items:center;gap:10px;padding:7px 0;font-size:.84rem}
.checklist .mk{width:20px;height:20px;border-radius:50%;flex:0 0 auto;display:grid;place-items:center;font-size:.68rem;font-weight:900;background:var(--primary-soft);color:var(--primary);border:1.5px solid var(--border-strong)}
.checklist li.done .mk{background:var(--success);color:#fff;border-color:var(--success)}
.checklist li.done .lbl{color:var(--text-muted);text-decoration:line-through;text-decoration-thickness:1.5px}
.checklist .lbl{flex:1 1 auto}

/* ============================================================
   11. SECTION BLOCKS
   ============================================================ */
.section-block{margin-top:40px}
.section-head{display:flex;align-items:flex-end;justify-content:space-between;gap:20px;flex-wrap:wrap;margin-bottom:20px;padding-bottom:14px;border-bottom:1px solid var(--border)}
.section-head h2{font-size:1.32rem;font-weight:800;color:var(--text);letter-spacing:-.02em;display:flex;align-items:center;gap:10px}
.section-head h2 .ico{font-size:1.15rem}
.section-head p{font-size:.86rem;color:var(--text-muted);margin-top:3px}
.card{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius-lg);padding:var(--space);box-shadow:var(--shadow-sm)}
.card h3{font-size:1rem;font-weight:800;color:var(--primary);margin-bottom:14px}
.timeline{position:relative;padding-left:28px;margin-top:6px}
.timeline::before{content:"";position:absolute;left:9px;top:6px;bottom:6px;width:2px;background:linear-gradient(180deg,var(--primary),var(--border));border-radius:2px}
.timeline li{position:relative;padding:0 0 22px 4px}
.timeline li:last-child{padding-bottom:0}
.timeline li::before{content:"";position:absolute;left:-28px;top:4px;width:14px;height:14px;border-radius:50%;background:var(--surface);border:3px solid var(--primary);box-shadow:0 0 0 3px var(--surface)}
.timeline .when{font-size:.74rem;font-weight:800;letter-spacing:.05em;text-transform:uppercase;color:var(--primary)}
.timeline .what{font-weight:700;font-size:.92rem;margin-top:1px}
.timeline .desc{font-size:.84rem;color:var(--text-muted);margin-top:3px}
.gallery{display:grid;grid-template-columns:repeat(auto-fit,minmax(190px,1fr));gap:var(--space-sm)}
.thumb{border:1px solid var(--border);border-radius:var(--radius);overflow:hidden;background:var(--surface-2);transition:.2s}
.thumb:hover{border-color:var(--primary);box-shadow:var(--shadow)}
.thumb img{width:100%;aspect-ratio:4/3;object-fit:cover;cursor:zoom-in;transition:transform .35s}
.thumb:hover img{transform:scale(1.04)}
.thumb figcaption{padding:9px 12px;font-size:.76rem;font-weight:600;background:var(--surface);border-top:1px solid var(--border)}
.thumb .tag{font-weight:800;color:var(--primary)}
.compare{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:var(--space-sm);margin-top:var(--space-sm)}
.compare figure{border:1px solid var(--border);border-radius:var(--radius);overflow:hidden;background:var(--surface-2)}
.compare img{width:100%;aspect-ratio:4/3;object-fit:cover;cursor:zoom-in}
.compare figcaption{display:flex;align-items:center;justify-content:space-between;gap:10px;padding:10px 14px;font-size:.78rem;font-weight:700;background:var(--surface);border-top:1px solid var(--border)}
.rx-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(290px,1fr));gap:var(--space)}
.rx-card h3{display:flex;align-items:center;justify-content:space-between;gap:10px}
.rx-lines{display:flex;flex-direction:column}
.rx-line{display:flex;align-items:center;justify-content:space-between;gap:16px;padding:10px 0;border-bottom:1px dashed var(--border);font-size:.88rem}
.rx-line:last-child{border-bottom:0;padding-bottom:0}
.rx-line .k{color:var(--text-muted);font-weight:600}
.rx-line .v{font-weight:800;font-variant-numeric:tabular-nums;text-align:right}
.rx-line .v.changed{color:var(--primary)}
.note{margin-top:16px;padding:13px 16px;border-radius:0 var(--radius-sm) var(--radius-sm) 0;background:var(--warning-soft);border-left:4px solid var(--warning);font-size:.82rem;color:var(--text);line-height:1.5}
.note strong{color:var(--text)}
.tips{padding-left:20px;list-style:disc;font-size:.86rem;line-height:1.9;color:var(--text)}
.tips li::marker{color:var(--primary)}
.finalize-actions{display:flex;flex-wrap:wrap;gap:12px;padding-top:20px;margin-top:4px;border-top:1px solid var(--border)}
.signature{display:flex;align-items:center;gap:10px;padding:10px 14px;border:1.5px dashed var(--border-strong);border-radius:var(--radius-sm);font-size:.82rem;color:var(--text-muted);background:var(--surface-2)}

/* ============================================================
   12. LIGHTBOX
   ============================================================ */
.lightbox{position:fixed;inset:0;z-index:200;display:grid;place-items:center;padding:24px;background:rgba(8,20,30,.82);backdrop-filter:blur(4px)}
.lightbox[hidden]{display:none}
.lightbox-inner{background:var(--surface);border-radius:var(--radius-lg);max-width:min(1000px,100%);width:100%;overflow:hidden;box-shadow:var(--shadow-lg);animation:pop .18s ease}
@keyframes pop{from{transform:scale(.97);opacity:0}to{transform:none;opacity:1}}
.lightbox-inner img{width:100%;max-height:74vh;object-fit:contain;background:#0b1620}
.lightbox-bar{display:flex;align-items:center;justify-content:space-between;gap:16px;padding:14px 18px;border-top:1px solid var(--border)}
.lightbox-bar p{font-size:.86rem;color:var(--text-muted);font-weight:500}

/* ============================================================
   13. TOASTS
   ============================================================ */
.toast-stack{position:fixed;right:24px;bottom:24px;z-index:300;display:flex;flex-direction:column;gap:10px;max-width:min(380px,calc(100vw - 48px))}
.toast{padding:14px 18px;border-radius:var(--radius);font-size:.87rem;font-weight:600;background:var(--surface);color:var(--text);border:1.5px solid var(--border);border-left-width:5px;box-shadow:var(--shadow-lg);transform:translateY(12px);opacity:0;transition:.25s ease}
.toast.show{transform:none;opacity:1}
.toast-success{border-left-color:var(--success)}
.toast-error{border-left-color:var(--danger)}
.toast-info{border-left-color:var(--primary)}

/* ============================================================
   14. FOOTER
   ============================================================ */
.footer{margin-top:56px;padding-block:26px;background:var(--surface);border-top:1px solid var(--border);font-size:.82rem;color:var(--text-muted)}
.footer-inner{display:grid;grid-template-columns:auto 1fr auto;align-items:center;gap:20px}
.footer a{font-weight:600;color:var(--text-muted);transition:.15s}
.footer a:hover{color:var(--primary)}
.footer-links{display:flex;flex-wrap:wrap;gap:20px}
.footer-copy{text-align:center}

/* ============================================================
   15. RESPONSIVE
   ============================================================ */
@media (max-width:1180px){
  .layout{grid-template-columns:minmax(0,1fr)}
  .rail{position:static;display:grid;grid-template-columns:repeat(2,minmax(0,1fr))}
}
@media (max-width:980px){
  .tabbar{grid-template-columns:repeat(3,minmax(0,1fr))}
  .quick-stats{grid-template-columns:repeat(2,minmax(0,1fr))}
  .qstat:nth-child(2){border-right:0}
  .qstat:nth-child(3),.qstat:nth-child(4){border-top:1px solid var(--border)}
  .patient-head{grid-template-columns:1fr}
  .cols-3{grid-template-columns:repeat(2,minmax(0,1fr))}
  .footer-inner{grid-template-columns:1fr;justify-items:center;text-align:center}
}
@media (max-width:720px){
  :root{--gutter:16px;--space:18px}
  .topbar-inner{grid-template-columns:auto 1fr;gap:12px}
  .search-field{display:none}
  .autosave span.text{display:none}
  .doctor-chip .who{display:none}
  .doctor-chip{padding:5px}
  .cols-2,.cols-3,.split,.split-wide,.compare{grid-template-columns:1fr}
  .rail{grid-template-columns:1fr}
  .tabbar{grid-template-columns:repeat(2,minmax(0,1fr))}
  .tab{min-height:70px}
  .kbd-hint{display:none}
  .quick-stats{grid-template-columns:1fr}
  .qstat{border-right:0;border-bottom:1px solid var(--border)}
  .qstat:last-child{border-bottom:0}
  .toast-stack{left:16px;right:16px;bottom:16px;max-width:none}
}
@media (prefers-reduced-motion:reduce){
  *,*::before,*::after{animation-duration:.001ms !important;transition-duration:.001ms !important}
  html{scroll-behavior:auto}
}

/* ============================================================
   16. PRINT
   ============================================================ */
@media print{
  .topbar,.tabbar-wrap,.rail,.patient-actions,.finalize-actions,.toast-stack,.lightbox,.skip-link,.footer-links{display:none !important}
  body{background:#fff;color:#000;font-size:12px}
  .patient-hero{background:#fff !important;color:#000;padding-block:0 16px}
  .patient-hero .chip{background:#eee;color:#000;border-color:#ccc}
  .quick-stats-wrap{margin-top:16px}
  .quick-stats{box-shadow:none;border:1px solid #ccc}
  .layout{grid-template-columns:1fr}
  .panel[hidden]{display:block !important}
  .panel,.card,.rail-card{box-shadow:none;border:1px solid #ccc;break-inside:avoid}
  .media-frame img,.thumb img,.compare img{aspect-ratio:auto;max-height:220px}
  .section-block{break-before:auto}
}
</style>
</head>
<body>

<a class="skip-link" href="#main">Skip to main content</a>

<header class="topbar" role="banner">
  <div class="container topbar-inner">
    <a href="#main" class="brand" aria-label="ClearSight Eye Care — Clinical Portal, back to top">
      <span class="brand-mark" aria-hidden="true">👁</span>
      <span>ClearSight <span class="brand-sub">| Clinical</span></span>
    </a>
    <div class="search-field">
      <span class="search-icon" aria-hidden="true">🔍</span>
      <label class="sr-only" for="patientSearch">Search patient by name or ID</label>
      <input id="patientSearch" type="search" placeholder="Search patient by name or ID…" autocomplete="off" aria-describedby="patientSearchHint">
      <span id="patientSearchHint" class="sr-only">Type a name or patient ID to find a record.</span>
    </div>
    <div class="topbar-actions">
      <p id="saveStatus" class="autosave" aria-live="polite" aria-atomic="true">
        <span class="dot" aria-hidden="true"></span>
        <span class="text">All changes saved</span>
      </p>
      <button id="themeToggle" class="icon-btn" type="button" aria-pressed="false" aria-label="Switch to dark mode">
        <span class="theme-icon" aria-hidden="true">🌙</span>
      </button>
      <div class="doctor-chip">
        <img src="https://placehold.co/80x80/e6f2f8/0b5e8a?text=SM" alt="">
        <span class="who"><strong>Dr. S. Mitchell</strong><span>Optometrist</span></span>
      </div>
    </div>
  </div>
</header>

<section class="patient-hero" aria-labelledby="patientName">
  <div class="container">
    <nav class="breadcrumbs" aria-label="Breadcrumb">
      <a href="#main">Clinic</a><span class="sep" aria-hidden="true">/</span>
      <a href="#main">Today’s schedule</a><span class="sep" aria-hidden="true">/</span>
      <span aria-current="page">Emily Carter</span>
    </nav>
    <div class="patient-head">
      <div class="patient-identity">
        <img class="patient-avatar" src="https://placehold.co/160x160/e6f2f8/0b5e8a?text=EC" alt="Portrait of Emily Carter">
        <div>
          <h1 id="patientName">Emily Carter</h1>
          <p class="meta">
            <span>Female · 34 years</span>
            <span>DOB 12 Mar 1992</span>
            <span>Patient ID #EC-2026-0891</span>
          </p>
        </div>
      </div>
      <div class="patient-actions">
        <span class="chip">📅 <strong>23 Nov 2026</strong></span>
        <span class="chip">🕒 <strong>10:30 AM</strong></span>
        <button class="btn btn-ghost btn-sm" type="button" id="switchPatientBtn">🔄 Switch patient</button>
      </div>
    </div>
  </div>
</section>

<div class="container quick-stats-wrap">
  <div class="quick-stats" role="group" aria-label="Patient vitals and key information">
    <div class="qstat"><span class="k">Blood pressure</span><span class="v">120/80 <small>mmHg</small></span></div>
    <div class="qstat"><span class="k">Blood sugar</span><span class="v">98 <small>mg/dL</small></span></div>
    <div class="qstat"><span class="k">Allergies</span><span class="v is-danger">None known</span></div>
    <div class="qstat"><span class="k">Last visit</span><span class="v">May 2026</span></div>
  </div>
</div>

<main id="main" class="container page-main" tabindex="-1">
  <div class="layout">
    <div class="main-col">
      <div class="tabbar-wrap">
        <div class="tabbar" role="tablist" aria-label="Eye examination sections">
          <button class="tab" id="tab-acuity" role="tab" aria-selected="true" aria-controls="panel-acuity" tabindex="0" data-target="acuity" aria-keyshortcuts="Alt+1">
            <span class="tab-ico" aria-hidden="true">👁</span><span class="tab-label">Acuity</span><span class="tab-dot" aria-hidden="true"></span>
          </button>
          <button class="tab" id="tab-refraction" role="tab" aria-selected="false" aria-controls="panel-refraction" tabindex="-1" data-target="refraction" aria-keyshortcuts="Alt+2">
            <span class="tab-ico" aria-hidden="true">🔬</span><span class="tab-label">Refraction</span><span class="tab-dot" aria-hidden="true"></span>
          </button>
          <button class="tab" id="tab-pressure" role="tab" aria-selected="false" aria-controls="panel-pressure" tabindex="-1" data-target="pressure" aria-keyshortcuts="Alt+3">
            <span class="tab-ico" aria-hidden="true">📊</span><span class="tab-label">Pressure</span><span class="tab-dot" aria-hidden="true"></span>
          </button>
          <button class="tab" id="tab-slitlamp" role="tab" aria-selected="false" aria-controls="panel-slitlamp" tabindex="-1" data-target="slitlamp" aria-keyshortcuts="Alt+4">
            <span class="tab-ico" aria-hidden="true">🔎</span><span class="tab-label">Slit lamp</span><span class="tab-dot" aria-hidden="true"></span>
          </button>
          <button class="tab" id="tab-fundus" role="tab" aria-selected="false" aria-controls="panel-fundus" tabindex="-1" data-target="fundus" aria-keyshortcuts="Alt+5">
            <span class="tab-ico" aria-hidden="true">🖼️</span><span class="tab-label">Fundus</span><span class="tab-dot" aria-hidden="true"></span>
          </button>
          <button class="tab" id="tab-diagnosis" role="tab" aria-selected="false" aria-controls="panel-diagnosis" tabindex="-1" data-target="diagnosis" aria-keyshortcuts="Alt+6">
            <span class="tab-ico" aria-hidden="true">📝</span><span class="tab-label">Diagnosis</span><span class="tab-dot" aria-hidden="true"></span>
          </button>
        </div>
        <div class="tabbar-meta">
          <div class="progress" aria-hidden="true">
            <span>Exam progress</span>
            <span class="progress-track"><span class="progress-fill" id="progressFill"></span></span>
            <strong id="progressText">1 of 6</strong>
          </div>
          <span class="kbd-hint">Tip: <kbd>Alt</kbd> + <kbd>1</kbd>–<kbd>6</kbd></span>
        </div>
      </div>

      <section class="panel" id="panel-acuity" role="tabpanel" aria-labelledby="tab-acuity" tabindex="0">
        <div class="panel-head">
          <div><h3>Visual Acuity</h3><p>Snellen chart assessment · 20 ft distance</p></div>
          <span class="badge badge-success">Reviewed</span>
        </div>
        <div class="field-grid cols-2">
          <div class="field">
            <label for="va-od-uc">Right eye (OD) — uncorrected</label>
            <select class="control" id="va-od-uc"><option>20/20</option><option>20/25</option><option>20/30</option><option>20/40</option><option>20/50</option><option>20/70</option><option>20/100</option><option>20/200</option><option>20/400</option></select>
          </div>
          <div class="field">
            <label for="va-os-uc">Left eye (OS) — uncorrected</label>
            <select class="control" id="va-os-uc"><option>20/20</option><option>20/25</option><option>20/30</option><option>20/40</option><option>20/50</option><option>20/70</option><option>20/100</option><option>20/200</option><option>20/400</option></select>
          </div>
          <div class="field">
            <label for="va-od-c">Right eye (OD) — corrected</label>
            <select class="control" id="va-od-c"><option>20/20</option><option>20/25</option><option>20/30</option><option>20/40</option></select>
          </div>
          <div class="field">
            <label for="va-os-c">Left eye (OS) — corrected</label>
            <select class="control" id="va-os-c"><option>20/20</option><option>20/25</option><option>20/30</option><option>20/40</option></select>
          </div>
        </div>
        <figure class="media-frame">
          <img class="zoomable" src="https://placehold.co/1200x420/e6f2f8/0b5e8a?text=Snellen+Chart+%7C+20%2F20+Reference" data-caption="Standard Snellen acuity chart used at 20 feet" alt="Standard Snellen eye chart showing rows of letters decreasing in size from 20/200 down to 20/20.">
          <figcaption>Standard Snellen chart · click image to enlarge</figcaption>
        </figure>
      </section>

      <section class="panel" id="panel-refraction" role="tabpanel" aria-labelledby="tab-refraction" tabindex="0" hidden>
        <div class="panel-head">
          <div><h3>Refraction</h3><p>Auto-refraction and subjective refinement</p></div>
          <span class="badge badge-info">Updates prescription</span>
        </div>
        <div class="field-grid">
          <div class="field">
            <label for="rx-od-s">Right eye (OD) — sphere / cylinder / axis</label>
            <div class="field-grid cols-3">
              <input class="control rx-input" id="rx-od-s" type="text" inputmode="decimal" value="-2.50" aria-label="Right eye sphere value">
              <input class="control rx-input" id="rx-od-c" type="text" inputmode="decimal" value="-0.50" aria-label="Right eye cylinder value">
              <input class="control rx-input" id="rx-od-a" type="text" inputmode="numeric" value="180" aria-label="Right eye axis value">
            </div>
            <span class="hint">Sphere, cylinder, axis — e.g. −2.50 / −0.50 × 180</span>
          </div>
          <div class="field">
            <label for="rx-os-s">Left eye (OS) — sphere / cylinder / axis</label>
            <div class="field-grid cols-3">
              <input class="control rx-input" id="rx-os-s" type="text" inputmode="decimal" value="-2.25" aria-label="Left eye sphere value">
              <input class="control rx-input" id="rx-os-c" type="text" inputmode="decimal" value="-0.25" aria-label="Left eye cylinder value">
              <input class="control rx-input" id="rx-os-a" type="text" inputmode="numeric" value="175" aria-label="Left eye axis value">
            </div>
            <span class="hint">Sphere, cylinder, axis — e.g. −2.25 / −0.25 × 175</span>
          </div>
          <div class="field-grid cols-2">
            <div class="field">
              <label for="rx-add">Near addition (add)</label>
              <input class="control" id="rx-add" type="text" inputmode="decimal" placeholder="e.g. +1.50">
            </div>
            <div class="field">
              <label for="rx-pd">Pupillary distance (PD)</label>
              <input class="control" id="rx-pd" type="text" inputmode="numeric" value="64" aria-describedby="pdHint">
              <span class="hint" id="pdHint">Millimetres, binocular</span>
            </div>
          </div>
          <div class="field">
            <label for="rx-notes">Refraction notes</label>
            <textarea class="control" id="rx-notes" rows="2" placeholder="Patient tolerance, vertex distance, etc."></textarea>
          </div>
        </div>
        <figure class="media-frame">
          <img class="zoomable" src="https://placehold.co/1200x360/e6f2f8/0b5e8a?text=Phoropter+%7C+Subjective+Refraction" data-caption="Phoropter used for subjective refraction" alt="A phoropter, the instrument with adjustable lenses used to refine a patient's spectacle prescription.">
          <figcaption>Phoropter · subjective refraction instrument</figcaption>
        </figure>
      </section>

      <section class="panel" id="panel-pressure" role="tabpanel" aria-labelledby="tab-pressure" tabindex="0" hidden>
        <div class="panel-head">
          <div><h3>Eye Pressure (Tonometry)</h3><p>Intraocular pressure (IOP) measurement</p></div>
          <span class="badge badge-warning">Monitor</span>
        </div>
        <div class="field-grid cols-3">
          <div class="field">
            <label for="iop-od">Right eye (OD) — IOP</label>
            <input class="control" id="iop-od" type="text" inputmode="decimal" value="16" aria-describedby="iopUnit">
            <span class="hint" id="iopUnit">mmHg · normal 10–21</span>
          </div>
          <div class="field">
            <label for="iop-os">Left eye (OS) — IOP</label>
            <input class="control" id="iop-os" type="text" inputmode="decimal" value="15" aria-describedby="iopUnit2">
            <span class="hint" id="iopUnit2">mmHg · normal 10–21</span>
          </div>
          <div class="field">
            <label for="iop-method">Method</label>
            <select class="control" id="iop-method"><option>Goldmann applanation</option><option>Non-contact (air puff)</option><option>Tonopen</option></select>
          </div>
        </div>
        <figure class="media-frame">
          <img class="zoomable" src="https://placehold.co/1200x360/e6f2f8/0b5e8a?text=Non-Contact+Tonometer+%7C+Eye+Pressure" data-caption="Non-contact tonometer for IOP measurement" alt="A non-contact tonometer, used to measure intraocular pressure with a brief puff of air.">
          <figcaption>Non-contact tonometer · IOP measurement</figcaption>
        </figure>
      </section>

      <section class="panel" id="panel-slitlamp" role="tabpanel" aria-labelledby="tab-slitlamp" tabindex="0" hidden>
        <div class="panel-head">
          <div><h3>Slit Lamp Examination</h3><p>Anterior segment and adnexa</p></div>
          <span class="badge badge-warning">Pending</span>
        </div>
        <div class="field-grid cols-2">
          <div class="field">
            <label for="sl-lids">Lids &amp; lashes</label>
            <select class="control" id="sl-lids"><option>Normal</option><option>Mild blepharitis</option><option>Chalazion</option><option>Hordeolum</option></select>
          </div>
          <div class="field">
            <label for="sl-conj">Conjunctiva / sclera</label>
            <select class="control" id="sl-conj"><option>Clear</option><option>Injection</option><option>Pinguecula</option><option>Pterygium</option></select>
          </div>
          <div class="field">
            <label for="sl-cornea">Cornea</label>
            <select class="control" id="sl-cornea"><option>Clear</option><option>Edema</option><option>Opacity</option><option>Keratoconus</option></select>
          </div>
          <div class="field">
            <label for="sl-ac">Anterior chamber</label>
            <select class="control" id="sl-ac"><option>Quiet</option><option>Cells / flare</option><option>Hyphema</option></select>
          </div>
          <div class="field" style="grid-column:1/-1">
            <label for="sl-notes">Additional findings</label>
            <textarea class="control" id="sl-notes" rows="2" placeholder="e.g. arcus senilis, corneal scarring…"></textarea>
          </div>
        </div>
        <figure class="media-frame">
          <img class="zoomable" src="https://placehold.co/1200x420/e6f2f8/0b5e8a?text=Slit+Lamp+Biomicroscope" data-caption="Slit lamp biomicroscope for anterior segment examination" alt="A slit lamp biomicroscope, the table-mounted instrument used to examine the front of the eye under magnification.">
          <figcaption>Slit lamp biomicroscope</figcaption>
        </figure>
      </section>

      <section class="panel" id="panel-fundus" role="tabpanel" aria-labelledby="tab-fundus" tabindex="0" hidden>
        <div class="panel-head">
          <div><h3>Fundus Examination</h3><p>Dilated retinal examination</p></div>
          <span class="badge badge-warning">Pending</span>
        </div>
        <div class="field-grid cols-2">
          <div class="field">
            <label for="fu-disc">Optic disc</label>
            <select class="control" id="fu-disc"><option>Normal</option><option>Cupping (raised C/D ratio)</option><option>Pallor</option><option>Edema</option></select>
          </div>
          <div class="field">
            <label for="fu-macula">Macula</label>
            <select class="control" id="fu-macula"><option>Normal</option><option>Drusen</option><option>Hemorrhage</option><option>Exudate</option></select>
          </div>
          <div class="field">
            <label for="fu-vessels">Vessels</label>
            <select class="control" id="fu-vessels"><option>Normal</option><option>AV nicking</option><option>Hemorrhage</option></select>
          </div>
          <div class="field">
            <label for="fu-periphery">Periphery</label>
            <select class="control" id="fu-periphery"><option>Normal</option><option>Lattice degeneration</option><option>Retinal tear</option></select>
          </div>
        </div>
        <figure class="media-frame">
          <img class="zoomable" src="https://placehold.co/1200x480/e6f2f8/0b5e8a?text=Fundus+Photograph+%7C+Normal+Retina" data-caption="Normal fundus reference photograph" alt="Reference fundus photograph of a healthy retina showing the optic disc, macula and retinal vessels.">
          <figcaption>Normal fundus reference</figcaption>
        </figure>
      </section>

      <section class="panel" id="panel-diagnosis" role="tabpanel" aria-labelledby="tab-diagnosis" tabindex="0" hidden>
        <div class="panel-head">
          <div><h3>Diagnosis &amp; Plan</h3><p>Assessment and treatment recommendations</p></div>
          <span class="badge badge-info">Required</span>
        </div>
        <div class="field-grid">
          <div class="field" id="dxField">
            <label for="dx-input">Diagnosis <span aria-hidden="true" style="color:var(--danger)">*</span></label>
            <input class="control" id="dx-input" type="text" required aria-required="true" aria-describedby="dxError" value="Myopia (moderate), mild dry eye">
            <p class="error-msg" id="dxError" hidden><span aria-hidden="true">⚠</span> Please enter a diagnosis before saving the exam.</p>
          </div>
          <div class="field">
            <label for="dx-plan">Treatment plan</label>
            <textarea class="control" id="dx-plan" rows="3">Prescribe single-vision glasses with blue-light filter. Artificial tears as needed for dry eye. Follow-up in 6 months.</textarea>
          </div>
          <div class="field">
            <label for="dx-followup">Follow-up interval</label>
            <select class="control" id="dx-followup"><option>3 months</option><option selected>6 months</option><option>12 months</option><option>As needed</option></select>
          </div>
        </div>
      </section>
    </div>

    <aside class="rail" aria-label="Patient context and quick actions">
      <section class="rail-card" aria-labelledby="snapTitle">
        <h3 id="snapTitle">Patient snapshot</h3>
        <div class="snapshot">
          <img src="https://placehold.co/100x100/e6f2f8/0b5e8a?text=EC" alt="">
          <div><div class="nm">Emily Carter</div><div class="id">#EC-2026-0891 · 34 y</div></div>
        </div>
        <ul class="snapshot-list">
          <li><span class="k">Last refraction</span><span class="v">−2.50 / −2.25</span></li>
          <li><span class="k">Dry eye</span><span class="v">Mild, managed</span></li>
          <li><span class="k">Family history</span><span class="v">Glaucoma (maternal)</span></li>
          <li><span class="k">Smoking</span><span class="v">Non-smoker</span></li>
        </ul>
      </section>

      <section class="rail-card" aria-labelledby="iopTrendTitle">
        <h3 id="iopTrendTitle">IOP trend · last 5 visits</h3>
        <svg class="spark" viewBox="0 0 240 80" role="img" aria-labelledby="iopTitle iopDesc" preserveAspectRatio="xMidYMid meet">
          <title id="iopTitle">Intraocular pressure trend</title>
          <desc id="iopDesc">Right eye IOP readings across the last five visits: 16, 15, 17, 16 and 15 millimetres of mercury. All within the normal range.</desc>
          <line x1="14" y1="58" x2="226" y2="58" stroke="var(--border)" stroke-width="1" stroke-dasharray="4 4"/>
          <line x1="14" y1="38" x2="226" y2="38" stroke="var(--border)" stroke-width="1" stroke-dasharray="2 5" opacity=".6"/>
          <polyline points="26,32 76,36 126,24 176,32 216,36" fill="none" stroke="var(--primary)" stroke-width="2.6" stroke-linecap="round" stroke-linejoin="round"/>
          <g fill="var(--surface)" stroke="var(--primary)" stroke-width="2.4">
            <circle cx="26" cy="32" r="4"/><circle cx="76" cy="36" r="4"/><circle cx="126" cy="24" r="4"/><circle cx="176" cy="32" r="4"/><circle cx="216" cy="36" r="4.6" fill="var(--primary)"/>
          </g>
        </svg>
        <div class="spark-legend"><span>May 25</span><span>Nov 25</span><span>Feb 26</span><span>May 26</span><span>Nov 26</span></div>
        <div class="spark-meta">
          <span class="latest">15 mmHg <span style="font-weight:600;color:var(--text-muted);font-size:.78rem">OD</span></span>
          <span class="badge badge-success">Within target ≤ 21</span>
        </div>
      </section>

      <section class="rail-card" aria-labelledby="progressTitle">
        <h3 id="progressTitle">Exam checklist</h3>
        <ul class="checklist" id="checklist" aria-live="polite">
          <li data-step="acuity"><span class="mk" aria-hidden="true">✓</span><span class="lbl">Visual acuity</span></li>
          <li data-step="refraction"><span class="mk" aria-hidden="true">✓</span><span class="lbl">Refraction</span></li>
          <li data-step="pressure"><span class="mk" aria-hidden="true">✓</span><span class="lbl">Eye pressure</span></li>
          <li data-step="slitlamp"><span class="mk" aria-hidden="true">✓</span><span class="lbl">Slit lamp</span></li>
          <li data-step="fundus"><span class="mk" aria-hidden="true">✓</span><span class="lbl">Fundus</span></li>
          <li data-step="diagnosis"><span class="mk" aria-hidden="true">✓</span><span class="lbl">Diagnosis &amp; plan</span></li>
        </ul>
      </section>

      <section class="rail-card" aria-labelledby="actionsTitle">
        <h3 id="actionsTitle">Quick actions</h3>
        <div class="stack" style="gap:10px">
          <button class="btn btn-primary" type="button" id="quickSave">💾 Save exam</button>
          <button class="btn btn-secondary" type="button" id="quickPrint">🖨️ Print summary</button>
          <button class="btn btn-secondary" type="button" id="quickEmail">📧 Email patient</button>
        </div>
      </section>
    </aside>
  </div>

  <section class="section-block" id="history" aria-labelledby="historyTitle">
    <div class="section-head">
      <div><h2 id="historyTitle"><span class="ico" aria-hidden="true">📋</span> Patient history</h2><p>Past visits, medical background and clinical notes</p></div>
      <button class="btn btn-secondary btn-sm" type="button" id="exportHistory">⬇ Export history</button>
    </div>
    <div class="split split-wide">
      <article class="card">
        <h3>Visit timeline</h3>
        <ol class="timeline">
          <li><div class="when">23 Nov 2026 · Today</div><div class="what">Comprehensive eye exam — in progress</div><div class="desc">Routine review; occasional headaches after long screen use.</div></li>
          <li><div class="when">14 May 2026</div><div class="what">Routine exam — stable</div><div class="desc">IOP 16 / 15 mmHg. Prescription unchanged. Advised lubricating drops.</div></li>
          <li><div class="when">18 Nov 2025</div><div class="what">Routine exam — mild dry eye noted</div><div class="desc">Started artificial tears as needed. No retinal changes.</div></li>
          <li><div class="when">02 Jun 2024</div><div class="what">Contact lens fitting</div><div class="desc">Fit confirmed, teaching completed. Good compliance.</div></li>
        </ol>
      </article>
      <div class="stack">
        <article class="card">
          <h3>Key metrics</h3>
          <div class="quick-stats" style="grid-template-columns:repeat(3,1fr);box-shadow:none;border:0;border-radius:0">
            <div class="qstat" style="padding:12px 8px"><span class="k">Visits</span><span class="v">8</span></div>
            <div class="qstat" style="padding:12px 8px"><span class="k">Years</span><span class="v">6</span></div>
            <div class="qstat" style="padding:12px 8px;border-right:0"><span class="k">Compliance</span><span class="v">100%</span></div>
          </div>
          <div class="note" style="margin-top:16px"><strong>Previous note:</strong> “Patient advised to use lubricating drops during extended screen time. Re-check in 12 months or sooner if symptoms worsen.”</div>
        </article>
        <article class="card">
          <h3>Medical background</h3>
          <p style="font-size:.86rem;color:var(--text-muted)">Family history of glaucoma (maternal grandmother). No history of ocular surgery or trauma. Recommend monitoring IOP at each visit.</p>
        </article>
      </div>
    </div>
  </section>

  <section class="section-block" id="imaging" aria-labelledby="imagingTitle">
    <div class="section-head">
      <div><h2 id="imagingTitle"><span class="ico" aria-hidden="true">🖼️</span> Diagnostic imaging</h2><p>Captured today · click any image to enlarge</p></div>
      <span class="badge badge-info">4 captures</span>
    </div>
    <div class="card">
      <h3>Today's captures</h3>
      <div class="gallery">
        <figure class="thumb"><img class="zoomable" src="https://placehold.co/600x450/e6f2f8/0b5e8a?text=Fundus+OD" data-caption="Fundus photograph — right eye (OD), 23 Nov 2026" alt="Fundus photograph of the right eye showing the optic disc, macula and retinal vessels."><figcaption><span class="tag">OD</span> · Fundus</figcaption></figure>
        <figure class="thumb"><img class="zoomable" src="https://placehold.co/600x450/e6f2f8/0b5e8a?text=Fundus+OS" data-caption="Fundus photograph — left eye (OS), 23 Nov 2026" alt="Fundus photograph of the left eye showing the optic disc, macula and retinal vessels."><figcaption><span class="tag">OS</span> · Fundus</figcaption></figure>
        <figure class="thumb"><img class="zoomable" src="https://placehold.co/600x450/e6f2f8/0b5e8a?text=Slit+Lamp+Cornea" data-caption="Slit lamp image — cornea, 23 Nov 2026" alt="Slit lamp image of the cornea showing a clear, healthy anterior surface."><figcaption><span class="tag">OD</span> · Cornea</figcaption></figure>
        <figure class="thumb"><img class="zoomable" src="https://placehold.co/600x450/e6f2f8/0b5e8a?text=Corneal+Topography" data-caption="Corneal topography map, 23 Nov 2026" alt="Corneal topography map showing a regular astigmatic pattern."><figcaption>Corneal topography</figcaption></figure>
      </div>
      <h3 style="margin-top:28px">Baseline comparison</h3>
      <div class="compare">
        <figure>
          <img class="zoomable" src="https://placehold.co/800x600/e6f2f8/0b5e8a?text=Baseline+%7C+May+2026" data-caption="Baseline fundus photograph — May 2026" alt="Baseline fundus photograph from May 2026 used for comparison.">
          <figcaption><span>Baseline · May 2026</span><span class="badge badge-info">Reference</span></figcaption>
        </figure>
        <figure>
          <img class="zoomable" src="https://placehold.co/800x600/e6f2f8/0b5e8a?text=Current+%7C+Nov+2026" data-caption="Current fundus photograph — November 2026" alt="Current fundus photograph from November 2026 used for comparison.">
          <figcaption><span>Current · Nov 2026</span><span class="badge badge-success">Stable</span></figcaption>
        </figure>
      </div>
    </div>
  </section>

  <section class="section-block" id="prescription" aria-labelledby="rxTitle">
    <div class="section-head">
      <div><h2 id="rxTitle"><span class="ico" aria-hidden="true">📝</span> Prescription &amp; recommendations</h2><p>Updates automatically as you refine refraction</p></div>
      <span class="badge badge-success" id="rxStatusBadge">Ready</span>
    </div>
    <div class="rx-grid">
      <article class="card rx-card">
        <h3>Glasses prescription <span class="badge badge-success">Final</span></h3>
        <div class="rx-lines">
          <div class="rx-line"><span class="k">Right eye (OD)</span><span class="v" id="out-od">−2.50 / −0.50 × 180</span></div>
          <div class="rx-line"><span class="k">Left eye (OS)</span><span class="v" id="out-os">−2.25 / −0.25 × 175</span></div>
          <div class="rx-line"><span class="k">Near addition</span><span class="v" id="out-add">—</span></div>
          <div class="rx-line"><span class="k">Pupillary distance</span><span class="v" id="out-pd">64 mm</span></div>
          <div class="rx-line"><span class="k">Lens type</span><span class="v">Single vision · blue-light filter</span></div>
        </div>
        <div class="note"><strong>Recommendation:</strong> Prescribe computer glasses with a blue-light filter for screen use. Artificial tears as needed for dry eye.</div>
      </article>
      <article class="card">
        <h3>Patient education</h3>
        <ul class="tips">
          <li>Follow the 20-20-20 rule: every 20 minutes, look 20 feet away for 20 seconds.</li>
          <li>Use lubricating eye drops before prolonged screen time.</li>
          <li>Schedule a follow-up in 6 months, or sooner if vision changes.</li>
        </ul>
      </article>
      <article class="card">
        <h3>Next appointment</h3>
        <div class="rx-lines">
          <div class="rx-line"><span class="k">Suggested follow-up</span><span class="v">23 May 2027</span></div>
          <div class="rx-line"><span class="k">Interval</span><span class="v">6 months</span></div>
        </div>
        <div class="stack" style="gap:10px;margin-top:18px">
          <button class="btn btn-primary" type="button" id="scheduleBtn">📅 Schedule appointment</button>
          <button class="btn btn-secondary" type="button" id="reminderBtn">🔔 Send reminder</button>
        </div>
      </article>
    </div>
  </section>

  <section class="section-block" id="finalize" aria-labelledby="finalizeTitle">
    <div class="section-head">
      <div><h2 id="finalizeTitle"><span class="ico" aria-hidden="true">✅</span> Finalize examination</h2><p>Review the summary and save it to the patient’s chart</p></div>
    </div>
    <div class="card">
      <div class="field-grid cols-2">
        <div class="field"><label for="fin-doctor">Doctor</label><input class="control" id="fin-doctor" type="text" value="Dr. Sarah Mitchell" readonly></div>
        <div class="field"><label for="fin-date">Date</label><input class="control" id="fin-date" type="text" value="23 Nov 2026" readonly></div>
        <div class="field"><label for="fin-patient">Patient</label><input class="control" id="fin-patient" type="text" value="Emily Carter" readonly></div>
        <div class="field"><label for="fin-id">Patient ID</label><input class="control" id="fin-id" type="text" value="#EC-2026-0891" readonly></div>
      </div>
      <div class="field-grid" style="margin-top:16px">
        <div class="field">
          <label for="fin-notes">Additional notes or instructions</label>
          <textarea class="control" id="fin-notes" rows="3" placeholder="Anything else the patient or next clinician should know…"></textarea>
        </div>
      </div>
      <div class="signature" style="margin-top:16px"><span aria-hidden="true">🖊</span><span>Electronically signed by Dr. Sarah Mitchell · 23 Nov 2026, 10:30</span></div>
      <div class="finalize-actions">
        <button class="btn btn-primary" type="button" id="saveExam">💾 Save exam record</button>
        <button class="btn btn-secondary" type="button" id="printBtn">🖨️ Print summary</button>
        <button class="btn btn-secondary" type="button" id="emailBtn">📧 Email to patient</button>
      </div>
    </div>
  </section>
</main>

<footer class="footer" role="contentinfo">
  <div class="container footer-inner">
    <ul class="footer-links">
      <li><a href="#main">Privacy policy</a></li>
      <li><a href="#main">Terms of service</a></li>
      <li><a href="#main">IT support</a></li>
    </ul>
    <p class="footer-copy">© 2026 ClearSight Eye Care — Clinical Portal v2.4</p>
    <p class="footer-copy">Design: <a href="https://www.tooplate.com" target="_blank" rel="noopener">Tooplate</a></p>
  </div>
</footer>

<div class="lightbox" id="lightbox" role="dialog" aria-modal="true" aria-labelledby="lightboxCaption" hidden tabindex="-1">
  <div class="lightbox-inner">
    <img id="lightboxImg" src="" alt="">
    <div class="lightbox-bar">
      <p id="lightboxCaption">Image</p>
      <button class="btn btn-secondary btn-sm" type="button" id="lightboxClose">Close (Esc)</button>
    </div>
  </div>
</div>

<div class="toast-stack" id="toastStack" aria-live="polite" aria-atomic="false"></div>

<script>
(function(){
'use strict';

/* 1. THEME */
var root=document.documentElement;
var themeBtn=document.getElementById('themeToggle');
var themeIcon=themeBtn.querySelector('.theme-icon');
function applyTheme(t){root.setAttribute('data-theme',t);var d=t==='dark';themeBtn.setAttribute('aria-pressed',String(d));themeBtn.setAttribute('aria-label',d?'Switch to light mode':'Switch to dark mode');themeIcon.textContent=d?'☀️':'🌙'}
var stored=localStorage.getItem('cs-theme');
if(stored==='dark'||stored==='light'){applyTheme(stored)}
else if(window.matchMedia&&window.matchMedia('(prefers-color-scheme: dark)').matches){applyTheme('dark')}
else{applyTheme('light')}
themeBtn.addEventListener('click',function(){var n=root.getAttribute('data-theme')==='dark'?'light':'dark';applyTheme(n);localStorage.setItem('cs-theme',n);toast('Switched to '+n+' mode','info')});

/* 2. TOASTS */
var toastStack=document.getElementById('toastStack');
function toast(msg,type){var el=document.createElement('div');el.className='toast toast-'+(type||'success');el.setAttribute('role','status');el.textContent=msg;toastStack.appendChild(el);requestAnimationFrame(function(){el.classList.add('show')});setTimeout(function(){el.classList.remove('show');setTimeout(function(){el.remove()},300)},4000)}

/* 3. TABS */
var tablist=document.querySelector('[role="tablist"]');
var tabs=Array.prototype.slice.call(tablist.querySelectorAll('[role="tab"]'));
var panels=Array.prototype.slice.call(document.querySelectorAll('[role="tabpanel"]'));
var progressFill=document.getElementById('progressFill');
var progressText=document.getElementById('progressText');
var checklist=document.getElementById('checklist');
var visited=new Set();
function activateTab(tab){var target=tab.dataset.target;tabs.forEach(function(t){var a=t===tab;t.setAttribute('aria-selected',String(a));t.tabIndex=a?0:-1});panels.forEach(function(p){if(p.id==='panel-'+target){p.removeAttribute('hidden')}else{p.setAttribute('hidden','')}});visited.add(target);updateProgress()}
function updateProgress(){var total=tabs.length,done=visited.size,pct=Math.round((done/total)*100);progressFill.style.width=pct+'%';progressText.textContent=done+' of '+total;tabs.forEach(function(t){t.classList.toggle('is-visited',visited.has(t.dataset.target))});if(checklist){Array.prototype.forEach.call(checklist.children,function(li){li.classList.toggle('done',visited.has(li.dataset.step))})}if(done===total){document.getElementById('rxStatusBadge').textContent='All reviewed'}}
tabs.forEach(function(t){t.addEventListener('click',function(){activateTab(t)})});
tablist.addEventListener('keydown',function(e){var idx=tabs.indexOf(document.activeElement);if(idx===-1)return;var next=null;if(e.key==='ArrowRight'||e.key==='ArrowDown'){next=(idx+1)%tabs.length}else if(e.key==='ArrowLeft'||e.key==='ArrowUp'){next=(idx-1+tabs.length)%tabs.length}else if(e.key==='Home'){next=0}else if(e.key==='End'){next=tabs.length-1}else{return}e.preventDefault();tabs[next].focus();activateTab(tabs[next])});
activateTab(tabs[0]);
document.addEventListener('keydown',function(e){if(!e.altKey||e.ctrlKey||e.metaKey)return;var n=parseInt(e.key,10);if(n>=1&&n<=tabs.length){e.preventDefault();activateTab(tabs[n-1]);tabs[n-1].focus();tabs[n-1].scrollIntoView({block:'nearest',behavior:'smooth'})}});

/* 4. AUTOSAVE INDICATOR */
var saveStatus=document.getElementById('saveStatus');
var saveText=saveStatus.querySelector('.text');
var saveTimer;
function markSaving(){clearTimeout(saveTimer);saveStatus.classList.add('is-saving');saveText.textContent='Saving…';saveTimer=setTimeout(function(){saveStatus.classList.remove('is-saving');var now=new Date();var hh=String(now.getHours()).padStart(2,'0');var mm=String(now.getMinutes()).padStart(2,'0');saveText.textContent='Saved · '+hh+':'+mm},800)}
document.getElementById('main').addEventListener('input',markSaving);
document.getElementById('main').addEventListener('change',markSaving);

/* 5. LIVE PRESCRIPTION */
function fmtRx(s,c,a){s=(s||'').trim();c=(c||'').trim();a=(a||'').trim();if(!s)return'—';if(!c||parseFloat(c)===0)return s+' DS';return s+' / '+c+' × '+(a||'—')}
function updateRx(){var od=fmtRx(document.getElementById('rx-od-s').value,document.getElementById('rx-od-c').value,document.getElementById('rx-od-a').value);var os=fmtRx(document.getElementById('rx-os-s').value,document.getElementById('rx-os-c').value,document.getElementById('rx-os-a').value);var add=document.getElementById('rx-add').value.trim()||'—';var pd=document.getElementById('rx-pd').value.trim()||'—';document.getElementById('out-od').textContent=od;document.getElementById('out-os').textContent=os;document.getElementById('out-add').textContent=add;document.getElementById('out-pd').textContent=pd?pd+' mm':'—'}
['rx-od-s','rx-od-c','rx-od-a','rx-os-s','rx-os-c','rx-os-a','rx-add','rx-pd'].forEach(function(id){var el=document.getElementById(id);if(el)el.addEventListener('input',updateRx)});
updateRx();

/* 6. LIGHTBOX */
var lightbox=document.getElementById('lightbox');
var lightboxImg=document.getElementById('lightboxImg');
var lightboxCaption=document.getElementById('lightboxCaption');
var lightboxClose=document.getElementById('lightboxClose');
var lastFocus=null;
document.querySelectorAll('.zoomable').forEach(function(img){img.addEventListener('click',function(){lastFocus=img;lightboxImg.src=img.src;lightboxImg.alt=img.alt;lightboxCaption.textContent=img.dataset.caption||img.alt;lightbox.removeAttribute('hidden');lightbox.focus()})});
function closeLightbox(){lightbox.setAttribute('hidden','');if(lastFocus)lastFocus.focus()}
lightboxClose.addEventListener('click',closeLightbox);
lightbox.addEventListener('click',function(e){if(e.target===lightbox)closeLightbox()});
document.addEventListener('keydown',function(e){if(e.key==='Escape'&&!lightbox.hasAttribute('hidden'))closeLightbox()});

/* 7. SAVE + VALIDATION */
var dxInput=document.getElementById('dx-input');
var dxError=document.getElementById('dxError');
function validateAndSave(){if(!dxInput.value.trim()){dxInput.setAttribute('aria-invalid','true');dxInput.parentElement.classList.add('has-error');dxError.hidden=false;dxInput.focus();toast('Please add a diagnosis before saving the exam.','error');return}dxInput.removeAttribute('aria-invalid');dxInput.parentElement.classList.remove('has-error');dxError.hidden=true;toast('Exam saved to Emily Carter’s chart.','success');saveText.textContent='Saved · just now'}
document.getElementById('saveExam').addEventListener('click',validateAndSave);
document.getElementById('quickSave').addEventListener('click',validateAndSave);

/* 8. OTHER ACTIONS */
function bindToast(id,msg,type){var el=document.getElementById(id);if(el)el.addEventListener('click',function(){toast(msg,type)})}
bindToast('quickEmail','Summary emailed to the patient.','success');
bindToast('emailBtn','Summary emailed to the patient.','success');
bindToast('scheduleBtn','Follow-up appointment requested for 23 May 2027.','success');
bindToast('reminderBtn','Reminder scheduled 7 days before the appointment.','success');
bindToast('exportHistory','Patient history exported as PDF.','info');
bindToast('switchPatientBtn','Patient search opened — type a name or ID.','info');
document.getElementById('printBtn').addEventListener('click',function(){window.print()});
document.getElementById('quickPrint').addEventListener('click',function(){window.print()});

/* 9. SEARCH */
var search=document.getElementById('patientSearch');
if(search){search.addEventListener('keydown',function(e){if(e.key==='Enter'&&search.value.trim()){e.preventDefault();toast('Searching for “'+search.value.trim()+'”…','info')}})}

/* 10. SKIP LINK FOCUS SCROLL */
document.getElementById('main').addEventListener('focus',function(){this.scrollIntoView({block:'start',behavior:'smooth'})});

})();
</script>
</body>
</html>
