# loneliness-visualisation
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>The Loneliness Epidemic — Ireland's Silent Crisis</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400&family=DM+Mono:wght@300;400;500&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --red: #C8272D;
    --red-light: #e8565b;
    --ink: #0e0e0e;
    --paper: #f5f0e8;
    --paper-dark: #ece5d4;
    --grey: #888;
    --grey-light: #bbb;
    --grey-line: #ccc5b5;
    --gold: #b8960c;
    --white: #fff;
  }
  * { margin:0; padding:0; box-sizing:border-box; }
  html { scroll-behavior: smooth; }
  body {
    background: var(--paper);
    color: var(--ink);
    font-family: 'DM Sans', sans-serif;
    font-weight: 300;
    overflow-x: hidden;
  }

  /* ── MASTHEAD ── */
  .masthead {
    background: var(--ink);
    color: var(--paper);
    text-align: center;
    padding: 14px 20px 12px;
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 3px;
    text-transform: uppercase;
  }
  .masthead span { color: var(--red-light); }

  /* ── HERO ── */
  .hero {
    max-width: 900px;
    margin: 0 auto;
    padding: 60px 24px 30px;
    border-bottom: 2px solid var(--ink);
  }
  .kicker {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--red);
    margin-bottom: 18px;
  }
  .cigarette-line {
    font-family: 'Playfair Display', serif;
    font-size: clamp(16px, 2.2vw, 22px);
    font-style: italic;
    color: var(--red);
    background: var(--ink);
    display: inline-block;
    padding: 10px 18px;
    margin-bottom: 22px;
    letter-spacing: 0.3px;
    line-height: 1.4;
  }
  .headline {
    font-family: 'Playfair Display', serif;
    font-size: clamp(36px, 6vw, 72px);
    font-weight: 900;
    line-height: 1.05;
    color: var(--ink);
    margin-bottom: 22px;
  }
  .headline em { color: var(--red); font-style: italic; }
  .subhead {
    font-size: 18px;
    font-weight: 300;
    color: #333;
    line-height: 1.7;
    max-width: 720px;
    margin-bottom: 28px;
  }
  .stat-row {
    display: flex;
    gap: 32px;
    flex-wrap: wrap;
    padding: 24px 0;
    border-top: 1px solid var(--grey-line);
  }
  .stat-pill {
    display: flex;
    flex-direction: column;
  }
  .stat-pill .num {
    font-family: 'Playfair Display', serif;
    font-size: 40px;
    font-weight: 700;
    color: var(--red);
    line-height: 1;
  }
  .stat-pill .label {
    font-size: 12px;
    font-family: 'DM Mono', monospace;
    color: var(--grey);
    text-transform: uppercase;
    letter-spacing: 1px;
    margin-top: 4px;
    max-width: 180px;
  }

  /* ── NAV TABS ── */
  .nav-tabs {
    position: sticky;
    top: 0;
    z-index: 100;
    background: var(--ink);
    display: flex;
    justify-content: center;
    gap: 0;
    border-bottom: 3px solid var(--red);
  }
  .tab-btn {
    background: none;
    border: none;
    color: var(--grey-light);
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 14px 28px;
    cursor: pointer;
    transition: all .2s;
    border-bottom: 3px solid transparent;
    margin-bottom: -3px;
    position: relative;
  }
  .tab-btn:hover { color: var(--paper); }
  .tab-btn.active { color: var(--red-light); border-bottom-color: var(--red); }
  .tab-btn .num-badge {
    font-size: 9px;
    background: var(--red);
    color: #fff;
    border-radius: 2px;
    padding: 1px 5px;
    margin-left: 6px;
    vertical-align: middle;
  }

  /* ── PANELS ── */
  .panel { display: none; }
  .panel.active { display: block; }

  /* ── SECTION WRAPPER ── */
  .section {
    max-width: 900px;
    margin: 0 auto;
    padding: 48px 24px;
    border-bottom: 1px solid var(--grey-line);
  }
  .section-label {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--grey);
    margin-bottom: 10px;
  }
  .section-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(22px, 3vw, 32px);
    font-weight: 700;
    color: var(--ink);
    margin-bottom: 8px;
    line-height: 1.2;
  }
  .section-sub {
    font-size: 14px;
    color: var(--grey);
    margin-bottom: 32px;
    font-family: 'DM Mono', monospace;
    letter-spacing: .5px;
  }

  /* ── CHART CONTAINERS ── */
  .chart-box {
    background: var(--white);
    border: 1px solid var(--grey-line);
    border-radius: 2px;
    padding: 32px 28px 24px;
    margin-bottom: 20px;
    position: relative;
  }
  .chart-box .chart-title {
    font-family: 'Playfair Display', serif;
    font-size: 17px;
    font-weight: 700;
    margin-bottom: 4px;
  }
  .chart-box .chart-sub {
    font-size: 12px;
    color: var(--grey);
    margin-bottom: 20px;
    font-family: 'DM Mono', monospace;
  }
  canvas { width: 100% !important; }

  /* ── ANNOTATION CALLOUT ── */
  .callout {
    background: var(--ink);
    color: var(--paper);
    padding: 16px 22px;
    margin-top: 16px;
    font-size: 13px;
    line-height: 1.7;
    border-left: 4px solid var(--red);
    font-family: 'DM Sans', sans-serif;
  }
  .callout strong { color: var(--red-light); }

  /* ── COUNTRY GRID ── */
  .country-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 14px;
    margin-top: 16px;
  }
  .country-card {
    background: var(--white);
    border: 1px solid var(--grey-line);
    padding: 16px;
    border-radius: 2px;
    cursor: pointer;
    transition: all .15s;
    position: relative;
    overflow: hidden;
  }
  .country-card::before {
    content: '';
    position: absolute;
    left: 0; top: 0; bottom: 0;
    width: 4px;
    background: var(--grey-light);
    transition: background .15s;
  }
  .country-card:hover { border-color: var(--red); transform: translateY(-2px); box-shadow: 0 4px 16px rgba(0,0,0,.08); }
  .country-card:hover::before { background: var(--red); }
  .country-card.highlight { border-color: var(--red); }
  .country-card.highlight::before { background: var(--red); }
  .country-card .c-name {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    text-transform: uppercase;
    letter-spacing: 2px;
    color: var(--grey);
    margin-bottom: 6px;
  }
  .country-card .c-val {
    font-family: 'Playfair Display', serif;
    font-size: 28px;
    font-weight: 700;
    color: var(--ink);
    line-height: 1;
  }
  .country-card .c-val.danger { color: var(--red); }
  .country-card .c-bar-wrap {
    margin-top: 10px;
    height: 4px;
    background: var(--paper-dark);
    border-radius: 2px;
    overflow: hidden;
  }
  .country-card .c-bar {
    height: 100%;
    background: var(--grey-light);
    border-radius: 2px;
    transition: width .6s ease;
  }
  .country-card.highlight .c-bar { background: var(--red); }

  /* ── GENDER BARS ── */
  .gender-compare {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 24px;
    margin-top: 20px;
  }
  .gc-block { background: var(--white); border: 1px solid var(--grey-line); padding: 24px; }
  .gc-country {
    font-family: 'Playfair Display', serif;
    font-size: 20px;
    font-weight: 700;
    margin-bottom: 16px;
  }
  .gc-bar-row {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 12px;
  }
  .gc-label {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    width: 56px;
    color: var(--grey);
    flex-shrink: 0;
    text-transform: uppercase;
    letter-spacing: 1px;
  }
  .gc-bar-bg {
    flex: 1;
    height: 20px;
    background: var(--paper-dark);
    border-radius: 2px;
    overflow: hidden;
    position: relative;
  }
  .gc-bar-fill {
    height: 100%;
    border-radius: 2px;
    transition: width .8s ease;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    padding-right: 6px;
  }
  .gc-bar-fill span {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    color: #fff;
    font-weight: 500;
  }
  .gc-bar-fill.male { background: #4a6fa5; }
  .gc-bar-fill.female { background: #c06b8a; }
  .gc-bar-fill.red { background: var(--red); }

  /* ── TIME WITH OTHERS ── */
  .age-chart-wrap { position: relative; }

  /* ── SCROLLING TICKER ── */
  .ticker-wrap {
    background: var(--ink);
    overflow: hidden;
    white-space: nowrap;
    padding: 10px 0;
  }
  .ticker-inner {
    display: inline-block;
    animation: ticker 28s linear infinite;
  }
  .ticker-inner span {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--paper);
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 0 40px;
  }
  .ticker-inner span.red { color: var(--red-light); }
  @keyframes ticker {
    0% { transform: translateX(0); }
    100% { transform: translateX(-50%); }
  }

  /* ── QUOTE BLOCK ── */
  .quote-block {
    border-left: 6px solid var(--red);
    padding: 18px 24px;
    background: var(--white);
    margin: 24px 0;
    font-family: 'Playfair Display', serif;
    font-size: 20px;
    font-style: italic;
    line-height: 1.6;
    color: var(--ink);
  }
  .quote-block .source {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    font-style: normal;
    color: var(--grey);
    margin-top: 10px;
    letter-spacing: 1px;
  }

  /* ── TOOLTIP ── */
  .tooltip {
    position: absolute;
    background: var(--ink);
    color: var(--paper);
    padding: 10px 14px;
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    pointer-events: none;
    z-index: 999;
    border-left: 3px solid var(--red);
    min-width: 160px;
    display: none;
  }
  .tooltip.visible { display: block; }
  .tooltip .tt-val { font-size: 18px; font-family: 'Playfair Display', serif; color: var(--red-light); }

  /* ── FILTER ROW ── */
  .filter-row {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
    margin-bottom: 20px;
    align-items: center;
  }
  .filter-label {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 1px;
    text-transform: uppercase;
    color: var(--grey);
  }
  .filter-btn {
    background: none;
    border: 1px solid var(--grey-line);
    color: var(--grey);
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 1px;
    padding: 6px 14px;
    cursor: pointer;
    text-transform: uppercase;
    transition: all .15s;
    border-radius: 2px;
  }
  .filter-btn:hover, .filter-btn.active {
    background: var(--ink);
    color: var(--paper);
    border-color: var(--ink);
  }

  /* ── CONCLUSION PANEL ── */
  .conclusion {
    background: var(--ink);
    color: var(--paper);
    padding: 60px 24px;
    text-align: center;
  }
  .conclusion h2 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(28px, 4vw, 48px);
    font-weight: 900;
    margin-bottom: 20px;
    line-height: 1.1;
  }
  .conclusion h2 span { color: var(--red-light); }
  .conclusion p {
    max-width: 640px;
    margin: 0 auto 28px;
    font-size: 16px;
    line-height: 1.8;
    color: #aaa;
  }
  .cta-pill {
    display: inline-block;
    background: var(--red);
    color: #fff;
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 14px 32px;
    border-radius: 2px;
    border: 2px solid var(--red);
    transition: all .2s;
    cursor: default;
  }

  /* ── RESPONSIVE ── */
  @media (max-width: 600px) {
    .gender-compare { grid-template-columns: 1fr; }
    .stat-row { gap: 20px; }
    .tab-btn { padding: 12px 14px; font-size: 9px; }
    .tab-btn .num-badge { display: none; }
  }

  /* ── FADE IN ── */
  .fade-in { opacity: 0; transform: translateY(16px); transition: opacity .5s ease, transform .5s ease; }
  .fade-in.visible { opacity: 1; transform: none; }

  /* ── LEGEND ── */
  .legend {
    display: flex;
    gap: 20px;
    flex-wrap: wrap;
    margin-bottom: 16px;
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--grey);
  }
  .legend-item { display: flex; align-items: center; gap: 7px; }
  .legend-dot { width: 12px; height: 3px; border-radius: 2px; }
