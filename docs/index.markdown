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
    img { display: block; width: 100%; object-fit: cover; }

    /* ── GRID BACKGROUND (blueprint feel) ──────────────────── */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image:
        radial-gradient(circle, #2a2a3a 1px, transparent 1px);
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
    .nav-links a.active {
      color: var(--text);
      background: var(--bg-hover);
    }

    .nav-links a.active {
      color: var(--accent);
    }

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

    .hero h1 span {
      color: var(--accent);
    }

    .hero p {
      font-size: 1.05rem;
      color: var(--muted);
      max-width: 520px;
      line-height: 1.8;
      margin-bottom: 2.5rem;
    }

    .hero-cta {
      display: flex;
      gap: 1rem;
      flex-wrap: wrap;
    }

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

    .btn-primary {
      background: var(--accent);
      border-color: var(--accent);
      color: #0d0d14;
    }
    .btn-primary:hover { background: #6ab8e2; border-color: #6ab8e2; }

    .btn-ghost {
      background: transparent;
      color: var(--muted);
    }
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
    .divider-line {
      flex: 1;
      height: 1px;
      background: var(--border);
    }

    /* ── SECTION ────────────────────────────────────────────── */
    .section {
      padding: 0 clamp(1.5rem, 8vw, 6rem) 6rem;
    }

    .section-header {
      display: flex;
      align-items: baseline;
      justify-content: space-between;
      margin-bottom: 0.5rem;
    }

    .section-title {
      font-family: var(--font-display);
      font-size: clamp(1.6rem, 3.5vw, 2.5rem);
      font-weight: 700;
      letter-spacing: -0.02em;
    }

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

    .tab-btn.active {
      color: var(--text);
      border-bottom-color: var(--accent);
    }

    .tab-dot {
      width: 6px;
      height: 6px;
      border-radius: 50%;
    }
    .tab-btn[data-tab="cad"] .tab-dot    { background: var(--tag-cad); }
    .tab-btn[data-tab="built"] .tab-dot  { background: var(--tag-built); }
    .tab-btn[data-tab="code"] .tab-dot   { background: var(--tag-code); }
    .tab-btn[data-tab="all"] .tab-dot    { background: var(--accent); }

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

    .project-card:hover {
      border-color: var(--border-lit);
      transform: translateY(-3px);
    }

    .project-img {
      aspect-ratio: 16 / 9;
      background: var(--bg-hover);
      overflow: hidden;
      position: relative;
    }

    .project-img img { height: 100%; transition: transform 0.4s var(--ease); }
    .project-card:hover .project-img img { transform: scale(1.04); }

    /* placeholder when no image */
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

    .project-body {
      padding: 1.5rem;
      display: flex;
      flex-direction: column;
      flex: 1;
    }

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

    .tag-cad   { background: rgba(201,127,59,0.15); color: var(--tag-cad); }
    .tag-built { background: rgba(90,171,109,0.15); color: var(--tag-built); }
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

    .project-blurb {
      font-size: 0.875rem;
      color: var(--muted);
      line-height: 1.75;
      flex: 1;
    }

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

    /* ── ABOUT PAGE ─────────────────────────────────────────── */
    .about-layout {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 5rem;
      align-items: start;
    }

    @media (max-width: 760px) {
      .about-layout { grid-template-columns: 1fr; gap: 3rem; }
    }

    .about-photo {
      aspect-ratio: 3/4;
      background: var(--bg-card);
      border: 1px solid var(--border);
      border-radius: 8px;
      overflow: hidden;
      position: relative;
    }

    .about-photo-placeholder {
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: var(--font-mono);
      font-size: 0.7rem;
      color: var(--border-lit);
      letter-spacing: 0.1em;
      text-transform: uppercase;
    }

    .about-content h2 {
      font-family: var(--font-display);
      font-size: clamp(1.8rem, 3.5vw, 2.8rem);
      font-weight: 800;
      letter-spacing: -0.03em;
      line-height: 1.1;
      margin-bottom: 1.5rem;
    }

    .about-content p {
      font-size: 0.95rem;
      color: var(--muted);
      line-height: 1.9;
      margin-bottom: 1.25rem;
    }

    .about-content p strong {
      color: var(--text);
      font-weight: 500;
    }

    .skills-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 0.75rem;
      margin-top: 2rem;
    }

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

    .about-links {
      display: flex;
      gap: 1rem;
      flex-wrap: wrap;
      margin-top: 2rem;
    }

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

    footer p {
      font-family: var(--font-mono);
      font-size: 0.72rem;
      color: var(--muted);
      letter-spacing: 0.05em;
    }

    footer a {
      color: var(--muted);
      transition: color 0.2s;
    }
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

    .empty-state p {
      font-family: var(--font-mono);
      font-size: 0.8rem;
      color: var(--border-lit);
      letter-spacing: 0.06em;
    }

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
        <p class="section-sub">Things I've designed, built, and coded — organized by discipline.</p>

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

        <!-- ALL -->
        <div class="tab-panel project-grid active" id="tab-all">
          <!-- ═══ ADD YOUR PROJECTS BELOW — COPY THIS CARD BLOCK ═══ -->

          <!-- PROJECT CARD TEMPLATE:
          <article class="project-card">
            <div class="project-img">
              <img src="images/your-image.jpg" alt="Project Name" loading="lazy" />
              — OR if no image yet: —
              <div class="project-img-placeholder">[ image ]</div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-cad">CAD</span>   ← use tag-cad / tag-built / tag-code
                <span class="project-timeline">Jan 2024 – Mar 2024</span>
              </div>
              <h3 class="project-title">Your Project Title</h3>
              <p class="project-blurb">
                A short paragraph about what you built, why it mattered, and what role you played. 
                Keep it to 2–3 sentences so cards stay uniform.
              </p>
              <a class="project-link" href="#" target="_blank">View details →</a>
            </div>
          </article>
          -->

          <!-- SAMPLE — delete or replace these once you add real projects -->
          <article class="project-card">
            <div class="project-img">
              <div class="project-img-placeholder">[ image ]</div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-cad">CAD</span>
                <span class="project-timeline">Jan 2025 – Present</span>
              </div>
              <h3 class="project-title">Your First CAD Project</h3>
              <p class="project-blurb">
                Replace this with a real project. Describe the design problem, your approach, and what you delivered. Two or three sentences works well here.
              </p>
            </div>
          </article>

          <article class="project-card">
            <div class="project-img">
              <div class="project-img-placeholder">[ image ]</div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-built">Built</span>
                <span class="project-timeline">Sep 2024 – Dec 2024</span>
              </div>
              <h3 class="project-title">Your First Built Project</h3>
              <p class="project-blurb">
                Replace this with a real project. Describe what you fabricated or assembled, any challenges you solved, and the outcome.
              </p>
            </div>
          </article>

          <article class="project-card">
            <div class="project-img">
              <div class="project-img-placeholder">[ image ]</div>
            </div>
            <div class="project-body">
              <div class="project-meta">
                <span class="project-tag tag-code">Code</span>
                <span class="project-timeline">Mar 2024 – May 2024</span>
              </div>
              <h3 class="project-title">Your First Code Project</h3>
              <p class="project-blurb">
                Replace this with a real project. Name the languages/tools you used and what the software does or automates.
              </p>
              <a class="project-link" href="#" target="_blank">View on GitHub →</a>
            </div>
          </article>
          <!-- ═══════════════════════════════════════════════════════ -->
        </div>

        <!-- CAD -->
        <div class="tab-panel project-grid" id="tab-cad">
          <!-- Copy tag-cad cards here, or leave the empty state below -->
          <div class="empty-state">
            <p>// no CAD projects yet</p>
            <p>Copy a project-card block from the "All" tab and paste it here.</p>
          </div>
        </div>

        <!-- BUILT -->
        <div class="tab-panel project-grid" id="tab-built">
          <div class="empty-state">
            <p>// no built projects yet</p>
            <p>Copy a project-card block from the "All" tab and paste it here.</p>
          </div>
        </div>

        <!-- CODE -->
        <div class="tab-panel project-grid" id="tab-code">
          <div class="empty-state">
            <p>// no code projects yet</p>
            <p>Copy a project-card block from the "All" tab and paste it here.</p>
          </div>
        </div>

      </div><!-- /section -->
    </div>

  </div><!-- /page-projects -->


  <!-- ═══════════════════════════════════════════════════════════
       PAGE: ABOUT
  ═══════════════════════════════════════════════════════════ -->
  <div class="page" id="page-about">

    <div class="hero">
      <p class="hero-eyebrow">About Me</p>
      <h1>Engineer.<br/><span>Builder.</span></h1>
    </div>

    <div class="divider">
      <span class="divider-label">Background</span>
      <div class="divider-line"></div>
    </div>

    <div class="section">
      <div class="about-layout">

      <div class="about-photo">
        <img src="images/Headshot.png" alt="Haedyn Darling Hill" />
      </div>

        <div class="about-content">
          <h2>Haedyn<br/>Darling Hill</h2>

          <!-- ═══ EDIT THIS SECTION ═══ -->
          <p>
            <strong>Mechanical Engineering, student-athlete </strong> — I am persuing a Mechanical Engineering BS on track to graduate in 2028. Since 2020, I have gained experience in underwater ROVs, FRC and VEX robotics, full-system design, CAD and project design, MATLAB, Python, and biomechanical research.
          </p>
          <p>
            From 2019–2021, I worked on a <a href="https://20693798.fs1.hubspotusercontent-na1.net/hubfs/20693798/TechReportArchives/2021/Seattle%20Academy_Blueshift%20Robotics_Technical%20Documentation_2021.pdf" target="_blank" rel="noopener">MATE Underwater ROV team</a> team at Seattle Academy, designing an ROV for autonomous coral reef monitoring. Commercially available ESCs didn't meet our control requirements, so I designed and integrated a custom one from scratch. The team placed top-10 at the 2021 World Championships. I also contributed to the FRC team's electrical division, collaborating with mechanical to produce competition-ready component housings.
            After transferring schools, I founded a VEX robotics team from the ground up: building the curriculum, leading three subteams, and running an internal competition model by end of year one.
            My junior and senior years, I participated in an invite-only research program in partnership with a Sikorsky Lockheed Martin engineer. Working on the X2 helicopter's main gearbox, I designed an electrical transmission system using back-EMF to reduce the vibrational instability inherent in the aircraft's mechanical drivetrain at high speeds and demonstrated proof-of-concept viability at scale.
          </p>
          <p>
          Both university summers have been spent in technical roles outside the classroom.
          After freshman year, I interned at Synthesia.io on the R&D team, contributing to AI model design with a focus on improving the naturalism of synthesized speech and image output.
          After sophomore year, I was awarded the largest undergraduate research grant available at my institution to study the relationship between inter-limb hip asymmetry and musculoskeletal pain — applying biomechanical analysis to a clinical research context.
          </p>

          <p>
            I play as a fullback/wing for Boston University's Women's Rugby team! Team commitments take upwards of 10-15 hours per week, and I love every minute of it. I have been an athlete in various sports for the better of 8 years, and it has made me who I am. Sports, and rugby in particular, have taught me to be resiliant, hard working, and collaborative. Playing on the rugby team makes me a better engineer every day.
          </p>
          <!-- ════════════════════════ -->

          <div class="skills-grid">
            <!-- ═══ EDIT THESE SKILLS ═══ -->
            <span class="skill-item">SolidWorks</span>
            <span class="skill-item">Fusion 360</span>
            <span class="skill-item">Python</span>
            <span class="skill-item">MATLAB</span>
            <span class="skill-item">FDM / SLA printing</span>
            <span class="skill-item">PCB Design</span>
            <span class="skill-item">C / C++</span>
            <span class="skill-item">Arduino / RPi</span>
            <!-- Add or remove as needed -->
          </div>

          <div class="about-links">
            <a class="btn btn-primary" href="mailto:your@email.com">Get in touch</a>
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
      <a href="mailto:your@email.com">Email</a>
    </p>
  </footer>

  <script>
    // ── Page switching ───────────────────────────────────────
    function showPage(name) {
      document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
      document.querySelectorAll('.nav-links a').forEach(a => a.classList.remove('active'));

      document.getElementById('page-' + name).classList.add('active');
      document.getElementById('nav-' + name).classList.add('active');
      window.scrollTo({ top: 0, behavior: 'smooth' });
      return false;
    }

    // ── Tab switching ────────────────────────────────────────
    function switchTab(tab) {
      document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
      document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));

      document.querySelector(`[data-tab="${tab}"]`).classList.add('active');
      document.getElementById('tab-' + tab).classList.add('active');
    }

    // Prevent default on nav links
    document.querySelectorAll('.nav-links a[onclick]').forEach(a => {
      a.addEventListener('click', e => e.preventDefault());
    });
  </script>
</body>
</html>