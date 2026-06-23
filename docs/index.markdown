<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Haedyn Darling-Hill — Engineering Portfolio</title>
  <meta name="description" content="Engineering portfolio — CAD, built projects, and code." />
  <meta name="theme-color" content="#0d0d14" />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=Inter:wght@300;400;500&family=DM+Mono:wght@300;400;500&display=swap" rel="stylesheet" />
  <style>
    /* ── CAROUSEL ───────────────────────────────────────────── */
    .carousel { position: relative; overflow: hidden; }
    .carousel-track {
      display: flex;
      height: 100%;
      transition: transform 0.35s var(--ease);
    }
    .carousel-track img,
    .carousel-track video {
      min-width: 100%;
      height: 100%;
      object-fit: contain;
      flex-shrink: 0;
      background: #0d0d14;
    }
    .carousel-btn {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      background: rgba(13,13,20,0.7);
      border: 1px solid var(--border);
      color: var(--text);
      width: 32px;
      height: 32px;
      border-radius: 4px;
      font-size: 1.1rem;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: background 0.2s;
      z-index: 2;
    }
    .carousel-btn:hover { background: rgba(74,158,202,0.3); }
    .carousel-prev { left: 0.6rem; }
    .carousel-next { right: 0.6rem; }
    .carousel-dots {
      position: absolute;
      bottom: 0.6rem;
      left: 50%;
      transform: translateX(-50%);
      display: flex;
      gap: 0.4rem;
      z-index: 2;
    }
    .carousel-dot {
      width: 6px;
      height: 6px;
      border-radius: 50%;
      background: var(--border-lit);
      cursor: pointer;
      transition: background 0.2s;
    }
    .carousel-dot.active { background: var(--accent); }

    /* ── TOKENS ─────────────────────────────────────────────── */
    :root {
      --bg:        #0d0d14;
      --bg-card:   #16161f;
      --bg-hover:  #1e1e2a;
      --border:    #2a2a3a;
      --border-lit:#3a3a50;
      --text:      #eceae4;
      --muted:     #7a7a90;
      --accent:    #4a9eca;
      --accent-dim:#1f3d52;
      --tag-cad:   #c97f3b;
      --tag-built: #5aab6d;
      --tag-code:  #7b7bea;
      --font-display: 'Syne', sans-serif;
      --font-body:    'Inter', sans-serif;
      --font-mono:    'DM Mono', monospace;
      --ease: cubic-bezier(0.4, 0, 0.2, 1);
    }

    /* ── RESET ──────────────────────────────────────────────── */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    body {
      background: var(--bg);
      color: var(--text);
      font-family: var(--font-body);
      font-weight: 300;
      line-height: 1.7;
      -webkit-font-smoothing: antialiased;
    }
    a { color: inherit; text-decoration: none; }
    img { display: block; width: 100%; object-fit: contain; }

    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image: radial-gradient(circle, #2a2a3a 1px, transparent 1px);
      background-size: 32px 32px;
      opacity: 0.25;
      pointer-events: none;
      z-index: 0;
    }

    /* ── NAV ────────────────────────────────────────────────── */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 100;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 clamp(1.5rem, 5vw, 4rem);
      height: 64px;
      background: rgba(13, 13, 20, 0.85);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid var(--border);
    }
    .nav-logo {
      font-family: var(--font-mono);
      font-size: 0.85rem;
      font-weight: 400;
      color: var(--accent);
      letter-spacing: 0.04em;
    }
    .nav-links {
      display: flex;
      gap: 0.25rem;
      list-style: none;
    }
    .nav-links a {
      font-family: var(--font-mono);
      font-size: 0.78rem;
      font-weight: 400;
      letter-spacing: 0.06em;
      text-transform: uppercase;
      color: var(--muted);
      padding: 0.4rem 0.85rem;
      border-radius: 4px;
      transition: color 0.2s var(--ease), background 0.2s var(--ease);
      cursor: pointer;
    }
    .nav-links a:hover,
    .nav-links a.active { color: var(--text); background: var(--bg-hover); }
    .nav-links a.active { color: var(--accent); }

    /* ── PAGES ──────────────────────────────────────────────── */
    .page {
      display: none;
      min-height: 100vh;
      padding-top: 64px;
      position: relative;
      z-index: 1;
    }
    .page.active { display: block; }

    /* ── HERO ───────────────────────────────────────────────── */
    .hero {
      padding: clamp(5rem, 12vw, 9rem) clamp(1.5rem, 8vw, 6rem) clamp(4rem, 8vw, 6rem);
      max-width: 900px;
    }
    .hero-eyebrow {
      font-family: var(--font-mono);
      font-size: 0.75rem;
      font-weight: 300;
      letter-spacing: 0.14em;
      text-transform: uppercase;
      color: var(--accent);
      margin-bottom: 1.25rem;
    }
    .hero h1 {
      font-family: var(--font-display);
      font-size: clamp(2.8rem, 7vw, 5.5rem);
      font-weight: 800;
      line-height: 1.05;
      letter-spacing: -0.03em;
      margin-bottom: 1.5rem;
    }
    .hero h1 span { color: var(--accent); }
    .hero p {
      font-size: 1.05rem;
      color: var(--muted);
      max-width: 520px;
      line-height: 1.8;
      margin-bottom: 2.5rem;
    }
    .hero-cta { display: flex; gap: 1rem; flex-wrap: wrap; }

    .btn {
      display: inline-flex;
      align-items: center;
      gap: 0.45rem;
      font-family: var(--font-mono);
      font-size: 0.78rem;
      font-weight: 400;
      letter-spacing: 0.06em;
      text-transform: uppercase;
      padding: 0.7rem 1.4rem;
      border-radius: 4px;
      border: 1px solid var(--border-lit);
      cursor: pointer;
      transition: all 0.2s var(--ease);
    }
    .btn-primary { background: var(--accent); border-color: var(--accent); color: #0d0d14; }
    .btn-primary:hover { background: #6ab8e2; border-color: #6ab8e2; }
    .btn-ghost { background: transparent; color: var(--muted); }
    .btn-ghost:hover { color: var(--text); border-color: var(--border-lit); background: var(--bg-hover); }

    /* ── DIVIDER ────────────────────────────────────────────── */
    .divider {
      display: flex;
      align-items: center;
      gap: 1rem;
      padding: 0 clamp(1.5rem, 8vw, 6rem);
      margin-bottom: 3rem;
    }
    .divider-label {
      font-family: var(--font-mono);
      font-size: 0.7rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--muted);
      white-space: nowrap;
    }
    .divider-line { flex: 1; height: 1px; background: var(--border); }

    /* ── SECTION ────────────────────────────────────────────── */
    .section { padding: 0 clamp(1.5rem, 8vw, 6rem) 6rem; }
    .section-sub {
      font-size: 0.88rem;
      color: var(--muted);
      margin-bottom: 2.5rem;
      line-height: 1.6;
    }

    /* ── PROJECT TABS ───────────────────────────────────────── */
    .tab-bar {
      display: flex;
      gap: 0;
      border-bottom: 1px solid var(--border);
      margin-bottom: 3rem;
    }
    .tab-btn {
      font-family: var(--font-mono);
      font-size: 0.78rem;
      font-weight: 400;
      letter-spacing: 0.07em;
      text-transform: uppercase;
      color: var(--muted);
      padding: 0.75rem 1.4rem;
      border: none;
      background: transparent;
      cursor: pointer;
      border-bottom: 2px solid transparent;
      margin-bottom: -1px;
      transition: all 0.2s var(--ease);
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }
    .tab-btn:hover { color: var(--text); }
    .tab-btn.active { color: var(--text); border-bottom-color: var(--accent); }
    .tab-dot { width: 6px; height: 6px; border-radius: 50%; }
    .tab-btn[data-tab="cad"]   .tab-dot { background: var(--tag-cad); }
    .tab-btn[data-tab="built"] .tab-dot { background: var(--tag-built); }
    .tab-btn[data-tab="code"]  .tab-dot { background: var(--tag-code); }
    .tab-btn[data-tab="all"]   .tab-dot { background: var(--accent); }

    .tab-panel { display: none; }
    .tab-panel.active { display: grid; }

    /* ── PROJECT GRID ───────────────────────────────────────── */
    .project-grid {
      grid-template-columns: repeat(auto-fill, minmax(min(100%, 360px), 1fr));
      gap: 1.5rem;
    }
    .project-card {
      background: var(--bg-card);
      border: 1px solid var(--border);
      border-radius: 8px;
      overflow: hidden;
      display: flex;
      flex-direction: column;
      transition: border-color 0.2s var(--ease), transform 0.2s var(--ease);
    }
    .project-card:hover { border-color: var(--border-lit); transform: translateY(-3px); }
    .project-img {
      aspect-ratio: 16 / 9;
      background: var(--bg-hover);
      overflow: hidden;
      position: relative;
    }
    .project-img img,
    .project-img video {
      height: 100%;
      width: 100%;
      object-fit: contain;
      background: #0d0d14;
      transition: transform 0.4s var(--ease);
      cursor: zoom-in;
    }
    .project-card:hover .project-img img,
    .project-card:hover .project-img video { transform: scale(1.02); }

    /* expand icon overlay */
    .project-img::after {
      content: '⤢';
      position: absolute;
      top: 0.5rem;
      right: 0.6rem;
      font-size: 1rem;
      color: rgba(236,234,228,0.55);
      pointer-events: none;
      opacity: 0;
      transition: opacity 0.2s;
      z-index: 3;
    }
    .project-img:hover::after { opacity: 1; }
    .project-img-placeholder {
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: var(--font-mono);
      font-size: 0.7rem;
      letter-spacing: 0.1em;
      color: var(--border-lit);
      text-transform: uppercase;
    }
    .project-body { padding: 1.5rem; display: flex; flex-direction: column; flex: 1; }
    .project-meta {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 0.75rem;
    }
    .project-tag {
      font-family: var(--font-mono);
      font-size: 0.65rem;
      font-weight: 500;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      padding: 0.2rem 0.55rem;
      border-radius: 3px;
    }
    .tag-cad   { background: rgba(201,127,59,0.15);  color: var(--tag-cad); }
    .tag-built { background: rgba(90,171,109,0.15);  color: var(--tag-built); }
    .tag-code  { background: rgba(123,123,234,0.15); color: var(--tag-code); }
    .project-timeline {
      font-family: var(--font-mono);
      font-size: 0.68rem;
      color: var(--muted);
      letter-spacing: 0.05em;
    }
    .project-title {
      font-family: var(--font-display);
      font-size: 1.2rem;
      font-weight: 700;
      letter-spacing: -0.01em;
      line-height: 1.3;
      margin-bottom: 0.75rem;
    }
    .project-blurb { font-size: 0.875rem; color: var(--muted); line-height: 1.75; flex: 1; }
    .project-link {
      display: inline-flex;
      align-items: center;
      gap: 0.35rem;
      margin-top: 1.25rem;
      font-family: var(--font-mono);
      font-size: 0.72rem;
      letter-spacing: 0.07em;
      text-transform: uppercase;
      color: var(--accent);
      transition: gap 0.2s var(--ease);
    }
    .project-link:hover { gap: 0.6rem; }

    /* ── LIGHTBOX ───────────────────────────────────────────── */
    .lightbox {
      display: none;
      position: fixed;
      inset: 0;
      z-index: 1000;
      background: rgba(5,5,10,0.95);
      align-items: center;
      justify-content: center;
      flex-direction: column;
    }
    .lightbox.open { display: flex; }

    .lightbox-media {
      max-width: 92vw;
      max-height: 82vh;
      object-fit: contain;
      border-radius: 4px;
      box-shadow: 0 8px 48px rgba(0,0,0,0.7);
      display: block;
    }
    .lightbox-media video {
      max-width: 92vw;
      max-height: 82vh;
      border-radius: 4px;
    }

    .lightbox-close {
      position: absolute;
      top: 1.25rem;
      right: 1.5rem;
      background: none;
      border: 1px solid var(--border-lit);
      color: var(--muted);
      font-size: 1.4rem;
      line-height: 1;
      width: 36px;
      height: 36px;
      border-radius: 4px;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: color 0.2s, border-color 0.2s;
    }
    .lightbox-close:hover { color: var(--text); border-color: var(--text); }

    .lightbox-nav {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      background: rgba(13,13,20,0.7);
      border: 1px solid var(--border-lit);
      color: var(--text);
      width: 40px;
      height: 40px;
      border-radius: 4px;
      font-size: 1.4rem;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: background 0.2s;
    }
    .lightbox-nav:hover { background: rgba(74,158,202,0.3); }
    .lightbox-prev { left: 1.25rem; }
    .lightbox-next { right: 1.25rem; }
    .lightbox-nav.hidden { display: none; }

    .lightbox-counter {
      margin-top: 1rem;
      font-family: var(--font-mono);
      font-size: 0.72rem;
      color: var(--muted);
      letter-spacing: 0.08em;
    }

    /* ── ABOUT PAGE ─────────────────────────────────────────── */
    .about-layout {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 5rem;
      align-items: start;
    }
    @media (max-width: 760px) { .about-layout { grid-template-columns: 1fr; gap: 3rem; } }
    .about-photo {
      aspect-ratio: 3/4;
      background: var(--bg-card);
      border: 1px solid var(--border);
      border-radius: 8px;
      overflow: hidden;
      position: relative;
    }
    .about-content h2 {
      font-family: var(--font-display);
      font-size: clamp(1.8rem, 3.5vw, 2.8rem);
      font-weight: 800;
      letter-spacing: -0.03em;
      line-height: 1.1;
      margin-bottom: 1.5rem;
    }
    .about-content p { font-size: 0.95rem; color: var(--muted); line-height: 1.9; margin-bottom: 1.25rem; }
    .about-content p strong { color: var(--text); font-weight: 500; }
    .skills-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 0.75rem; margin-top: 2rem; }
    .skill-item {
      display: flex;
      align-items: center;
      gap: 0.6rem;
      font-family: var(--font-mono);
      font-size: 0.75rem;
      color: var(--muted);
      letter-spacing: 0.04em;
    }
    .skill-item::before {
      content: '';
      width: 5px;
      height: 5px;
      border-radius: 50%;
      background: var(--accent);
      flex-shrink: 0;
    }
    .about-links { display: flex; gap: 1rem; flex-wrap: wrap; margin-top: 2rem; }

    /* ── FOOTER ─────────────────────────────────────────────── */
    footer {
      position: relative;
      z-index: 1;
      border-top: 1px solid var(--border);
      padding: 2rem clamp(1.5rem, 8vw, 6rem);
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 1rem;
      flex-wrap: wrap;
    }
    footer p { font-family: var(--font-mono); font-size: 0.72rem; color: var(--muted); letter-spacing: 0.05em; }
    footer a { color: var(--muted); transition: color 0.2s; }
    footer a:hover { color: var(--accent); }

    /* ── EMPTY STATE ────────────────────────────────────────── */
    .empty-state {
      grid-column: 1 / -1;
      padding: 4rem 2rem;
      text-align: center;
      border: 1px dashed var(--border);
      border-radius: 8px;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 0.75rem;
    }
    .empty-state p { font-family: var(--font-mono); font-size: 0.8rem; color: var(--border-lit); letter-spacing: 0.06em; }

    /* ── RESPONSIVE ─────────────────────────────────────────── */
    @media (max-width: 600px) {
      nav { padding: 0 1.25rem; }
      .hero { padding: 4rem 1.25rem 3rem; }
      .section { padding: 0 1.25rem 4rem; }
      .divider { padding: 0 1.25rem; }
      .skills-grid { grid-template-columns: 1fr; }
    }
    @media (prefers-reduced-motion: reduce) {
      * { transition-duration: 0.01ms !important; animation-duration: 0.01ms !important; }
    }
  </style>