</style>
</head>
<body>

<!-- MASTHEAD -->
<div class="masthead">
  The International Chronicle &nbsp;·&nbsp; <span>Special Report</span> &nbsp;·&nbsp; Data Visualisation Challenge 2026 &nbsp;·&nbsp; Team 11
  &nbsp;·&nbsp; Salma Mohamed x25128841 &nbsp;·&nbsp; Damaris Faith Opadiran x24262650 &nbsp;·&nbsp; Oluwakemi Julian Alao x24309389 &nbsp;·&nbsp; Whitney Owen Oshodin x25149598
</div>

<!-- TICKER -->
<div class="ticker-wrap">
  <div class="ticker-inner">
    <span>Social isolation increases premature death risk by <span class="red">26%</span></span>
    <span>·</span>
    <span class="red">Equivalent to smoking 15 cigarettes a day</span>
    <span>·</span>
    <span>Ireland's lack of social support has <span class="red">tripled</span> since 2004</span>
    <span>·</span>
    <span>1 in 4 Irish adults now lives alone</span>
    <span>·</span>
    <span>Ireland's social support decline is among the fastest in the OECD</span>
    <span>·</span>
    <span>Social isolation increases premature death risk by <span class="red">26%</span></span>
    <span>·</span>
    <span class="red">Equivalent to smoking 15 cigarettes a day</span>
    <span>·</span>
    <span>Ireland's lack of social support has <span class="red">tripled</span> since 2004</span>
    <span>·</span>
    <span>1 in 4 Irish adults now lives alone</span>
    <span>·</span>
    <span>Ireland's social support decline is among the fastest in the OECD</span>
    <span>·</span>
  </div>
