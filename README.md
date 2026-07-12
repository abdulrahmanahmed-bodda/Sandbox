<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Bosta — Last-Mile Delivery</title>
  <link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet"/>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    :root {
      --bg: #0a0a0f; --surface: #13131a; --border: #2a2a3a;
      --accent: #7c5cfc; --accent2: #fc5c7d; --text: #e8e8f0; --muted: #888899; --card: #16161f;
    }
    html { scroll-behavior: smooth; }
    body { background: var(--bg); color: var(--text); font-family: "DM Sans", sans-serif; font-weight: 300; overflow-x: hidden; }
    nav {
      position: fixed; top: 0; left: 0; right: 0; z-index: 100;
      display: flex; align-items: center; justify-content: space-between;
      padding: 1.25rem 3rem;
      background: rgba(10,10,15,0.8); backdrop-filter: blur(16px);
      border-bottom: 1px solid var(--border);
    }
    .logo { font-family: "Syne", sans-serif; font-weight: 800; font-size: 1.4rem; background: linear-gradient(135deg, var(--accent), var(--accent2)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
    .nav-links { display: flex; gap: 2.5rem; list-style: none; }
    .nav-links a { color: var(--muted); text-decoration: none; font-size: 0.9rem; letter-spacing: 0.04em; transition: color 0.2s; }
    .nav-links a:hover { color: var(--text); }
    .nav-cta { background: var(--accent); color: #fff; border: none; padding: 0.6rem 1.4rem; border-radius: 6px; cursor: pointer; font-family: "DM Sans", sans-serif; font-size: 0.875rem; font-weight: 500; transition: opacity 0.2s; }
    .nav-cta:hover { opacity: 0.85; }
    .hero { min-height: 100vh; display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center; padding: 6rem 2rem 4rem; position: relative; overflow: hidden; }
    .hero::before { content: ""; position: absolute; inset: 0; background: radial-gradient(ellipse 70% 50% at 20% 40%, rgba(124,92,252,0.18) 0%, transparent 60%), radial-gradient(ellipse 60% 40% at 80% 60%, rgba(252,92,125,0.12) 0%, transparent 60%); pointer-events: none; }
    .grid-bg { position: absolute; inset: 0; pointer-events: none; opacity: 0.04; background-image: linear-gradient(var(--text) 1px, transparent 1px), linear-gradient(90deg, var(--text) 1px, transparent 1px); background-size: 60px 60px; }
    .badge { display: inline-block; background: rgba(124,92,252,0.12); border: 1px solid rgba(124,92,252,0.35); color: var(--accent); border-radius: 99px; padding: 0.35rem 1rem; font-size: 0.8rem; letter-spacing: 0.08em; text-transform: uppercase; margin-bottom: 1.5rem; animation: fadeUp 0.6s ease both; }
    h1 { font-family: "Syne", sans-serif; font-weight: 800; font-size: clamp(2.8rem, 7vw, 5.5rem); line-height: 1.05; letter-spacing: -0.02em; max-width: 820px; animation: fadeUp 0.6s 0.1s ease both; }
    h1 span { background: linear-gradient(135deg, var(--accent) 30%, var(--accent2)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
    .hero-sub { margin-top: 1.5rem; max-width: 520px; color: var(--muted); font-size: 1.05rem; line-height: 1.7; animation: fadeUp 0.6s 0.2s ease both; }
    .hero-actions { display: flex; gap: 1rem; margin-top: 2.5rem; animation: fadeUp 0.6s 0.3s ease both; }
    .btn-primary { background: linear-gradient(135deg, var(--accent), #5a3fcc); color: #fff; border: none; padding: 0.85rem 2rem; border-radius: 8px; font-family: "DM Sans", sans-serif; font-size: 0.95rem; font-weight: 500; cursor: pointer; transition: transform 0.15s, opacity 0.15s; }
    .btn-primary:hover { transform: translateY(-2px); opacity: 0.9; }
    .btn-ghost { background: transparent; color: var(--text); border: 1px solid var(--border); padding: 0.85rem 2rem; border-radius: 8px; font-family: "DM Sans", sans-serif; font-size: 0.95rem; cursor: pointer; transition: border-color 0.2s, background 0.2s; }
    .btn-ghost:hover { border-color: var(--accent); background: rgba(124,92,252,0.07); }
    .stats { display: flex; justify-content: center; gap: 4rem; padding: 2.5rem 2rem; flex-wrap: wrap; border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); }
    .stat { text-align: center; }
    .stat-num { font-family: "Syne", sans-serif; font-size: 2.2rem; font-weight: 800; background: linear-gradient(135deg, var(--accent), var(--accent2)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
    .stat-label { font-size: 0.8rem; color: var(--muted); letter-spacing: 0.05em; margin-top: 0.25rem; }
    .section { padding: 6rem 2rem; max-width: 1100px; margin: 0 auto; }
    .section-label { font-size: 0.75rem; letter-spacing: 0.12em; text-transform: uppercase; color: var(--accent); margin-bottom: 0.75rem; }
    .section-title { font-family: "Syne", sans-serif; font-weight: 700; font-size: clamp(1.8rem, 4vw, 2.8rem); line-height: 1.15; margin-bottom: 1rem; }
    .section-sub { color: var(--muted); max-width: 480px; line-height: 1.7; margin-bottom: 3rem; }
    .features-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 1.5rem; }
    .feature-card { background: var(--card); border: 1px solid var(--border); border-radius: 12px; padding: 1.75rem; transition: border-color 0.25s, transform 0.2s; position: relative; overflow: hidden; }
    .feature-card::before { content: ""; position: absolute; top: 0; left: 0; right: 0; height: 2px; background: linear-gradient(90deg, var(--accent), var(--accent2)); opacity: 0; transition: opacity 0.25s; }
    .feature-card:hover { border-color: var(--accent); transform: translateY(-3px); }
    .feature-card:hover::before { opacity: 1; }
    .feat-icon { width: 42px; height: 42px; border-radius: 10px; background: rgba(124,92,252,0.15); display: flex; align-items: center; justify-content: center; font-size: 1.2rem; margin-bottom: 1rem; }
    .feat-title { font-family: "Syne", sans-serif; font-weight: 600; font-size: 1rem; margin-bottom: 0.5rem; }
    .feat-desc { color: var(--muted); font-size: 0.875rem; line-height: 1.65; }
    .pricing-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 1.5rem; margin-top: 3rem; }
    .plan { background: var(--card); border: 1px solid var(--border); border-radius: 14px; padding: 2rem; transition: border-color 0.2s; }
    .plan.featured { border-color: var(--accent); background: linear-gradient(160deg, rgba(124,92,252,0.08), var(--card)); }
    .plan-name { font-family: "Syne", sans-serif; font-size: 1rem; font-weight: 700; margin-bottom: 0.5rem; }
    .plan-price { font-family: "Syne", sans-serif; font-size: 2.5rem; font-weight: 800; margin: 0.5rem 0; }
    .plan-price span { font-size: 1rem; font-weight: 400; color: var(--muted); }
    .plan-desc { color: var(--muted); font-size: 0.85rem; margin-bottom: 1.5rem; }
    .plan-features { list-style: none; margin-bottom: 1.75rem; }
    .plan-features li { font-size: 0.875rem; padding: 0.4rem 0; border-bottom: 1px solid var(--border); color: var(--muted); }
    .plan-features li::before { content: "Check  "; color: var(--accent); font-weight: 700; }
    .plan-btn { width: 100%; padding: 0.75rem; background: var(--accent); color: #fff; border: none; border-radius: 8px; font-family: "DM Sans", sans-serif; font-size: 0.9rem; cursor: pointer; transition: opacity 0.2s; }
    .plan-btn:hover { opacity: 0.85; }
    .plan-btn.outline { background: transparent; border: 1px solid var(--border); color: var(--text); }
    .plan-btn.outline:hover { border-color: var(--accent); }
    .faq-list { margin-top: 2rem; }
    .faq-item { border-bottom: 1px solid var(--border); padding: 1.25rem 0; }
    .faq-q { font-family: "Syne", sans-serif; font-weight: 600; font-size: 1rem; cursor: pointer; display: flex; justify-content: space-between; align-items: center; }
    .faq-a { color: var(--muted); font-size: 0.9rem; line-height: 1.7; margin-top: 0.75rem; }
    .cta-band { background: linear-gradient(135deg, rgba(124,92,252,0.15), rgba(252,92,125,0.08)); border: 1px solid rgba(124,92,252,0.2); border-radius: 16px; padding: 4rem 3rem; text-align: center; margin: 2rem auto; max-width: 1100px; }
    .cta-band h2 { font-family: "Syne", sans-serif; font-weight: 800; font-size: clamp(1.6rem, 4vw, 2.5rem); margin-bottom: 1rem; }
    .cta-band p { color: var(--muted); max-width: 420px; margin: 0 auto 2rem; line-height: 1.7; }
    footer { border-top: 1px solid var(--border); padding: 2rem 3rem; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 1rem; }
    footer p { color: var(--muted); font-size: 0.8rem; }
    /* Pre-chat styles */
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&display=swap');
    #prechat-overlay { display: none; position: fixed; inset: 0; z-index: 9999; background: rgba(15,10,30,0.65); backdrop-filter: blur(4px); align-items: flex-end; justify-content: flex-end; padding: 0 24px 90px; }
    #prechat-overlay.show { display: flex; }
    #prechat-box { width: 370px; background: #ffffff; border-radius: 20px; overflow: hidden; font-family: "Inter", "DM Sans", sans-serif; box-shadow: 0 24px 80px rgba(227,6,19,0.18), 0 4px 20px rgba(0,0,0,0.18); animation: popUp 0.35s cubic-bezier(.34,1.56,.64,1); }
    @keyframes popUp { from { opacity:0; transform: translateY(30px) scale(0.94); } to { opacity:1; transform: translateY(0) scale(1); } }
    #prechat-header { background: linear-gradient(135deg, #E30613 0%, #a80000 100%); padding: 1.35rem 1.25rem 1.1rem; color: #fff; position: relative; overflow: hidden; }
    #prechat-header::before { content: ""; position: absolute; top: -30px; right: -30px; width: 120px; height: 120px; background: rgba(255,255,255,0.07); border-radius: 50%; }
    #prechat-header::after { content: ""; position: absolute; bottom: -20px; left: 40px; width: 80px; height: 80px; background: rgba(255,255,255,0.05); border-radius: 50%; }
    #prechat-header .brand { font-size: 0.68rem; opacity: 0.75; letter-spacing: 0.1em; text-transform: uppercase; font-weight: 600; margin-bottom: 0.6rem; display: flex; align-items: center; gap: 0.4rem; }
    #prechat-header .brand::before { content: ""; width: 6px; height: 6px; background: #a8f08a; border-radius: 50%; display: inline-block; box-shadow: 0 0 6px #a8f08a; }
    #prechat-header h3 { font-family: "Syne", sans-serif; font-size: 1.15rem; font-weight: 800; margin: 0 0 0.3rem; letter-spacing: -0.01em; }
    #prechat-header p { font-size: 0.78rem; opacity: 0.8; margin: 0; font-weight: 400; }
    #prechat-close { position: absolute; top: 1rem; right: 1rem; background: rgba(255,255,255,0.18); border: 1px solid rgba(255,255,255,0.25); color: #fff; width: 28px; height: 28px; border-radius: 50%; font-size: 0.85rem; cursor: pointer; line-height: 28px; text-align: center; transition: background 0.2s; z-index: 1; }
    #prechat-close:hover { background: rgba(255,255,255,0.3); }
    #prechat-body { padding: 1rem 1rem 1.25rem; max-height: 460px; overflow-y: auto; scrollbar-width: thin; scrollbar-color: #ffcccc transparent; }
    #prechat-body::-webkit-scrollbar { width: 4px; }
    #prechat-body::-webkit-scrollbar-track { background: transparent; }
    #prechat-body::-webkit-scrollbar-thumb { background: #ffaaaa; border-radius: 4px; }
    .faq-step { display: none; }
    .faq-step.active { display: block; animation: fadeIn 0.2s ease; }
    @keyframes fadeIn { from { opacity:0; transform: translateY(6px); } to { opacity:1; transform: translateY(0); } }
    .step-label { font-size: 0.65rem; color: #cc6666; letter-spacing: 0.1em; text-transform: uppercase; font-weight: 600; margin-bottom: 0.65rem; padding-bottom: 0.5rem; border-bottom: 1px solid #ffe5e5; }
    .faq-btn { display: flex; align-items: center; gap: 0.75rem; width: 100%; text-align: left; background: #fafafa; border: 1.5px solid #ffe5e5; border-radius: 12px; padding: 0.7rem 0.9rem; font-family: "Inter", sans-serif; font-size: 0.83rem; font-weight: 500; color: #1a1a1a; cursor: pointer; margin-bottom: 0.45rem; transition: all 0.18s; }
    .faq-btn:hover { background: #fff0f0; border-color: #E30613; color: #b30000; transform: translateX(2px); }
    .faq-btn .icon { font-size: 1.25rem; flex-shrink: 0; width: 32px; height: 32px; background: #ffe5e5; border-radius: 8px; display: flex; align-items: center; justify-content: center; }
    .faq-btn:hover .icon { background: #ffd0d0; }
    .faq-btn .btn-label { flex: 1; }
    .faq-btn .arrow { color: #c4b8f8; font-size: 0.9rem; transition: transform 0.18s; }
    .faq-btn:hover .arrow { transform: translateX(3px); color: #7c5cfc; }
    .answer-box { background: linear-gradient(135deg, #f0fdf4, #e8faf0); border: 1.5px solid #86efac; border-radius: 12px; padding: 1rem 1.1rem; font-size: 0.84rem; color: #14532d; line-height: 1.7; margin-bottom: 0.75rem; font-weight: 400; }
    .answer-box::before { content: "✅ "; font-size: 1rem; }
    .prechat-actions { display: flex; gap: 0.6rem; margin-top: 0.75rem; flex-wrap: wrap; }
    .btn-chat { flex: 1; background: linear-gradient(135deg, #E30613, #a80000); color: #fff; border: none; border-radius: 10px; padding: 0.7rem 1rem; font-family: "Inter", sans-serif; font-size: 0.85rem; font-weight: 600; cursor: pointer; transition: all 0.2s; letter-spacing: 0.01em; }
    .btn-chat:hover { opacity: 0.9; transform: translateY(-1px); box-shadow: 0 4px 16px rgba(227,6,19,0.35); }
    .btn-back { background: #fff5f5; border: 1.5px solid #ffcccc; color: #b30000; border-radius: 10px; padding: 0.7rem 1rem; font-family: "Inter", sans-serif; font-size: 0.85rem; font-weight: 500; cursor: pointer; transition: all 0.18s; }
    .btn-back:hover { background: #fff0f0; border-color: #E30613; color: #b30000; }
    #fc-launcher { position: fixed; bottom: 24px; right: 24px; z-index: 9998; background: linear-gradient(135deg, #E30613, #a80000); color: #fff; border: none; border-radius: 50px; padding: 0.8rem 1.5rem; font-family: "Inter", sans-serif; font-size: 0.88rem; font-weight: 600; cursor: pointer; box-shadow: 0 4px 24px rgba(227,6,19,0.5); display: flex; align-items: center; gap: 0.5rem; transition: transform 0.2s, box-shadow 0.2s; }
    #fc-launcher:hover { transform: translateY(-2px); box-shadow: 0 8px 30px rgba(227,6,19,0.55); }
    #fc-launcher.hidden { display: none; }
    .breadcrumb { font-size: 0.7rem; color: #b0aac8; margin-bottom: 0.85rem; display: flex; align-items: center; gap: 0.35rem; flex-wrap: wrap; background: #fff5f5; padding: 0.45rem 0.75rem; border-radius: 8px; }
    .breadcrumb span { color: #E30613; cursor: pointer; font-weight: 600; }
    .breadcrumb span:hover { text-decoration: underline; }
    .breadcrumb .sep { color: #ffbbbb; }
    @keyframes fadeUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
  </style>
</head>
<body>

<nav>
  <div class="logo">Bosta</div>
  <ul class="nav-links">
    <li><a href="#features">Features</a></li>
    <li><a href="#pricing">Pricing</a></li>
    <li><a href="#faq">FAQ</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <button class="nav-cta">Get Started</button>
</nav>

<section class="hero">
  <div class="grid-bg"></div>
  <div class="badge">Rocket Now in public beta</div>
  <h1>Deliver faster with <span>intelligent</span> logistics</h1>
  <p class="hero-sub">Bosta powers fast, reliable last-mile delivery across the region — tracked end to end.</p>
  <div class="hero-actions">
    <button class="btn-primary" onclick="openPrechat()">Chat with us</button>
    <button class="btn-ghost">Watch demo</button>
  </div>
</section>

<div class="stats">
  <div class="stat"><div class="stat-num">12K+</div><div class="stat-label">Active Users</div></div>
  <div class="stat"><div class="stat-num">99.9%</div><div class="stat-label">Uptime SLA</div></div>
  <div class="stat"><div class="stat-num">4.8 Stars</div><div class="stat-label">Customer Rating</div></div>
  <div class="stat"><div class="stat-num">Under 2s</div><div class="stat-label">Avg. Response</div></div>
</div>

<section class="section" id="features">
  <div class="section-label">Platform</div>
  <h2 class="section-title">Everything you need,<br>nothing you don't</h2>
  <p class="section-sub">Purpose-built tools that integrate seamlessly so you can focus on shipping great products.</p>
  <div class="features-grid">
    <div class="feature-card"><div class="feat-icon">Flash</div><div class="feat-title">Instant Deploys</div><div class="feat-desc">Push to production in under 30 seconds with zero-downtime blue-green deployments.</div></div>
    <div class="feature-card"><div class="feat-icon">Shield</div><div class="feat-title">Enterprise Security</div><div class="feat-desc">SOC 2 Type II, end-to-end encryption, and granular role-based access controls.</div></div>
    <div class="feature-card"><div class="feat-icon">Chart</div><div class="feat-title">Real-time Analytics</div><div class="feat-desc">Live dashboards for usage, performance, and customer behaviour across every touchpoint.</div></div>
    <div class="feature-card"><div class="feat-icon">Chat</div><div class="feat-title">Live Chat Support</div><div class="feat-desc">Embedded Freshchat widget so customers get answers instantly.</div></div>
    <div class="feature-card"><div class="feat-icon">Link</div><div class="feat-title">100+ Integrations</div><div class="feat-desc">Connect Slack, GitHub, Jira, HubSpot and more with one-click OAuth flows.</div></div>
    <div class="feature-card"><div class="feat-icon">Bot</div><div class="feat-title">AI Automation</div><div class="feat-desc">Route tickets, draft replies, and flag anomalies automatically with built-in ML models.</div></div>
  </div>
</section>

<section class="section" id="pricing">
  <div class="section-label">Pricing</div>
  <h2 class="section-title">Simple, transparent plans</h2>
  <p class="section-sub">No surprise fees. Cancel anytime. Switch plans as you grow.</p>
  <div class="pricing-grid">
    <div class="plan">
      <div class="plan-name">Starter</div>
      <div class="plan-price">$0<span>/mo</span></div>
      <div class="plan-desc">Perfect for side projects and early-stage testing.</div>
      <ul class="plan-features"><li>Up to 3 team members</li><li>5 GB storage</li><li>Community support</li><li>Basic analytics</li></ul>
      <button class="plan-btn outline">Get started free</button>
    </div>
    <div class="plan featured">
      <div class="plan-name">Pro</div>
      <div class="plan-price">$49<span>/mo</span></div>
      <div class="plan-desc">For growing teams who need more power and priority support.</div>
      <ul class="plan-features"><li>Unlimited team members</li><li>100 GB storage</li><li>Priority live chat</li><li>Advanced analytics</li><li>Custom integrations</li></ul>
      <button class="plan-btn">Start Pro trial</button>
    </div>
    <div class="plan">
      <div class="plan-name">Enterprise</div>
      <div class="plan-price">Custom</div>
      <div class="plan-desc">Tailored for large organisations with specific compliance needs.</div>
      <ul class="plan-features"><li>SSO and SAML</li><li>Dedicated infrastructure</li><li>SLA guarantees</li><li>Dedicated CSM</li></ul>
      <button class="plan-btn outline">Contact sales</button>
    </div>
  </div>
</section>

<section class="section" id="faq">
  <div class="section-label">FAQ</div>
  <h2 class="section-title">Common questions</h2>
  <div class="faq-list">
    <div class="faq-item">
      <div class="faq-q" onclick="toggleFaq(this)">How do I integrate Freshchat on my site? <span>+</span></div>
      <div class="faq-a" style="display:none">Click the Chat with us button, select your topic, and follow the pre-chat flow. If you need an agent, the Freshchat widget will open automatically.</div>
    </div>
    <div class="faq-item">
      <div class="faq-q" onclick="toggleFaq(this)">Is there a free trial for Pro? <span>+</span></div>
      <div class="faq-a" style="display:none">Yes, you get 14 days of Pro free, no credit card required. You will be downgraded to Starter automatically if you do not upgrade.</div>
    </div>
    <div class="faq-item">
      <div class="faq-q" onclick="toggleFaq(this)">Can I use this page as a Freshchat sandbox? <span>+</span></div>
      <div class="faq-a" style="display:none">Absolutely. The Freshchat widget is embedded with a sandbox token. Click Chat with us to test the full pre-chat flow.</div>
    </div>
  </div>
</section>

<div class="cta-band" id="contact">
  <h2>Ready to get started?</h2>
  <p>Need help with a shipment? Our support team is ready for you.</p>
  <div style="display:flex;gap:1rem;justify-content:center;flex-wrap:wrap">
    <button class="btn-primary" onclick="openPrechat()">Chat with us</button>
    <button class="btn-ghost">Book a demo</button>
  </div>
</div>

<footer>
  <div class="logo">Bosta</div>
  <p>2026 Bosta Inc. Sandbox demo for Freshchat widget testing.</p>
</footer>

<!-- Custom launcher -->
<button id="fc-launcher" onclick="openPrechat()">💬 Chat with us</button>

<!-- Pre-chat overlay -->
<div id="prechat-overlay">
  <div id="prechat-box">
    <div id="prechat-header">
      <button id="prechat-close" onclick="closePrechat()">✕</button>
      <div class="brand">Bosta Logistics &mdash; Support</div>
      <h3 id="header-title">👋 How can we help?</h3>
      <p id="header-sub">Select a topic and we'll guide you to the right answer</p>
    </div>
    <div id="prechat-body">

      <!-- Main menu -->
      <div class="faq-step active" id="step-main">
        <div class="step-label">📋 Choose a topic</div>
        <button class="faq-btn" onclick="showTopic('shipment')"><span class="icon">📦</span><span class="btn-label">Shipment tracking &amp; status</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showTopic('pickup')"><span class="icon">🚚</span><span class="btn-label">Pickup scheduling &amp; issues</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showTopic('delivery')"><span class="icon">🏠</span><span class="btn-label">Delivery problems &amp; delays</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showTopic('returns')"><span class="icon">↩️</span><span class="btn-label">Returns &amp; reverse logistics</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showTopic('billing')"><span class="icon">💳</span><span class="btn-label">Billing, invoices &amp; pricing</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showTopic('integration')"><span class="icon">🔗</span><span class="btn-label">API &amp; system integration</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showTopic('account')"><span class="icon">👤</span><span class="btn-label">Account &amp; contract management</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showTopic('create-order')"><span class="icon">📝</span><span class="btn-label">How to create an order</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="startChat('general')" style="border-color:#d4c9ff;background:#f5f0ff;"><span class="icon">💬</span><span class="btn-label" style="color:#5a3fcc;font-weight:600;">Other &mdash; chat with an agent</span><span class="arrow" style="color:#9b7aff;">›</span></button>
      </div>

      <!-- Shipment -->
      <div class="faq-step" id="step-shipment">
        <div class="breadcrumb"><span onclick="backToMain()">🏠 Home</span><span class="sep">›</span>Shipment tracking</div>
        <div class="step-label">📦 Shipment tracking</div>
        <button class="faq-btn" onclick="showAnswer('track-order')"><span class="icon">🔍</span><span class="btn-label">How do I track my shipment?</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showAnswer('lost-shipment')"><span class="icon">❓</span><span class="btn-label">My shipment shows lost or stuck</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showAnswer('status-not-updating')"><span class="icon">🔄</span><span class="btn-label">Tracking status not updating</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="startChat('shipment')" style="border-color:#d4c9ff;background:#f5f0ff;"><span class="icon">💬</span><span class="btn-label" style="color:#5a3fcc;font-weight:600;">My issue is not listed &mdash; chat now</span><span class="arrow" style="color:#9b7aff;">›</span></button>
      </div>

      <!-- Pickup -->
      <div class="faq-step" id="step-pickup">
        <div class="breadcrumb"><span onclick="backToMain()">🏠 Home</span><span class="sep">›</span>Pickup</div>
        <div class="step-label">🚚 Pickup scheduling</div>
        <button class="faq-btn" onclick="showAnswer('schedule-pickup')"><span class="icon">📅</span><span class="btn-label">How do I schedule a pickup?</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showAnswer('missed-pickup')"><span class="icon">⚠️</span><span class="btn-label">Courier did not show up for pickup</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showAnswer('pickup-cutoff')"><span class="icon">⏰</span><span class="btn-label">What is the pickup cutoff time?</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="startChat('pickup')" style="border-color:#d4c9ff;background:#f5f0ff;"><span class="icon">💬</span><span class="btn-label" style="color:#5a3fcc;font-weight:600;">Chat with an agent</span><span class="arrow" style="color:#9b7aff;">›</span></button>
      </div>

      <!-- Delivery -->
      <div class="faq-step" id="step-delivery">
        <div class="breadcrumb"><span onclick="backToMain()">🏠 Home</span><span class="sep">›</span>Delivery</div>
        <div class="step-label">🏠 Delivery issues</div>
        <button class="faq-btn" onclick="showTrackingStep()"><span class="icon">⏳</span><span class="btn-label">My delivery is delayed</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showAnswer('wrong-address')"><span class="icon">📍</span><span class="btn-label">Delivered to wrong address</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showAnswer('damaged')"><span class="icon">💔</span><span class="btn-label">Package arrived damaged</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="startChat('delivery')" style="border-color:#d4c9ff;background:#f5f0ff;"><span class="icon">💬</span><span class="btn-label" style="color:#5a3fcc;font-weight:600;">Chat with an agent</span><span class="arrow" style="color:#9b7aff;">›</span></button>
      </div>

      <!-- Tracking number input -->
      <div class="faq-step" id="step-tracking-input">
        <div class="breadcrumb"><span onclick="backToMain()">🏠 Home</span><span class="sep">›</span><span onclick="showTopic('delivery')">Delivery</span><span class="sep">›</span>Delayed delivery</div>
        <div class="step-label">🔍 Check your order status</div>
        <div style="background:#f5f0ff;border:1.5px solid #d4c9ff;border-radius:12px;padding:0.85rem 1rem;margin-bottom:1rem;font-size:0.82rem;color:#4c3a8a;line-height:1.6;">
          <strong>⏳ Before contacting support</strong><br>Please enter your tracking number so we can check if your order is still within the normal delivery window.
        </div>
        <input id="tracking-input" type="text" placeholder="e.g. BST-123456789" style="width:100%;padding:0.7rem 1rem;border:1.5px solid #e0d9ff;border-radius:10px;font-size:0.875rem;font-family:Inter,sans-serif;outline:none;margin-bottom:0.5rem;color:#1a1a2e;background:#fafafa;transition:border-color 0.2s;" onfocus="this.style.borderColor='#7c5cfc'" onblur="this.style.borderColor='#e0d9ff'" />
        <div id="tracking-error" style="display:none;font-size:0.78rem;color:#dc2626;margin-bottom:0.5rem;padding:0.4rem 0.75rem;background:#fef2f2;border-radius:6px;">⚠️ Please enter a valid tracking number.</div>
        <div class="prechat-actions">
          <button class="btn-back" onclick="showTopic('delivery')">← Back</button>
          <button class="btn-chat" onclick="checkTracking()">🔍 Check status</button>
        </div>
      </div>

      <!-- Blocked -->
      <div class="faq-step" id="step-tracking-blocked">
        <div class="breadcrumb"><span onclick="backToMain()">🏠 Home</span><span class="sep">›</span><span onclick="showTopic('delivery')">Delivery</span><span class="sep">›</span>Status check</div>
        <div class="step-label">📊 Order status</div>
        <div style="background:linear-gradient(135deg,#f0fdf4,#dcfce7);border:1.5px solid #86efac;border-radius:14px;padding:1.1rem 1.1rem;margin-bottom:0.85rem;text-align:center;">
          <div style="font-size:2.5rem;margin-bottom:0.5rem;">🚀</div>
          <div style="font-weight:700;font-size:0.95rem;color:#14532d;margin-bottom:0.4rem;">Your order is on its way!</div>
          <div style="font-size:0.8rem;color:#166534;line-height:1.6;">Tracking <strong id="blocked-tracking-num" style="background:#bbf7d0;padding:0.1rem 0.4rem;border-radius:4px;"></strong> is within the normal <strong>3–5 business day</strong> delivery window.</div>
        </div>
        <div style="background:#fff7ed;border:1.5px solid #fed7aa;border-radius:12px;padding:0.85rem 1rem;margin-bottom:0.85rem;font-size:0.81rem;color:#9a3412;line-height:1.65;">
          💡 <strong>Track in real time:</strong> Log in to your Bosta dashboard and go to <strong>Shipments → Tracking</strong> to see live courier updates.
        </div>
        <div class="prechat-actions">
          <button class="btn-back" onclick="showTopic('delivery')">← Back</button>
          <button class="btn-chat" style="background:#e5e7eb;color:#9ca3af;cursor:not-allowed;box-shadow:none;" disabled>🔒 Chat unavailable</button>
        </div>
        <p style="font-size:0.72rem;color:#c0b8d8;margin-top:0.75rem;text-align:center;">💬 Support chat for delays opens after your estimated delivery date passes.</p>
      </div>

      <!-- Returns -->
      <div class="faq-step" id="step-returns">
        <div class="breadcrumb"><span onclick="backToMain()">🏠 Home</span><span class="sep">›</span>Returns</div>
        <div class="step-label">↩️ Returns &amp; reverse logistics</div>
        <button class="faq-btn" onclick="showAnswer('initiate-return')"><span class="icon">↩️</span><span class="btn-label">How do I initiate a return?</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showAnswer('return-status')"><span class="icon">🔍</span><span class="btn-label">Track my return shipment</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showAnswer('return-policy')"><span class="icon">📋</span><span class="btn-label">What is your return policy?</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="startChat('returns')" style="border-color:#d4c9ff;background:#f5f0ff;"><span class="icon">💬</span><span class="btn-label" style="color:#5a3fcc;font-weight:600;">Chat with an agent</span><span class="arrow" style="color:#9b7aff;">›</span></button>
      </div>

      <!-- Billing -->
      <div class="faq-step" id="step-billing">
        <div class="breadcrumb"><span onclick="backToMain()">🏠 Home</span><span class="sep">›</span>Billing</div>
        <div class="step-label">💳 Billing &amp; pricing</div>
        <button class="faq-btn" onclick="showAnswer('invoice')"><span class="icon">🧾</span><span class="btn-label">Where can I find my invoice?</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showAnswer('pricing')"><span class="icon">💰</span><span class="btn-label">How is shipping cost calculated?</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showAnswer('dispute')"><span class="icon">⚠️</span><span class="btn-label">I want to dispute a charge</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="startChat('billing')" style="border-color:#d4c9ff;background:#f5f0ff;"><span class="icon">💬</span><span class="btn-label" style="color:#5a3fcc;font-weight:600;">Chat with an agent</span><span class="arrow" style="color:#9b7aff;">›</span></button>
      </div>

      <!-- Integration -->
      <div class="faq-step" id="step-integration">
        <div class="breadcrumb"><span onclick="backToMain()">🏠 Home</span><span class="sep">›</span>API &amp; Integration</div>
        <div class="step-label">🔗 API &amp; system integration</div>
        <button class="faq-btn" onclick="showAnswer('api-docs')"><span class="icon">📄</span><span class="btn-label">Where are the API docs?</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showAnswer('webhook')"><span class="icon">🔔</span><span class="btn-label">How do webhooks work?</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showAnswer('api-error')"><span class="icon">🐛</span><span class="btn-label">I am getting API errors</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="startChat('integration')" style="border-color:#d4c9ff;background:#f5f0ff;"><span class="icon">💬</span><span class="btn-label" style="color:#5a3fcc;font-weight:600;">Chat with a tech agent</span><span class="arrow" style="color:#9b7aff;">›</span></button>
      </div>

      <!-- Account -->
      <div class="faq-step" id="step-account">
        <div class="breadcrumb"><span onclick="backToMain()">🏠 Home</span><span class="sep">›</span>Account</div>
        <div class="step-label">👤 Account &amp; contracts</div>
        <button class="faq-btn" onclick="showAnswer('reset-password')"><span class="icon">🔐</span><span class="btn-label">Reset my password</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showAnswer('add-user')"><span class="icon">👥</span><span class="btn-label">Add a team member to my account</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="showAnswer('contract')"><span class="icon">📝</span><span class="btn-label">Questions about my contract</span><span class="arrow">›</span></button>
        <button class="faq-btn" onclick="startChat('account')" style="border-color:#d4c9ff;background:#f5f0ff;"><span class="icon">💬</span><span class="btn-label" style="color:#5a3fcc;font-weight:600;">Chat with an agent</span><span class="arrow" style="color:#9b7aff;">›</span></button>
      </div>

      <!-- Create order -->
      <div class="faq-step" id="step-create-order">
        <div class="breadcrumb"><span onclick="backToMain()">🏠 Home</span><span class="sep">›</span>How to create an order</div>
        <div class="step-label">📝 Step-by-step guide</div>
        <div style="font-size:0.84rem;color:#2d2550;line-height:1.8;margin-bottom:1rem;">
          <ol style="margin:0;padding:0 0 0 1.2rem;display:flex;flex-direction:column;gap:0.55rem;">
            <li>🔑 <strong>Log in</strong> to your dashboard at <span style="color:#7c5cfc;font-weight:600;">app.bosta.co</span></li>
            <li>➕ Click <strong>New Shipment</strong> from the sidebar</li>
            <li>👤 Enter <strong>recipient details</strong> — name, phone, address</li>
            <li>📦 Fill in <strong>package details</strong> — weight, dimensions, COD</li>
            <li>📅 Select your <strong>pickup date and time slot</strong></li>
            <li>✅ Review and click <strong>Confirm Shipment</strong></li>
            <li>🏷️ Print your <strong>AWB label</strong> and attach it to the package</li>
            <li>🚚 Courier arrives on the <strong>scheduled pickup date</strong></li>
          </ol>
        </div>
        <div style="background:#f5f0ff;border:1.5px solid #d4c9ff;border-radius:12px;padding:0.8rem 1rem;font-size:0.8rem;color:#4c3a8a;line-height:1.6;margin-bottom:1rem;">
          💡 <strong>Pro tip:</strong> Create bulk orders via CSV upload or the Bosta API. Docs at <span style="color:#7c5cfc;">docs.bosta.co</span>
        </div>
        <button class="btn-chat" style="width:100%;font-size:0.9rem;" onclick="backToMain()">✓ Got it — back to main menu</button>
      </div>

      <!-- Answer view -->
      <div class="faq-step" id="step-answer">
        <div class="breadcrumb" id="answer-breadcrumb"></div>
        <div class="step-label">💡 Answer</div>
        <div class="answer-box" id="answer-text"></div>
        <p style="font-size:0.78rem;color:#b0aac8;margin-bottom:0.75rem;text-align:center;">Still not resolved? Our agents are ready to help 👇</p>
        <div class="prechat-actions">
          <button class="btn-back" id="answer-back-btn" onclick="backFromAnswer()">← Back</button>
          <button class="btn-chat" onclick="startChat('answer')">💬 Chat with an agent</button>
        </div>
      </div>

    </div>
  </div>
</div>

<script>
  function toggleFaq(el) {
    var answer = el.nextElementSibling;
    var icon = el.querySelector('span');
    var isOpen = answer.style.display === 'block';
    answer.style.display = isOpen ? 'none' : 'block';
    icon.textContent = isOpen ? '+' : '-';
  }
</script>

<script>
  var currentTopic = 'main';
  var flowPath = [];

  function recordStep(label) { flowPath.push(label); }

  function buildFlowSummary() {
    return 'Pre-chat flow: ' + flowPath.join(' > ');
  }

  var answers = {
    'track-order':         { text: 'Log in to your Bosta dashboard and go to Shipments then Tracking. Enter your AWB number to see real-time status updates and courier location.', back: 'shipment' },
    'lost-shipment':       { text: 'If your shipment shows lost or has had no movement for 5 or more business days, please chat with us so we can file an investigation with the courier team.', back: 'shipment' },
    'status-not-updating': { text: 'Status updates can take up to 2 hours after a scan event. If it has been more than 24 hours with no update, please contact our support team.', back: 'shipment' },
    'schedule-pickup':     { text: 'Go to Dashboard, then Create Shipment, then Schedule Pickup. You can book same-day pickup if requested before 12:00 PM, or next-day pickup anytime.', back: 'pickup' },
    'missed-pickup':       { text: 'We apologise for the inconvenience. Please chat with us with your pickup order ID and we will reschedule your pickup as a priority.', back: 'pickup' },
    'pickup-cutoff':       { text: 'The cutoff time for same-day pickup is 12:00 PM. Orders placed after that will be scheduled for the next business day.', back: 'pickup' },
    'wrong-address':       { text: 'Please chat with us immediately with your AWB number. We will coordinate with the courier to correct the delivery address or arrange a re-delivery.', back: 'delivery' },
    'damaged':             { text: 'Take photos of the damaged package and item, then chat with us within 48 hours of delivery. We will open a claim with our insurance and courier team.', back: 'delivery' },
    'initiate-return':     { text: 'Go to Dashboard, then Shipments, find your order and click Create Return. Our courier will pick up the item from the end customer within 1 to 3 business days.', back: 'returns' },
    'return-status':       { text: 'Return shipments can be tracked using the reverse AWB number found in Dashboard under Returns. Status updates in real time just like forward shipments.', back: 'returns' },
    'return-policy':       { text: 'Returns are accepted within 14 days of delivery. The item must be in original condition. Bosta covers return courier costs for eligible claims.', back: 'returns' },
    'invoice':             { text: 'Invoices are auto-generated on the 1st of each month and sent to your registered email. You can also download them from Dashboard under Billing then Invoices.', back: 'billing' },
    'pricing':             { text: 'Shipping costs are calculated based on package weight, dimensions, destination zone, and your contracted rate. View your rate card in Dashboard under Billing then Rate Card.', back: 'billing' },
    'dispute':             { text: 'To dispute a charge, go to Dashboard then Billing, find the charge and click Dispute. Or chat with us and our billing team will review within 2 business days.', back: 'billing' },
    'api-docs':            { text: 'Our full API documentation is available at docs.bosta.co. You will find REST endpoints, webhooks, authentication guides, and code samples.', back: 'integration' },
    'webhook':             { text: 'Webhooks notify your system of shipment events in real time. Configure them in Dashboard under Settings then Webhooks. Supported events include created, picked up, delivered, and failed.', back: 'integration' },
    'api-error':           { text: 'Common API errors: 401 means invalid API key, 422 means missing required fields, 429 means rate limit exceeded. Check our docs or chat with our tech team for help.', back: 'integration' },
    'reset-password':      { text: 'Go to bosta.co/login, click Forgot Password, then enter your email. You will receive a reset link within 5 minutes. Check your spam folder if you do not see it.', back: 'account' },
    'add-user':            { text: 'Go to Dashboard then Settings then Team Members then Invite User. Enter their email and assign a role such as Admin, Operations, or Finance. They will receive an invite email.', back: 'account' },
    'contract':            { text: 'For contract renewals, amendments, or pricing negotiations please chat with us and your dedicated account manager will reach out within 1 business day.', back: 'account' }
  };

  function openPrechat() {
    document.getElementById('prechat-overlay').classList.add('show');
    document.getElementById('fc-launcher').classList.add('hidden');
  }

  function closePrechat() {
    document.getElementById('prechat-overlay').classList.remove('show');
    document.getElementById('fc-launcher').classList.remove('hidden');
  }

  function showTopic(topic) {
    currentTopic = topic;
    recordStep(topicTitle(topic));
    document.querySelectorAll('.faq-step').forEach(function(s) { s.classList.remove('active'); });
    document.getElementById('step-' + topic).classList.add('active');
    document.getElementById('header-title').textContent = topicTitle(topic);
    document.getElementById('header-sub').textContent = 'Select your question below';
  }

  function topicTitle(t) {
    var map = {
      shipment: 'Shipment tracking', pickup: 'Pickup issues',
      delivery: 'Delivery problems', returns: 'Returns and reverse logistics',
      billing: 'Billing and invoices', integration: 'API and integration',
      account: 'Account management', 'create-order': 'How to create an order'
    };
    return map[t] || 'How can we help?';
  }

  function backToMain() {
    currentTopic = 'main';
    flowPath = [];
    document.querySelectorAll('.faq-step').forEach(function(s) { s.classList.remove('active'); });
    document.getElementById('step-main').classList.add('active');
    document.getElementById('header-title').textContent = 'How can we help?';
    document.getElementById('header-sub').textContent = 'Select a topic or chat with an agent';
  }

  function showAnswer(key) {
    var a = answers[key];
    if (!a) return;
    recordStep(key.replace(/-/g, ' '));
    document.getElementById('answer-text').textContent = a.text;
    document.getElementById('answer-back-btn').setAttribute('data-back', a.back);
    document.getElementById('answer-breadcrumb').innerHTML =
      '<span onclick="backToMain()">Topics</span> › <span onclick="showTopic(\'' + a.back + '\')">' + topicTitle(a.back) + '</span> › Answer';
    document.querySelectorAll('.faq-step').forEach(function(s) { s.classList.remove('active'); });
    document.getElementById('step-answer').classList.add('active');
    document.getElementById('header-title').textContent = 'Answer';
    document.getElementById('header-sub').textContent = 'Still need help? Chat with us';
  }

  function backFromAnswer() {
    var back = document.getElementById('answer-back-btn').getAttribute('data-back') || 'main';
    if (back === 'main') { backToMain(); } else { showTopic(back); }
  }

  function showTrackingStep() {
    recordStep('My delivery is delayed');
    document.querySelectorAll('.faq-step').forEach(function(s) { s.classList.remove('active'); });
    document.getElementById('step-tracking-input').classList.add('active');
    document.getElementById('header-title').textContent = 'Check delivery status';
    document.getElementById('header-sub').textContent = 'Enter your tracking number';
    document.getElementById('tracking-input').value = '';
    document.getElementById('tracking-error').style.display = 'none';
  }

  function checkTracking() {
    var val = document.getElementById('tracking-input').value.trim();
    if (!val) { document.getElementById('tracking-error').style.display = 'block'; return; }
    document.getElementById('tracking-error').style.display = 'none';
    recordStep('Delayed delivery - Tracking: ' + val);
    startChat('delayed-delivery');
  }

  function startChat(context) {
    var summary = buildFlowSummary();
    window._lastFlowSummary = summary;
    closePrechat();
    if (window.openFreshchat) {
      window.openFreshchat(summary);
    } else {
      setTimeout(function() {
        if (window.openFreshchat) { window.openFreshchat(summary); }
      }, 1500);
    }
  }
</script>

<script>
  var FC_API_TOKEN = window.FC_API_TOKEN = "eyJraWQiOiJjdXN0b20tb2F1dGgta2V5aWQiLCJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJmcmVzaGNoYXQiLCJhdWQiOiJmcmVzaGNoYXQiLCJpYXQiOjE3Nzg3OTQ5NDMsInNjb3BlIjoiYWdlbnQ6cmVhZCBhZ2VudDpjcmVhdGUgYWdlbnQ6dXBkYXRlIGFnZW50OmRlbGV0ZSBjb252ZXJzYXRpb246Y3JlYXRlIGNvbnZlcnNhdGlvbjpyZWFkIGNvbnZlcnNhdGlvbjp1cGRhdGUgbWVzc2FnZTpjcmVhdGUgbWVzc2FnZTpnZXQgYmlsbGluZzp1cGRhdGUgcmVwb3J0czpmZXRjaCByZXBvcnRzOmV4dHJhY3QgcmVwb3J0czpyZWFkIHJlcG9ydHM6ZXh0cmFjdDpyZWFkIGFjY291bnQ6cmVhZCBkYXNoYm9hcmQ6cmVhZCB1c2VyOnJlYWQgdXNlcjpjcmVhdGUgdXNlcjp1cGRhdGUgdXNlcjpkZWxldGUgb3V0Ym91bmRtZXNzYWdlOnNlbmQgb3V0Ym91bmRtZXNzYWdlOmdldCBtZXNzYWdpbmctY2hhbm5lbHM6bWVzc2FnZTpzZW5kIG1lc3NhZ2luZy1jaGFubmVsczptZXNzYWdlOmdldCBtZXNzYWdpbmctY2hhbm5lbHM6dGVtcGxhdGU6Y3JlYXRlIG1lc3NhZ2luZy1jaGFubmVsczp0ZW1wbGF0ZTpnZXQgZmlsdGVyaW5ib3g6cmVhZCBmaWx0ZXJpbmJveDpjb3VudDpyZWFkIHJvbGU6cmVhZCBpbWFnZTp1cGxvYWQiLCJ0eXAiOiJCZWFyZXIiLCJjbGllbnRJZCI6ImZjLTdmOGZmNDFmLTAwN2ItNDA0YS05ZDI1LWYwOGMzZDBkYjUyNCIsInN1YiI6ImZhMWJjMDg1LWMwODktNGFkMS04YzdiLWMxMzBhY2U2MjYzNyIsImp0aSI6ImVhOTEzOGQxLTZhYzAtNDg4OC1hYmE4LTA3NmRhNmY4NGM0ZCIsImV4cCI6MjA5NDQxNDE0M30.OShqwfrNQT-ayCRBWLUpjx-nmPd885txPSgUtP1IQK4";
  var FC_API_HOST  = "https://api.freshchat.com";

  /* POST message via REST API — works on all devices including mobile */
  function sendFlowViaAPI(conversationId, flowSummary) {
    fetch(FC_API_HOST + '/v2/conversations/' + conversationId + '/messages', {
      method: 'POST',
      headers: {
        'Authorization': 'Bearer ' + FC_API_TOKEN,
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        message_type: 'normal',
        actor_type: 'system',
        message_parts: [{ text: { content: flowSummary } }]
      })
    })
    .then(function(r) { return r.json(); })
    .then(function(d) {
      console.log('Flow sent via API:', d);
      /* Store conversation ID from successful send response */
      if (d && d.conversation_id && !window._conversationId) {
        window._conversationId = d.conversation_id;
        console.log('Conversation ID from send response:', window._conversationId);
      }
    })
    .catch(function(e) { console.error('Flow send error:', e); });
  }

  /* Fetch full conversation details from REST API */
  function fetchConversationDetails(convId) {
    return fetch(FC_API_HOST + '/v2/conversations/' + convId, {
      headers: { 'Authorization': 'Bearer ' + FC_API_TOKEN }
    })
    .then(function(r) { return r.json(); })
    .then(function(d) {
      console.log('Conversation details:', d);
      if (d && d.conversation_id) {
        window._conversationId = d.conversation_id;
        if (d.assigned_agent) {
          window._agentName = (d.assigned_agent.first_name || '') + ' ' + (d.assigned_agent.last_name || '');
          window._agentName = window._agentName.trim();
        }
        if (d.channel && d.channel.name) window._channelName = d.channel.name;
      }
      return d;
    })
    .catch(function(e) { console.error('Fetch conversation error:', e); });
  }

  window.fcSettings = {
    token: "259d6c03-7a44-45ac-bd57-2a43ba360080",
    host: "https://wchat-fs.freshchat.com",
    config: { hideFAB: true }
  };

  var fcStyle = document.createElement('style');
  fcStyle.textContent = '#fc_frame:not(.fc-open){display:none!important}.fc-widget-btn{display:none!important}';
  document.head.appendChild(fcStyle);

  window.openFreshchat = function(flowSummary) {
    function tryOpen() {
      if (window.fcWidget && window.fcWidget.isInitialized()) {

        /* Set user meta visible in agent contact panel */
        try {
          window.fcWidget.user.setMeta({
            pre_chat_topic:    flowPath[0] || '',
            pre_chat_question: flowPath[1] || '',
            pre_chat_path:     flowSummary
          });
        } catch(e) {}

        /* Open on correct topic */
        try { window.fcWidget.open({ topic: 'Chat with us' }); }
        catch(e) { window.fcWidget.open(); }

        window.fcWidget.show();

        /* When conversation is created — store ID and send flow via REST API (works on mobile too) */
        try {
          window.fcWidget.on('conversation:created', function(resp) {
            console.log('conversation:created full response:', JSON.stringify(resp));
            var convId = resp && resp.data && (resp.data.conversationId || resp.data.conversation_id);
            if (convId) {
              console.log('Conversation created ID:', convId);
              window._conversationId = convId;
              setTimeout(function() {
                sendFlowViaAPI(convId, flowSummary);
                fetchConversationDetails(convId);
              }, 1000);
            }
          });
        } catch(e) {}

        /* Fallback: poll getConversationId every second for up to 10s */
        var pollCount = 0;
        var pollInterval = setInterval(function() {
          pollCount++;
          try {
            window.fcWidget.getConversationId().then(function(convId) {
              if (convId) {
                clearInterval(pollInterval);
                if (!window._conversationId) {
                  window._conversationId = convId;
                  sendFlowViaAPI(convId, flowSummary);
                }
              }
            }).catch(function() {});
          } catch(e) {}
          if (pollCount >= 10) clearInterval(pollInterval);
        }, 1000);

        /* Capture user info from widget — alias is available even without email */
        try {
          window.fcWidget.user.get().then(function(resp) {
            if (resp && resp.data) {
              window._fcUser = {
                email:      resp.data.email || '',
                firstName:  resp.data.firstName || resp.data.first_name || '',
                lastName:   resp.data.lastName || resp.data.last_name || '',
                alias:      resp.data.alias || ''
              };
              console.log('User info:', window._fcUser);
            }
          }).catch(function() {});
        } catch(e) {}

        /* Show survey when conversation is resolved */
        try {
          window.fcWidget.on('conversation:resolved', function(resp) {
            console.log('Conversation resolved event:', JSON.stringify(resp));

            /* ── Business hours check ──────────────────────────────
               Only show survey during business hours
               Timezone: Africa/Cairo (UTC+3)
               Hours: Sun-Thu 9:00 AM - 6:00 PM
               Adjust BUSINESS_HOURS to match your actual hours  */
            var BUSINESS_HOURS = {
              timezone:  'Africa/Cairo',
              days:      [0, 1, 2, 3, 4, 6], /* 0=Sun, 1=Mon, 2=Tue, 3=Wed, 4=Thu, 6=Sat */
              startHour: 10,
              endHour:   18
            };

            function isWithinBusinessHours() {
              try {
                var now = new Date();
                var localTime = new Date(now.toLocaleString('en-US', { timeZone: BUSINESS_HOURS.timezone }));
                var day  = localTime.getDay();
                var hour = localTime.getHours();
                var inDay  = BUSINESS_HOURS.days.indexOf(day) !== -1;
                var inHour = hour >= BUSINESS_HOURS.startHour && hour < BUSINESS_HOURS.endHour;
                console.log('Business hours check — day:', day, 'hour:', hour, 'inDay:', inDay, 'inHour:', inHour);
                return inDay && inHour;
              } catch(e) {
                return true; /* If check fails, show survey anyway */
              }
            }

            if (!isWithinBusinessHours()) {
              console.log('Outside business hours — survey skipped');
              return;
            }
            /* ─────────────────────────────────────────────────────── */

            /* Reset so survey shows again */
            window._csatShown = false;

            /* Set resolved_at immediately */
            window._resolvedAt = new Date().toISOString();

            /* Extract conversation ID from event */
            try {
              var conv = resp && resp.data && resp.data.conversation;
              if (conv && conv.conversationId) {
                window._conversationId = String(conv.conversationId);
              }
              if (resp.data && resp.data.resolvedAt) {
                window._resolvedAt = resp.data.resolvedAt;
              }
            } catch(e) {}

            console.log('conversation_id:', window._conversationId);
            console.log('resolved_at:', window._resolvedAt);

            /* Fetch agent name + group name via REST API using conversation ID */
            if (window._conversationId && window.FC_API_TOKEN) {
              fetch('https://api.freshchat.com/v2/conversations/' + window._conversationId, {
                headers: { 'Authorization': 'Bearer ' + window.FC_API_TOKEN }
              })
              .then(function(r) { return r.json(); })
              .then(function(d) {
                console.log('Conversation details:', d);
                if (d && d.assigned_agent) {
                  window._agentName = (d.assigned_agent.first_name || '') + ' ' + (d.assigned_agent.last_name || '');
                  window._agentName = window._agentName.trim();
                }
                if (d && d.assigned_group) {
                  window._groupName = d.assigned_group.name || '';
                }
                console.log('Agent:', window._agentName, 'Group:', window._groupName);
                setTimeout(showSurvey, 300);
              })
              .catch(function() {
                /* CORS blocked — show survey without agent/group */
                setTimeout(showSurvey, 300);
              });
            } else {
              setTimeout(showSurvey, 800);
            }
          });
        } catch(e) {}

        window.fcWidget.on('widget:closed', function() {
          clearInterval(pollInterval);
          window.fcWidget.hide();
          document.getElementById('fc-launcher').classList.remove('hidden');
        });

      } else {
        setTimeout(tryOpen, 400);
      }
    }
    tryOpen();
  };
</script>
<script src="https://wchat-fs.freshchat.com/js/widget.js" async></script>

<!-- Custom CSAT Flow -->
<style>
  #csat-widget {
    display: none; position: fixed; bottom: 15px; right: 15px; z-index: 99999;
    width: 380px; border-radius: 16px; overflow: hidden;
    box-shadow: 0 8px 40px rgba(0,0,0,0.25);
    flex-direction: column; animation: popUp 0.35s cubic-bezier(.34,1.56,.64,1);
    font-family: 'DM Sans', sans-serif; direction: rtl;
  }
  #csat-widget.show { display: flex; }
  #csat-widget-header {
    background: linear-gradient(135deg, #E30613, #a80000);
    padding: 0.9rem 1.1rem; flex-shrink: 0;
  }
  #csat-widget-header .hw-title {
    color: #fff; font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.9rem;
  }
  #csat-progress { height: 3px; background: #f0e0e0; flex-shrink: 0; }
  #csat-progress-bar { height: 100%; background: linear-gradient(90deg, #E30613, #ff6666); transition: width 0.4s ease; width: 20%; }
  #csat-body { padding: 1.5rem 1.25rem 1.25rem; background: #fff; }
  .csat-step { display: none; animation: fadeIn 0.22s ease; }
  .csat-step.active { display: block; }
  .csat-q {
    font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.95rem;
    color: #1a1a2e; line-height: 1.6; margin-bottom: 1.25rem; text-align: right;
  }
  .csat-choices { display: flex; flex-direction: column; gap: 0.5rem; }
  .csat-choice {
    width: 100%; padding: 0.7rem 1rem; border-radius: 10px;
    border: 1.5px solid #ffe5e5; background: #fafafa;
    font-family: 'DM Sans', sans-serif; font-size: 0.875rem; font-weight: 500;
    color: #1a1a2e; cursor: pointer; text-align: right; transition: all 0.18s;
  }
  .csat-choice:hover { background: #fff0f0; border-color: #E30613; color: #b30000; }
  .csat-choice.selected { background: #E30613; border-color: #E30613; color: #fff; }
  .star-scale { display: flex; justify-content: space-between; gap: 0.3rem; margin-bottom: 0.5rem; }
  .star-num {
    flex: 1; padding: 0.65rem 0; border-radius: 8px; border: 1.5px solid #ffe5e5;
    background: #fafafa; font-size: 1rem; font-weight: 700; color: #888;
    cursor: pointer; text-align: center; transition: all 0.18s;
  }
  .star-num:hover { background: #fff0f0; border-color: #E30613; color: #E30613; }
  .star-num.selected { background: #E30613; border-color: #E30613; color: #fff; }
  .star-labels { display: flex; justify-content: space-between; font-size: 0.72rem; color: #aaa; margin-bottom: 1rem; }
  .csat-textarea {
    width: 100%; padding: 0.75rem; border: 1.5px solid #ffe5e5; border-radius: 10px;
    font-family: 'DM Sans', sans-serif; font-size: 0.875rem; color: #1a1a2e;
    resize: none; outline: none; transition: border-color 0.2s; box-sizing: border-box;
    text-align: right; direction: rtl;
  }
  .csat-textarea:focus { border-color: #E30613; }
  .csat-next {
    width: 100%; padding: 0.75rem; border-radius: 10px;
    background: linear-gradient(135deg, #E30613, #a80000);
    color: #fff; border: none; font-family: 'Syne', sans-serif;
    font-weight: 700; font-size: 0.875rem; cursor: pointer; transition: opacity 0.2s; margin-top: 0.75rem;
  }
  .csat-next:hover { opacity: 0.88; }
  .csat-next:disabled { background: #e5e7eb; color: #9ca3af; cursor: not-allowed; }
  .csat-skip { display: block; text-align: center; font-size: 0.75rem; color: #bbb; cursor: pointer; margin-top: 0.6rem; text-decoration: underline; }
  .csat-skip:hover { color: #888; }
  .csat-ending { text-align: center; padding: 0.5rem 0 0.25rem; }
  .csat-ending .e-icon { font-size: 2.8rem; display: block; margin-bottom: 0.75rem; }
  .csat-ending p { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.95rem; color: #1a1a2e; line-height: 1.7; direction: rtl; }
  @media (max-width: 480px) { #csat-widget { width: 100%; bottom: 0; right: 0; border-radius: 0; } }
</style>

<div id="csat-widget">
  <div id="csat-widget-header">
    <div class="hw-title">&#11088; &#1603;&#1610;&#1601; &#1603;&#1575;&#1606;&#1578; &#1578;&#1580;&#1585;&#1576;&#1578;&#1603;&#1567;</div>
  </div>
  <div id="csat-progress"><div id="csat-progress-bar"></div></div>
  <div id="csat-body">

    <div class="csat-step active" id="csat-q1">
      <div class="csat-q">&#1602;&#1610;&#1605; &#1578;&#1580;&#1585;&#1576;&#1578;&#1603; &#1605;&#1593; &#1576;&#1608;&#1587;&#1591;&#1607; &#1582;&#1604;&#1575;&#1604; &#1575;&#1604;&#1605;&#1581;&#1575;&#1583;&#1579;&#1607;<br><span style="font-weight:400;font-size:0.82rem;color:#888;">&#1578;&#1602;&#1610;&#1610;&#1605;&#1603; &#1610;&#1607;&#1605;&#1606;&#1575; &#128522;</span></div>
      <div class="csat-choices">
        <button class="csat-choice" onclick="csatChoice('q1','rate',2)">&#11088; &#1578;&#1602;&#1610;&#1610;&#1605; &#1575;&#1604;&#1605;&#1581;&#1575;&#1583;&#1579;&#1577;</button>
        <button class="csat-choice" onclick="csatContinueChat()">&#128172; &#1575;&#1587;&#1578;&#1605;&#1585;&#1575;&#1585; &#1575;&#1604;&#1605;&#1581;&#1575;&#1583;&#1579;&#1577;</button>
      </div>
    </div>

    <div class="csat-step" id="csat-q2">
      <div class="csat-q">&#1603;&#1610;&#1601; &#1603;&#1575;&#1606;&#1578; &#1578;&#1580;&#1585;&#1576;&#1578;&#1603; &#1605;&#1593; &#1605;&#1608;&#1592;&#1601; &#1582;&#1583;&#1605;&#1577; &#1575;&#1604;&#1593;&#1605;&#1604;&#1575;&#1569;&#1567;</div>
      <div class="star-scale" id="scale-q2">
        <button class="star-num" onclick="csatStar('q2',1)">1</button>
        <button class="star-num" onclick="csatStar('q2',2)">2</button>
        <button class="star-num" onclick="csatStar('q2',3)">3</button>
        <button class="star-num" onclick="csatStar('q2',4)">4</button>
        <button class="star-num" onclick="csatStar('q2',5)">5</button>
      </div>
      <div class="star-labels"><span>&#1587;&#1610;&#1569; &#128542;</span><span>&#1605;&#1605;&#1578;&#1575;&#1586; &#129321;</span></div>
      <button class="csat-next" id="next-q2" onclick="csatStep(3)" disabled>&#1575;&#1604;&#1578;&#1575;&#1604;&#1610; &#8592;</button>
    </div>

    <div class="csat-step" id="csat-q3">
      <div class="csat-q">&#1607;&#1604; &#1578;&#1605; &#1581;&#1604; &#1605;&#1588;&#1603;&#1604;&#1578;&#1603; &#1582;&#1604;&#1575;&#1604; &#1607;&#1584;&#1607; &#1575;&#1604;&#1605;&#1581;&#1575;&#1583;&#1579;&#1577;&#1567;</div>
      <div class="csat-choices">
        <button class="csat-choice" onclick="csatChoice('q3','yes','ending-yes')">&#9989; &#1606;&#1593;&#1605;&#1548; &#1578;&#1605; &#1581;&#1604;&#1607;&#1575; &#1576;&#1575;&#1604;&#1603;&#1575;&#1605;&#1604;</button>
        <button class="csat-choice" onclick="csatChoice('q3','partial',4)">&#9888;&#65039; &#1578;&#1605; &#1581;&#1604;&#1607;&#1575; &#1580;&#1586;&#1574;&#1610;&#1575;&#1611;</button>
        <button class="csat-choice" onclick="csatChoice('q3','no',4)">&#10060; &#1604;&#1575;&#1548; &#1604;&#1605; &#1610;&#1578;&#1605; &#1581;&#1604;&#1607;&#1575;</button>
      </div>
    </div>

    <div class="csat-step" id="csat-q4">
      <div class="csat-q">&#1605;&#1575; &#1587;&#1576;&#1576; &#1593;&#1583;&#1605; &#1575;&#1604;&#1581;&#1604; &#1575;&#1604;&#1603;&#1575;&#1605;&#1604;&#1567;</div>
      <div class="csat-choices" id="reasons-list">
        <button class="csat-choice" onclick="csatReason(this,'bot')">&#129302; &#1575;&#1604;&#1576;&#1608;&#1578; &#1604;&#1605; &#1610;&#1601;&#1607;&#1605; &#1605;&#1588;&#1603;&#1604;&#1578;&#1610;</button>
        <button class="csat-choice" onclick="csatReason(this,'policy')">&#128203; &#1594;&#1610;&#1585; &#1585;&#1575;&#1590;&#1613; &#1593;&#1606; &#1575;&#1604;&#1581;&#1604; &#1571;&#1608; &#1587;&#1610;&#1575;&#1587;&#1577; &#1575;&#1604;&#1578;&#1593;&#1608;&#1610;&#1590;&#1575;&#1578;</button>
        <button class="csat-choice" onclick="csatReason(this,'sla')">&#9203; &#1575;&#1587;&#1578;&#1594;&#1585;&#1602; &#1575;&#1604;&#1581;&#1604; &#1608;&#1602;&#1578;&#1611;&#1575; &#1571;&#1591;&#1608;&#1604; &#1605;&#1606; SLA</button>
        <button class="csat-choice" onclick="csatReason(this,'unclear')">&#10067; &#1604;&#1605; &#1571;&#1581;&#1589;&#1604; &#1593;&#1604;&#1609; &#1581;&#1604; &#1608;&#1575;&#1590;&#1581; &#1571;&#1608; &#1605;&#1608;&#1593;&#1583; &#1604;&#1604;&#1605;&#1578;&#1575;&#1576;&#1593;&#1577;</button>
        <button class="csat-choice" onclick="csatReason(this,'other')">&#128172; &#1571;&#1582;&#1585;&#1609;</button>
      </div>
      <button class="csat-next" id="next-q4" onclick="csatStep(5)" disabled>&#1575;&#1604;&#1578;&#1575;&#1604;&#1610; &#8592;</button>
    </div>

    <div class="csat-step" id="csat-q5">
      <div class="csat-q">&#1607;&#1604; &#1604;&#1583;&#1610;&#1603; &#1575;&#1610; &#1578;&#1593;&#1604;&#1610;&#1602; &#1578;&#1585;&#1610;&#1583; &#1605;&#1588;&#1575;&#1585;&#1603;&#1578;&#1607;&#1567;</div>
      <textarea class="csat-textarea" id="csat-comment" rows="4" placeholder="&#1575;&#1603;&#1578;&#1576; &#1578;&#1593;&#1604;&#1610;&#1602;&#1603; &#1607;&#1606;&#1575;..."></textarea>
      <button class="csat-next" onclick="csatSubmit()">&#1573;&#1585;&#1587;&#1575;&#1604; &#10003;</button>
      <span class="csat-skip" onclick="csatSubmit()">&#1578;&#1582;&#1591;&#1610;</span>
    </div>

    <div class="csat-step" id="csat-ending-yes">
      <div class="csat-ending">
        <span class="e-icon">&#127881;</span>
        <p>&#1588;&#1603;&#1585;&#1611;&#1575; &#1604;&#1578;&#1608;&#1575;&#1589;&#1604;&#1603; &#1605;&#1593; &#1576;&#1608;&#1587;&#1591;&#1607;<br>&#1606;&#1578;&#1605;&#1606;&#1609; &#1578;&#1602;&#1583;&#1610;&#1605; &#1575;&#1601;&#1590;&#1604; &#1582;&#1583;&#1605;&#1607; &#1604;&#1588;&#1585;&#1575;&#1603;&#1574;&#1606;&#1575; &#1583;&#1575;&#1574;&#1605;&#1575;</p>
      </div>
    </div>

    <div class="csat-step" id="csat-ending-final">
      <div class="csat-ending">
        <span class="e-icon">&#127881;</span>
        <p>&#1588;&#1603;&#1585;&#1611;&#1575; &#1604;&#1578;&#1608;&#1575;&#1589;&#1604;&#1603; &#1605;&#1593; &#1576;&#1608;&#1587;&#1591;&#1607;<br>&#1606;&#1578;&#1605;&#1606;&#1609; &#1578;&#1602;&#1583;&#1610;&#1605; &#1575;&#1601;&#1590;&#1604; &#1582;&#1583;&#1605;&#1607; &#1604;&#1588;&#1585;&#1575;&#1603;&#1574;&#1606;&#1575; &#1583;&#1575;&#1574;&#1605;&#1575;</p>
      </div>
    </div>

  </div>
</div>

<script>
  var csatData  = {};
  var csatSteps = { 2:25, 3:50, 4:65, 5:85 };

  function showSurvey() {
    if (window._csatShown) return;
    window._csatShown = true;
    try { if (window.fcWidget) { window.fcWidget.close(); window.fcWidget.hide(); } } catch(e) {}
    var fc = document.getElementById('fc_frame');
    if (fc) fc.style.display = 'none';
    var launcher = document.getElementById('fc-launcher');
    if (launcher) launcher.classList.add('hidden');
    csatData = {
      conversation_id: window._conversationId || '',
      resolved_at:     window._resolvedAt     || '',
      agent_name:      window._agentName      || '',
      group_name:      window._groupName      || '',
      pre_chat_topic:  window.flowPath && window.flowPath[0] ? window.flowPath[0] : '',
      first_name:      window._fcUser && window._fcUser.firstName ? window._fcUser.firstName : ''
    };
    document.querySelectorAll('.csat-step').forEach(function(s) { s.classList.remove('active'); });
    document.getElementById('csat-q1').classList.add('active');
    document.getElementById('csat-progress-bar').style.width = '20%';
    document.querySelectorAll('.star-num, .csat-choice').forEach(function(b) { b.classList.remove('selected'); });
    document.getElementById('next-q2').disabled = true;
    document.getElementById('next-q4').disabled = true;
    document.getElementById('csat-comment').value = '';
    document.getElementById('csat-widget').classList.add('show');
  }

  function csatStep(n) {
    document.querySelectorAll('.csat-step').forEach(function(s) { s.classList.remove('active'); });
    var id = (n === 'ending-yes' || n === 'ending-final') ? 'csat-' + n : 'csat-q' + n;
    document.getElementById(id).classList.add('active');
    var pct = (n === 'ending-yes' || n === 'ending-final') ? 100 : (csatSteps[n] || 20);
    document.getElementById('csat-progress-bar').style.width = pct + '%';
    saveProgress();
  }

  function csatChoice(key, val, next) {
    csatData[key] = val;
    if (next === 'ending-yes') { csatStep('ending-yes'); autoClose(); }
    else { csatStep(next); }
    saveProgress();
  }

  function csatContinueChat() {
    document.getElementById('csat-widget').classList.remove('show');
    window._csatShown = false;
    var fc = document.getElementById('fc_frame');
    if (fc) fc.style.display = '';
    try { if (window.fcWidget) { window.fcWidget.show(); window.fcWidget.open(); } } catch(e) {}
  }

  function csatStar(key, val) {
    csatData[key] = val;
    document.querySelectorAll('#scale-' + key + ' .star-num').forEach(function(b, i) {
      b.classList.toggle('selected', i < val);
    });
    document.getElementById('next-' + key).disabled = false;
    saveProgress();
  }

  function csatReason(el, val) {
    csatData['reason'] = val;
    document.querySelectorAll('#reasons-list .csat-choice').forEach(function(b) { b.classList.remove('selected'); });
    el.classList.add('selected');
    document.getElementById('next-q4').disabled = false;
    saveProgress();
  }

  function csatSubmit() {
    csatData['comment'] = document.getElementById('csat-comment').value;
    csatData['status']  = 'completed';
    csatStep('ending-final');
    autoClose();
    saveProgress();
    console.log('CSAT submitted:', csatData);
  }

  function autoClose() {
    setTimeout(function() {
      document.getElementById('csat-widget').classList.remove('show');
      window._csatShown = false;
      var launcher = document.getElementById('fc-launcher');
      if (launcher) launcher.classList.remove('hidden');
    }, 4000);
  }

  function saveProgress() {
    csatData['timestamp'] = new Date().toISOString();
    csatData['status']    = csatData['status'] || 'partial';
    console.log('CSAT progress:', csatData);
  }

  function showTypeform() { showSurvey(); }
  function closeTypeform() {
    document.getElementById('csat-widget').classList.remove('show');
    window._csatShown = false;
    var launcher = document.getElementById('fc-launcher');
    if (launcher) launcher.classList.remove('hidden');
  }
</script>

<!-- Freshdesk Widget -->
<script>
function initFreshdesk() {
  window.fdWidget.init({
    token: "01KXAS39C57EY6T3SPNEV63BP7",
    host: "https://bosta1922.freshdesk.com",
    widgetId: "01KXAS3BYNPDXXAFTXEF7HXMZ6"
  });
}
function initialize(i,t){var e;i.getElementById(t)?initFreshdesk():((e=i.createElement("script")).id=t,e.async=!0,e.src="https://bosta1922.freshdesk.com/webchat/js/widget.js",e.onload=initFreshdesk,i.head.appendChild(e))}function initiateCall(){initialize(document,"Freshdesk-js-sdk")}window.addEventListener?window.addEventListener("load",initiateCall,!1):window.attachEvent("load",initiateCall,!1);
</script>

</body>
</html>
