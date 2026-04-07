<!DOCTYPE html>
<html lang="zh">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>my-notes</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Serif+JP:wght@300;400;600&family=Noto+Sans+SC:wght@300;400;500&family=DM+Mono:ital,wght@0,300;0,400;1,300&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0f0f13;
    --surface: #16161d;
    --surface2: #1e1e28;
    --border: #2a2a38;
    --accent: #e8c96d;
    --accent2: #7eb8c9;
    --text: #e8e4d8;
    --muted: #6b6880;
    --tag-jp: #c47b5a;
    --tag-grammar: #7eb8c9;
    --tag-vocab: #9bc47a;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Noto Sans SC', sans-serif;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* noise overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 0;
    opacity: 0.6;
  }

  .page {
    position: relative;
    z-index: 1;
    max-width: 860px;
    margin: 0 auto;
    padding: 64px 32px 100px;
  }

  /* Header */
  .header {
    margin-bottom: 56px;
    animation: fadeUp 0.6s ease both;
  }

  .header-top {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 8px;
  }

  .logo-mark {
    width: 32px;
    height: 32px;
    border: 1.5px solid var(--accent);
    border-radius: 6px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Noto Serif JP', serif;
    font-size: 14px;
    color: var(--accent);
    flex-shrink: 0;
  }

  h1 {
    font-family: 'DM Mono', monospace;
    font-size: 1.1rem;
    font-weight: 400;
    color: var(--accent);
    letter-spacing: 0.08em;
  }

  .header-desc {
    font-size: 0.82rem;
    color: var(--muted);
    letter-spacing: 0.06em;
    padding-left: 44px;
    font-family: 'DM Mono', monospace;
  }

  .divider {
    height: 1px;
    background: linear-gradient(90deg, var(--border) 0%, transparent 100%);
    margin: 24px 0;
  }

  /* Section label */
  .section-label {
    font-family: 'DM Mono', monospace;
    font-size: 0.65rem;
    letter-spacing: 0.18em;
    color: var(--muted);
    text-transform: uppercase;
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  /* Cards grid */
  .cards {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
    gap: 12px;
    margin-bottom: 48px;
  }

  .card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 22px 22px 18px;
    text-decoration: none;
    color: inherit;
    display: block;
    position: relative;
    overflow: hidden;
    transition: border-color 0.2s, transform 0.2s, background 0.2s;
    animation: fadeUp 0.5s ease both;
  }

  .card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--accent), transparent);
    opacity: 0;
    transition: opacity 0.2s;
  }

  .card:hover {
    border-color: var(--accent);
    background: var(--surface2);
    transform: translateY(-2px);
  }
  .card:hover::before { opacity: 1; }

  .card-icon {
    font-size: 1.4rem;
    margin-bottom: 12px;
    display: block;
  }

  .card-title {
    font-family: 'Noto Serif JP', serif;
    font-size: 1rem;
    font-weight: 600;
    color: var(--text);
    margin-bottom: 6px;
    line-height: 1.4;
  }

  .card-sub {
    font-size: 0.75rem;
    color: var(--muted);
    margin-bottom: 14px;
    font-family: 'DM Mono', monospace;
    letter-spacing: 0.02em;
  }

  .card-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
  }

  .tag {
    font-size: 0.62rem;
    padding: 3px 8px;
    border-radius: 20px;
    letter-spacing: 0.06em;
    font-family: 'DM Mono', monospace;
  }
  .tag.jp   { background: rgba(196,123,90,0.15); color: var(--tag-jp); border: 1px solid rgba(196,123,90,0.3); }
  .tag.gram { background: rgba(126,184,201,0.15); color: var(--tag-grammar); border: 1px solid rgba(126,184,201,0.3); }
  .tag.voc  { background: rgba(155,196,122,0.15); color: var(--tag-vocab); border: 1px solid rgba(155,196,122,0.3); }

  .card-arrow {
    position: absolute;
    bottom: 18px;
    right: 18px;
    font-size: 0.75rem;
    color: var(--muted);
    transition: color 0.2s, transform 0.2s;
    font-family: 'DM Mono', monospace;
  }
  .card:hover .card-arrow {
    color: var(--accent);
    transform: translate(2px, -2px);
  }

  /* Stagger animation delays */
  .card:nth-child(1) { animation-delay: 0.1s; }
  .card:nth-child(2) { animation-delay: 0.18s; }
  .card:nth-child(3) { animation-delay: 0.26s; }
  .card:nth-child(4) { animation-delay: 0.34s; }
  .card:nth-child(5) { animation-delay: 0.42s; }

  /* Add new card (placeholder style) */
  .card-add {
    border-style: dashed;
    border-color: var(--border);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 130px;
    gap: 8px;
    cursor: default;
    opacity: 0.5;
    transition: opacity 0.2s;
  }
  .card-add:hover {
    opacity: 0.75;
    border-color: var(--muted);
    transform: none;
    background: var(--surface);
  }
  .card-add span {
    font-size: 1.4rem;
    color: var(--muted);
  }
  .card-add p {
    font-size: 0.72rem;
    color: var(--muted);
    font-family: 'DM Mono', monospace;
    letter-spacing: 0.06em;
  }

  /* Footer */
  .footer {
    border-top: 1px solid var(--border);
    padding-top: 20px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 8px;
  }

  .footer-left {
    font-size: 0.7rem;
    color: var(--muted);
    font-family: 'DM Mono', monospace;
    letter-spacing: 0.06em;
  }

  .footer-right {
    font-size: 0.7rem;
    color: var(--muted);
    font-family: 'Noto Serif JP', serif;
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(16px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  @media (max-width: 500px) {
    .page { padding: 40px 20px 80px; }
    .cards { grid-template-columns: 1fr; }
    h1 { font-size: 0.95rem; }
  }
</style>
</head>
<body>
<div class="page">

  <header class="header">
    <div class="header-top">
      <div class="logo-mark">学</div>
      <h1>my-notes</h1>
    </div>
    <div class="header-desc">// Japanese learning notes · JLPT N4→N2 roadmap</div>
    <div class="divider"></div>
  </header>

  <div class="section-label">笔记文件</div>

  <div class="cards" id="cards">

    <a class="card" href="japanese_hours_1.html">
      <span class="card-icon">🕐</span>
      <div class="card-title">24時間の言い方</div>
      <div class="card-sub">japanese_hours_1.html</div>
      <div class="card-tags">
        <span class="tag jp">日本語</span>
        <span class="tag voc">词汇</span>
        <span class="tag voc">N4-N5</span>
      </div>
      <span class="card-arrow">↗</span>
    </a>

    <a class="card" href="n5_n4_grammar_reference.html">
      <span class="card-icon">📐</span>
      <div class="card-title">N5 · N4 文法リファレンス</div>
      <div class="card-sub">n5_n4_grammar_reference.html</div>
      <div class="card-tags">
        <span class="tag jp">日本語</span>
        <span class="tag gram">文法</span>
        <span class="tag gram">N5·N4</span>
      </div>
      <span class="card-arrow">↗</span>
    </a>

    <div class="card card-add">
      <span>＋</span>
      <p>上传新笔记后在这里添加卡片</p>
    </div>

  </div>

  <footer class="footer">
    <div class="footer-left">github.com/Miyazawa-ron/my-notes</div>
    <div class="footer-right">勉強中 📖</div>
  </footer>

</div>
</body>
</html>