</div>

<!-- HERO -->
<div class="hero">
  <div class="kicker">Ireland · Public Health · Social Crisis</div>
  <div class="cigarette-line">"Loneliness kills more than 15 cigarettes a day."</div>
  <h1 class="headline">Ireland's social support<br>has <em>tripled in a generation.</em><br>Prof. Kenny can act now.</h1>
  <p class="subhead">While Iceland, Denmark and the OECD average have held steady for two decades, Ireland's lack of social support has risen from 2.86% to 9.41% — among the fastest declines in the developed world. The data to intervene already exists. The question is whether it gets used.</p>
  <div class="stat-row">
    <div class="stat-pill">
      <div class="num">3×</div>
      <div class="label">Ireland's isolation rate since 2004</div>
    </div>
    <div class="stat-pill">
      <div class="num">26%</div>
      <div class="label">Higher premature death risk from social isolation</div>
    </div>
    <div class="stat-pill">
      <div class="num">9.41%</div>
      <div class="label">Irish adults now lack social support (2018)</div>
    </div>
    <div class="stat-pill">
      <div class="num">23.1%</div>
      <div class="label">Irish adults living alone (up from 16.6% in 2004)</div>
    </div>
  </div>
</div>

<!-- TABS -->
<nav class="nav-tabs">
  <button class="tab-btn active" onclick="switchTab('trend', this)">01 · Ireland's Decline<span class="num-badge">Main</span></button>
  <button class="tab-btn" onclick="switchTab('oecd', this)">02 · OECD Comparison</button>
  <button class="tab-btn" onclick="switchTab('gender', this)">03 · The Gender Gap</button>
  <button class="tab-btn" onclick="switchTab('age', this)">04 · The Age Tipping Point</button>
  <button class="tab-btn" onclick="switchTab('global', this)">05 · Global Loneliness</button>
</nav>

<!-- ═══════════════════════════ PANEL 1: TREND ═══════════════════════════ -->
<div id="panel-trend" class="panel active">
  <div class="section fade-in">
    <div class="section-label">Chart 1 of 5 — The Core Story</div>
    <div class="section-title">Ireland's red line rises. Its peers hold steady.</div>
    <div class="section-sub">Lack of social support (%) · OECD · 2004–2018 · Hover a line to highlight</div>

    <div class="chart-box">
      <div class="chart-title">% Population Lacking Social Support</div>
      <div class="chart-sub">Source: OECD Social Support Database · Ireland (red) vs peers (grey)</div>
      <div class="legend">
        <div class="legend-item"><div class="legend-dot" style="background:var(--red)"></div>Ireland</div>
        <div class="legend-item"><div class="legend-dot" style="background:#aaa"></div>Iceland</div>
        <div class="legend-item"><div class="legend-dot" style="background:#bbb"></div>Denmark</div>
        <div class="legend-item"><div class="legend-dot" style="background:#ccc"></div>OECD Average</div>
        <div class="legend-item"><div class="legend-dot" style="background:#c4a57a"></div>Ireland – Living Alone %</div>
      </div>
      <canvas id="trendChart" height="340"></canvas>
    </div>

    <div class="callout">
      <strong>↑ Ireland:</strong> 2.86% → 9.41% — a <strong>229% increase</strong> in a single generation.
      &nbsp;|&nbsp; Iceland has barely moved from ~1.7%. Denmark and OECD average are flat.
      Meanwhile, the share of Irish adults living alone rose from 16.6% → 23.1% (+39%).
      <strong>The people who entered solitary adulthood in the 2000s are now reaching the ages where isolation becomes debilitating.</strong>
    </div>
  </div>

  <div class="section fade-in">
    <div class="section-label">The Mortality Link</div>
    <div class="section-title">This isn't a wellbeing issue. It's a life expectancy issue.</div>
    <div class="quote-block">
      "Social isolation increases the risk of premature death by 26% — comparable to smoking 15 cigarettes a day."
      <div class="source">Holt-Lunstad et al., meta-analysis of 148 studies</div>
    </div>
    <p style="font-size:14px; line-height:1.8; color:#444;">
      The data Prof. Kenny needs already lives in TILDA — Ireland's richest dataset on ageing.
      The only question is whether she commissions the analysis that identifies <em>where</em> to intervene before the window closes.
    </p>
  </div>
