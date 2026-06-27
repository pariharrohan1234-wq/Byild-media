<!DOCTYPE html>

<html data-theme="dark" lang="en">
<head>
<meta charset="utf-8"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<meta content="BYILD Media creates distinctive, interactive websites that make brands impossible to ignore." name="description"/>
<title>BYILD Media | Making Your Website Less Boring</title>
<link href="https://fonts.googleapis.com" rel="preconnect"/>
<link crossorigin="" href="https://fonts.gstatic.com" rel="preconnect"/>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght,SOFT,WONK@9..144,300..800,50..100,0..1&amp;family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&amp;display=swap" rel="stylesheet"/>
<style>
    /* ─── TOKENS: DARK (default) ─── */
    :root {
      --black:       #080808;
      --surface:     #111111;
      --surface-2:   #181818;
      --border:      rgba(201,185,154,0.14);
      --gold:        #C9B99A;
      --gold-bright: #E2CFA8;
      --gold-dim:    rgba(201,185,154,0.3);
      --white:       #FFFFFF;
      --text:        rgba(255,255,255,0.88);
      --text-muted:  rgba(255,255,255,0.48);
      --text-dim:    rgba(255,255,255,0.28);

      --font-head: 'Fraunces', Georgia, serif;
      --font-body: 'Plus Jakarta Sans', system-ui, sans-serif;

      --ease: cubic-bezier(0.22,1,0.36,1);
      --t:    200ms var(--ease);
      --ts:   400ms var(--ease);

      --r-sm: 6px;
      --r-md: 12px;
      --r-lg: 20px;

      --shadow-gold: 0 0 40px rgba(201,185,154,0.1);
    }

    /* ─── TOKENS: LIGHT ─── */
    [data-theme="light"] {
      --black:       #F7F4EE;
      --surface:     #EDE9E1;
      --surface-2:   #E5E0D6;
      --border:      rgba(100,80,50,0.18);
      --gold:        #7A6245;
      --gold-bright: #9A7C56;
      --gold-dim:    rgba(100,80,50,0.25);
      --white:       #1C1208;
      --text:        rgba(28,18,8,0.88);
      --text-muted:  rgba(28,18,8,0.55);
      --text-dim:    rgba(28,18,8,0.32);
      --shadow-gold: 0 0 40px rgba(100,80,50,0.12);
    }

    /* ─── RESET ─── */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; font-size: 16px; }
    body {
      font-family: var(--font-body);
      background: var(--black);
      color: var(--text);
      line-height: 1.7;
      overflow-x: hidden;
      cursor: auto;
      transition: background 0.4s ease, color 0.4s ease;
    }
    body::before {
      content: ''; position: fixed; inset: 0; z-index: -2; pointer-events: none;
      background:
        radial-gradient(circle at 16% 12%, rgba(226,207,168,0.10), transparent 28%),
        radial-gradient(circle at 84% 26%, rgba(201,185,154,0.08), transparent 30%),
        radial-gradient(circle at 52% 90%, rgba(226,207,168,0.055), transparent 34%);
      transform: translate3d(0, calc(var(--scroll, 0) * -0.025px), 0);
    }
    body::after {
      content: ''; position: fixed; inset: 0; z-index: 9997; pointer-events: none; opacity: 0.035;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 220 220' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.7' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.75'/%3E%3C/svg%3E");
      mix-blend-mode: overlay;
    }
    img  { display: block; max-width: 100%; }
    a    { text-decoration: none; color: inherit; cursor: auto; }
    button { cursor: auto; border: none; background: none; font-family: inherit; }
    ul   { list-style: none; }

    .skip-link {
      position: absolute; top: -50px; left: 1rem;
      background: var(--gold); color: var(--black);
      padding: 10px 18px; border-radius: 0 0 6px 6px;
      font-size: 0.85rem; font-weight: 600; z-index: 9999;
      transition: top var(--t);
    }
    .skip-link:focus { top: 0; }

    /* ─── SCROLLBAR ─── */
    ::-webkit-scrollbar { width: 3px; }
    ::-webkit-scrollbar-track { background: var(--black); }
    ::-webkit-scrollbar-thumb { background: var(--gold-dim); border-radius: 2px; }

    /* ─── SELECTION ─── */
    ::selection { background: var(--gold); color: var(--black); }

    /* ─── CUSTOM CURSOR ─── */
    .cursor-orb {
      position: fixed;
      pointer-events: none;
      z-index: 9998;
      width: 36px; height: 36px;
      border-radius: 50%;
      background: rgba(201,185,154,0.08);
      backdrop-filter: blur(6px);
      -webkit-backdrop-filter: blur(6px);
      border: 1px solid rgba(201,185,154,0.25);
      transform: translate(-50%, -50%);
      transition: width 0.3s var(--ease), height 0.3s var(--ease), background 0.3s ease, border-color 0.3s ease, opacity 0.3s ease;
      top: 0; left: 0;
    }
    .cursor-dot {
      position: fixed;
      pointer-events: none;
      z-index: 9999;
      width: 5px; height: 5px;
      border-radius: 50%;
      background: var(--gold);
      transform: translate(-50%, -50%);
      top: 0; left: 0;
      transition: opacity 0.3s ease;
    }
    .cursor-orb.expanded {
      width: 64px; height: 64px;
      background: rgba(201,185,154,0.12);
      border-color: rgba(201,185,154,0.4);
    }
    [data-theme="light"] .cursor-orb {
      background: rgba(100,80,50,0.08);
      border-color: rgba(100,80,50,0.25);
    }
    [data-theme="light"] .cursor-orb.expanded {
      background: rgba(100,80,50,0.12);
      border-color: rgba(100,80,50,0.4);
    }
    [data-theme="light"] .cursor-dot { background: var(--gold); }
    @media (hover: none) {
      .cursor-orb, .cursor-dot { display: none; }
      body, a, button { cursor: auto; }
    }

    /* ─── LAYOUT ─── */
    section { padding: 7rem 0; }
    .container { max-width: 1200px; margin: 0 auto; padding: 0 2rem; }
    .section-label {
      display: inline-block;
      font-size: 0.65rem; font-weight: 600; letter-spacing: 0.28em; text-transform: uppercase;
      color: var(--gold); margin-bottom: 1rem; font-family: var(--font-body);
    }
    .section-title {
      font-family: var(--font-head);
      font-size: clamp(2.4rem, 5vw, 4rem); font-weight: 600;
      color: var(--white); line-height: 1.08; letter-spacing: -0.01em;
    }
    .section-sub {
      font-size: 1rem; color: var(--text-muted); line-height: 1.85;
      max-width: 560px; margin-top: 1rem; font-weight: 300;
    }
    .text-center { text-align: center; }
    .text-center .section-sub { margin: 1rem auto 0; }
    .gold { color: var(--gold); }

    /* ─── BUTTONS ─── */
    .btn {
      display: inline-flex; align-items: center; gap: 0.5rem;
      padding: 0.9rem 2rem; min-height: 50px;
      font-family: var(--font-body); font-size: 0.78rem; font-weight: 600;
      letter-spacing: 0.1em; text-transform: uppercase;
      border-radius: var(--r-sm); cursor: auto;
      touch-action: manipulation;
      transition: transform var(--t), box-shadow var(--t), background var(--t), border-color var(--t);
    }
    .btn:active { transform: scale(0.97) !important; }
    .btn:focus  { outline: 2px solid var(--gold); outline-offset: 3px; }

    .btn-gold {
      background: var(--gold); color: #080808;
    }
    .btn-gold:hover { background: var(--gold-bright); transform: translateY(-2px); box-shadow: 0 12px 30px rgba(201,185,154,0.25); }

    .btn-outline {
      border: 1px solid var(--border); color: var(--text);
      background: transparent;
    }
    .btn-outline:hover { border-color: var(--gold); color: var(--gold); transform: translateY(-2px); }

    /* ─── THEME TOGGLE ─── */
    .theme-toggle {
      width: 44px; height: 44px;
      display: flex; align-items: center; justify-content: center;
      border: 1px solid var(--border); border-radius: var(--r-sm);
      color: var(--text-muted); cursor: auto;
      transition: border-color var(--t), color var(--t), background var(--t);
      flex-shrink: 0;
    }
    .theme-toggle:hover { border-color: var(--gold); color: var(--gold); }
    .theme-toggle:focus { outline: 2px solid var(--gold); outline-offset: 3px; }
    .theme-toggle svg { width: 16px; height: 16px; pointer-events: none; }
    .icon-moon { display: block; }
    .icon-sun  { display: none; }
    [data-theme="light"] .icon-moon { display: none; }
    [data-theme="light"] .icon-sun  { display: block; }

    /* ─── NAV ─── */
    .nav {
      position: fixed; top: 0; left: 0; right: 0; z-index: 100;
      padding: 1.4rem 2rem;
      display: flex; align-items: center; justify-content: space-between;
      transition: background var(--ts), backdrop-filter var(--ts), padding var(--ts), border-color var(--ts);
    }
    .nav.scrolled {
      background: rgba(8,8,8,0.88);
      backdrop-filter: blur(24px);
      -webkit-backdrop-filter: blur(24px);
      padding: 1rem 2rem;
      border-bottom: 1px solid var(--border);
    }
    [data-theme="light"] .nav.scrolled {
      background: rgba(247,244,238,0.88);
    }

    .nav-logo {
      display: flex; align-items: center; gap: 0.75rem;
    }
    .nav-logo img {
      width: 46px; height: 58px; object-fit: cover; object-position: center;
      border-radius: 14px; box-shadow: 0 10px 30px rgba(0,0,0,.20);
      transition: transform var(--t), box-shadow var(--t);
    }
    .nav-logo:hover img { transform: translateY(-2px) rotate(-2deg); box-shadow: 0 15px 38px rgba(0,0,0,.28); }

    .nav-right {
      display: flex; align-items: center; gap: 1rem;
    }
    .nav-links {
      display: flex; align-items: center; gap: 2.5rem;
    }
    .nav-links a {
      font-size: 0.72rem; font-weight: 500; letter-spacing: 0.1em; text-transform: uppercase;
      color: var(--text-muted); transition: color var(--t);
      position: relative; padding-bottom: 3px; cursor: auto;
    }
    .nav-links a::after {
      content: ''; position: absolute; bottom: 0; left: 0;
      width: 0; height: 1px; background: var(--gold);
      transition: width var(--t);
    }
    .nav-links a:hover { color: var(--white); }
    [data-theme="light"] .nav-links a:hover { color: var(--white); }
    .nav-links a:hover::after { width: 100%; }
    .nav-links a:focus { outline: 2px solid var(--gold); outline-offset: 4px; border-radius: 2px; }

    .nav-ham {
      display: none; flex-direction: column; gap: 5px;
      min-width: 44px; min-height: 44px;
      align-items: center; justify-content: center;
      border-radius: var(--r-sm); touch-action: manipulation; cursor: auto;
    }
    .nav-ham span {
      display: block; width: 22px; height: 1.5px;
      background: var(--gold); border-radius: 2px;
      transition: transform var(--t), opacity var(--t);
    }
    .nav-ham[aria-expanded="true"] span:nth-child(1) { transform: translateY(6.5px) rotate(45deg); }
    .nav-ham[aria-expanded="true"] span:nth-child(2) { opacity: 0; }
    .nav-ham[aria-expanded="true"] span:nth-child(3) { transform: translateY(-6.5px) rotate(-45deg); }

    .nav-mobile {
      display: none; position: fixed; inset: 0; z-index: 99;
      background: var(--black);
      flex-direction: column; align-items: center; justify-content: center; gap: 2.5rem;
    }
    .nav-mobile.open { display: flex; }
    .nav-mobile a {
      font-family: var(--font-head); font-size: 2.5rem; font-weight: 600;
      color: var(--text-muted); transition: color var(--t); cursor: auto;
    }
    .nav-mobile a:hover { color: var(--gold); }


    main > section:not(.hero), .marquee-strip { position: relative; z-index: 3; }
    main > section:not(.hero) { background: var(--black); }
    .hero { z-index: 2; }
    @media (max-width: 700px) {
      .nav-logo img { width: 52px; height: 52px; border-radius: 14px; }
    }

    /* ─── HERO ─── */
    .hero {
      position: relative; min-height: 100dvh;
      display: flex; align-items: center; justify-content: center;
      overflow: hidden; text-align: center;
    }

    .hero-video {
      position: absolute; inset: 0; width: 100%; height: 100%;
      object-fit: cover; object-position: center; z-index: -2; pointer-events: none; display:block; background:#020306;
      opacity: var(--hero-video-opacity, 1);
      transform: scale(calc(1.03 + var(--hero-video-scale, 0)));
      transition: opacity .12s linear;
      will-change: opacity, transform;
    }
    .hero-video-overlay {
      position: absolute; inset: 0; height: 100%; z-index: -1; pointer-events:none;
      opacity: var(--hero-video-opacity, 1);
      background: linear-gradient(
        to bottom,
        rgba(8,8,8,0.72) 0%,
        rgba(8,8,8,0.5) 50%,
        rgba(8,8,8,0.88) 100%
      );
    }
    [data-theme="light"] .hero-video-overlay {
      background: linear-gradient(
        to bottom,
        rgba(247,244,238,0.75) 0%,
        rgba(247,244,238,0.55) 50%,
        rgba(247,244,238,0.92) 100%
      );
    }

    .hero-bg-fallback {
      position: absolute; inset: 0; height: 100%; z-index: -3;
      background:
        radial-gradient(ellipse 80% 60% at 50% 0%, rgba(201,185,154,0.07) 0%, transparent 60%),
        radial-gradient(ellipse 60% 40% at 80% 80%, rgba(201,185,154,0.04) 0%, transparent 50%),
        var(--black);
    }
    .hero-orb {
      position: absolute; border-radius: 50%;
      background: radial-gradient(circle, rgba(201,185,154,0.1), transparent 70%);
      animation: orbFloat 14s ease-in-out infinite;
      z-index: 1; pointer-events: none;
    }
    .hero-orb-1 { width: 700px; height: 700px; top: -150px; right: -150px; animation-delay: 0s; }
    .hero-orb-2 { width: 500px; height: 500px; bottom: -80px; left: -100px; animation-delay: -7s; }
    @keyframes orbFloat {
      0%,100% { transform: translate(0,0) scale(1); }
      33%      { transform: translate(28px,-28px) scale(1.04); }
      66%      { transform: translate(-18px,18px) scale(0.97); }
    }

    .hero-grid {
      position: absolute; inset: 0; z-index: 1; pointer-events: none;
      opacity: 0.03;
      background-image:
        linear-gradient(to right, var(--gold) 1px, transparent 1px),
        linear-gradient(to bottom, var(--gold) 1px, transparent 1px);
      background-size: 80px 80px;
    }

    .hero-content {
      position: relative; z-index: 2; padding: 2rem; max-width: 860px;
    }

    .hero-h1 {
      font-family: var(--font-head);
      font-size: clamp(2.75rem, 6.2vw, 5.65rem); font-weight: 650;
      line-height: 0.98; letter-spacing: -0.02em;
      color: var(--white); margin-bottom: 2rem;
      opacity: 0; animation: fadeUp 1s var(--ease) 0.2s forwards;
    }
    .hero-h1 .line-gold {
      background: linear-gradient(100deg, var(--gold), var(--gold-bright), var(--gold));
      -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
      background-size: 200% auto; animation: shimmer 4s linear infinite;
      font-style: italic;
    }
    @keyframes shimmer { to { background-position: 200% center; } }

    .hero-sub {
      font-size: clamp(1.02rem, 1.8vw, 1.18rem); font-weight: 600;
      color: rgba(255,255,255,.88); max-width: 620px; margin: 0 auto 3rem; line-height: 1.75;
      letter-spacing: .01em; text-shadow: 0 2px 18px rgba(0,0,0,.72);
      opacity: 0; animation: fadeUp 0.9s var(--ease) 0.45s forwards;
    }
    .hero-actions {
      display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap;
      opacity: 0; animation: fadeUp 0.9s var(--ease) 0.65s forwards;
    }
    .hero-scroll {
      position: absolute; bottom: 2rem; left: 50%; transform: translateX(-50%);
      display: flex; flex-direction: column; align-items: center; gap: 0.6rem;
      color: var(--text-dim); font-size: 0.6rem; letter-spacing: 0.22em; text-transform: uppercase;
      font-family: var(--font-body);
      opacity: 0; animation: fadeIn 1s ease 1.2s forwards;
    }
    .hero-scroll-line {
      width: 1px; height: 48px;
      background: linear-gradient(to bottom, var(--gold-dim), transparent);
      animation: scrollAnim 2.8s ease-in-out infinite;
    }
    @keyframes scrollAnim { 0%,100% { opacity: 0.6; transform: scaleY(1) translateY(0); } 50% { opacity: 0.1; transform: scaleY(0.2) translateY(0); } }

    @keyframes fadeUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: none; } }
    @keyframes fadeIn { to { opacity: 1; } }

    @media (prefers-reduced-motion: reduce) {
      .hero-orb { animation: none; }
      *, *::before, *::after { animation-duration: 0.01ms !important; transition-duration: 0.01ms !important; }
    }

    /* ─── MARQUEE ─── */
    .marquee-strip {
      position: relative;
      overflow: hidden;
      padding: 1.05rem 0;
      white-space: nowrap;
      background:
        linear-gradient(90deg,
          rgba(9, 9, 12, 0) 0%,
          rgba(168, 121, 31, 0.10) 12%,
          rgba(226, 183, 86, 0.20) 48%,
          rgba(168, 121, 31, 0.10) 88%,
          rgba(9, 9, 12, 0) 100%);
      border-top: 1px solid rgba(226, 183, 86, 0.12);
      border-bottom: 1px solid rgba(226, 183, 86, 0.12);
      box-shadow: inset 0 14px 32px rgba(226, 183, 86, 0.035), inset 0 -14px 32px rgba(226, 183, 86, 0.025);
      -webkit-mask-image: linear-gradient(90deg, transparent 0%, #000 9%, #000 91%, transparent 100%);
      mask-image: linear-gradient(90deg, transparent 0%, #000 9%, #000 91%, transparent 100%);
    }
    .marquee-strip::before {
      content: '';
      position: absolute;
      inset: 0;
      pointer-events: none;
      background: radial-gradient(circle at 50% 50%, rgba(241, 202, 111, 0.10), transparent 58%);
      filter: blur(16px);
    }
    [data-theme="light"] .marquee-strip {
      background: linear-gradient(90deg, transparent, rgba(177, 126, 24, 0.12) 18%, rgba(205, 154, 48, 0.19) 50%, rgba(177, 126, 24, 0.12) 82%, transparent);
    }
    .marquee-track {
      position: relative;
      z-index: 1;
      display: flex;
      width: max-content;
      gap: 0;
      animation: marquee 48s linear infinite;
      will-change: transform;
      transform: translate3d(0,0,0);
    }
    .marquee-group {
      display: flex;
      flex-shrink: 0;
      align-items: center;
      gap: 3.25rem;
      padding-right: 3.25rem;
    }
    @media (prefers-reduced-motion: reduce) { .marquee-track { animation: none; } }
    @keyframes marquee { from { transform: translate3d(0,0,0); } to { transform: translate3d(-50%,0,0); } }
    .marquee-item {
      font-size: 0.72rem;
      font-weight: 650;
      letter-spacing: 0.19em;
      text-transform: uppercase;
      color: rgba(244, 210, 132, 0.92);
      text-shadow: 0 0 16px rgba(226, 183, 86, 0.26);
      display: inline-flex;
      align-items: center;
      gap: 1.6rem;
      font-family: var(--font-body);
    }
    .marquee-item::after {
      content: '•';
      color: rgba(226, 183, 86, 0.42);
      text-shadow: 0 0 10px rgba(226, 183, 86, 0.35);
    }

    /* ─── SERVICES ─── */
    #services { background: var(--surface); }
    .services-intro {
      display: grid; grid-template-columns: minmax(0, 1.15fr) minmax(280px, .85fr);
      gap: clamp(2rem, 6vw, 6rem); align-items: center;
    }
    .services-intro {
      display: block;
      max-width: 760px;
    }
    .services-grid {
      display: grid; grid-template-columns: repeat(2, 1fr); gap: 1.2rem 2.4rem; margin-top: 4rem;
    }
    .service-card {
      position: relative; overflow: hidden; isolation: isolate;
      background: transparent; border: 1px solid transparent;
      border-radius: 22px; padding: 2.25rem 2.35rem;
      transition: transform var(--ts), background var(--ts), box-shadow var(--ts);
    }
    .service-card::before,
    .service-card::after {
      content: ''; position: absolute; inset: 0; border-radius: inherit; pointer-events: none;
    }
    .service-card::before {
      padding: 1px;
      background: conic-gradient(from var(--service-angle, 0deg), transparent 0 72%, rgba(201,185,154,0.18) 78%, var(--gold) 88%, transparent 96%);
      -webkit-mask: linear-gradient(#000 0 0) content-box, linear-gradient(#000 0 0);
      -webkit-mask-composite: xor; mask-composite: exclude;
      opacity: 0; transform: scale(.985);
    }
    .service-card::after {
      background: radial-gradient(circle at 50% 50%, rgba(201,185,154,0.13), transparent 44%);
      opacity: 0; transition: opacity var(--ts);
    }
    .service-card:hover,
    .service-card:focus-visible {
      transform: translateY(-3px);
      background: linear-gradient(145deg, rgba(255,255,255,0.028), rgba(201,185,154,0.018));
      box-shadow: 0 20px 55px rgba(0,0,0,.24), 0 0 38px rgba(201,185,154,.06);
      outline: none;
    }
    .service-card:hover::before,
    .service-card:focus-visible::before { opacity: 1; animation: serviceBorderDraw 1.05s ease-out forwards; }
    .service-card:hover::after,
    .service-card:focus-visible::after { opacity: 1; }
    @property --service-angle { syntax: '<angle>'; inherits: false; initial-value: 0deg; }
    @keyframes serviceBorderDraw { from { --service-angle: 0deg; } to { --service-angle: 360deg; } }
    .service-card {
      min-height: 310px; display: flex; flex-direction: column; align-items: center;
      justify-content: center; text-align: center;
    }
    .service-num {
      font-family: var(--font-body); font-size: 0.63rem; font-weight: 700;
      letter-spacing: 0.24em; color: var(--gold); margin-bottom: 1.3rem; display: block;
    }
    .service-title {
      font-family: var(--font-head); font-size: clamp(1.55rem, 2vw, 1.95rem); font-weight: 600;
      color: var(--white); margin-bottom: 0.9rem; max-width: 15ch;
    }
    .service-desc {
      font-size: 0.92rem; color: var(--text-muted); line-height: 1.82; font-weight: 300;
      max-width: 46ch; margin-inline: auto;
    }
    @media (max-width: 900px) {
      .services-intro { grid-template-columns: 1fr; }
      .services-astronaut { min-height: 320px; }
      .services-astronaut video { min-height: 320px; }
    }
    @media (max-width: 760px) {
      .services-grid { grid-template-columns: 1fr; gap: .75rem; }
      .service-card { padding: 1.8rem 1.35rem; min-height: 260px; }
    }

    /* ─── WHY ─── */
    #why { background: var(--black); }
    .why-grid {
      display: grid; grid-template-columns: 1fr 1fr; gap: 5rem; align-items: center; margin-top: 4rem;
    }
    .why-card-main {
      background: var(--surface); border: 1px solid var(--border); border-radius: var(--r-lg);
      padding: 3rem; position: relative; overflow: hidden;
    }
    .why-card-main::after {
      content: ''; position: absolute; inset: 0; border-radius: inherit;
      background: radial-gradient(ellipse at 0% 0%, rgba(201,185,154,0.06), transparent 60%);
      pointer-events: none;
    }
    .why-big-num {
      font-family: var(--font-head); font-size: 5.5rem; font-weight: 700;
      color: var(--gold); line-height: 1; margin-bottom: 0.4rem; letter-spacing: -0.04em;
    }
    .why-big-label { font-size: 0.88rem; color: var(--text-muted); font-weight: 300; }
    .why-stats {
      display: grid; grid-template-columns: 1fr 1fr; gap: 1rem; margin-top: 1.5rem;
    }
    .why-stat {
      background: var(--surface-2); border: 1px solid var(--border);
      border-radius: var(--r-md); padding: 1.25rem;
    }
    .why-stat-num { font-family: var(--font-head); font-size: 2rem; font-weight: 700; color: var(--white); }
    .why-stat-lbl { font-size: 0.72rem; color: var(--text-dim); margin-top: 0.2rem; font-weight: 300; }

    .why-points { display: flex; flex-direction: column; gap: 1.25rem; }
    .why-point {
      display: flex; gap: 1.25rem; align-items: flex-start;
      padding: 1.5rem; background: var(--surface);
      border: 1px solid var(--border); border-radius: var(--r-md);
      transition: border-color var(--t), transform var(--t);
    }
    .why-point:hover { border-color: var(--gold-dim); transform: translateX(4px); }
    .why-point-icon {
      width: 44px; height: 44px; flex-shrink: 0;
      background: rgba(201,185,154,0.07); border: 1px solid var(--border);
      border-radius: var(--r-sm); display: flex; align-items: center; justify-content: center;
    }
    .why-point-icon svg { width: 20px; height: 20px; stroke: var(--gold); fill: none; stroke-width: 1.5; }
    .why-point-title { font-weight: 600; font-size: 0.95rem; color: var(--white); margin-bottom: 0.3rem; }
    .why-point-desc  { font-size: 0.85rem; color: var(--text-muted); line-height: 1.7; font-weight: 300; }

    /* ─── PORTFOLIO ─── */
    #portfolio { background: var(--surface); }
    .portfolio-grid {
      display: grid; grid-template-columns: repeat(3, 1fr); gap: 1.5rem; margin-top: 4rem;
    }
    .portfolio-card {
      position: relative; border-radius: var(--r-md); overflow: hidden;
      aspect-ratio: 4/3; background: var(--surface-2); cursor: auto;
    }
    .portfolio-img {
      width: 100%; height: 100%; object-fit: cover;
      transition: transform 700ms var(--ease);
    }
    .portfolio-card:hover .portfolio-img { transform: scale(1.07); }
    .portfolio-overlay {
      position: absolute; inset: 0; z-index: 1;
      background: linear-gradient(to top, rgba(8,8,8,0.92) 0%, rgba(8,8,8,0.2) 60%, transparent 100%);
      opacity: 0; transition: opacity var(--ts);
      display: flex; flex-direction: column; justify-content: flex-end; padding: 1.75rem;
    }
    .portfolio-card:hover .portfolio-overlay { opacity: 1; }
    .portfolio-cat { font-size: 0.62rem; font-weight: 600; letter-spacing: 0.2em; text-transform: uppercase; color: var(--gold); margin-bottom: 0.4rem; font-family: var(--font-body); }
    .portfolio-name { font-family: var(--font-head); font-size: 1.3rem; font-weight: 600; color: #ffffff; }

    /* ─── PROCESS ─── */
    #process { background: var(--black); }
    .process-steps {
      display: grid; grid-template-columns: repeat(4, 1fr); gap: 2rem; margin-top: 4rem;
      position: relative;
    }
    .process-steps::before {
      content: ''; position: absolute; top: 28px; left: 10%; right: 10%; height: 1px;
      background: linear-gradient(to right, transparent, var(--border), var(--gold-dim), var(--border), transparent);
    }
    .process-step { text-align: center; position: relative; }
    .process-num-wrap {
      width: 56px; height: 56px; border-radius: 50%;
      border: 1px solid var(--border); background: var(--surface);
      display: flex; align-items: center; justify-content: center;
      margin: 0 auto 1.5rem; position: relative; z-index: 1;
      transition: border-color var(--ts), background var(--ts);
    }
    .process-step:hover .process-num-wrap {
      border-color: var(--gold); background: rgba(201,185,154,0.07);
    }
    .process-num {
      font-family: var(--font-head); font-size: 1.2rem; font-weight: 700; color: var(--gold);
    }
    .process-title {
      font-family: var(--font-head); font-size: 1.15rem; font-weight: 600;
      color: var(--white); margin-bottom: 0.6rem;
    }
    .process-desc { font-size: 0.83rem; color: var(--text-muted); line-height: 1.7; font-weight: 300; }

    /* ─── ABOUT ─── */
    #about { background: var(--surface); }
    .about-grid {
      display: grid; grid-template-columns: 1fr 1fr; gap: 5rem; align-items: center;
    }
    .about-visual-wrap { position: relative; }
    .about-img-placeholder {
      width: 100%; aspect-ratio: 1/1; border-radius: var(--r-lg);
      border: 1px solid rgba(226,207,168,.18); background: radial-gradient(ellipse at 28% 24%, rgba(98,72,190,.28), transparent 58%), radial-gradient(ellipse at 75% 78%, rgba(185,139,77,.20), transparent 52%), linear-gradient(135deg, rgba(10,12,26,.96), rgba(14,10,30,.92));
      display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 1.5rem;
    }
    .about-logo-big svg { width: 100px; height: auto; }
    .about-floating-card {
      position: absolute; bottom: -1.5rem; right: -1.5rem;
      background: var(--gold); color: #080808;
      border-radius: var(--r-md); padding: 1.5rem 2rem; text-align: center;
      box-shadow: 0 20px 40px rgba(201,185,154,0.2);
    }
    .about-floating-num { font-family: var(--font-head); font-size: 2.5rem; font-weight: 700; line-height: 1; }
    .about-floating-lbl { font-size: 0.68rem; font-weight: 600; letter-spacing: 0.12em; text-transform: uppercase; margin-top: 0.3rem; font-family: var(--font-body); }
    .about-text p { font-size: 0.95rem; color: var(--text-muted); line-height: 1.9; margin-bottom: 1rem; font-weight: 300; }
    .about-certs { display: flex; flex-wrap: wrap; gap: 0.75rem; margin-top: 2rem; }
    .about-cert {
      font-size: 0.65rem; font-weight: 600; letter-spacing: 0.12em; text-transform: uppercase;
      padding: 0.45rem 1rem; border: 1px solid var(--border); border-radius: 100px; color: var(--gold);
      font-family: var(--font-body);
    }

    /* ─── TESTIMONIALS ─── */
    #testimonials { background: var(--black); }
    .testi-grid {
      display: grid; grid-template-columns: repeat(3, 1fr); gap: 1.5rem; margin-top: 4rem;
    }
    .testi-card {
      background: var(--surface); border: 1px solid var(--border); border-radius: var(--r-md);
      padding: 2.25rem; display: flex; flex-direction: column; gap: 1.5rem;
      transition: border-color var(--ts), transform var(--ts);
    }
    .testi-card:hover { border-color: var(--gold-dim); transform: translateY(-4px); }
    .testi-stars { color: var(--gold); font-size: 0.85rem; letter-spacing: 0.1em; }
    .testi-quote {
      font-family: var(--font-head); font-style: italic; font-size: 1.05rem; font-weight: 400;
      color: var(--text); line-height: 1.75; flex: 1;
    }
    .testi-quote::before { content: '\201C'; color: var(--gold); font-size: 1.8rem; line-height: 0; vertical-align: -0.4rem; margin-right: 0.1rem; }
    .testi-author { display: flex; align-items: center; gap: 1rem; }
    .testi-avatar {
      width: 44px; height: 44px; border-radius: 50%; border: 1px solid var(--border);
      background: var(--surface-2); display: flex; align-items: center; justify-content: center;
      font-family: var(--font-head); font-size: 1.2rem; font-weight: 600; color: var(--gold);
      flex-shrink: 0;
    }
    .testi-name { font-weight: 600; font-size: 0.88rem; color: var(--white); }
    .testi-role { font-size: 0.72rem; color: var(--text-dim); margin-top: 0.15rem; font-weight: 300; }

    /* ─── PRICING ─── */
    #pricing { background: var(--surface); }
    .pricing-grid {
      display: grid; grid-template-columns: repeat(3, 1fr); gap: 1.5rem; margin-top: 4rem; align-items: stretch;
    }
    .pricing-card {
      background: var(--surface-2); border: 1px solid var(--border); border-radius: var(--r-lg);
      padding: 2.5rem; position: relative; overflow: hidden;
      transition: border-color var(--ts), transform var(--ts), box-shadow var(--ts);
    }
    .pricing-card:hover { transform: translateY(-6px); box-shadow: var(--shadow-gold); }
    .pricing-card.featured {
      border-color: var(--gold); background: var(--surface);
      
    }
    .pricing-card.featured:hover { transform: translateY(-6px); }
    .pricing-badge {
      position: absolute; top: 1.5rem; right: 1.5rem;
      background: var(--gold); color: #080808;
      font-size: 0.58rem; font-weight: 700; letter-spacing: 0.14em; text-transform: uppercase;
      padding: 0.3rem 0.75rem; border-radius: 100px; font-family: var(--font-body);
    }
    .pricing-plan {
      font-size: 0.65rem; font-weight: 600; letter-spacing: 0.22em; text-transform: uppercase;
      color: var(--gold); margin-bottom: 0.75rem; font-family: var(--font-body);
    }
    .pricing-name {
      font-family: var(--font-head); font-size: 1.6rem; font-weight: 600;
      color: var(--white); margin-bottom: 1.5rem;
    }
    .pricing-amount { display: flex; align-items: flex-end; gap: 0.25rem; margin-bottom: 0.25rem; }
    .pricing-currency { font-size: 1.2rem; color: var(--gold); margin-bottom: 0.35rem; font-family: var(--font-head); }
    .pricing-num {
      font-family: var(--font-head); font-size: 3.2rem; font-weight: 700;
      color: var(--white); line-height: 1; letter-spacing: -0.03em;
    }
    .pricing-period { font-size: 0.78rem; color: var(--text-dim); margin-bottom: 0.25rem; font-weight: 300; }
    .pricing-note { font-size: 0.77rem; color: var(--text-dim); margin-bottom: 2rem; font-weight: 300; }
    .pricing-divider { border: none; border-top: 1px solid var(--border); margin-bottom: 2rem; }
    .pricing-features { display: flex; flex-direction: column; gap: 0.9rem; margin-bottom: 2.5rem; }
    .pricing-feature {
      display: flex; align-items: flex-start; gap: 0.75rem;
      font-size: 0.84rem; color: var(--text-muted); font-weight: 300;
    }
    .pricing-feature svg { width: 15px; height: 15px; stroke: var(--gold); fill: none; stroke-width: 2.5; flex-shrink: 0; margin-top: 3px; }
    .pricing-feature.dim { color: var(--text-dim); }
    .pricing-feature.dim svg { stroke: var(--text-dim); }
    .pricing-cta { width: 100%; justify-content: center; }
    .pricing-custom-icon {
      width: 64px; height: 64px; background: rgba(201,185,154,0.07); border: 1px solid var(--border);
      border-radius: 50%; display: flex; align-items: center; justify-content: center; margin: 0 auto 1.5rem;
    }
    .pricing-custom-icon svg { width: 28px; height: 28px; stroke: var(--gold); fill: none; stroke-width: 1.5; }

    /* ─── FAQ ─── */
    #faq { background: var(--black); }
    .faq-list { margin-top: 4rem; max-width: 760px; margin-left: auto; margin-right: auto; }
    .faq-item { border-bottom: 1px solid var(--border); }
    .faq-btn {
      width: 100%; display: flex; align-items: center; justify-content: space-between;
      padding: 1.6rem 0; text-align: left; cursor: auto;
      gap: 1rem; touch-action: manipulation; transition: color var(--t);
    }
    .faq-btn:hover .faq-q { color: var(--gold); }
    .faq-btn:focus { outline: 2px solid var(--gold); outline-offset: 2px; border-radius: 2px; }
    .faq-q { font-size: 0.95rem; font-weight: 500; color: var(--white); line-height: 1.4; }
    .faq-icon {
      width: 26px; height: 26px; flex-shrink: 0; border: 1px solid var(--border);
      border-radius: 50%; display: flex; align-items: center; justify-content: center;
      transition: border-color var(--t), transform var(--t), background var(--t);
    }
    .faq-icon svg { width: 10px; height: 10px; stroke: var(--gold); fill: none; stroke-width: 2.5; transition: transform var(--t); }
    .faq-item.open .faq-icon { border-color: var(--gold); background: rgba(201,185,154,0.1); }
    .faq-item.open .faq-icon svg { transform: rotate(45deg); }
    .faq-answer { overflow: hidden; max-height: 0; transition: max-height 400ms var(--ease); }
    .faq-answer-inner {
      padding-bottom: 1.5rem; font-size: 0.9rem; color: var(--text-muted); line-height: 1.85; font-weight: 300;
    }

    /* ─── CONTACT ─── */
    #contact { background: var(--surface); }
    .contact-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 5rem; align-items: start; }
    .contact-info-item { margin-bottom: 2rem; }
    .contact-info-label {
      font-size: 0.62rem; font-weight: 600; letter-spacing: 0.22em; text-transform: uppercase;
      color: var(--gold); margin-bottom: 0.4rem; font-family: var(--font-body);
    }
    .contact-info-value { font-size: 0.95rem; color: var(--text-muted); line-height: 1.6; font-weight: 300; }
    .contact-info-value a { color: var(--white); transition: color var(--t); }
    .contact-info-value a:hover { color: var(--gold); }
    .contact-form { display: flex; flex-direction: column; gap: 1.1rem; }
    .form-group { display: flex; flex-direction: column; gap: 0.5rem; }
    .form-group label {
      font-size: 0.68rem; font-weight: 600; letter-spacing: 0.14em; text-transform: uppercase;
      color: var(--text-dim); font-family: var(--font-body);
    }
    .form-control {
      padding: 0.88rem 1.1rem; min-height: 50px;
      background: var(--surface-2); border: 1px solid var(--border);
      border-radius: var(--r-sm); font-size: 0.9rem; font-family: var(--font-body); color: var(--white);
      transition: border-color var(--t), box-shadow var(--t); -webkit-appearance: none;
    }
    .form-control::placeholder { color: var(--text-dim); }
    .form-control:focus {
      outline: none; border-color: var(--gold);
      box-shadow: 0 0 0 3px rgba(201,185,154,0.1);
    }
    textarea.form-control { min-height: 130px; resize: vertical; }
    select.form-control option { background: var(--surface-2); }
    .form-error { font-size: 0.72rem; color: #E05555; display: none; font-family: var(--font-body); }
    .form-error.show { display: block; }
    .form-control.is-error { border-color: #E05555; }

    /* ─── FOOTER ─── */
    footer {
      background: var(--black); border-top: 1px solid var(--border);
      padding: 4rem 0 2rem;
    }
    .footer-grid {
      display: grid; grid-template-columns: 2fr 1fr 1fr 1fr; gap: 3rem; margin-bottom: 3.5rem;
    }
    .footer-brand svg { height: 44px; width: auto; margin-bottom: 1rem; }
    .footer-tagline { font-size: 0.85rem; color: var(--text-dim); line-height: 1.75; max-width: 260px; margin-top: 0.75rem; font-weight: 300; }
    .footer-social { display: flex; gap: 0.75rem; margin-top: 1.5rem; }
    .footer-social-link {
      width: 44px; height: 44px; border: 1px solid var(--border); border-radius: var(--r-sm);
      display: flex; align-items: center; justify-content: center;
      color: var(--text-dim); transition: border-color var(--t), color var(--t), background var(--t);
      touch-action: manipulation; cursor: auto;
    }
    .footer-social-link:hover { border-color: var(--gold); color: var(--gold); background: rgba(201,185,154,0.05); }
    .footer-social-link:focus { outline: 2px solid var(--gold); outline-offset: 3px; }
    .footer-social-link svg { width: 18px; height: 18px; }
    .footer-col-title {
      font-size: 0.62rem; font-weight: 600; letter-spacing: 0.22em; text-transform: uppercase;
      color: var(--gold); margin-bottom: 1.5rem; font-family: var(--font-body);
    }
    .footer-links { display: flex; flex-direction: column; gap: 0.7rem; }
    .footer-links a { font-size: 0.85rem; color: var(--text-dim); transition: color var(--t); font-weight: 300; }
    .footer-links a:hover { color: var(--white); }
    .footer-links a:focus { outline: 2px solid var(--gold); outline-offset: 3px; border-radius: 2px; }
    .footer-bottom {
      border-top: 1px solid var(--border); padding-top: 2rem;
      display: flex; align-items: center; justify-content: space-between;
      flex-wrap: wrap; gap: 1rem; font-size: 0.75rem; color: var(--text-dim); font-weight: 300;
    }
    .footer-bottom a { color: var(--gold); }

    /* ─── TOAST ─── */
    .toast {
      position: fixed; bottom: 2rem; right: 2rem; z-index: 300;
      background: var(--surface); border: 1px solid var(--gold-dim); color: var(--white);
      padding: 1rem 1.5rem; border-radius: var(--r-md);
      display: flex; align-items: center; gap: 0.75rem; max-width: 360px;
      transform: translateY(100px); opacity: 0;
      transition: transform var(--ts), opacity var(--ts); pointer-events: none;
      font-size: 0.88rem;
    }
    .toast.show { transform: translateY(0); opacity: 1; pointer-events: auto; }
    .toast-icon svg { width: 18px; height: 18px; stroke: var(--gold); fill: none; stroke-width: 2; flex-shrink: 0; }

    /* ─── SCROLL REVEAL ─── */
    .reveal {
      opacity: 0; transform: translateY(24px);
      transition: opacity 0.7s var(--ease), transform 0.7s var(--ease);
    }
    .reveal.in { opacity: 1; transform: none; }
    .reveal-d1 { transition-delay: 0.08s; }
    .reveal-d2 { transition-delay: 0.16s; }
    .reveal-d3 { transition-delay: 0.24s; }
    .reveal-d4 { transition-delay: 0.32s; }



    /* ─── PREMIUM INTERACTION LAYER ─── */
    .cosmic-transition {
      position: fixed; inset: 0; z-index: 9996; pointer-events: none;
      overflow: hidden; opacity: 0; background: radial-gradient(circle at var(--x, 50%) var(--y, 50%), rgba(226,207,168,0.95) 0 2px, rgba(226,207,168,0.34) 8%, rgba(8,8,8,0.92) 28%, transparent 62%);
      transform: scale(0.25); transition: opacity 240ms ease, transform 760ms cubic-bezier(0.16, 1, 0.3, 1);
      mix-blend-mode: screen;
    }
    .cosmic-transition.active { opacity: 1; transform: scale(2.8); }
    .star-particle {
      position: fixed; left: var(--x); top: var(--y); z-index: 9997; pointer-events: none;
      width: var(--size); height: var(--size); border-radius: 50%; background: var(--gold-bright);
      box-shadow: 0 0 18px var(--gold-bright); transform: translate(-50%, -50%);
      animation: starBurst 820ms cubic-bezier(0.16, 1, 0.3, 1) forwards;
    }
    @keyframes starBurst {
      to { transform: translate(calc(-50% + var(--dx)), calc(-50% + var(--dy))) scale(0); opacity: 0; }
    }
    .service-card, .pricing-card, .testi-card, .why-point, .portfolio-card {
      will-change: transform;
    }
    .service-card::after, .pricing-card::after, .testi-card::after {
      content: ''; position: absolute; inset: 0; opacity: 0; pointer-events: none;
      background: radial-gradient(circle at var(--mx, 50%) var(--my, 0%), rgba(226,207,168,0.16), transparent 36%);
      transition: opacity var(--t);
    }
    .service-card:hover::after, .pricing-card:hover::after, .testi-card:hover::after { opacity: 1; }
    .portfolio-card { transform-style: preserve-3d; }
    .portfolio-overlay { transform: translateY(14px); }
    .portfolio-card:hover .portfolio-overlay { transform: translateY(0); }
    .section-title { text-wrap: balance; }
    .scroll-progress {
      position: fixed; top: 0; left: 0; height: 2px; width: calc(var(--progress, 0) * 100%);
      background: linear-gradient(90deg, transparent, var(--gold-bright)); z-index: 9995; pointer-events: none;
    }
    .hero-kicker {
      display: inline-flex; align-items: center; gap: 0.65rem; margin-bottom: 1.1rem;
      font-size: 0.68rem; font-weight: 700; letter-spacing: 0.24em; text-transform: uppercase; color: var(--gold);
      opacity: 0; animation: fadeUp 0.9s var(--ease) 0.05s forwards;
    }
    .hero-kicker::before, .hero-kicker::after { content: ''; width: 28px; height: 1px; background: var(--gold-dim); }

    /* ─── RESPONSIVE ─── */
    @media (max-width: 1024px) {
      .services-grid  { grid-template-columns: 1fr; }
      .portfolio-grid { grid-template-columns: repeat(2, 1fr); }
      .process-steps  { grid-template-columns: repeat(2, 1fr); }
      .process-steps::before { display: none; }
      .footer-grid { grid-template-columns: 1fr 1fr; gap: 2rem; }
      .pricing-card.featured { transform: none; }
      .pricing-card.featured:hover { transform: translateY(-6px); }
    }
    @media (max-width: 768px) {
      section { padding: 5rem 0; }
      .nav-links, .nav .btn-gold { display: none; }
      .nav-ham { display: flex; }
      .services-grid  { grid-template-columns: 1fr; }
      .why-grid       { grid-template-columns: 1fr; gap: 3rem; }
      .about-grid     { grid-template-columns: 1fr; gap: 3rem; }
      .contact-grid   { grid-template-columns: 1fr; gap: 3rem; }
      .portfolio-grid { grid-template-columns: 1fr; }
      .testi-grid     { grid-template-columns: 1fr; }
      .pricing-grid   { grid-template-columns: 1fr; }
      .process-steps  { grid-template-columns: 1fr; }
      .footer-grid    { grid-template-columns: 1fr; gap: 2rem; }
      .footer-bottom  { flex-direction: column; text-align: center; }
      .about-floating-card { bottom: -1rem; right: -0.5rem; }
    }
    @media (max-width: 480px) {
      .hero-actions { flex-direction: column; align-items: stretch; }
      .hero-actions .btn { justify-content: center; }
      .why-stats { grid-template-columns: 1fr; }
    }
  
/* Preview adjustment: centered Why BYILD Media heading and icon-free benefit cards */
#why .why-heading-center {
  text-align: center;
  max-width: 980px;
  margin: 0 auto 3.5rem;
}
#why .why-brand-title {
  margin: 0 auto;
  font-size: clamp(3.25rem, 7vw, 7rem);
  line-height: .95;
  font-weight: 800;
  letter-spacing: -0.055em;
  text-align: center;
  text-wrap: balance;
}
#why .why-point {
  grid-template-columns: 1fr !important;
}
#why .why-point-icon { display: none !important; }

</style>
<style>
  /* Final premium direction */
  html { scroll-behavior: smooth; }
  body { background: #070910; cursor: auto; }
  body::before {
    background:
      radial-gradient(circle at 15% 15%, rgba(116,86,255,.18), transparent 30%),
      radial-gradient(circle at 82% 22%, rgba(0,210,255,.11), transparent 28%),
      radial-gradient(circle at 52% 82%, rgba(226,207,168,.10), transparent 34%),
      linear-gradient(135deg, #070910 0%, #0d1020 45%, #080b14 100%);
  }
  .theme-toggle,.cosmic-transition { display:none!important; }
  .nav-logo { gap:.85rem; }
  .nav-logo img { width:48px; height:48px; object-fit:contain; border-radius:0; box-shadow:none; background:transparent; }
  .nav-logo:hover img { transform:translateY(-2px) rotate(-3deg); box-shadow:none; }
  .nav-brand-text { color:#fff; font-size:.95rem; font-weight:700; letter-spacing:.12em; text-transform:uppercase; white-space:nowrap; }
  .hero-h1,.section-title,.pricing-name,.service-title,.process-title { font-style:normal!important; }
  .hero-h1 { font-family:var(--font-body); font-weight:700; letter-spacing:-.045em; }
  .line-gold { font-style:normal!important; }
  .hero-video { animation:none; }
  .hero-video-overlay { background:linear-gradient(180deg,rgba(7,9,16,.18),rgba(7,9,16,.34) 55%,rgba(7,9,16,.94)); }
  .hero-grid { opacity:.18; mask-image:linear-gradient(to bottom,black,transparent 82%); }
  #services,#why,#process,#about,#testimonials,#pricing,#faq,#contact {
    background:linear-gradient(160deg,rgba(12,16,30,.96),rgba(7,9,16,.98));
    position:relative; overflow:hidden;
  }
  section::before { content:""; position:absolute; width:420px; height:420px; border:1px solid rgba(226,207,168,.08); border-radius:50%; right:-240px; top:12%; box-shadow:0 0 100px rgba(116,86,255,.08); pointer-events:none; }
  .cursor-orb { width:46px; height:46px; border:0; background:transparent; backdrop-filter:none; display:flex; align-items:center; justify-content:center; font-size:30px; filter:drop-shadow(0 8px 12px rgba(0,0,0,.45)); transition:transform .2s ease,filter .2s ease; }
  .cursor-orb::before { content:""; }
  .cursor-orb.expanded { width:54px; height:54px; background:transparent; border:0; transform:translate(-50%,-50%) scale(1.15) rotate(8deg); }
  .cursor-dot { display:none; }
  .floating-quote { position:fixed; right:22px; bottom:22px; z-index:120; padding:.9rem 1.25rem; background:var(--gold); color:#080808; border-radius:999px; font-size:.72rem; font-weight:800; letter-spacing:.08em; text-transform:uppercase; box-shadow:0 16px 45px rgba(0,0,0,.35),0 0 30px rgba(201,185,154,.18); transition:transform .25s ease; }
  .floating-quote:hover { transform:translateY(-4px) scale(1.03); }
  #nav-cta { display:inline-flex!important; }
  .process-steps { position:relative; }
  .process-traveler { position:absolute; top:25px; left:6%; z-index:4; color:var(--gold-bright); font-size:1.4rem; filter:drop-shadow(0 0 10px rgba(226,207,168,.65)); animation:travelProcess 6s cubic-bezier(.65,0,.35,1) infinite; }
  @keyframes travelProcess { 0%,8%{left:6%;transform:scale(.8)} 27%{left:31%;transform:scale(1.05)} 52%{left:56%;transform:scale(1.05)} 77%,92%{left:81%;transform:scale(.8)} 100%{left:6%;transform:scale(.8)} }
  .pricing-card { cursor:none; }
  .pricing-card.featured { transform:none; }
  .pricing-card.selected { border-color:var(--gold)!important; box-shadow:0 0 0 2px rgba(201,185,154,.16),0 24px 70px rgba(0,0,0,.34); transform:translateY(-6px); }
  .pricing-card.featured:not(.selected) { border-color:var(--border); }
  @media(max-width:820px){ .nav-brand-text{font-size:.72rem;letter-spacing:.08em}.floating-quote{right:14px;bottom:14px}.process-traveler{display:none} }
  @media(prefers-reduced-motion:reduce){ .process-traveler{animation:none}.hero-video{transform:none!important} }
</style>
<style>
  /* Interactive background preview */
  :root { --bg-mx: 50vw; --bg-my: 35vh; }
  body {
    background: #080b14;
    isolation: isolate;
  }
  body::before {
    z-index: -5;
    background:
      radial-gradient(70rem 54rem at var(--bg-mx) var(--bg-my), rgba(98,72,190,.18), transparent 56%),
      radial-gradient(52rem 42rem at 9% 42%, rgba(31,121,145,.15), transparent 58%),
      radial-gradient(58rem 46rem at 92% 68%, rgba(185,139,77,.13), transparent 60%),
      linear-gradient(145deg,#070a12 0%,#11152a 37%,#0a1720 68%,#120f19 100%);
    transform:none;
    transition: background-position .25s ease-out;
  }
  .ambient-field {
    position:fixed; inset:0; z-index:-4; pointer-events:none; overflow:hidden;
    opacity:.95;
  }
  .ambient-field::before,
  .ambient-field::after {
    content:""; position:absolute; border-radius:50%; filter:blur(22px);
    will-change:transform;
  }
  .ambient-field::before {
    width:44vw; height:44vw; min-width:420px; min-height:420px;
    left:-12vw; top:18vh;
    background:conic-gradient(from 120deg,rgba(102,76,208,.16),rgba(38,151,169,.11),rgba(218,174,103,.10),rgba(102,76,208,.16));
    animation:ambientDriftA 18s ease-in-out infinite alternate;
  }
  .ambient-field::after {
    width:38vw; height:38vw; min-width:360px; min-height:360px;
    right:-8vw; bottom:-10vh;
    background:conic-gradient(from 30deg,rgba(218,174,103,.12),rgba(110,74,188,.13),rgba(36,126,151,.12),rgba(218,174,103,.12));
    animation:ambientDriftB 22s ease-in-out infinite alternate;
  }
  @keyframes ambientDriftA { to { transform:translate3d(18vw,10vh,0) rotate(38deg) scale(1.08); } }
  @keyframes ambientDriftB { to { transform:translate3d(-16vw,-15vh,0) rotate(-44deg) scale(.92); } }

  main > section:not(.hero) {
    background:transparent!important;
    position:relative;
    overflow:hidden;
  }
  main > section:not(.hero)::after {
    content:""; position:absolute; inset:1.1rem max(1.1rem,calc((100vw - 1320px)/2)); z-index:-1;
    border:1px solid rgba(255,255,255,.055);
    border-radius:32px;
    background:linear-gradient(135deg,rgba(20,25,44,.70),rgba(8,18,25,.54));
    box-shadow:inset 0 1px 0 rgba(255,255,255,.04),0 24px 90px rgba(0,0,0,.18);
    backdrop-filter:blur(10px);
    -webkit-backdrop-filter:blur(10px);
  }
  #why::after,#about::after,#pricing::after,#contact::after {
    background:linear-gradient(140deg,rgba(30,24,43,.68),rgba(11,24,31,.56));
  }
  #process::after,#testimonials::after,#faq::after {
    background:linear-gradient(140deg,rgba(10,27,34,.66),rgba(25,20,39,.56));
  }
  section::before {
    width:500px; height:500px; right:-230px; top:8%;
    border-color:rgba(226,207,168,.10);
    box-shadow:0 0 120px rgba(98,72,190,.11), inset 0 0 80px rgba(40,137,162,.035);
    transform:translateY(calc(var(--scroll,0) * -0.018px));
  }
  #services::before,#process::before,#pricing::before { left:-280px; right:auto; }

  .service-card,.why-card,.testi-card,.pricing-card,.contact-form,.about-visual {
    background:linear-gradient(145deg,rgba(28,31,49,.78),rgba(10,18,27,.74))!important;
    border-color:rgba(226,207,168,.13)!important;
    box-shadow:inset 0 1px 0 rgba(255,255,255,.035),0 18px 55px rgba(0,0,0,.16);
  }
  .service-card:hover,.testi-card:hover,.pricing-card:hover {
    box-shadow:inset 0 1px 0 rgba(255,255,255,.06),0 24px 75px rgba(44,30,92,.24),0 0 40px rgba(35,123,146,.10);
  }
  .nav,.nav.scrolled {
    background:linear-gradient(180deg,rgba(8,11,20,.82),rgba(8,11,20,.52));
    backdrop-filter:blur(22px) saturate(135%);
    -webkit-backdrop-filter:blur(22px) saturate(135%);
  }
  .footer { background:rgba(7,10,18,.76)!important; backdrop-filter:blur(14px); }
  @media(max-width:820px){
    main > section:not(.hero)::after { inset:.65rem; border-radius:22px; }
    .ambient-field{opacity:.72}
  }
  @media(prefers-reduced-motion:reduce){
    .ambient-field::before,.ambient-field::after{animation:none}
  }
</style>
<style>
  /* Non-video scroll background experiment */
  body { background:#070912; }
  .ambient-field { display:none!important; }
  .generative-bg {
    position:fixed; inset:0; z-index:-4; width:100%; height:100%;
    pointer-events:none; opacity:0; transition:opacity .7s ease;
  }
  body.past-hero .generative-bg { opacity:1; }
  body::before {
    z-index:-6;
    background:
      radial-gradient(55rem 38rem at 10% 18%, rgba(55,85,150,.16), transparent 64%),
      radial-gradient(50rem 42rem at 88% 58%, rgba(122,72,150,.14), transparent 65%),
      radial-gradient(44rem 36rem at 45% 95%, rgba(173,118,65,.11), transparent 62%),
      linear-gradient(160deg,#080a13 0%,#0c1422 38%,#111020 70%,#07131a 100%);
    transform:none;
  }
  .terrain-lines {
    position:fixed; inset:0; z-index:-3; pointer-events:none; opacity:0;
    transition:opacity .7s ease;
    background-image:
      repeating-radial-gradient(ellipse at 15% 20%, transparent 0 30px, rgba(214,194,151,.035) 31px 32px, transparent 33px 58px),
      repeating-radial-gradient(ellipse at 82% 72%, transparent 0 42px, rgba(121,160,184,.035) 43px 44px, transparent 45px 80px);
    background-size:120% 120%,130% 130%;
    transform:translate3d(0,calc(var(--scroll,0) * -0.018px),0) scale(1.08);
    filter:blur(.1px);
  }
  body.past-hero .terrain-lines { opacity:.72; }
  main > section:not(.hero)::after {
    background:linear-gradient(135deg,rgba(13,20,34,.72),rgba(19,14,31,.62))!important;
    border-color:rgba(255,255,255,.065)!important;
    box-shadow:inset 0 1px 0 rgba(255,255,255,.04),0 28px 100px rgba(0,0,0,.22),0 0 80px rgba(64,92,150,.05)!important;
  }
  #why::after,#about::after,#pricing::after,#contact::after {
    background:linear-gradient(140deg,rgba(22,17,38,.74),rgba(9,28,34,.60))!important;
  }
  #process::after,#testimonials::after,#faq::after {
    background:linear-gradient(140deg,rgba(8,25,38,.70),rgba(28,17,38,.62))!important;
  }
  @media(prefers-reduced-motion:reduce){.generative-bg{display:none}.terrain-lines{transform:none}}
</style>

<style id="full-page-video-preview">
  html, body { background: #05070c !important; }
  body::before { display: none !important; }
  .generative-bg, .terrain-lines, .ambient-field { display: none !important; }
  .hero-video {
    position: fixed !important; inset: 0 !important; width: 100vw !important; height: 100vh !important;
    object-fit: cover !important; object-position: center !important; z-index: -8 !important;
    opacity: 1 !important; transform: scale(1.035) !important;
    filter: saturate(.92) contrast(1.06) brightness(.72); pointer-events: none;
  }
  .hero-video-overlay {
    position: fixed !important; inset: 0 !important; width: 100vw !important; height: 100vh !important;
    z-index: -7 !important; opacity: 1 !important; pointer-events: none;
    background: radial-gradient(circle at 50% 15%, rgba(10,12,20,.12), rgba(4,5,9,.40) 58%, rgba(3,4,7,.68) 100%),
                linear-gradient(180deg, rgba(3,4,8,.18), rgba(3,4,8,.50));
  }
  .hero-bg-fallback { display: none !important; }
  main > section:not(.hero), .marquee-strip { background: transparent !important; }
  main > section:not(.hero)::before {
    content: ''; position: absolute; inset: 0; z-index: -2; pointer-events: none;
    background: linear-gradient(180deg, rgba(4,6,11,.26), rgba(4,6,11,.44));
  }
  main > section:not(.hero)::after {
    background: linear-gradient(135deg, rgba(10,13,21,.74), rgba(7,9,15,.58)) !important;
    border-color: rgba(255,255,255,.08) !important;
    box-shadow: inset 0 1px 0 rgba(255,255,255,.045), 0 30px 100px rgba(0,0,0,.26) !important;
    backdrop-filter: blur(12px) saturate(112%); -webkit-backdrop-filter: blur(12px) saturate(112%);
  }
  #why::after, #about::after, #pricing::after, #contact::after,
  #process::after, #testimonials::after, #faq::after {
    background: linear-gradient(140deg, rgba(12,15,24,.76), rgba(6,8,14,.60)) !important;
  }
  .footer { background: rgba(4,6,10,.72) !important; backdrop-filter: blur(16px) saturate(115%); -webkit-backdrop-filter: blur(16px) saturate(115%); }
  .marquee-strip { backdrop-filter: blur(8px); -webkit-backdrop-filter: blur(8px); }
  @media (max-width: 700px) {
    .hero-video { object-position: 52% center !important; filter: saturate(.9) contrast(1.04) brightness(.67); }
    main > section:not(.hero)::after { backdrop-filter: blur(9px); -webkit-backdrop-filter: blur(9px); }
  }
  @media (prefers-reduced-motion: reduce) { .hero-video { transform: none !important; } }
</style>
</head>
<body><script>
/* Lock all requestAnimationFrame-based animations to 90 fps */
(function(){
  var TARGET = 100;
  var INTERVAL = 1000 / TARGET; // 10 ms
  var _raf = window.requestAnimationFrame.bind(window);
  var _caf = window.cancelAnimationFrame.bind(window);
  var pending = new Map();
  var uid = 0;
  var lastTick = 0;

  function tick(ts){
    _raf(tick);
    var delta = ts - lastTick;
    if(delta < INTERVAL) return;
    lastTick = ts - (delta % INTERVAL);
    var snap = Array.from(pending);
    pending.clear();
    for(var i = 0; i < snap.length; i++){
      try{ snap[i][1](ts); }catch(e){}
    }
  }
  _raf(tick);

  window.requestAnimationFrame = function(cb){
    var id = ++uid;
    pending.set(id, cb);
    return id;
  };
  window.cancelAnimationFrame = function(id){
    pending.delete(id);
  };
})();
</script>
<video aria-hidden="true" autoplay="" class="hero-video" id="hero-video" loop="" muted="" playsinline="" poster="space-poster.jpg" preload="metadata">
<source src="space-hero.mp4" type="video/mp4"/>
</video>
<div aria-hidden="true" class="hero-video-overlay"></div>
<canvas aria-hidden="true" class="generative-bg" id="generative-bg"></canvas><div aria-hidden="true" class="terrain-lines"></div>
<a class="skip-link" href="#main">Skip to main content</a>
<div aria-hidden="true" class="scroll-progress"></div>
<div aria-hidden="true" class="cosmic-transition" id="cosmic-transition"></div>
<!-- NAV -->
<nav aria-label="Main navigation" class="nav" id="nav" role="navigation">
<a aria-label="BYILD Media Home" class="nav-logo" href="#">
<img alt="BYILD Media symbol" src="byild-logo-symbol.png"/>
<span class="nav-brand-text">BYILD Media</span>
</a>
<ul class="nav-links" role="list">
<li><a href="#services">Services</a></li>
<li><a href="#about">About</a></li>
<li><a href="#pricing">Pricing</a></li>
<li><a href="#faq">FAQ</a></li>
<li><a href="#contact">Contact</a></li>
</ul>
<div class="nav-right">
<a class="btn btn-gold" href="#contact" id="nav-cta">Get a Quote</a>
<button aria-controls="mob-nav" aria-expanded="false" aria-label="Open menu" class="nav-ham" id="ham">
<span></span><span></span><span></span>
</button>
</div>
</nav>
<div aria-label="Mobile navigation" aria-modal="true" class="nav-mobile" id="mob-nav" role="dialog">
<a class="mob-link" href="#services">Services</a>
<a class="mob-link" href="#about">About</a>
<a class="mob-link" href="#pricing">Pricing</a>
<a class="mob-link" href="#faq">FAQ</a>
<a class="mob-link" href="#contact">Contact</a>
</div>
<!-- HERO -->
<main id="main">
<section aria-label="BYILD Media hero" class="hero">
<div aria-hidden="true" class="hero-bg-fallback"></div>
<div aria-hidden="true" class="hero-orb hero-orb-1"></div>
<div aria-hidden="true" class="hero-orb hero-orb-2"></div>
<div aria-hidden="true" class="hero-grid"></div>
<div class="hero-content">
<div class="hero-kicker">code. design. impact</div>
<h1 class="hero-h1">
      Making Your Website<br/>
<span class="line-gold">Less Boring</span>
</h1>
<p class="hero-sub">
      Interactive, expressive, and strategically built   so scrolling through your website feels like an experience, not a chore.
    </p>
</div>
<div aria-hidden="true" class="hero-scroll">
<div class="hero-scroll-line"></div>
<span>Scroll</span>
</div>
</section>
<!-- MARQUEE -->
<div aria-hidden="true" class="marquee-strip">
<div class="marquee-track">
<div class="marquee-group">
<span class="marquee-item">Handcrafted</span>
<span class="marquee-item">Made With Love</span>
<span class="marquee-item">Fast Delivery</span>
<span class="marquee-item">Creative</span>
<span class="marquee-item">SEO Ready</span>
<span class="marquee-item">Handcrafted</span>
<span class="marquee-item">Made With Love</span>
<span class="marquee-item">Fast Delivery</span>
<span class="marquee-item">Creative</span>
<span class="marquee-item">SEO Ready</span>
<span class="marquee-item">Handcrafted</span>
<span class="marquee-item">Made With Love</span>
<span class="marquee-item">Fast Delivery</span>
<span class="marquee-item">Creative</span>
<span class="marquee-item">SEO Ready</span>
<span class="marquee-item">Handcrafted</span>
<span class="marquee-item">Made With Love</span>
<span class="marquee-item">Fast Delivery</span>
<span class="marquee-item">Creative</span>
<span class="marquee-item">SEO Ready</span>
</div>
<div class="marquee-group" aria-hidden="true">
<span class="marquee-item">Handcrafted</span>
<span class="marquee-item">Made With Love</span>
<span class="marquee-item">Fast Delivery</span>
<span class="marquee-item">Creative</span>
<span class="marquee-item">SEO Ready</span>
<span class="marquee-item">Handcrafted</span>
<span class="marquee-item">Made With Love</span>
<span class="marquee-item">Fast Delivery</span>
<span class="marquee-item">Creative</span>
<span class="marquee-item">SEO Ready</span>
<span class="marquee-item">Handcrafted</span>
<span class="marquee-item">Made With Love</span>
<span class="marquee-item">Fast Delivery</span>
<span class="marquee-item">Creative</span>
<span class="marquee-item">SEO Ready</span>
<span class="marquee-item">Handcrafted</span>
<span class="marquee-item">Made With Love</span>
<span class="marquee-item">Fast Delivery</span>
<span class="marquee-item">Creative</span>
<span class="marquee-item">SEO Ready</span>
</div>
</div>
</div>
<!-- SERVICES -->
<section id="services">
<div class="container">
<div class="services-intro">
<div class="reveal">
<span class="section-label">What We Do?</span>
<h2 class="section-title">Services Built for<br/><span class="gold">Real Business Results</span></h2>
<p class="section-sub">Every service we offer is designed with one goal: to make your business look credible, attract customers, and grow online.</p>
</div>
</div>
<div class="services-grid">
<div class="service-card reveal reveal-d1" tabindex="0">
<span class="service-num">01</span>

<h3 class="service-title">Website Design</h3>
<p class="service-desc">Custom, conversion-focused websites designed from scratch. We handle everything: design, development, copy structure, and launch. Your website will stand out.</p>
</div>
<div class="service-card reveal reveal-d2" tabindex="0">
<span class="service-num">02</span>

<h3 class="service-title">Landing Page Design</h3>
<p class="service-desc">High-converting single pages built to turn ad traffic into leads and sales. We design with psychology: the right layout, the right words, the right CTA at every scroll point.</p>
</div>
<div class="service-card reveal reveal-d3" tabindex="0">
<span class="service-num">03</span>

<h3 class="service-title">Website Maintenance</h3>
<p class="service-desc">We keep your website updated, secure, and running at full speed every month. No more wondering who to call when something breaks. We are already on it.</p>
</div>
<div class="service-card reveal reveal-d4" tabindex="0">
<span class="service-num">04</span>

<h3 class="service-title">Website Redesign</h3>
<p class="service-desc">Your old website is costing you customers. We identify what is broken and redesign it into something that actually performs: modern, fast, and on-brand.</p>
</div>
</div>
</div>
</section>
<!-- WHY CHOOSE US -->
<section id="why">
<div class="container">
<div class="reveal why-heading-center">
<h2 class="section-title why-brand-title">Why BYILD Media?</h2>
</div>
<div class="why-grid">
<div class="why-visual reveal">
<div class="why-card-main">
<div class="why-big-num" data-count="15" data-suffix="+">0+</div>
<div class="why-big-label">Projects delivered across industries</div>
<div class="why-stats">
<div class="why-stat">
<div class="why-stat-num" data-count="100" data-suffix="%">0%</div>
<div class="why-stat-lbl">Client Satisfaction</div>
</div>
<div class="why-stat">
<div class="why-stat-num">&lt;5d</div>
<div class="why-stat-lbl">Avg. Delivery Time</div>
</div>
<div class="why-stat">
<div class="why-stat-num">3s</div>
<div class="why-stat-lbl">Avg. Page Load</div>
</div>
<div class="why-stat">
<div class="why-stat-num">24h</div>
<div class="why-stat-lbl">Response Time</div>
</div>
</div>
</div>
</div>
<div class="why-points reveal reveal-d2">
<div class="why-point">
<div>
<div class="why-point-title">Results-First Approach</div>
<div class="why-point-desc">We do not design for awards. We design for your business goals. Every decision is made to get you more leads, calls, and sales.</div>
</div>
</div>
<div class="why-point">
<div>
<div class="why-point-title">Fast Turnaround</div>
<div class="why-point-desc">Most agencies take months. We deliver in days without cutting corners on quality. You will have a live site faster than you think.</div>
</div>
</div>
<div class="why-point">
<div>
<div class="why-point-title">You Own Everything</div>
<div class="why-point-desc">No lock-in. No subscriptions just to access your own site. Everything we build belongs to you, fully.</div>
</div>
</div>
<div class="why-point">
<div>
<div class="why-point-title">Transparent Pricing</div>
<div class="why-point-desc">You know exactly what you are paying and what you are getting before we start. No surprise invoices, no scope creep fees.</div>
</div>
</div>
</div>
</div>
</div>
</section>
<!-- PROCESS -->
<section id="process">
<div class="container">
<div class="text-center reveal">
<span class="section-label">How We Work</span>
<h2 class="section-title">Our Process</h2>
<p class="section-sub">Simple, transparent, and fast. From the first call to your live website, here is exactly what working with us looks like.</p>
</div>
<div class="process-steps"><svg id="process-glow-svg" class="process-glow-svg" viewBox="0 0 1000 60" preserveAspectRatio="none" aria-hidden="true"><path class="process-path-base" d="M 125,30 C 195,6 305,54 375,30 C 445,6 555,54 625,30 C 695,6 805,54 875,30"/><path id="process-path-glow" class="process-path-glow" d="M 125,30 C 195,6 305,54 375,30 C 445,6 555,54 625,30 C 695,6 805,54 875,30"/></svg>
<div aria-hidden="true" class="process-traveler">➜</div>
<div class="process-step reveal reveal-d1">
<div class="process-num-wrap"><span class="process-num">01</span></div>
<h3 class="process-title">Discovery Call</h3>
<p class="process-desc">We learn about your business, goals, target audience, and what you need the website to do. No forms, just a real conversation.</p>
</div>
<div class="process-step reveal reveal-d2">
<div class="process-num-wrap"><span class="process-num">02</span></div>
<h3 class="process-title">Design and Proposal</h3>
<p class="process-desc">We come back with a clear plan, timeline, and fixed price. You approve the direction before we start building anything.</p>
</div>
<div class="process-step reveal reveal-d3">
<div class="process-num-wrap"><span class="process-num">03</span></div>
<h3 class="process-title">Build and Review</h3>
<p class="process-desc">We build, you review. Two rounds of revisions included. We iterate until you are fully happy with every detail.</p>
</div>
<div class="process-step reveal reveal-d4">
<div class="process-num-wrap"><span class="process-num">04</span></div>
<h3 class="process-title">Launch and Support</h3>
<p class="process-desc">We push it live, hand over everything, and stay available for 30 days post-launch to handle any questions or tweaks.</p>
</div>
</div>
</div>
</section>
<!-- ABOUT -->
<section id="about">
<div class="container">
<div class="about-grid">
<div class="about-visual-wrap reveal">
<div class="about-img-placeholder">
<img src="byild-logo-symbol.png" alt="BYILD Media" style="width:130px;height:auto;object-fit:contain;filter:drop-shadow(0 8px 24px rgba(0,0,0,0.35));"/>
<span style="font-size:0.65rem; color: var(--text-dim); letter-spacing: 0.18em; text-transform: uppercase; font-family: var(--font-body);">BYILD Media</span>
</div>

</div>
<div class="about-text reveal reveal-d2">
<span class="section-label">About Us</span>
<h2 class="section-title">We Build Websites<br/><span class="gold">That Earn Their Keep</span></h2>
<div class="about-certs" style="margin-top: 1.5rem; margin-bottom: 1.75rem;">
<span class="about-cert">Est. 2026</span>
<span class="about-cert">India-Based</span>
<span class="about-cert">Remote-First</span>
</div>
<p>BYILD Media is a web design agency focused on one thing: building digital presence that delivers real business value. We work with startups, SMEs, and solo founders who are serious about growing online.</p>
<p>We are not a factory. We take on a limited number of projects each month so every client gets the attention their business deserves. When you work with BYILD Media, you get direct access to the person designing your site.</p>
<p>Our work spans industries: from e-commerce and hospitality to SaaS and consulting. What stays constant is our process: fast, transparent, and genuinely collaborative.</p>
<div style="margin-top: 2rem;">
<a class="btn btn-gold" href="#contact">Start a Project</a>
</div>
</div>
</div>
</div>
</section>
<!-- TESTIMONIALS -->
<section id="testimonials">
<div class="container">
<div class="text-center reveal">
<span class="section-label">Client Stories</span>
<h2 class="section-title">What Our Clients Say</h2>
</div>
<div class="testi-grid">
<div class="testi-card reveal reveal-d1">
<div aria-label="5 out of 5 stars" class="testi-stars">★★★★★</div>
<p class="testi-quote">BYILD Media delivered our website in under a week and it looks better than anything we had seen in our budget. We started getting enquiries within 3 days of going live.</p>
<div class="testi-author">
<div aria-hidden="true" class="testi-avatar">R</div>
<div>
<div class="testi-name">Rohan Gupta</div>
<div class="testi-role">Founder, Gupta Interiors, Delhi</div>
</div>
</div>
</div>
<div class="testi-card reveal reveal-d2">
<div aria-label="5 out of 5 stars" class="testi-stars">★★★★★</div>
<p class="testi-quote">Our old website was embarrassing. The redesign BYILD Media did made us look like a proper company for the first time. Clients actually comment on it now.</p>
<div class="testi-author">
<div aria-hidden="true" class="testi-avatar">S</div>
<div>
<div class="testi-name">Sneha Mehta</div>
<div class="testi-role">Director, Mehta Legal Associates, Mumbai</div>
</div>
</div>
</div>
<div class="testi-card reveal reveal-d3">
<div aria-label="5 out of 5 stars" class="testi-stars">★★★★★</div>
<p class="testi-quote">The landing page they built for our product launch converted at 14%, more than double what our previous page did. I cannot recommend them enough.</p>
<div class="testi-author">
<div aria-hidden="true" class="testi-avatar">A</div>
<div>
<div class="testi-name">Arjun Nair</div>
<div class="testi-role">Co-Founder, ClarkSaaS, Bangalore</div>
</div>
</div>
</div>
</div>
</div>
</section>
<!-- PRICING -->
<section id="pricing">
<div class="container">
<div class="text-center reveal">
<span class="section-label">Pricing</span>
<h2 class="section-title">Simple Honest Pricing</h2>
<p class="section-sub">No hidden fees. No monthly subscriptions. You pay once, you own it completely.</p>
</div>
<div class="pricing-grid">
<!-- Basic -->
<div class="pricing-card reveal reveal-d1">
<div class="pricing-plan">Project 1</div>
<div class="pricing-name">Standard Website</div>
<div class="pricing-amount">
<span class="pricing-currency">$</span>
<span class="pricing-num">450</span>
</div>
<div class="pricing-period">One-time payment</div>
<div class="pricing-note">Best for: New businesses, personal brands, local shops</div>
<hr class="pricing-divider"/>
<ul class="pricing-features" role="list">
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>Up to 5 pages</li>
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>Mobile responsive design</li>
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>Contact form included</li>
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>Basic SEO setup</li>
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>2 rounds of revisions</li>
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>30-day post-launch support</li>
<li class="pricing-feature dim"><svg aria-hidden="true" viewbox="0 0 24 24"><line x1="18" x2="6" y1="6" y2="18"></line><line x1="6" x2="18" y1="6" y2="18"></line></svg>Custom animations</li>
<li class="pricing-feature dim"><svg aria-hidden="true" viewbox="0 0 24 24"><line x1="18" x2="6" y1="6" y2="18"></line><line x1="6" x2="18" y1="6" y2="18"></line></svg>E-commerce / booking</li>
</ul>
<a class="btn btn-outline pricing-cta" href="#contact">Get Started</a>
</div>
<!-- Standard -->
<div class="pricing-card featured reveal reveal-d2">
<div class="pricing-badge">Most Popular</div>
<div class="pricing-plan">Project 2</div>
<div class="pricing-name">Professional Website</div>
<div class="pricing-amount">
<span class="pricing-currency">$</span>
<span class="pricing-num">600</span>
</div>
<div class="pricing-period">One-time payment</div>
<div class="pricing-note">Best for: Growing businesses, service providers, startups</div>
<hr class="pricing-divider"/>
<ul class="pricing-features" role="list">
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>Up to 10 pages</li>
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>Premium UI/UX design</li>
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>Custom animations and transitions</li>
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>Full SEO optimisation</li>
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>Blog / CMS integration</li>
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>Google Analytics setup</li>
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>3 rounds of revisions</li>
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>60-day post-launch support</li>
</ul>
<a class="btn btn-gold pricing-cta" href="#contact">Get Started</a>
</div>
<!-- Custom -->
<div class="pricing-card reveal reveal-d3">
<div class="pricing-plan">Project 3</div>
<div class="pricing-name">Custom Project</div>
<div style="text-align:center; padding: 1rem 0;">
<div class="pricing-custom-icon">
<svg aria-hidden="true" stroke-width="1.5" viewbox="0 0 24 24"><path d="M8.625 12a.375.375 0 11-.75 0 .375.375 0 01.75 0zm0 0H8.25m4.125 0a.375.375 0 11-.75 0 .375.375 0 01.75 0zm0 0H12m4.125 0a.375.375 0 11-.75 0 .375.375 0 01.75 0zm0 0h-.375M21 12c0 4.556-4.03 8.25-9 8.25a9.764 9.764 0 01-2.555-.337A5.972 5.972 0 015.41 20.97a5.969 5.969 0 01-.474-.065 4.48 4.48 0 00.978-2.025c.09-.457-.133-.901-.467-1.226C3.93 16.178 3 14.189 3 12c0-4.556 4.03-8.25 9-8.25s9 3.694 9 8.25z" stroke-linecap="round" stroke-linejoin="round"></path></svg>
</div>
<div style="font-family: var(--font-head); font-size: 1.6rem; font-weight: 600; color: var(--gold);">Let's Talk</div>
<div class="pricing-period" style="margin-top: 0.5rem;">Custom quote after discovery call</div>
</div>
<div class="pricing-note" style="text-align: center; margin-bottom: 2rem;">Best for: E-commerce, web apps, complex projects, large brands</div>
<hr class="pricing-divider"/>
<ul class="pricing-features" role="list">
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>Unlimited pages</li>
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>E-commerce / booking systems</li>
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>Custom functionality</li>
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>API integrations</li>
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>Dedicated project manager</li>
<li class="pricing-feature"><svg aria-hidden="true" viewbox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>Ongoing retainer available</li>
</ul>
<a class="btn btn-outline pricing-cta" href="#contact">Book a Call</a>
</div>
</div>
</div>
</section>
<!-- FAQ -->
<section id="faq">
<div class="container">
<div class="text-center reveal">
<span class="section-label">FAQ</span>
<h2 class="section-title">Frequently Asked Questions</h2>
</div>
<ul class="faq-list reveal reveal-d1" role="list">
<li class="faq-item">
<button aria-expanded="false" class="faq-btn">
<span class="faq-q">How long does it take to build my website?</span>
<span aria-hidden="true" class="faq-icon"><svg viewbox="0 0 24 24"><line x1="12" x2="12" y1="5" y2="19"></line><line x1="5" x2="19" y1="12" y2="12"></line></svg></span>
</button>
<div class="faq-answer" role="region">
<div class="faq-answer-inner">For the Basic plan, most websites are ready in 5 to 7 business days. The Standard plan typically takes 10 to 14 days depending on the number of pages and complexity. Custom projects are scoped individually on our discovery call.</div>
</div>
</li>
<li class="faq-item">
<button aria-expanded="false" class="faq-btn">
<span class="faq-q">Do I need to provide content and images?</span>
<span aria-hidden="true" class="faq-icon"><svg viewbox="0 0 24 24"><line x1="12" x2="12" y1="5" y2="19"></line><line x1="5" x2="19" y1="12" y2="12"></line></svg></span>
</button>
<div class="faq-answer" role="region">
<div class="faq-answer-inner">Ideally yes, you know your business best. But if you are stuck, we can help with placeholder copy, stock photography, and structure suggestions. Premium copywriting and photography sourcing are available as add-ons.</div>
</div>
</li>
<li class="faq-item">
<button aria-expanded="false" class="faq-btn">
<span class="faq-q">Will I be able to update the website myself?</span>
<span aria-hidden="true" class="faq-icon"><svg viewbox="0 0 24 24"><line x1="12" x2="12" y1="5" y2="19"></line><line x1="5" x2="19" y1="12" y2="12"></line></svg></span>
</button>
<div class="faq-answer" role="region">
<div class="faq-answer-inner">Yes. If you want a CMS like WordPress or Webflow, we set it up so you can update text, images, and blog posts yourself without touching any code. We walk you through everything on handover.</div>
</div>
</li>
<li class="faq-item">
<button aria-expanded="false" class="faq-btn">
<span class="faq-q">What is included in website maintenance?</span>
<span aria-hidden="true" class="faq-icon"><svg viewbox="0 0 24 24"><line x1="12" x2="12" y1="5" y2="19"></line><line x1="5" x2="19" y1="12" y2="12"></line></svg></span>
</button>
<div class="faq-answer" role="region">
<div class="faq-answer-inner">Our maintenance plans cover plugin and CMS updates, security monitoring, uptime monitoring, monthly performance reports, and minor content changes (up to 2 hours per month). Pricing is discussed based on your site's complexity.</div>
</div>
</li>
<li class="faq-item">
<button aria-expanded="false" class="faq-btn">
<span class="faq-q">Do you offer hosting?</span>
<span aria-hidden="true" class="faq-icon"><svg viewbox="0 0 24 24"><line x1="12" x2="12" y1="5" y2="19"></line><line x1="5" x2="19" y1="12" y2="12"></line></svg></span>
</button>
<div class="faq-answer" role="region">
<div class="faq-answer-inner">We do not resell hosting. We help you choose and set up the best hosting for your site (usually Cloudflare Pages, Vercel, or SiteGround). You pay the provider directly with no markup from us, and you own the account fully.</div>
</div>
</li>
<li class="faq-item">
<button aria-expanded="false" class="faq-btn">
<span class="faq-q">How do payments work?</span>
<span aria-hidden="true" class="faq-icon"><svg viewbox="0 0 24 24"><line x1="12" x2="12" y1="5" y2="19"></line><line x1="5" x2="19" y1="12" y2="12"></line></svg></span>
</button>
<div class="faq-answer" role="region">
<div class="faq-answer-inner">We take 50% upfront to begin the project and 50% on completion before the site goes live. For custom projects above Rs. 50,000, we can discuss milestone-based payment schedules. We accept bank transfer and UPI.</div>
</div>
</li>
<li class="faq-item">
<button aria-expanded="false" class="faq-btn">
<span class="faq-q">What if I do not like the design?</span>
<span aria-hidden="true" class="faq-icon"><svg viewbox="0 0 24 24"><line x1="12" x2="12" y1="5" y2="19"></line><line x1="5" x2="19" y1="12" y2="12"></line></svg></span>
</button>
<div class="faq-answer" role="region">
<div class="faq-answer-inner">We share designs before building and include revision rounds in every plan. We also do a thorough discovery call before we start. If for any reason a project is not working out, we handle it professionally and fairly.</div>
</div>
</li>
</ul>
</div>
</section>
<!-- CONTACT -->
<section id="contact">
<div class="container">
<div class="contact-grid">
<div>
<span class="section-label reveal">Get in Touch</span>
<h2 class="section-title reveal reveal-d1">Ready to Build<br/><span class="gold">Something Great?</span></h2>
<p class="section-sub reveal reveal-d2" style="margin-top: 1rem;">Tell us about your project and we will get back to you within 24 hours with a plan and next steps.</p>
<div class="reveal reveal-d2" style="margin-top: 3rem;">
<div class="contact-info-item">
<div class="contact-info-label">Email Us</div>
<div class="contact-info-value"><a href="mailto:company@byild.media">company@byild.media</a></div>
</div>
<div class="contact-info-item">
<div class="contact-info-label">WhatsApp</div>
<div class="contact-info-value">
<a href="https://wa.me/919893721918" rel="noopener" target="_blank">+91 9893721918</a><br/>
<a href="https://wa.me/918085762128" rel="noopener" target="_blank">+91 8085762128</a><br/>
<a href="https://wa.me/919171456190" rel="noopener" target="_blank">+91 9171456190</a>
</div>
</div>
<div class="contact-info-item">
<div class="contact-info-label">Response Time</div>
<div class="contact-info-value">Usually within 24 hours, Mon to Sat</div>
</div>
<div class="contact-info-item">
<div class="contact-info-label">Follow Our Work</div>
<div class="contact-info-value" style="display: flex; gap: 0.75rem; margin-top: 0.25rem;">
<a aria-label="BYILD Media on Instagram" class="footer-social-link" href="https://instagram.com/byildmedia" rel="noopener" target="_blank">
<svg aria-hidden="true" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><defs><radialGradient id="ig-rg" cx="30%" cy="105%" r="140%"><stop offset="0%" stop-color="#fdf497"/><stop offset="12%" stop-color="#fd8d32"/><stop offset="48%" stop-color="#ee2a7b"/><stop offset="82%" stop-color="#6228d7"/></radialGradient></defs><rect x="2" y="2" width="20" height="20" rx="5" fill="url(#ig-rg)"/><circle cx="12" cy="12" r="4" stroke="white" stroke-width="1.5" fill="none"/><circle cx="17.5" cy="6.5" r="1" fill="white"/></svg>
</a>

</div>
</div>
</div>
</div>
<div class="reveal reveal-d2">
<form action="https://api.web3forms.com/submit" aria-label="Contact form" class="contact-form" id="contact-form" method="POST" novalidate="">
<input name="access_key" type="hidden" value="527a0e7d-e0e6-451d-b69f-7f6c64ee77ab"/>
<input name="subject"    type="hidden" value="New BYILD Media Website Enquiry"/>
<input name="from_name"  type="hidden" value="BYILD Media Website"/>
<div class="form-group">
<label for="cf-name">Your Name *</label>
<input aria-required="true" autocomplete="name" class="form-control" id="cf-name" name="name" placeholder="" required="" type="text"/>
<span class="form-error" id="cf-name-err" role="alert">Please enter your name.</span>
</div>
<div class="form-group">
<label for="cf-email">Email Address *</label>
<input aria-required="true" autocomplete="email" class="form-control" id="cf-email" name="email" placeholder="rohan@company.com" required="" type="email"/>
<span class="form-error" id="cf-email-err" role="alert">Please enter a valid email.</span>
</div>
<div class="form-group">
<label for="cf-phone">Phone / WhatsApp</label>
<input autocomplete="tel" class="form-control" id="cf-phone" name="phone" placeholder="+91 98765 43210" type="tel"/>
</div>
<div class="form-group">
<label for="cf-service">Service Interested In *</label>
<select aria-required="true" class="form-control" id="cf-service" name="service" required="">
<option value="">Select a service...</option>
<option value="website">Website Design</option>
<option value="landing">Landing Page</option>
<option value="redesign">Website Redesign</option>
<option value="maintenance">Website Maintenance</option>
<option value="custom">Custom Project</option>
</select>
<span class="form-error" id="cf-service-err" role="alert">Please select a service.</span>
</div>
<div class="form-group">
<label for="cf-budget">Budget Range</label>
<select class="form-control" id="cf-budget" name="budget">
<option value="">Select a plan...</option>
<option value="450">$450 — Standard</option>
<option value="600">$600 — Professional</option>
<option value="custom">Custom Project</option>
</select>
</div>
<div class="form-group">
<label for="cf-message">Tell Us About Your Project *</label>
<textarea aria-required="true" class="form-control" id="cf-message" name="message" placeholder="What does your business do? What do you need the website to achieve?" required=""></textarea>
<span class="form-error" id="cf-msg-err" role="alert">Please tell us about your project.</span>
</div>
<button class="btn btn-gold" id="cf-submit" style="width:100%; justify-content:center;" type="submit">
<span class="cf-txt">Send Message</span>
<span aria-hidden="true" class="cf-spin" style="display:none; width:16px; height:16px; border-radius:50%; border:2px solid rgba(0,0,0,0.2); border-top-color:#000; animation: spin 0.6s linear infinite;"></span>
</button>
</form>
</div>
</div>
</div>
</section>
</main>

<!-- FOOTER -->
<footer>
<div class="container">
<div class="footer-grid">
<div class="footer-brand">
<img alt="BYILD Media logo" src="byild-logo-symbol.png" style="width:auto;height:100px;object-fit:contain;border-radius:22px;margin-bottom:1.25rem;box-shadow:0 18px 46px rgba(0,0,0,.22);"/>
<p class="footer-tagline">We build websites that work as hard as you do. Design-first, results-driven, always on time.</p>
<div aria-label="Social media links" class="footer-social" role="list">


</div>
</div>
<div>
<div class="footer-col-title">Services</div>
<ul class="footer-links" role="list">
<li><a href="#services">Website Design</a></li>
<li><a href="#services">Landing Pages</a></li>
<li><a href="#services">Website Redesign</a></li>
<li><a href="#services">Maintenance</a></li>
</ul>
</div>
<div>
<div class="footer-col-title">Company</div>
<ul class="footer-links" role="list">
<li><a href="#about">About Us</a></li>
<li><a href="#testimonials">Testimonials</a></li>
<li><a href="#process">Our Process</a></li>
</ul>
</div>
<div>
<div class="footer-col-title">Get Started</div>
<ul class="footer-links" role="list">
<li><a href="#pricing">Pricing</a></li>
<li><a href="#faq">FAQ</a></li>
<li><a href="#contact">Contact Us</a></li>
<li><a href="mailto:company@byild.media">company@byild.media</a></li>
</ul>
</div>
</div>
<div class="footer-bottom">
<span>© 2026 BYILD Media. All rights reserved.</span>
<span>Built by <a aria-label="BYILD Media" href="#">BYILD Media</a>, India</span>
</div>
</div>
</footer>
<div aria-atomic="true" aria-live="polite" class="toast" id="toast" role="status">
<span class="toast-icon"><svg aria-hidden="true" viewbox="0 0 24 24"><path d="M9 12.75L11.25 15 15 9.75M21 12a9 9 0 11-18 0 9 9 0 0118 0z" stroke-linecap="round" stroke-linejoin="round"></path></svg></span>
<span id="toast-msg">Message sent!</span>
</div>
<style>
  @keyframes spin { to { transform: rotate(360deg); } }

/* Preview update: BYILD Media branding and always-visible glass header */
.nav {
  background: transparent;
  border-bottom: 1px solid transparent;
  box-shadow: none;
  backdrop-filter: none;
  -webkit-backdrop-filter: none;
}
.nav.scrolled {
  background: linear-gradient(180deg, rgba(5,7,12,.88), rgba(5,7,12,.75));
  border-bottom-color: rgba(255,255,255,.10);
  box-shadow: 0 12px 40px rgba(0,0,0,.22);
  backdrop-filter: blur(24px) saturate(140%);
  -webkit-backdrop-filter: blur(24px) saturate(140%);
}
.nav-links a { color: rgba(255,255,255,.82); text-shadow: 0 1px 12px rgba(0,0,0,.55); }
.nav-links a:hover { color: #fff; }
.nav-brand-text { color:#fff; text-shadow:0 1px 14px rgba(0,0,0,.6); }
@media (max-width: 700px) {
  .nav { padding: .9rem 1rem; }
  .nav.scrolled { padding: .8rem 1rem; }
}

/* Preview update: centered What We Do intro */
#services .services-intro {
  max-width: 840px;
  margin-left: auto;
  margin-right: auto;
  text-align: center;
}
#services .services-intro .section-sub {
  margin: 1rem auto 0;
  max-width: 680px;
}


/* Preview adjustment: neutral black and ash-grey information surfaces */
main > section:not(.hero)::after,
#why::after,
#about::after,
#pricing::after,
#contact::after,
#process::after,
#testimonials::after,
#faq::after {
  background: linear-gradient(145deg, rgba(18,19,22,.82), rgba(8,9,11,.72)) !important;
  border-color: rgba(255,255,255,.075) !important;
  box-shadow: inset 0 1px 0 rgba(255,255,255,.035), 0 28px 90px rgba(0,0,0,.25) !important;
}

.service-card,
.why-card,
.why-card-main,
.process-step,
.testi-card,
.pricing-card,
.contact-form,
.about-visual,
.about-floating-card,
.faq-item {
  background: linear-gradient(145deg, rgba(27,28,31,.90), rgba(11,12,14,.88)) !important;
  border-color: rgba(255,255,255,.09) !important;
  box-shadow: inset 0 1px 0 rgba(255,255,255,.04), 0 18px 55px rgba(0,0,0,.24) !important;
}

.service-card:hover,
.service-card:focus-visible,
.why-card:hover,
.process-step:hover,
.testi-card:hover,
.pricing-card:hover,
.pricing-card.selected,
.faq-item:hover,
.faq-item.open {
  background: linear-gradient(145deg, rgba(34,35,38,.96), rgba(13,14,16,.94)) !important;
  border-color: rgba(201,185,154,.42) !important;
  box-shadow: inset 0 1px 0 rgba(255,255,255,.055), 0 24px 70px rgba(0,0,0,.34), 0 0 30px rgba(201,185,154,.08) !important;
}

.pricing-card.featured {
  background: linear-gradient(145deg, rgba(31,32,35,.96), rgba(10,11,13,.94)) !important;
}

.faq-btn,
.faq-answer,
.faq-answer-inner,
.pricing-note,
.pricing-divider {
  background-color: transparent !important;
}
</style>
<script>
(function(){
  'use strict';
  const html = document.documentElement;
  html.setAttribute('data-theme','dark');

  // ── Nav scroll ──────────────────────────────
  const nav    = document.getElementById('nav');
  const navCta = document.getElementById('nav-cta');
  let tick = false;
  window.addEventListener('scroll', () => {
    if (!tick) {
      requestAnimationFrame(() => {
        const scrollY = window.scrollY;
        const s = scrollY > 60;
        const fadeStart = window.innerHeight * 0.42;
        const fadeEnd = window.innerHeight * 1.28;
        const progress = Math.min(1, Math.max(0, (scrollY - fadeStart) / (fadeEnd - fadeStart)));
        document.documentElement.style.setProperty('--hero-video-opacity', '1');
        document.documentElement.style.setProperty('--hero-video-scale', '0');
        nav.classList.toggle('scrolled', s);
        navCta.style.display = 'inline-flex';
        tick = false;
      });
      tick = true;
    }
  }, { passive: true });

  window.dispatchEvent(new Event('scroll'));

  // ── Mobile nav ──────────────────────────────
  const ham    = document.getElementById('ham');
  const mobNav = document.getElementById('mob-nav');

  function openMob() {
    mobNav.classList.add('open');
    ham.setAttribute('aria-expanded','true');
    document.body.style.overflow = 'hidden';
    mobNav.querySelector('a').focus();
  }
  function closeMob() {
    mobNav.classList.remove('open');
    ham.setAttribute('aria-expanded','false');
    document.body.style.overflow = '';
    ham.focus();
  }
  ham.addEventListener('click', () => mobNav.classList.contains('open') ? closeMob() : openMob());
  document.querySelectorAll('.mob-link').forEach(a => a.addEventListener('click', closeMob));
  document.addEventListener('keydown', e => { if (e.key === 'Escape' && mobNav.classList.contains('open')) closeMob(); });

  // ── Scroll reveal ───────────────────────────
  const revEls = document.querySelectorAll('.reveal');
  if ('IntersectionObserver' in window) {
    const io = new IntersectionObserver(entries => {
      entries.forEach(e => {
        if (e.isIntersecting) {
          e.target.classList.add('in');
          io.unobserve(e.target);
        }
      });
    }, { threshold: 0.07, rootMargin: '0px 0px -20px 0px' });
    revEls.forEach(el => io.observe(el));
  } else {
    revEls.forEach(el => el.classList.add('in'));
  }


  // ── Scroll progress + subtle parallax ───────
  function updateScrollFx() {
    const max = Math.max(1, document.documentElement.scrollHeight - innerHeight);
    const progress = scrollY / max;
    html.style.setProperty('--progress', progress.toFixed(4));
    html.style.setProperty('--scroll', Math.round(scrollY));
  }
  updateScrollFx();
  addEventListener('scroll', updateScrollFx, { passive: true });

  // ── Magnetic glow cards ─────────────────────
  document.querySelectorAll('.service-card, .pricing-card, .testi-card').forEach(card => {
    card.addEventListener('pointermove', e => {
      const r = card.getBoundingClientRect();
      card.style.setProperty('--mx', ((e.clientX - r.left) / r.width * 100).toFixed(1) + '%');
      card.style.setProperty('--my', ((e.clientY - r.top) / r.height * 100).toFixed(1) + '%');
    });
  });

  // ── Count-up animation ──────────────────────
  function countUp(el) {
    const target = parseInt(el.getAttribute('data-count'), 10);
    const suffix = el.getAttribute('data-suffix') || '';
    const duration = 1400;
    const start = performance.now();
    function frame(now) {
      const progress = Math.min((now - start) / duration, 1);
      const ease = 1 - Math.pow(1 - progress, 3);
      el.textContent = Math.floor(ease * target) + suffix;
      if (progress < 1) requestAnimationFrame(frame);
    }
    requestAnimationFrame(frame);
  }

  const countEls = document.querySelectorAll('[data-count]');
  if ('IntersectionObserver' in window) {
    const cio = new IntersectionObserver(entries => {
      entries.forEach(e => {
        if (e.isIntersecting) { countUp(e.target); cio.unobserve(e.target); }
      });
    }, { threshold: 0.5 });
    countEls.forEach(el => cio.observe(el));
  }

  // ── FAQ accordion ───────────────────────────
  document.querySelectorAll('.faq-btn').forEach(btn => {
    btn.addEventListener('click', () => {
      const item   = btn.closest('.faq-item');
      const answer = item.querySelector('.faq-answer');
      const isOpen = item.classList.contains('open');

      document.querySelectorAll('.faq-item.open').forEach(el => {
        el.classList.remove('open');
        el.querySelector('.faq-answer').style.maxHeight = null;
        el.querySelector('.faq-btn').setAttribute('aria-expanded','false');
      });

      if (!isOpen) {
        item.classList.add('open');
        answer.style.maxHeight = answer.scrollHeight + 'px';
        btn.setAttribute('aria-expanded','true');
      }
    });
  });

  // ── Toast ───────────────────────────────────
  function showToast(msg) {
    const t = document.getElementById('toast');
    document.getElementById('toast-msg').textContent = msg;
    t.classList.add('show');
    setTimeout(() => t.classList.remove('show'), 5000);
  }

  // ── Contact form ────────────────────────────
  const form   = document.getElementById('contact-form');
  const cfBtn  = document.getElementById('cf-submit');
  const cfTxt  = cfBtn.querySelector('.cf-txt');
  const cfSpin = cfBtn.querySelector('.cf-spin');

  const rules = [
    { id:'cf-name',    err:'cf-name-err',    test: v => v.trim().length >= 2 },
    { id:'cf-email',   err:'cf-email-err',   test: v => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(v) },
    { id:'cf-service', err:'cf-service-err', test: v => !!v },
    { id:'cf-message', err:'cf-msg-err',     test: v => v.trim().length >= 10 },
  ];

  rules.forEach(({id, err}) => {
    const el = document.getElementById(id);
    ['input','change'].forEach(ev => el.addEventListener(ev, () => {
      el.classList.remove('is-error');
      document.getElementById(err).classList.remove('show');
    }));
  });

  form.addEventListener('submit', e => {
    e.preventDefault();
    let first = null;
    rules.forEach(({id, err, test}) => {
      const el = document.getElementById(id);
      const ok = test(el.value);
      el.classList.toggle('is-error', !ok);
      document.getElementById(err).classList.toggle('show', !ok);
      if (!ok && !first) first = el;
    });
    if (first) { first.focus(); return; }

    const svcLabel = { website:'Website Design', landing:'Landing Page', redesign:'Website Redesign', maintenance:'Website Maintenance', custom:'Custom Project' };
    const bdgLabel = { '10k':'Rs. 10,000 (Basic)', '20k':'Rs. 20,000 (Standard)', 'custom':'Rs. 20,000+', 'unsure':'Not sure yet' };

    const name    = document.getElementById('cf-name').value.trim();
    const email   = document.getElementById('cf-email').value.trim();
    const phone   = document.getElementById('cf-phone').value.trim();
    const service = document.getElementById('cf-service').value;
    const budget  = document.getElementById('cf-budget').value;
    const message = document.getElementById('cf-message').value.trim();

    cfTxt.style.display = 'none'; cfSpin.style.display = 'inline-block'; cfBtn.disabled = true;

    // Mailto fallback — built upfront, used only if Web3Forms fails
    const mailSubject = 'New Enquiry from ' + name + ' - BYILD Media';
    const mailBody = [
      'Name:    ' + name,
      'Email:   ' + email,
      'Phone:   ' + (phone || 'Not provided'),
      'Service: ' + (svcLabel[service] || service),
      'Budget:  ' + (bdgLabel[budget]  || 'Not specified'),
      '',
      'Message:',
      message,
      '',
      '---',
      'Sent via BYILD Media website'
    ].join('\n');
    const mailtoHref = 'mailto:company@byild.media?subject=' + encodeURIComponent(mailSubject) + '&body=' + encodeURIComponent(mailBody);

    function openMailto() {
      const a = document.createElement('a');
      a.href = mailtoHref;
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
    }

    // Primary: Web3Forms — delivers directly to your inbox, no client email app needed
    fetch('https://api.web3forms.com/submit', {
      method: 'POST',
      body: new FormData(form),
      headers: { 'Accept': 'application/json' }
    })
    .then(res => res.json())
    .then(data => {
      cfTxt.style.display = ''; cfSpin.style.display = 'none'; cfBtn.disabled = false;
      if (data.success) {
        form.reset();
        showToast('Message sent! We will get back to you within 24 hours.');
      } else {
        openMailto();
        showToast('Please hit Send in your email app to complete your enquiry.');
      }
    })
    .catch(() => {
      cfTxt.style.display = ''; cfSpin.style.display = 'none'; cfBtn.disabled = false;
      openMailto();
      showToast('Please hit Send in your email app to complete your enquiry.');
    });
  });

  // Pricing selection follows the visitor
  document.querySelectorAll('.pricing-card').forEach((card,index) => {
    card.addEventListener('click', e => {
      if (e.target.closest('a')) return;
      document.querySelectorAll('.pricing-card').forEach(c => c.classList.remove('selected'));
      card.classList.add('selected');
    });
    if (index === 1) card.classList.add('selected');
  });

})();
</script>
<script>
(function(){
  const video=document.getElementById('hero-video');
  if(!video) return;
  video.muted=true; video.defaultMuted=true; video.setAttribute('muted','');
  const tryPlay=()=>{ const p=video.play(); if(p&&p.catch) p.catch(()=>{}); };
  if(document.readyState==='loading') document.addEventListener('DOMContentLoaded',tryPlay,{once:true}); else tryPlay();
  window.addEventListener('load',tryPlay,{once:true});
  document.addEventListener('visibilitychange',()=>{ if(!document.hidden) tryPlay(); });
  document.addEventListener('pointerdown',tryPlay,{once:true});
  video.addEventListener('timeupdate',()=>{ if(video.duration && video.currentTime > video.duration - 0.08) video.currentTime = 0.02; });
})();
</script>
<script>
(function(){
  let tx=innerWidth*.5, ty=innerHeight*.35, x=tx, y=ty, raf=0;
  const root=document.documentElement;
  function draw(){
    x+=(tx-x)*.07; y+=(ty-y)*.07;
    root.style.setProperty('--bg-mx',x+'px');
    root.style.setProperty('--bg-my',y+'px');
    raf=requestAnimationFrame(draw);
  }
  addEventListener('pointermove',e=>{tx=e.clientX;ty=e.clientY},{passive:true});
  draw();
})();
</script>
<script>
(function(){
  const canvas=document.getElementById('generative-bg');
  if(!canvas) return;
  const ctx=canvas.getContext('2d');
  let w=0,h=0,dpr=1,pts=[],raf=0;
  const reduce=matchMedia('(prefers-reduced-motion: reduce)').matches;
  function resize(){
    dpr=Math.min(devicePixelRatio||1,2); w=innerWidth; h=innerHeight;
    canvas.width=Math.round(w*dpr); canvas.height=Math.round(h*dpr);
    canvas.style.width=w+'px'; canvas.style.height=h+'px';
    ctx.setTransform(dpr,0,0,dpr,0,0);
    const count=Math.max(32,Math.min(76,Math.round(w*h/23000)));
    pts=Array.from({length:count},(_,i)=>({
      x:Math.random()*w,y:Math.random()*h,
      vx:(Math.random()-.5)*.16,vy:(Math.random()-.5)*.16,
      r:.7+Math.random()*1.6,p:Math.random()*Math.PI*2
    }));
  }
  function frame(t){
    ctx.clearRect(0,0,w,h);
    const sy=scrollY||0;
    const hueShift=(sy*.012)%40;
    const g=ctx.createRadialGradient(w*.52,h*.45,10,w*.52,h*.45,Math.max(w,h)*.72);
    g.addColorStop(0,`hsla(${220+hueShift},45%,32%,.10)`);
    g.addColorStop(.48,`hsla(${275-hueShift*.3},38%,25%,.055)`);
    g.addColorStop(1,'rgba(0,0,0,0)');
    ctx.fillStyle=g; ctx.fillRect(0,0,w,h);
    for(const p of pts){
      if(!reduce){p.x+=p.vx;p.y+=p.vy;p.p+=.008;}
      if(p.x<-20)p.x=w+20;if(p.x>w+20)p.x=-20;if(p.y<-20)p.y=h+20;if(p.y>h+20)p.y=-20;
    }
    const maxD=Math.min(150,w*.16);
    for(let i=0;i<pts.length;i++){
      const a=pts[i];
      for(let j=i+1;j<pts.length;j++){
        const b=pts[j],dx=a.x-b.x,dy=a.y-b.y,d=Math.hypot(dx,dy);
        if(d<maxD){
          ctx.strokeStyle=`rgba(156,177,210,${(1-d/maxD)*.075})`;
          ctx.lineWidth=.65;ctx.beginPath();ctx.moveTo(a.x,a.y);ctx.lineTo(b.x,b.y);ctx.stroke();
        }
      }
      const glow=.35+.25*Math.sin(a.p+t*.00045);
      ctx.fillStyle=`rgba(225,208,170,${glow})`;
      ctx.beginPath();ctx.arc(a.x,a.y,a.r,0,Math.PI*2);ctx.fill();
    }
    raf=requestAnimationFrame(frame);
  }
  function heroState(){document.body.classList.toggle('past-hero',scrollY>innerHeight*.72)}
  resize();heroState();addEventListener('resize',resize,{passive:true});addEventListener('scroll',heroState,{passive:true});
  frame(0);
})();
</script>
<style>
/* -- Pricing equal-height fix -- */
.pricing-grid { align-items: stretch !important; }
.pricing-card { display: flex !important; flex-direction: column !important; }
.pricing-card .pricing-cta { margin-top: auto !important; }
.pricing-card.featured { transform: none !important; }
.pricing-card.selected { transform: none !important; }
.pricing-card.featured:hover,
.pricing-card.selected:hover { transform: translateY(-6px) !important; }

/* -- Rocket orbit around logo -- */
.logo-img-wrap {
  position: relative;
  width: 48px;
  height: 48px;
  flex-shrink: 0;
}
.logo-img-wrap img {
  width: 100%;
  height: 100%;
  display: block;
}
.rocket-orbit {
  position: absolute;
  left: 50%;
  top: 50%;
  width: 0;
  height: 0;
  pointer-events: none;
  z-index: 200;
}
.rocket-el {
  position: absolute;
  font-size: 13px;
  line-height: 1;
  filter: drop-shadow(0 0 5px rgba(226,207,168,0.75)) drop-shadow(0 0 12px rgba(201,185,154,0.4));
  will-change: transform, opacity;
}
</style>

<script>
/* -- 3-D rocket orbiting the logo -- */
(function () {
  var rocketEl = document.querySelector('.rocket-el');
  if (!rocketEl) return;
  var RX = 50, RY = 22, angle = 0, t = 0;
  function go() {
    t += 0.013; angle += 0.020;
    var bx = Math.cos(angle)*RX, by = Math.sin(angle)*RY;
    var dx = Math.sin(t*0.73+1.1)*10 + Math.cos(t*1.61+0.4)*5 + Math.sin(t*2.30+2.7)*3;
    var dy = Math.cos(t*0.59+2.0)*6  + Math.sin(t*1.37+0.9)*3 + Math.cos(t*2.10+1.5)*2;
    var vx = -Math.sin(angle)*RX*0.020 + Math.cos(t*0.73+1.1)*10*0.013*0.73;
    var vy =  Math.cos(angle)*RY*0.020 - Math.sin(t*0.59+2.0)*6 *0.013*0.59;
    var rot = Math.atan2(vy,vx)*(180/Math.PI)+90;
    var d   = Math.sin(angle);
    rocketEl.style.transform = 'translate(calc('+(bx+dx)+'px - 50%),calc('+(by+dy)+'px - 50%)) rotate('+rot.toFixed(1)+'deg) scale('+(0.60+(d+1)*0.22).toFixed(3)+')';
    rocketEl.style.opacity   = (0.40+(d+1)*0.30).toFixed(3);
    requestAnimationFrame(go);
  }
  go();
})();
</script>

<!-- ── batch-3 enhancements ── -->
<style>
/* 1. Marquee strip: shift slightly above (overlaps hero bottom) */
.marquee-strip {
  margin-top: -56px !important;
  position: relative !important;
  z-index: 5 !important;
}

/* 3. Process boxes: more padding so text doesn't touch edges */
.process-step {
  padding: 2rem 1.5rem !important;
}

/* 4. Process traveler: disable CSS animation (JS takes over) */
.process-traveler {
  animation: none !important;
  transition: left 0.65s cubic-bezier(0.65,0,0.35,1), transform 0.35s ease !important;
}
</style>

<script>
(function(){
  /* ── 4. Process traveler: hover-driven movement ── */
  var traveler = document.querySelector('.process-traveler');
  var stepsWrap = document.querySelector('.process-steps');
  var steps = stepsWrap ? stepsWrap.querySelectorAll('.process-step') : [];
  if(traveler && stepsWrap && steps.length){
    traveler.style.left = '6%';
    traveler.style.transform = 'scale(0.82)';
    steps.forEach(function(step){
      step.addEventListener('pointerenter', function(){
        var wRect = stepsWrap.getBoundingClientRect();
        var sRect = step.getBoundingClientRect();
        var centerPct = ((sRect.left + sRect.width * 0.5 - wRect.left) / wRect.width * 100);
        traveler.style.left = (centerPct - 1).toFixed(1) + '%';
        traveler.style.transform = 'scale(1.12)';
      });
      step.addEventListener('pointerleave', function(){
        traveler.style.transform = 'scale(0.88)';
      });
    });
  }

  /* ── 6. Space video: smooth crossfade loop ── */
  var video = document.getElementById('hero-video');
  if(!video) return;
  var veil = document.createElement('div');
  veil.style.cssText = 'position:fixed;inset:0;z-index:-6;background:#05070c;opacity:0;pointer-events:none;transition:opacity 1.1s ease;';
  document.body.insertBefore(veil, document.body.firstChild);
  var looping = false;
  video.addEventListener('timeupdate', function(){
    if(!video.duration || looping) return;
    if(video.duration - video.currentTime < 2.2){
      looping = true;
      veil.style.opacity = '0.96';
      setTimeout(function(){
        video.currentTime = 0;
        video.play().catch(function(){});
        veil.style.opacity = '0';
        setTimeout(function(){ looping = false; }, 1200);
      }, 1050);
    }
  });
})();
</script>
<!-- ── process glow-line + pricing batch ── -->
<style>
/* hide old arrow traveler */
.process-traveler { display: none !important; }

/* glow fill line overlaying the existing dim connector */
.process-line-fill {
  position: absolute;
  top: 26px;
  left: 10%;
  height: 2px;
  width: 0%;
  background: linear-gradient(to right, var(--gold-dim, #9a7f50), var(--gold, #e2cfa8), var(--gold-bright, #f5e6c8));
  box-shadow: 0 0 7px 3px rgba(226,207,168,.55), 0 0 18px 7px rgba(226,207,168,.22);
  border-radius: 2px;
  transition: width 0.58s cubic-bezier(0.65,0,0.35,1);
  pointer-events: none;
  z-index: 5;
}
</style>

<script>
(function(){
  var fill = document.getElementById('process-line-fill');
  var wrap = document.querySelector('.process-steps');
  if(!fill || !wrap) return;
  var steps = wrap.querySelectorAll('.process-step');

  steps.forEach(function(step){
    step.addEventListener('pointerenter', function(){
      var wRect = wrap.getBoundingClientRect();
      var sRect = step.getBoundingClientRect();
      var centerPct = (sRect.left + sRect.width * 0.5 - wRect.left) / wRect.width * 100;
      var w = Math.max(0, centerPct - 10).toFixed(1);
      fill.style.width = w + '%';
    });
  });

  wrap.addEventListener('pointerleave', function(){
    fill.style.width = '0%';
  });
})();
</script>
<!-- ── batch-4 styles + process glow SVG ── -->
<style>
/* Process: hide old straight connector, show SVG wave */
.process-steps::before { display: none !important; }
.process-traveler { display: none !important; }

.process-glow-svg {
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 60px;
  overflow: visible;
  pointer-events: none;
  z-index: 5;
}
.process-path-base {
  fill: none;
  stroke: rgba(226,207,168,.14);
  stroke-width: 1.5;
  stroke-linecap: round;
}
.process-path-glow {
  fill: none;
  stroke: var(--gold, #e2cfa8);
  stroke-width: 2.5;
  stroke-linecap: round;
  filter: drop-shadow(0 0 5px rgba(226,207,168,.75)) drop-shadow(0 0 14px rgba(226,207,168,.4));
  transition: stroke-dashoffset 0.6s cubic-bezier(0.65,0,0.35,1);
}
@media (max-width: 820px){
  .process-glow-svg { display: none; }
}

/* FAQ: capsule opener boxes */
.faq-item {
  background: none !important;
  border: none !important;
  box-shadow: none !important;
  padding: 0 !important;
}
.faq-btn {
  border-radius: 100px !important;
  border: 1px solid rgba(255,255,255,.6) !important;
  background: linear-gradient(135deg, rgba(18,20,32,.90), rgba(10,12,20,.88)) !important;
  padding: 1rem 1.75rem !important;
}
.faq-btn[aria-expanded="true"] {
  border-radius: 18px 18px 0 0 !important;
}
.faq-item .faq-answer {
  border-left: 1px solid rgba(255,255,255,.18) !important;
  border-right: 1px solid rgba(255,255,255,.18) !important;
  border-bottom: 1px solid rgba(255,255,255,.18) !important;
  border-radius: 0 0 18px 18px !important;
  background: rgba(12,14,24,.70) !important;
}

/* Contact form: remove border on name field */
#cf-name {
  border: none !important;
  box-shadow: none !important;
  outline: none !important;
}
#cf-name:focus {
  border-bottom: 1px solid var(--gold-dim, #9a7f50) !important;
}

/* Footer social icon sizing */
.footer-social-link svg { width: 22px; height: 22px; }
</style>

<script>
(function(){
  /* Process glow line: draws to hovered step */
  var pathGlow = document.getElementById('process-path-glow');
  var wrap = document.querySelector('.process-steps');
  if(!pathGlow || !wrap) return;
  var steps = wrap.querySelectorAll('.process-step');

  var L = pathGlow.getTotalLength();
  pathGlow.style.strokeDasharray = L;
  pathGlow.style.strokeDashoffset = L;

  /* 4 stops: tiny bit, 1/3, 2/3, full */
  var stops = [0.04, 1/3, 2/3, 1.0];

  steps.forEach(function(step, i){
    step.addEventListener('pointerenter', function(){
      pathGlow.style.strokeDashoffset = (L * (1 - stops[i])).toFixed(1);
    });
  });

  wrap.addEventListener('pointerleave', function(){
    pathGlow.style.strokeDashoffset = L;
  });
})();
</script>
<!-- ── batch-5 fixes ── -->
<style>
/* FAQ: proper padding so text doesn't touch left/right border */
.faq-btn {
  padding: 1.25rem 2.25rem !important;
}
.faq-answer-inner {
  padding: 1rem 2.25rem 1.25rem !important;
}

/* Contact form: remove the grey card background entirely */
.contact-form {
  background: transparent !important;
  border: none !important;
  box-shadow: none !important;
  padding: 0 !important;
}

/* Form controls: white border instead of grey */
.form-control,
.form-control:not(:focus) {
  border-color: rgba(255,255,255,.45) !important;
  background: rgba(255,255,255,.04) !important;
}
.form-control:focus {
  border-color: rgba(255,255,255,.85) !important;
  box-shadow: 0 0 0 2px rgba(255,255,255,.08) !important;
}
select.form-control option {
  background: #0e1018;
}

/* Pricing: bigger dollar / currency symbol */
.pricing-currency {
  font-size: 2rem !important;
  margin-bottom: 0.6rem !important;
}

/* Instagram icon alignment in footer social box */
.footer-social-link {
  display: flex !important;
  align-items: center !important;
  justify-content: center !important;
  overflow: hidden !important;
}
.footer-social-link > svg {
  width: 22px !important;
  height: 22px !important;
  flex-shrink: 0 !important;
  display: block !important;
}
</style>
<!-- ── batch-6 fixes ── -->
<style>
/* Pricing cards: restore visible cursor */
.pricing-card,
.pricing-card * {
  cursor: default !important;
}
.pricing-card .pricing-cta,
.pricing-card a {
  cursor: pointer !important;
}

/* Your Name input: white border same as other fields */
#cf-name {
  border: 1px solid rgba(255,255,255,.45) !important;
  box-shadow: none !important;
}
#cf-name:focus {
  border-color: rgba(255,255,255,.85) !important;
  box-shadow: 0 0 0 2px rgba(255,255,255,.08) !important;
}
</style>
<!-- ── mobile optimisation (390-480px) ── -->
<style>
@media (max-width: 480px) {

  /* ─ Layout ─ */
  .container { padding: 0 1.1rem !important; }
  section { padding: 3.75rem 0 !important; }

  /* ─ Hero ─ */
  .hero-h1 { font-size: clamp(2.4rem, 9.5vw, 3.2rem) !important; line-height: 1.02 !important; }
  .hero-sub { font-size: 0.88rem !important; max-width: 100% !important; }
  .hero-actions { flex-direction: column !important; align-items: stretch !important; gap: 0.75rem !important; }
  .hero-actions .btn { justify-content: center !important; width: 100% !important; }

  /* ─ Marquee: smaller pull-up on mobile ─ */
  .marquee-strip { margin-top: -28px !important; }

  /* ─ Section headings ─ */
  .section-title { font-size: clamp(1.8rem, 7.5vw, 2.8rem) !important; }

  /* ─ Why BYILD ─ */
  .why-big-num { font-size: 3.5rem !important; }
  .why-stat-num { font-size: 1.5rem !important; }
  .why-stats { grid-template-columns: 1fr 1fr !important; gap: 1rem !important; }

  /* ─ Pricing ─ */
  .pricing-grid { gap: 1.25rem !important; }
  .pricing-card { padding: 1.75rem 1.4rem !important; }
  .pricing-num { font-size: 2.6rem !important; }
  .pricing-currency { font-size: 1.6rem !important; margin-bottom: 0.45rem !important; }
  .pricing-badge { font-size: 0.62rem !important; }

  /* ─ Process steps (vertical on mobile) ─ */
  .process-step { padding: 1.5rem 1rem !important; text-align: left !important; }
  .process-num-wrap { margin: 0 0 1rem 0 !important; }

  /* ─ FAQ ─ */
  .faq-btn { padding: 1rem 1.4rem !important; gap: 0.75rem !important; }
  .faq-answer-inner { padding: 0.75rem 1.4rem 1rem !important; }
  .faq-q { font-size: 0.88rem !important; }

  /* ─ Contact form ─ */
  .contact-grid { gap: 2.5rem !important; }
  .form-control { font-size: 0.85rem !important; padding: 0.75rem 0.9rem !important; }
  label { font-size: 0.62rem !important; }

  /* ─ About ─ */
  .about-img-placeholder { max-width: 280px !important; margin: 0 auto !important; }

  /* ─ Testimonials ─ */
  .testi-card { padding: 1.5rem !important; }
  .testi-quote { font-size: 0.88rem !important; }

  /* ─ Footer ─ */
  .footer-brand img { height: 80px !important; }
  .footer-grid { gap: 1.75rem !important; }
  .footer-bottom { font-size: 0.7rem !important; }
  .footer-col-title { font-size: 0.7rem !important; margin-bottom: 0.75rem !important; }
  .footer-links a { font-size: 0.8rem !important; }
}

/* Slightly larger phones (481-768px) */
@media (min-width: 481px) and (max-width: 768px) {
  .container { padding: 0 1.5rem !important; }
  .pricing-card { padding: 2rem 1.75rem !important; }
  .pricing-num { font-size: 2.8rem !important; }
  .pricing-currency { font-size: 1.8rem !important; }
  .why-big-num { font-size: 4.5rem !important; }
  .faq-btn { padding: 1.1rem 1.75rem !important; }
}
</style>
<!-- ── mobile nav fix ── -->
<style>
@media (max-width: 768px) {
  .nav { padding: 0.95rem 1.25rem !important; }
  .nav.scrolled { padding: 0.8rem 1.25rem !important; }
  .nav-logo img { width: 36px !important; height: 36px !important; border-radius: 8px !important; }
  .nav-brand-text { font-size: 0.82rem !important; letter-spacing: 0.06em !important; }

  /* Shrink the Get a Quote button to fit mobile nav */
  #nav-cta {
    font-size: 0.65rem !important;
    padding: 0.45rem 0.85rem !important;
    letter-spacing: 0.06em !important;
    border-radius: 6px !important;
    white-space: nowrap !important;
  }
}

@media (max-width: 480px) {
  .nav { padding: 0.85rem 1rem !important; }
  .nav-logo img { width: 32px !important; height: 32px !important; }
  .nav-brand-text { font-size: 0.76rem !important; }
  #nav-cta {
    font-size: 0.6rem !important;
    padding: 0.4rem 0.7rem !important;
  }
  .nav-ham { width: 34px !important; height: 34px !important; }
}
</style></body>
</html>