</head>
<body>

  <!-- NAV -->
  <nav>
    <span class="nav-logo">haedyndh.github.io/haedyndarlinghillportfolio/</span>
    <ul class="nav-links">
      <li><a href="#" onclick="showPage('projects')" id="nav-projects" class="active">Projects</a></li>
      <li><a href="#" onclick="showPage('about')" id="nav-about">About</a></li>
      <li><a href="https://github.com/haedyndh" target="_blank" rel="noopener">GitHub ↗</a></li>
    </ul>
  </nav>

  <!-- ═══════════════════════════════════════════════════════════
       PAGE: PROJECTS
  ═══════════════════════════════════════════════════════════ -->
  <div class="page active" id="page-projects">

    <div class="hero">
      <p class="hero-eyebrow">Engineering Portfolio</p>
      <h1>Design.<br/>Build. <span>Iterate.</span></h1>
      <p>Mechanical engineering student at Boston University. These are the projects I've worked on — CAD models, physical builds, and software tools.</p>
      <div class="hero-cta">
        <a class="btn btn-primary" href="#projects-section">See the work ↓</a>
        <a class="btn btn-ghost" href="#" onclick="showPage('about')">About me</a>
      </div>
    </div>

    <div id="projects-section">
      <div class="divider">
        <span class="divider-label">Projects</span>
        <div class="divider-line"></div>
      </div>

      <div class="section">
        <p class="section-sub">Things I've designed, built, and coded — organized by discipline. Click on the individual sections to see more details.</p>

        <!-- Tab Bar -->
        <div class="tab-bar">
          <button class="tab-btn active" data-tab="all" onclick="switchTab('all')">
            <span class="tab-dot"></span> All
          </button>
          <button class="tab-btn" data-tab="cad" onclick="switchTab('cad')">
            <span class="tab-dot"></span> CAD
          </button>
          <button class="tab-btn" data-tab="built" onclick="switchTab('built')">
            <span class="tab-dot"></span> Built
          </button>
          <button class="tab-btn" data-tab="code" onclick="switchTab('code')">
            <span class="tab-dot"></span> Code
          </button>
        </div>

        <!-- ═══════════════════════════════════════════════════
             TAB: ALL
        ════════════════════════════════════════════════════ -->
        <div class="tab-panel project-grid active" id="tab-all">

          <article class="project-card">
            <div class="project-img carousel" data-carousel>
              <div class="carousel-track">
                <img src="/haedyndarlinghillportfolio/images/Truss1.png" alt="Warren Truss - view 1" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/Truss2.png" alt="Warren Truss - view 2" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/Truss3.png" alt="Warren Truss - view 3" loading="lazy" />
              </div>
              <button class="carousel-btn carousel-prev" aria-label="Previous">‹</button>
              <button class="carousel-btn carousel-next" aria-label="Next">›</button>
              <div class="carousel-dots"></div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-built">Built</span>
                <span class="project-timeline">Jan 2026 – Apr 2026</span>
              </div>
              <h3 class="project-title">Truss Design (JANICE)</h3>
              <p class="project-blurb">
                Designed and built a Warren truss within strict material and geometric constraints. Developed MATLAB code to predict collapse load based on joint placement and member length, then iterated in CAD to optimize the design before fabrication and assembly.
              </p>
            </div>
          </article>

          <article class="project-card">
            <div class="project-img carousel" data-carousel>
              <div class="carousel-track">
                <img src="/haedyndarlinghillportfolio/images/P2P1.png" alt="Point-to-Point - view 1" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/P2P3.png" alt="Point-to-Point - view 2" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/P2P4.png" alt="Point-to-Point - view 3" loading="lazy" />
              </div>
              <button class="carousel-btn carousel-prev" aria-label="Previous">‹</button>
              <button class="carousel-btn carousel-next" aria-label="Next">›</button>
              <div class="carousel-dots"></div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-built">Built</span>
                <span class="project-timeline">Sep 2025 – Dec 2025</span>
              </div>
              <h3 class="project-title">Point-to-Point Communication System (HERMES)</h3>
              <p class="project-blurb">
                Built in my sophomore-year project class. We were tasked with designing a system that could transmit 8 messages at a distance of 10 feet. I was completely responsible for the transmission system (metal box). I designed a communication system based on morse, integrated and programmed the user-input keypad, laser, and motor (to rotate laser). I designed the housing with aluminum to gain experience working with metal on the waterjet cutter and spot welding.
              </p>
            </div>
          </article>

          <article class="project-card">
            <div class="project-img carousel" data-carousel>
              <div class="carousel-track">
                <img src="/haedyndarlinghillportfolio/images/TempBox1.png" alt="Temperature Sensor Box - view 1" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/TempBox2.png" alt="Temperature Sensor Box - view 2" loading="lazy" />
              </div>
              <button class="carousel-btn carousel-prev" aria-label="Previous">‹</button>
              <button class="carousel-btn carousel-next" aria-label="Next">›</button>
              <div class="carousel-dots"></div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-built">Built</span>
                <span class="project-timeline">Sep 2024 – Dec 2024</span>
              </div>
              <h3 class="project-title">Temperature Sensor (JAKE)</h3>
              <p class="project-blurb">
                Built in my freshman-year project class. I was tasked with building a box to read the ambient temperature in the room and buzz periodically when the temperature exceeded a certain threshold. This project involved integrating multiple sensors and an LCD screen into one system using an Arduino. While rather simple, it helped me get my bearings, and I use it every day in my apartment.
              </p>
            </div>
          </article>

          <article class="project-card">
            <div class="project-img">
              <img src="/haedyndarlinghillportfolio/images/Sikorsky1.png" alt="Sikorsky Transmission" loading="lazy" />
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-built">Built</span>
                <span class="project-timeline">Sep 2023 – May 2024</span>
              </div>
              <h3 class="project-title">X2 Helicopter Transmission</h3>
              <p class="project-blurb">
                Assessed viability of back-emf based transmission in X2 helicopter. I partnered with a Sikorsky engineer to test if alternative transmission systems were possible in the X2. Designed and assembled scaled-down system, measured torque output, and concluded large-scale viability.
              </p>
            </div>
          </article>

          <article class="project-card">
            <div class="project-img carousel" data-carousel>
              <div class="carousel-track">
                <img src="/haedyndarlinghillportfolio/images/MATE2.png" alt="MATE ROV - view 1" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/MATE1.png" alt="MATE ROV - view 2" loading="lazy" />
              </div>
              <button class="carousel-btn carousel-prev" aria-label="Previous">‹</button>
              <button class="carousel-btn carousel-next" aria-label="Next">›</button>
              <div class="carousel-dots"></div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-built">Built</span>
                <span class="project-timeline">Nov 2020 – Sep 2023</span>
              </div>
              <h3 class="project-title">Underwater ROV (FLOAT-E)</h3>
              <p class="project-blurb">
                In 8th grade, I was invited to join the high-school MATE ROV Underwater Robotics team. My main responsibility was researching, designing, and building a compatible ESC for underwater use. The team placed top-10 at the 2021 World Championships. Designing ESCs for BLDC motors taught me fundamentals of oscilloscope debugging, PCB design in Altium, and surface mount soldering.
              </p>
            </div>
          </article>

          <article class="project-card">
            <div class="project-img carousel" data-carousel>
              <div class="carousel-track">
                <img src="/haedyndarlinghillportfolio/images/Vex2.png" alt="Vex Robotics - view 1" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/Vex1.png" alt="Vex Robotics - view 2" loading="lazy" />
              </div>
              <button class="carousel-btn carousel-prev" aria-label="Previous">‹</button>
              <button class="carousel-btn carousel-next" aria-label="Next">›</button>
              <div class="carousel-dots"></div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-built">Built</span>
                <span class="project-timeline">Sep 2022 – May 2024</span>
              </div>
              <h3 class="project-title">VEX Robotics (HANSEL &amp; GRETEL)</h3>
              <p class="project-blurb">
                I founded and led the robotics team at the Berkshire School. Over my tenure, I taught ~30 students the basics of robotics across programming, electrical, and mechanical disciplines, and coordinated inter-school competitions between two chassis teams.
              </p>
            </div>
          </article>

          <article class="project-card">
            <div class="project-img carousel" data-carousel>
              <div class="carousel-track">
                <img src="/haedyndarlinghillportfolio/images/cap1.png" alt="Fuel Cap - view 1" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/cap2.png" alt="Fuel Cap - view 2" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/cap3.png" alt="Fuel Cap - view 3" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/capdrawing.png" alt="Fuel Cap - drawing" loading="lazy" />
              </div>
              <button class="carousel-btn carousel-prev" aria-label="Previous">‹</button>
              <button class="carousel-btn carousel-next" aria-label="Next">›</button>
              <div class="carousel-dots"></div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-cad">CAD</span>
                <span class="project-timeline">Apr 2026 – May 2026</span>
              </div>
              <h3 class="project-title">Motorcycle Fuel Cap</h3>
              <p class="project-blurb">
                Completed for CAD/SolidWorks class.
              </p>
            </div>
          </article>

          <article class="project-card">
            <div class="project-img carousel" data-carousel>
              <div class="carousel-track">
                <img src="/haedyndarlinghillportfolio/images/4barlinkage1.png" alt="4-Bar-Linkage - view 1" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/4barlinkage2.png" alt="4-Bar-Linkage - view 2" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/4barlinkage3.png" alt="4-Bar-Linkage - view 3" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/4barlinkage4.png" alt="4-Bar-Linkage - view 4" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/4barexplodeddrawing.png" alt="4-Bar-Linkage - drawing" loading="lazy" />
              </div>
              <button class="carousel-btn carousel-prev" aria-label="Previous">‹</button>
              <button class="carousel-btn carousel-next" aria-label="Next">›</button>
              <div class="carousel-dots"></div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-cad">CAD</span>
                <span class="project-timeline">Mar 2026 – Apr 2026</span>
              </div>
              <h3 class="project-title">4-Bar Linkage</h3>
              <p class="project-blurb">
                Completed for CAD/SolidWorks class with creative freedom on design and rotation style. Motion calculations completed alongside the model.
              </p>
            </div>
          </article>

          <article class="project-card">
            <div class="project-img carousel" data-carousel>
              <div class="carousel-track">
                <img src="/haedyndarlinghillportfolio/images/ballandsocket.png" alt="Ball Valve - view 1" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/ballandsocketexploded.png" alt="Ball Valve - exploded" loading="lazy" />
              </div>
              <button class="carousel-btn carousel-prev" aria-label="Previous">‹</button>
              <button class="carousel-btn carousel-next" aria-label="Next">›</button>
              <div class="carousel-dots"></div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-cad">CAD</span>
                <span class="project-timeline">Mar 2026</span>
              </div>
              <h3 class="project-title">Ball Valve</h3>
              <p class="project-blurb">
                Parts and assembly completed for CAD/SolidWorks class. Handle turns the ball accordingly.
              </p>
            </div>
          </article>

          <article class="project-card">
            <div class="project-img carousel" data-carousel>
              <div class="carousel-track">
                <img src="/haedyndarlinghillportfolio/images/latheattatchment1.png" alt="Lathe Part - view 1" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/latheattatchment2.png" alt="Lathe Part - view 2" loading="lazy" />
              </div>
              <button class="carousel-btn carousel-prev" aria-label="Previous">‹</button>
              <button class="carousel-btn carousel-next" aria-label="Next">›</button>
              <div class="carousel-dots"></div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-cad">CAD</span>
                <span class="project-timeline">Mar 2026</span>
              </div>
              <h3 class="project-title">Lathe Headstock Body Part</h3>
              <p class="project-blurb">
                For CAD/SolidWorks class. Part of a lathe headstock body.
              </p>
            </div>
          </article>

        </div><!-- /tab-all -->

        <!-- ═══════════════════════════════════════════════════
             TAB: CAD
        ════════════════════════════════════════════════════ -->
        <div class="tab-panel project-grid" id="tab-cad">

          <article class="project-card">
            <div class="project-img carousel" data-carousel>
              <div class="carousel-track">
                <img src="/haedyndarlinghillportfolio/images/cap1.png" alt="Fuel Cap - view 1" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/cap2.png" alt="Fuel Cap - view 2" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/cap3.png" alt="Fuel Cap - view 3" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/capdrawing.png" alt="Fuel Cap - drawing" loading="lazy" />
              </div>
              <button class="carousel-btn carousel-prev" aria-label="Previous">‹</button>
              <button class="carousel-btn carousel-next" aria-label="Next">›</button>
              <div class="carousel-dots"></div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-cad">CAD</span>
                <span class="project-timeline">Apr 2026 – May 2026</span>
              </div>
              <h3 class="project-title">Motorcycle Fuel Cap</h3>
              <p class="project-blurb">
                Completed for CAD/SolidWorks class.
              </p>
            </div>
          </article>

          <article class="project-card">
            <div class="project-img carousel" data-carousel>
              <div class="carousel-track">
                <img src="/haedyndarlinghillportfolio/images/4barlinkage1.png" alt="4-Bar-Linkage - view 1" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/4barlinkage2.png" alt="4-Bar-Linkage - view 2" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/4barlinkage3.png" alt="4-Bar-Linkage - view 3" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/4barlinkage4.png" alt="4-Bar-Linkage - view 4" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/4barexplodeddrawing.png" alt="4-Bar-Linkage - drawing" loading="lazy" />
              </div>
              <button class="carousel-btn carousel-prev" aria-label="Previous">‹</button>
              <button class="carousel-btn carousel-next" aria-label="Next">›</button>
              <div class="carousel-dots"></div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-cad">CAD</span>
                <span class="project-timeline">Mar 2026 – Apr 2026</span>
              </div>
              <h3 class="project-title">4-Bar Linkage</h3>
              <p class="project-blurb">
                Completed for CAD/SolidWorks class with creative freedom on design and rotation style. Motion calculations completed alongside the model.
              </p>
            </div>
          </article>

          <article class="project-card">
            <div class="project-img carousel" data-carousel>
              <div class="carousel-track">
                <img src="/haedyndarlinghillportfolio/images/ballandsocket.png" alt="Ball Valve - view 1" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/ballandsocketexploded.png" alt="Ball Valve - exploded" loading="lazy" />
              </div>
              <button class="carousel-btn carousel-prev" aria-label="Previous">‹</button>
              <button class="carousel-btn carousel-next" aria-label="Next">›</button>
              <div class="carousel-dots"></div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-cad">CAD</span>
                <span class="project-timeline">Mar 2026</span>
              </div>
              <h3 class="project-title">Ball Valve</h3>
              <p class="project-blurb">
                Parts and assembly completed for CAD/SolidWorks class. Handle turns the ball accordingly.
              </p>
            </div>
          </article>

          <article class="project-card">
            <div class="project-img carousel" data-carousel>
              <div class="carousel-track">
                <img src="/haedyndarlinghillportfolio/images/latheattatchment1.png" alt="Lathe Part - view 1" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/latheattatchment2.png" alt="Lathe Part - view 2" loading="lazy" />
              </div>
              <button class="carousel-btn carousel-prev" aria-label="Previous">‹</button>
              <button class="carousel-btn carousel-next" aria-label="Next">›</button>
              <div class="carousel-dots"></div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-cad">CAD</span>
                <span class="project-timeline">Mar 2026</span>
              </div>
              <h3 class="project-title">Lathe Headstock Body Part</h3>
              <p class="project-blurb">
                For CAD/SolidWorks class. Part of a lathe headstock body.
              </p>
            </div>
          </article>

        </div><!-- /tab-cad -->

        <!-- ═══════════════════════════════════════════════════
             TAB: BUILT
        ════════════════════════════════════════════════════ -->
        <div class="tab-panel project-grid" id="tab-built">

          <article class="project-card">
            <div class="project-img carousel" data-carousel>
              <div class="carousel-track">
                <img src="/haedyndarlinghillportfolio/images/Truss1.png" alt="Warren Truss - view 1" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/Truss2.png" alt="Warren Truss - view 2" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/Truss3.png" alt="Warren Truss - view 3" loading="lazy" />
              </div>
              <button class="carousel-btn carousel-prev" aria-label="Previous">‹</button>
              <button class="carousel-btn carousel-next" aria-label="Next">›</button>
              <div class="carousel-dots"></div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-built">Built</span>
                <span class="project-timeline">Jan 2026 – Apr 2026</span>
              </div>
              <h3 class="project-title">Truss Design (JANICE)</h3>
              <p class="project-blurb">
                Designed and built a Warren truss within strict material and geometric constraints. Developed MATLAB code to predict collapse load based on joint placement and member length, then iterated in CAD to optimize the design before fabrication and assembly.
              </p>
            </div>
          </article>

          <article class="project-card">
            <div class="project-img carousel" data-carousel>
              <div class="carousel-track">
                <img src="/haedyndarlinghillportfolio/images/P2P1.png" alt="Point-to-Point - view 1" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/P2P3.png" alt="Point-to-Point - view 2" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/P2P4.png" alt="Point-to-Point - view 3" loading="lazy" />
              </div>
              <button class="carousel-btn carousel-prev" aria-label="Previous">‹</button>
              <button class="carousel-btn carousel-next" aria-label="Next">›</button>
              <div class="carousel-dots"></div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-built">Built</span>
                <span class="project-timeline">Sep 2025 – Dec 2025</span>
              </div>
              <h3 class="project-title">Point-to-Point Communication System (HERMES)</h3>
              <p class="project-blurb">
                Built in my sophomore-year project class. We were tasked with designing a system that could transmit 8 messages at a distance of 10 feet. I was completely responsible for the transmission system (metal box). I designed a communication system based on morse, integrated and programmed the user-input keypad, laser, and motor (to rotate laser). I designed the housing with aluminum to gain experience working with metal on the waterjet cutter and spot welding.
              </p>
            </div>
          </article>

          <article class="project-card">
            <div class="project-img carousel" data-carousel>
              <div class="carousel-track">
                <img src="/haedyndarlinghillportfolio/images/TempBox1.png" alt="Temperature Sensor Box - view 1" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/TempBox2.png" alt="Temperature Sensor Box - view 2" loading="lazy" />
              </div>
              <button class="carousel-btn carousel-prev" aria-label="Previous">‹</button>
              <button class="carousel-btn carousel-next" aria-label="Next">›</button>
              <div class="carousel-dots"></div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-built">Built</span>
                <span class="project-timeline">Sep 2024 – Dec 2024</span>
              </div>
              <h3 class="project-title">Temperature Sensor (JAKE)</h3>
              <p class="project-blurb">
                Built in my freshman-year project class. I was tasked with building a box to read the ambient temperature in the room and buzz periodically when the temperature exceeded a certain threshold. This project involved integrating multiple sensors and an LCD screen into one system using an Arduino. While rather simple, it helped me get my bearings, and I use it every day in my apartment.
              </p>
            </div>
          </article>

          <article class="project-card">
            <div class="project-img">
              <img src="/haedyndarlinghillportfolio/images/Sikorsky1.png" alt="Sikorsky Transmission" loading="lazy" />
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-built">Built</span>
                <span class="project-timeline">Sep 2023 – May 2024</span>
              </div>
              <h3 class="project-title">X2 Helicopter Transmission</h3>
              <p class="project-blurb">
                Assessed viability of back-emf based transmission in X2 helicopter. I partnered with a Sikorsky engineer to test if alternative transmission systems were possible in the X2. Designed and assembled scaled-down system, measured torque output, and concluded large-scale viability.
              </p>
            </div>
          </article>

          <article class="project-card">
            <div class="project-img carousel" data-carousel>
              <div class="carousel-track">
                <img src="/haedyndarlinghillportfolio/images/MATE2.png" alt="MATE ROV - view 1" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/MATE1.png" alt="MATE ROV - view 2" loading="lazy" />
              </div>
              <button class="carousel-btn carousel-prev" aria-label="Previous">‹</button>
              <button class="carousel-btn carousel-next" aria-label="Next">›</button>
              <div class="carousel-dots"></div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-built">Built</span>
                <span class="project-timeline">Nov 2020 – Sep 2023</span>
              </div>
              <h3 class="project-title">Underwater ROV (FLOAT-E)</h3>
              <p class="project-blurb">
                In 8th grade, I was invited to join the high-school MATE ROV Underwater Robotics team. My main responsibility was researching, designing, and building a compatible ESC for underwater use. The team placed top-10 at the 2021 World Championships. Designing ESCs for BLDC motors taught me fundamentals of oscilloscope debugging, PCB design in Altium, and surface mount soldering.
              </p>
            </div>
          </article>

          <article class="project-card">
            <div class="project-img carousel" data-carousel>
              <div class="carousel-track">
                <img src="/haedyndarlinghillportfolio/images/Vex2.png" alt="Vex Robotics - view 1" loading="lazy" />
                <img src="/haedyndarlinghillportfolio/images/Vex1.png" alt="Vex Robotics - view 2" loading="lazy" />
              </div>
              <button class="carousel-btn carousel-prev" aria-label="Previous">‹</button>
              <button class="carousel-btn carousel-next" aria-label="Next">›</button>
              <div class="carousel-dots"></div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-built">Built</span>
                <span class="project-timeline">Sep 2022 – May 2024</span>
              </div>
              <h3 class="project-title">VEX Robotics (HANSEL &amp; GRETEL)</h3>
              <p class="project-blurb">
                I founded and led the robotics team at the Berkshire School. Over my tenure, I taught ~30 students the basics of robotics across programming, electrical, and mechanical disciplines, and coordinated inter-school competitions between two chassis teams.
              </p>
            </div>
          </article>

        </div><!-- /tab-built -->

        <!-- ═══════════════════════════════════════════════════
             TAB: CODE
        ════════════════════════════════════════════════════ -->
        <div class="tab-panel project-grid" id="tab-code">
          <div class="empty-state">
            <p>// no code projects yet</p>
            <p>Copy a project-card block from the "All" tab and paste it here.</p>
          </div>
        </div><!-- /tab-code -->

      </div><!-- /section -->
    </div>

  </div><!-- /page-projects -->


  <!-- ═══════════════════════════════════════════════════════════
       PAGE: ABOUT
  ═══════════════════════════════════════════════════════════ -->
  <div class="page" id="page-about">

    <div class="hero">
      <p class="hero-eyebrow">About Me</p>
      <h1>Engineer.<br/><span>Problem-Solver.</span></h1>
    </div>

    <div class="divider">
      <span class="divider-label">Background</span>
      <div class="divider-line"></div>
    </div>

    <div class="section">
      <div class="about-layout">

        <div class="about-photo">
          <img src="/haedyndarlinghillportfolio/images/Headshot.png" alt="Haedyn Darling-Hill" />
        </div>

        <div class="about-content">
          <h2>Haedyn<br/>Darling Hill</h2>

          <p>
            <strong>Mechanical Engineer, Student-Athlete</strong> — I am pursuing a Mechanical Engineering BS on track to graduate in 2028. I have gained experience in CAD and project design, underwater ROVs, FRC and VEX robotics, full-system design, MATLAB, Python, and biomechanical research.
          </p>
          <p>
            From 2020–2023, I worked on a <a href="https://20693798.fs1.hubspotusercontent-na1.net/hubfs/20693798/TechReportArchives/2021/Seattle%20Academy_Blueshift%20Robotics_Technical%20Documentation_2021.pdf" target="_blank" rel="noopener">MATE Underwater ROV team</a> at Seattle Academy, designing an ROV for autonomous coral reef monitoring. Commercially available ESCs didn't meet our control requirements, so I designed and integrated a custom one. The team placed top-10 at the 2021 World Championships. I also contributed to the FRC team's electrical division, collaborating with mechanical to produce competition-ready component housings.
            After transferring schools, I founded a VEX robotics team: building the curriculum, leading three subteams, and running an internal competition model by end of year one.
            My junior and senior years, I participated in an invite-only research program in partnership with a Sikorsky Lockheed Martin engineer. Working on the X2 helicopter's main gearbox, I designed an electrical transmission system using back-EMF to reduce vibrational instability and demonstrated proof-of-concept viability at scale.
          </p>
          <p>
            Both university summers have been spent in technical roles outside the classroom.
            After freshman year, I interned at Synthesia.io on the R&amp;D team, contributing to AI model design with a focus on improving the naturalism of synthesized speech and image output.
            After sophomore year, I was awarded the largest undergraduate research grant available at my institution to study the relationship between inter-limb hip asymmetry and pain, applying biomechanical analysis to a clinical research context.
          </p>
          <p>
            I play as a fullback/wing for Boston University's Women's Rugby team! Team commitments take upwards of 10–15 hours per week, and I love every minute of it. Sports, and rugby in particular, have taught me to be resilient, hard working, and collaborative.
          </p>

          <div class="skills-grid">
            <span class="skill-item">SolidWorks</span>
            <span class="skill-item">Onshape</span>
            <span class="skill-item">Python</span>
            <span class="skill-item">MATLAB</span>
            <span class="skill-item">FDM / SLA printing</span>
            <span class="skill-item">PCB Design</span>
            <span class="skill-item">Arduino / RPi</span>
            <span class="skill-item">Visual3D</span>
            <span class="skill-item">Vicon</span>
          </div>

          <div class="about-links">
            <a class="btn btn-primary" href="mailto:haedyndh@bu.edu">Get in touch</a>
            <a class="btn btn-ghost" href="https://github.com/haedyndh" target="_blank" rel="noopener">GitHub ↗</a>
            <a class="btn btn-ghost" href="resume.pdf" target="_blank">Résumé ↗</a>
          </div>
        </div>

      </div>
    </div>

  </div><!-- /page-about -->


  <!-- FOOTER -->
  <footer>
    <p>Haedyn Darling-Hill · Engineering Portfolio</p>
    <p>
      <a href="https://github.com/haedyndh" target="_blank" rel="noopener">GitHub</a>
      &nbsp;·&nbsp;
      <a href="mailto:haedyndh@bu.edu">Email</a>
    </p>
  </footer>

  <!-- LIGHTBOX -->
  <div class="lightbox" id="lightbox" role="dialog" aria-modal="true" aria-label="Media viewer">
    <button class="lightbox-close" id="lb-close" aria-label="Close">✕</button>
    <button class="lightbox-nav lightbox-prev hidden" id="lb-prev" aria-label="Previous">‹</button>
    <div id="lb-content"></div>
    <button class="lightbox-nav lightbox-next hidden" id="lb-next" aria-label="Next">›</button>
    <div class="lightbox-counter" id="lb-counter"></div>
  </div>

  <script>
    // ── Page switching ──────────────────────────────────────
    function showPage(name) {
      document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
      document.querySelectorAll('.nav-links a').forEach(a => a.classList.remove('active'));
      document.getElementById('page-' + name).classList.add('active');
      document.getElementById('nav-' + name).classList.add('active');
      window.scrollTo({ top: 0, behavior: 'smooth' });
      return false;
    }

    // ── Tab switching ───────────────────────────────────────
    function switchTab(tab) {
      document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
      document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
      document.querySelector(`[data-tab="${tab}"]`).classList.add('active');
      document.getElementById('tab-' + tab).classList.add('active');
    }

    document.querySelectorAll('.nav-links a[onclick]').forEach(a => {
      a.addEventListener('click', e => e.preventDefault());
    });

    // ── Lightbox ────────────────────────────────────────────
    const lb        = document.getElementById('lightbox');
    const lbContent = document.getElementById('lb-content');
    const lbCounter = document.getElementById('lb-counter');
    const lbPrev    = document.getElementById('lb-prev');
    const lbNext    = document.getElementById('lb-next');
    const lbClose   = document.getElementById('lb-close');

    let lbItems  = [];   // array of {type:'img'|'video', src, poster?}
    let lbIndex  = 0;

    function lbOpen(items, startIndex) {
      lbItems = items;
      lbIndex = startIndex;
      lb.classList.add('open');
      document.body.style.overflow = 'hidden';
      lbRender();
    }

    function lbClose_() {
      lb.classList.remove('open');
      document.body.style.overflow = '';
      // pause any playing video
      const vid = lbContent.querySelector('video');
      if (vid) vid.pause();
      lbContent.innerHTML = '';
    }

    function lbRender() {
      // pause any playing video before switching
      const prevVid = lbContent.querySelector('video');
      if (prevVid) prevVid.pause();

      const item = lbItems[lbIndex];
      lbContent.innerHTML = '';

      if (item.type === 'video') {
        const v = document.createElement('video');
        v.className = 'lightbox-media';
        v.controls = true;
        v.autoplay = true;
        v.loop = true;
        v.style.maxWidth  = '92vw';
        v.style.maxHeight = '82vh';
        if (item.poster) v.poster = item.poster;
        const s = document.createElement('source');
        s.src  = item.src;
        s.type = 'video/mp4';
        v.appendChild(s);
        lbContent.appendChild(v);
      } else {
        const img = document.createElement('img');
        img.className = 'lightbox-media';
        img.src = item.src;
        img.alt = item.alt || '';
        lbContent.appendChild(img);
      }

      // nav arrows
      lbPrev.classList.toggle('hidden', lbItems.length <= 1);
      lbNext.classList.toggle('hidden', lbItems.length <= 1);

      // counter
      lbCounter.textContent = lbItems.length > 1
        ? `${lbIndex + 1} / ${lbItems.length}`
        : '';
    }

    lbClose.addEventListener('click', lbClose_);
    lb.addEventListener('click', e => { if (e.target === lb) lbClose_(); });

    lbPrev.addEventListener('click', () => {
      lbIndex = (lbIndex - 1 + lbItems.length) % lbItems.length;
      lbRender();
    });
    lbNext.addEventListener('click', () => {
      lbIndex = (lbIndex + 1) % lbItems.length;
      lbRender();
    });

    document.addEventListener('keydown', e => {
      if (!lb.classList.contains('open')) return;
      if (e.key === 'Escape')      lbClose_();
      if (e.key === 'ArrowLeft')  { lbIndex = (lbIndex - 1 + lbItems.length) % lbItems.length; lbRender(); }
      if (e.key === 'ArrowRight') { lbIndex = (lbIndex + 1) % lbItems.length;                  lbRender(); }
    });

    // ── Carousels ───────────────────────────────────────────
    // Helper: gather all media items from a carousel track
    function gatherItems(track) {
      return Array.from(track.querySelectorAll('img, video')).map(el => {
        if (el.tagName === 'VIDEO') {
          return { type: 'video', src: el.querySelector('source')?.src || el.src, poster: el.poster || '' };
        }
        return { type: 'img', src: el.src, alt: el.alt };
      });
    }

    document.querySelectorAll('[data-carousel]').forEach(carousel => {
      const track        = carousel.querySelector('.carousel-track');
      const slides       = track.querySelectorAll('img, video');
      const dotsContainer = carousel.querySelector('.carousel-dots');
      let current = 0;

      // Build dots
      slides.forEach((_, i) => {
        const dot = document.createElement('div');
        dot.className = 'carousel-dot' + (i === 0 ? ' active' : '');
        dot.addEventListener('click', () => goTo(i));
        dotsContainer.appendChild(dot);
      });

      function goTo(n) {
        current = (n + slides.length) % slides.length;
        track.style.transform = `translateX(-${current * 100}%)`;
        dotsContainer.querySelectorAll('.carousel-dot').forEach((d, i) => {
          d.classList.toggle('active', i === current);
        });
        // pause any videos that aren't current
        slides.forEach((s, i) => {
          if (s.tagName === 'VIDEO' && i !== current) s.pause();
        });
      }

      carousel.querySelector('.carousel-prev').addEventListener('click', e => {
        e.stopPropagation();
        goTo(current - 1);
      });
      carousel.querySelector('.carousel-next').addEventListener('click', e => {
        e.stopPropagation();
        goTo(current + 1);
      });

      // click on the image/video area → open lightbox at current slide
      track.addEventListener('click', e => {
        // don't trigger if a button inside was clicked
        if (e.target.closest('.carousel-btn')) return;
        lbOpen(gatherItems(track), current);
      });
    });

    // Single (non-carousel) project images → lightbox
    document.querySelectorAll('.project-img:not([data-carousel]) img, .project-img:not([data-carousel]) video').forEach(el => {
      el.style.cursor = 'zoom-in';
      el.addEventListener('click', () => {
        const item = el.tagName === 'VIDEO'
          ? { type: 'video', src: el.querySelector('source')?.src || el.src, poster: el.poster || '' }
          : { type: 'img', src: el.src, alt: el.alt };
        lbOpen([item], 0);
      });
    });
  </script>
</body>
</html>