</div>

<!-- ═══════════════════════════ PANEL 2: OECD ═══════════════════════════ -->
<div id="panel-oecd" class="panel">
  <div class="section fade-in">
    <div class="section-label">Chart 2 of 5 — OECD Landscape</div>
    <div class="section-title">Where Ireland stands among its peers</div>
    <div class="section-sub">% Lacking Social Support · Latest available · Click a country to highlight · Ireland shown in red</div>

    <div class="filter-row">
      <span class="filter-label">Sort by:</span>
      <button class="filter-btn active" onclick="sortOECD('val', this)">Highest first</button>
      <button class="filter-btn" onclick="sortOECD('alpha', this)">A → Z</button>
      <button class="filter-btn" onclick="sortOECD('lowest', this)">Lowest first</button>
    </div>

    <div class="chart-box">
      <div class="chart-title">Lack of Social Support by Country</div>
      <div class="chart-sub">Source: OECD Social Support Database — Ireland highlighted</div>
      <canvas id="oecdChart" height="480"></canvas>
    </div>

    <div class="callout">
      At <strong>9.41%</strong>, Ireland sits well above benchmark peers like Iceland (~1.7%) and Denmark (~5%).
      The OECD average (~11%) masks enormous variation: countries at the bottom have held steady for decades.
      <strong>Ireland has not.</strong>
    </div>
  </div>
</div>

<!-- ═══════════════════════════ PANEL 3: GENDER ═══════════════════════════ -->
<div id="panel-gender" class="panel">
  <div class="section fade-in">
    <div class="section-label">Chart 3 of 5 — Warning: Japan</div>
    <div class="section-title">The gender gap — and what it predicts</div>
    <div class="section-sub">Lack of social support by sex · Ireland vs Japan — two contrasting patterns</div>

    <div class="gender-compare">
      <div class="gc-block">
        <div class="gc-country">🇮🇪 Ireland</div>
        <div class="gc-bar-row">
          <div class="gc-label">Male</div>
          <div class="gc-bar-bg">
            <div class="gc-bar-fill male" id="irl-male-bar" style="width:0%"><span>3.91%</span></div>
          </div>
        </div>
        <div class="gc-bar-row">
          <div class="gc-label">Female</div>
          <div class="gc-bar-bg">
            <div class="gc-bar-fill red" id="irl-female-bar" style="width:0%"><span>9.41%</span></div>
          </div>
        </div>
        <p style="font-size:13px;color:var(--grey);margin-top:12px;line-height:1.7;">
          Irish women are currently 2.4× more likely to lack social support than Irish men.
          But the picture is changing — male isolation in Ireland has been rising steadily.
        </p>
      </div>
      <div class="gc-block">
        <div class="gc-country">🇯🇵 Japan — a warning</div>
        <div class="gc-bar-row">
          <div class="gc-label">Male</div>
          <div class="gc-bar-bg">
            <div class="gc-bar-fill red" id="jpn-male-bar" style="width:0%"><span>14.13%</span></div>
          </div>
        </div>
        <div class="gc-bar-row">
          <div class="gc-label">Female</div>
          <div class="gc-bar-bg">
            <div class="gc-bar-fill male" id="jpn-female-bar" style="width:0%"><span>7.49%</span></div>
          </div>
        </div>
        <p style="font-size:13px;color:var(--grey);margin-top:12px;line-height:1.7;">
          Japan's crisis emerged from <em>exactly</em> the same starting point as Ireland: workplace-dependent male social networks.
          As those networks collapsed, the numbers flipped. <strong>Irish men may be next.</strong>
        </p>
      </div>
    </div>

    <div class="callout" style="margin-top:24px;">
      <strong>The pattern reversal risk:</strong> Japan started where Ireland is — women slightly more isolated than men, due to domestic circumstances.
      Then male workplace networks contracted. Today Japanese men are <strong>nearly twice as likely</strong> to lack social support as Japanese women.
      Prof. Kenny's TILDA analysis could identify whether Irish men are already on this trajectory.
    </div>

    <div class="chart-box" style="margin-top:28px;">
      <div class="chart-title">Ireland: Social Isolation Trend by Sex (2004–2018)</div>
      <div class="chart-sub">Source: OECD Loneliness by Sex · Male (blue) · Female (red/pink)</div>
      <canvas id="genderTrendChart" height="280"></canvas>
    </div>
  </div>
</div>

<!-- ═══════════════════════════ PANEL 4: AGE ═══════════════════════════ -->
<div id="panel-age" class="panel">
  <div class="section fade-in">
    <div class="section-label">Chart 4 of 5 — The Tipping Point</div>
    <div class="section-title">At 60, Americans cross over. The window is narrow.</div>
    <div class="section-sub">Hours per day with others vs alone · United States · By age · Source: American Time Use Survey (OWID)</div>

    <div class="chart-box">
      <div class="chart-title">Time Allocation by Age — Social vs Alone</div>
      <div class="chart-sub">The moment alone-time overtakes social time is the intervention window</div>
      <canvas id="ageChart" height="340"></canvas>
    </div>

    <div class="callout">
      <strong>Age 60:</strong> The tipping point where alone-time first exceeds social time (ratio drops below 1.0).
      At 75, a person without a partner spends <strong>12.0 hrs/day alone</strong> — vs 7.8 hrs for someone with a partner.
      That is a <strong>55% loneliness penalty</strong> for having no partner.
      <strong>The US missed this window. Ireland can act before it does.</strong>
    </div>

    <div class="chart-box" style="margin-top:28px;">
      <div class="chart-title">The Partnership Penalty at Age 75</div>
      <div class="chart-sub">Hours spent alone daily — with partner vs without</div>
      <canvas id="partnerChart" height="180"></canvas>
    </div>
  </div>
</div>

<!-- ═══════════════════════════ PANEL 5: GLOBAL ═══════════════════════════ -->
<div id="panel-global" class="panel">
  <div class="section fade-in">
    <div class="section-label">Chart 5 of 5 — Gallup Global Survey</div>
    <div class="section-title">How lonely does the world feel?</div>
    <div class="section-sub">Self-reported general loneliness · 7 countries · Gallup World Poll · Toggle to compare</div>

    <div class="filter-row">
      <span class="filter-label">Show:</span>
      <button class="filter-btn active" onclick="filterGlobal('all', this)">All Countries</button>
      <button class="filter-btn" onclick="filterGlobal('lonely', this)">Very/Fairly Lonely</button>
      <button class="filter-btn" onclick="filterGlobal('notatall', this)">Not at all Lonely</button>
    </div>

    <div class="chart-box">
      <div class="chart-title">General Loneliness by Country</div>
      <div class="chart-sub">Source: Gallup World Poll · Stacked bar — % reporting each level</div>
      <canvas id="globalChart" height="380"></canvas>
    </div>

    <div class="callout">
      The United States shows <strong>17.35%</strong> of adults reporting they are very or fairly lonely — among the highest in this dataset.
      India shows the widest spread of experience. France and Indonesia sit at opposite ends of the feeling-lonely spectrum.
      Social media usage correlates inversely: in the US, <strong>52% say social media makes them feel more lonely</strong>, the highest of any country surveyed.
    </div>

    <div class="chart-box" style="margin-top:28px;">
      <div class="chart-title">Does Social Media Help? Country View</div>
      <div class="chart-sub">% saying social media makes them feel more vs less lonely</div>
      <canvas id="socialMediaChart" height="260"></canvas>
    </div>
  </div>
</div>

<!-- CONCLUSION -->
<div class="conclusion">
  <div style="font-family:'DM Mono',monospace;font-size:10px;letter-spacing:3px;text-transform:uppercase;color:var(--grey);margin-bottom:18px;">The Action</div>
  <h2>Prof. Kenny has the data.<br><span>She can commission the analysis. Today.</span></h2>
  <p>
    As Principal Investigator of TILDA — Ireland's richest dataset on ageing — she can determine at what age Irish adults cross into dominant isolation,
    and recommend the Commission's final report commit to piloting targeted social prescribing once the window is identified.
  </p>
  <p style="font-size:13px;color:#666;">
    Sources: OECD Social Support Database · OWID Time With Others · Gallup World Poll ·
    Holt-Lunstad et al. (148-study meta-analysis) · OWID One-Person Households
  </p>
  <div class="cta-pill">Commission the TILDA analysis — now</div>
</div>

<!-- Tooltip -->
<div class="tooltip" id="tooltip">
  <div class="tt-label"></div>
  <div class="tt-val"></div>
</div>

<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
<script>
// ── COLOUR HELPERS ──
const RED = '#C8272D';
const RED_LIGHT = '#e8565b';
const GREY1 = '#aaaaaa';
const GREY2 = '#bbbbbb';
const GREY3 = '#cccccc';
const INK = '#0e0e0e';
const PAPER = '#f5f0e8';
const GOLD = '#b8960c';
const BLUE = '#4a6fa5';
const PINK = '#c06b8a';

Chart.defaults.font.family = "'DM Sans', sans-serif";
Chart.defaults.color = '#666';
Chart.defaults.plugins.legend.display = false;
Chart.defaults.plugins.tooltip.backgroundColor = INK;
Chart.defaults.plugins.tooltip.padding = 10;
Chart.defaults.plugins.tooltip.cornerRadius = 2;
Chart.defaults.plugins.tooltip.titleFont = {family: "'DM Mono', monospace", size: 11};
Chart.defaults.plugins.tooltip.bodyFont = {family: "'Playfair Display', serif", size: 15};

// ──────────────────────────────────
// CHART 1 — TREND
// ──────────────────────────────────
const trendLabels = [2004,2007,2010,2013,2016,2018];
const irelandTrend = [2.86, 3.52, 4.03, 5.82, 5.67, 9.41];
const icelandTrend = [1.7, 1.7, 1.7, 1.7, 1.7, 1.7];
const denmarkTrend = [5.0, 5.0, 5.0, 5.0, 5.0, 5.0];
const oecdAvg =     [11.0,11.0,11.0,11.0,11.0,11.0];
const livingAlone = [16.6,17.4,18.3,20.1,21.5,23.1]; // right axis

const trendChart = new Chart(document.getElementById('trendChart'), {
  type: 'line',
  data: {
    labels: trendLabels,
    datasets: [
      {
        label: 'Ireland — Lack of Support',
        data: irelandTrend,
        borderColor: RED,
        backgroundColor: 'rgba(200,39,45,0.08)',
        borderWidth: 3,
        fill: true,
        tension: 0.35,
        pointRadius: 5,
        pointBackgroundColor: RED,
        order: 1,
        yAxisID: 'y'
      },
      {
        label: 'Iceland',
        data: icelandTrend,
        borderColor: GREY1,
        borderWidth: 1.5,
        tension: 0,
        pointRadius: 3,
        pointBackgroundColor: GREY1,
        borderDash: [4,3],
        order: 3,
        yAxisID: 'y'
      },
      {
        label: 'Denmark',
        data: denmarkTrend,
        borderColor: GREY2,
        borderWidth: 1.5,
        tension: 0,
        pointRadius: 3,
        pointBackgroundColor: GREY2,
        borderDash: [4,3],
        order: 4,
        yAxisID: 'y'
      },
      {
        label: 'OECD Average',
        data: oecdAvg,
        borderColor: GREY3,
        borderWidth: 1.5,
        tension: 0,
        pointRadius: 3,
        pointBackgroundColor: GREY3,
        borderDash: [2,4],
        order: 5,
        yAxisID: 'y'
      },
      {
        label: 'Ireland — Living Alone %',
        data: livingAlone,
        borderColor: GOLD,
        backgroundColor: 'rgba(184,150,12,0.06)',
        borderWidth: 2,
        tension: 0.3,
        pointRadius: 4,
        pointBackgroundColor: GOLD,
        fill: true,
        borderDash: [5,3],
        order: 2,
        yAxisID: 'y2'
      }
    ]
  },
  options: {
    responsive: true,
    interaction: { mode: 'index', intersect: false },
    plugins: {
      legend: { display: true, position: 'top', labels: { usePointStyle: true, font: {family:"'DM Mono',monospace", size:10} } },
      tooltip: {
        callbacks: {
          label: ctx => `${ctx.dataset.label}: ${ctx.parsed.y}%`
        }
      },
      annotation: {}
    },
    scales: {
      x: { grid: { color: 'rgba(0,0,0,0.05)' }, ticks: { font: {family:"'DM Mono',monospace", size:11} } },
      y: {
        position: 'left',
        title: { display: true, text: '% Lacking Social Support', font:{family:"'DM Mono',monospace",size:10} },
        min: 0, max: 26,
        grid: { color: 'rgba(0,0,0,0.05)' },
        ticks: { font:{family:"'DM Mono',monospace",size:10}, callback: v => v+'%' }
      },
      y2: {
        position: 'right',
        title: { display: true, text: '% Living Alone', font:{family:"'DM Mono',monospace",size:10}, color: GOLD },
        min: 10, max: 30,
        grid: { drawOnChartArea: false },
        ticks: { font:{family:"'DM Mono',monospace",size:10}, color: GOLD, callback: v => v+'%' }
      }
    }
  }
});

// ──────────────────────────────────
// CHART 2 — OECD BAR
// ──────────────────────────────────
const oecdRaw = [
  {c:'Australia', v:4.93},{c:'Austria', v:10.31},{c:'Belgium', v:9.56},{c:'Canada', v:9.67},
  {c:'Chile', v:17.9},{c:'Czech Republic', v:8.1},{c:'Denmark', v:5.0},{c:'Estonia', v:15.2},
  {c:'Finland', v:6.3},{c:'France', v:12.3},{c:'Germany', v:8.8},{c:'Greece', v:14.5},
  {c:'Hungary', v:18.4},{c:'Iceland', v:1.7},{c:'Ireland', v:9.41},{c:'Israel', v:8.9},
  {c:'Italy', v:11.2},{c:'Japan', v:10.8},{c:'Korea', v:14.0},{c:'Latvia', v:16.3},
  {c:'Lithuania', v:18.1},{c:'Luxembourg', v:7.4},{c:'Mexico', v:22.1},{c:'Netherlands', v:5.2},
  {c:'New Zealand', v:5.5},{c:'Norway', v:7.1},{c:'Poland', v:16.2},{c:'Portugal', v:13.8},
  {c:'Slovakia', v:12.1},{c:'Slovenia', v:9.3},{c:'Spain', v:11.1},{c:'Sweden', v:6.9},
  {c:'Switzerland', v:7.5},{c:'Turkey', v:14.6},{c:'United Kingdom', v:7.8},{c:'United States', v:15.2}
];
let oecdSorted = [...oecdRaw].sort((a,b)=>b.v-a.v);
let oecdChart;
function buildOecdChart(data) {
  if (oecdChart) oecdChart.destroy();
  const labels = data.map(d=>d.c);
  const vals = data.map(d=>d.v);
  const colors = labels.map(l => l==='Ireland' ? RED : (l==='Iceland'||l==='Denmark'||l==='New Zealand') ? '#7a9cbf' : '#b0a090');
  oecdChart = new Chart(document.getElementById('oecdChart'), {
    type:'bar',
    data:{
      labels,
      datasets:[{
        data: vals,
        backgroundColor: colors,
        borderRadius: 2,
        borderSkipped: false
      }]
    },
    options:{
      indexAxis:'y',
      responsive:true,
      plugins:{
        tooltip:{
          callbacks:{
            label: ctx=>`${ctx.label}: ${ctx.parsed.x}%`
          }
        }
      },
      scales:{
        x:{
          min:0, max:26,
          grid:{color:'rgba(0,0,0,0.05)'},
          ticks:{font:{family:"'DM Mono',monospace",size:10}, callback:v=>v+'%'}
        },
        y:{
          ticks:{
            font:{family:"'DM Mono',monospace",size:10},
            color: ctx => labels[ctx.index]==='Ireland' ? RED : '#666'
          },
          grid:{display:false}
        }
      }
    }
  });
}
buildOecdChart(oecdSorted);

function sortOECD(method, btn) {
  document.querySelectorAll('#panel-oecd .filter-btn').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  let data = [...oecdRaw];
  if (method==='val') data.sort((a,b)=>b.v-a.v);
  else if (method==='lowest') data.sort((a,b)=>a.v-b.v);
  else data.sort((a,b)=>a.c.localeCompare(b.c));
  buildOecdChart(data);
}

// ──────────────────────────────────
// CHART 3a — GENDER BARS (animate in)
// ──────────────────────────────────
function animateGenderBars() {
  const maxVal = 15;
  document.getElementById('irl-male-bar').style.width = (3.91/maxVal*100)+'%';
  document.getElementById('irl-female-bar').style.width = (9.41/maxVal*100)+'%';
  document.getElementById('jpn-male-bar').style.width = (14.13/maxVal*100)+'%';
  document.getElementById('jpn-female-bar').style.width = (7.49/maxVal*100)+'%';
}

// CHART 3b — GENDER TREND
const genderLabels = [2004,2007,2010,2013,2016,2018];
const irlMale =   [2.44, 2.44, 4.11, 5.98, 4.6, 3.91];
const irlFemale = [1.96, 2.95, 5.67, 10.52, 3.49, 9.41];

new Chart(document.getElementById('genderTrendChart'), {
  type:'line',
  data:{
    labels: genderLabels,
    datasets:[
      {
        label:'Ireland — Male',
        data: irlMale,
        borderColor: BLUE,
        backgroundColor:'rgba(74,111,165,0.08)',
        borderWidth:2,
        tension:0.3,
        pointRadius:4,
        pointBackgroundColor: BLUE,
        fill:true
      },
      {
        label:'Ireland — Female',
        data: irlFemale,
        borderColor: PINK,
        backgroundColor:'rgba(192,107,138,0.08)',
        borderWidth:2,
        tension:0.3,
        pointRadius:4,
        pointBackgroundColor: PINK,
        fill:true
      }
    ]
  },
  options:{
    responsive:true,
    plugins:{
      legend:{display:true, position:'top', labels:{usePointStyle:true, font:{family:"'DM Mono',monospace",size:10}}},
      tooltip:{callbacks:{label:ctx=>`${ctx.dataset.label}: ${ctx.parsed.y}%`}}
    },
    scales:{
      x:{grid:{color:'rgba(0,0,0,0.05)'}, ticks:{font:{family:"'DM Mono',monospace",size:11}}},
      y:{min:0, max:12, grid:{color:'rgba(0,0,0,0.05)'}, ticks:{font:{family:"'DM Mono',monospace",size:10}, callback:v=>v+'%'}}
    }
  }
});

// ──────────────────────────────────
// CHART 4a — AGE / TIME WITH OTHERS
// ──────────────────────────────────
// Data from OWID_time_with_others_by_age_US.csv (sampled key ages)
const ageData = [
  {age:15, alone:3.63, social:1.58+4.32+0+0.17},
  {age:20, alone:4.5, social:2.1+3.2+0.2+1.6},
  {age:25, alone:5.1, social:1.9+2.8+0.8+1.8},
  {age:30, alone:5.3, social:1.6+2.5+1.4+1.7},
  {age:35, alone:5.6, social:1.3+2.3+2.1+1.5},
  {age:40, alone:5.9, social:1.1+2.1+2.5+1.3},
  {age:45, alone:6.2, social:1.0+2.0+2.8+1.1},
  {age:50, alone:6.5, social:1.0+1.9+3.1+1.0},
  {age:55, alone:6.8, social:0.9+1.8+3.5+0.8},
  {age:60, alone:7.2, social:0.85+1.6+3.7+0.55},
  {age:65, alone:7.8, social:0.7+1.4+3.5+0.4},
  {age:70, alone:8.4, social:0.6+1.2+3.2+0.3},
  {age:75, alone:9.1, social:0.5+1.0+2.8+0.2},
  {age:80, alone:9.8, social:0.4+0.8+2.3+0.15}
];

new Chart(document.getElementById('ageChart'), {
  type:'line',
  data:{
    labels: ageData.map(d=>d.age),
    datasets:[
      {
        label:'Time Alone',
        data: ageData.map(d=>d.alone),
        borderColor: RED,
        backgroundColor:'rgba(200,39,45,0.1)',
        borderWidth:2.5,
        tension:0.4,
        pointRadius:4,
        pointBackgroundColor: RED,
        fill:true
      },
      {
        label:'Time with Others',
        data: ageData.map(d=>d.social),
        borderColor: BLUE,
        backgroundColor:'rgba(74,111,165,0.1)',
        borderWidth:2.5,
        tension:0.4,
        pointRadius:4,
        pointBackgroundColor: BLUE,
        fill:true
      }
    ]
  },
  options:{
    responsive:true,
    plugins:{
      legend:{display:true, position:'top', labels:{usePointStyle:true, font:{family:"'DM Mono',monospace",size:10}}},
      tooltip:{
        callbacks:{
          title: ctx=>`Age ${ctx[0].label}`,
          label: ctx=>`${ctx.dataset.label}: ${ctx.parsed.y.toFixed(1)} hrs/day`
        }
      },
      annotation:{
        annotations:{
          tipPoint:{
            type:'line', xMin:60, xMax:60,
            borderColor: GOLD, borderWidth:2, borderDash:[5,4],
            label:{content:'Tipping Point — Age 60', display:true, backgroundColor:GOLD, color:'#fff',
                   font:{family:"'DM Mono',monospace",size:10}, position:'start', yAdjust:-10}
          }
        }
      }
    },
    scales:{
      x:{
        title:{display:true, text:'Age', font:{family:"'DM Mono',monospace",size:11}},
        grid:{color:'rgba(0,0,0,0.05)'},
        ticks:{font:{family:"'DM Mono',monospace",size:10}}
      },
      y:{
        title:{display:true, text:'Hours per Day', font:{family:"'DM Mono',monospace",size:11}},
        min:0, max:12,
        grid:{color:'rgba(0,0,0,0.05)'},
        ticks:{font:{family:"'DM Mono',monospace",size:10}}
      }
    }
  }
});

// CHART 4b — PARTNER PENALTY
new Chart(document.getElementById('partnerChart'), {
  type:'bar',
  data:{
    labels:['With Partner', 'Without Partner'],
    datasets:[{
      data:[7.8, 12.0],
      backgroundColor:[BLUE, RED],
      borderRadius:3
    }]
  },
  options:{
    indexAxis:'y',
    responsive:true,
    plugins:{
      tooltip:{callbacks:{label:ctx=>`${ctx.parsed.x} hrs/day alone`}},
      annotation:{
        annotations:{
          diff:{
            type:'label',
            xValue:10, yValue:0.5,
            content:'+55% more alone time',
            color:'#fff',
            backgroundColor: RED,
            font:{family:"'DM Mono',monospace",size:11},
            padding:6,
            borderRadius:2
          }
        }
      }
    },
    scales:{
      x:{min:0, max:14, ticks:{font:{family:"'DM Mono',monospace",size:10}, callback:v=>v+' hrs'}},
      y:{ticks:{font:{family:"'DM Mono',monospace",size:11}}}
    }
  }
});

// ──────────────────────────────────
// CHART 5a — GLOBAL LONELINESS (Gallup)
// ──────────────────────────────────
const gallupCountries = ['Brazil','Egypt','France','Indonesia','India','Mexico','United States'];
const gallupData = {
  'Not at all lonely': [53.3, 51.66, 62.56, 70.0, 40.09, 59.0, 57.77],
  'A little lonely':   [35.66, 18.29, 23.33, 19.08, 26.09, 25.0, 24.46],
  'Fairly lonely':     [5.14, 23.19, 10.22, 7.53, 20.7, 12.24, 10.62],
  'Very lonely':       [5.6, 6.8, 3.86, 2.37, 12.73, 3.64, 6.73]
};

let globalChart;
function buildGlobalChart(filter) {
  if (globalChart) globalChart.destroy();
  let datasets;
  const colors = { 'Not at all lonely':'#5a8a62','A little lonely':'#b8960c','Fairly lonely': RED_LIGHT,'Very lonely': RED };
  if (filter==='all') {
    datasets = Object.keys(gallupData).map(k=>({
      label:k, data:gallupData[k],
      backgroundColor: colors[k], borderWidth:0
    }));
  } else if (filter==='lonely') {
    const sum = gallupCountries.map((_,i)=>gallupData['Fairly lonely'][i]+gallupData['Very lonely'][i]);
    datasets = [{label:'Fairly + Very Lonely', data:sum, backgroundColor: RED, borderWidth:0, borderRadius:3}];
  } else {
    datasets = [{label:'Not at all Lonely', data:gallupData['Not at all lonely'], backgroundColor:'#5a8a62', borderWidth:0, borderRadius:3}];
  }

  globalChart = new Chart(document.getElementById('globalChart'), {
    type:'bar',
    data:{ labels:gallupCountries, datasets },
    options:{
      responsive:true,
      plugins:{
        legend:{display:filter==='all', position:'top', labels:{usePointStyle:true,font:{family:"'DM Mono',monospace",size:10}}},
        tooltip:{callbacks:{label:ctx=>`${ctx.dataset.label}: ${ctx.parsed.y.toFixed(1)}%`}}
      },
      scales:{
        x:{
          stacked: filter==='all',
          grid:{display:false},
          ticks:{font:{family:"'DM Mono',monospace",size:10}}
        },
        y:{
          stacked: filter==='all',
          min:0, max:filter==='all'?102:80,
          grid:{color:'rgba(0,0,0,0.05)'},
          ticks:{font:{family:"'DM Mono',monospace",size:10}, callback:v=>v+'%'}
        }
      }
    }
  });
}
buildGlobalChart('all');

function filterGlobal(f, btn) {
  document.querySelectorAll('#panel-global .filter-btn').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  buildGlobalChart(f);
}

// CHART 5b — SOCIAL MEDIA
const smCountries = ['Brazil','Egypt','France','Indonesia','India','Mexico','United States'];
const smLess = [55.95, 65.55, 51.61, 78.64, 61.32, 65.65, 39.56];
const smMore = [41.44, 26.58, 38.77, 13.53, 29.53, 31.7, 52.43];

new Chart(document.getElementById('socialMediaChart'), {
  type:'bar',
  data:{
    labels: smCountries,
    datasets:[
      {label:'Makes me less lonely', data:smLess, backgroundColor:'#5a8a62', borderWidth:0},
      {label:'Makes me more lonely', data:smMore, backgroundColor: RED, borderWidth:0}
    ]
  },
  options:{
    responsive:true,
    plugins:{
      legend:{display:true, position:'top', labels:{usePointStyle:true,font:{family:"'DM Mono',monospace",size:10}}},
      tooltip:{callbacks:{label:ctx=>`${ctx.dataset.label}: ${ctx.parsed.y}%`}}
    },
    scales:{
      x:{grid:{display:false}, ticks:{font:{family:"'DM Mono',monospace",size:10}}},
      y:{min:0, max:90, grid:{color:'rgba(0,0,0,0.05)'}, ticks:{font:{family:"'DM Mono',monospace",size:10}, callback:v=>v+'%'}}
    }
  }
});

// ──────────────────────────────────
// TAB LOGIC
// ──────────────────────────────────
function switchTab(id, btn) {
  document.querySelectorAll('.tab-btn').forEach(b=>b.classList.remove('active'));
  document.querySelectorAll('.panel').forEach(p=>p.classList.remove('active'));
  btn.classList.add('active');
  document.getElementById('panel-'+id).classList.add('active');
  if (id==='gender') setTimeout(animateGenderBars, 200);
  window.scrollTo({top: document.querySelector('.nav-tabs').offsetTop - 2, behavior:'smooth'});
}

// ──────────────────────────────────
// FADE-IN OBSERVER
// ──────────────────────────────────
const obs = new IntersectionObserver(entries=>{
  entries.forEach(e=>{ if(e.isIntersecting) e.target.classList.add('visible'); });
},{threshold:0.1});
document.querySelectorAll('.fade-in').forEach(el=>obs.observe(el));

// ── Init gender bars if on that panel from load ──
window.addEventListener('load', () => {
  if (document.getElementById('panel-gender').classList.contains('active')) animateGenderBars();
});
</script>
</body>
</html>
