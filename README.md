<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Voltex Energy Drink — Enerjini Keşfet</title>
<style>
  :root{
    --bg:#08090a;
    --bg-raised:#101113;
    --bg-card:#131417;
    --line:#212226;
    --volt:#c6ff1a;
    --volt-dim:#8fbf00;
    --white:#f2f2f2;
    --grey:#8d8f94;
    --grey-dim:#54565b;
    --radius:10px;
  }
  *{box-sizing:border-box;margin:0;padding:0;}
  html{scroll-behavior:smooth;}
  body{
    background:var(--bg);
    font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',Helvetica,Arial,sans-serif;
    color:var(--white);
    overflow-x:hidden;
    cursor:default;
  }
  a{color:inherit;text-decoration:none;}
  img{max-width:100%;display:block;}
  .wrap{max-width:1220px;margin:0 auto;padding:0 32px;}
  .display{
    font-family:'Arial Black','Helvetica Neue',sans-serif;
    font-style:italic;
    letter-spacing:-0.5px;
  }
  ::selection{background:var(--volt);color:#0a0a0a;}

  /* ---------- SMOKE CANVAS ---------- */
  #smokeCanvas{
    position:fixed;inset:0;
    pointer-events:none;
    z-index:9999;
    mix-blend-mode:screen;
  }

  /* ---------- NAV ---------- */
  nav{
    position:sticky;top:0;z-index:200;
    background:rgba(8,9,10,0.82);
    backdrop-filter:blur(14px);
    -webkit-backdrop-filter:blur(14px);
    border-bottom:1px solid var(--line);
  }
  .nav-inner{
    max-width:1220px;margin:0 auto;padding:16px 32px;
    display:flex;align-items:center;justify-content:space-between;
  }
  .brand{display:flex;align-items:center;gap:12px;}
  .brand svg{width:36px;height:36px;}
  .brand .name{font-size:21px;}
  .brand .name .x{color:var(--volt);}
  .nav-links{display:flex;gap:36px;font-size:13.5px;color:var(--grey);}
  .nav-links a{transition:color .15s ease;}
  .nav-links a:hover{color:var(--white);}
  .nav-cta{
    background:var(--volt);color:#0a0a0a;font-weight:800;font-size:13px;
    padding:11px 22px;border-radius:30px;
  }
  @media(max-width:860px){ .nav-links{display:none;} }

  /* ---------- HERO ---------- */
  .hero{
    position:relative;
    padding:100px 32px 0;
    text-align:center;
    background:
      radial-gradient(ellipse 1000px 520px at 50% 8%, rgba(198,255,26,0.09), transparent 65%),
      var(--bg);
    border-bottom:1px solid var(--line);
    overflow:hidden;
  }
  .eyebrow{
    display:inline-block;
    color:var(--volt);
    font-size:11.5px;
    font-weight:700;
    letter-spacing:4px;
    margin-bottom:20px;
    border:1px solid rgba(198,255,26,0.3);
    padding:6px 14px;
    border-radius:20px;
  }
  .hero h1{
    font-size:clamp(38px,7vw,76px);
    line-height:1.04;
    max-width:840px;
    margin:0 auto;
  }
  .hero h1 .hi{color:var(--volt);}
  .hero-sub{
    max-width:500px;
    margin:24px auto 0;
    color:var(--grey);
    font-size:16px;
    line-height:1.65;
  }
  .hero-actions{margin-top:36px;display:flex;gap:16px;justify-content:center;flex-wrap:wrap;}
  .btn-primary{
    background:var(--volt);
    color:#0a0a0a;
    font-weight:800;
    font-size:14px;
    padding:16px 36px;
    border-radius:8px;
    border:none;
    cursor:pointer;
    transition:transform .15s ease, box-shadow .15s ease;
  }
  .btn-primary:hover{transform:translateY(-2px);box-shadow:0 10px 30px rgba(198,255,26,0.25);}
  .btn-ghost{
    border:1px solid #2a2b2f;
    color:var(--white);
    font-size:14px;
    padding:16px 36px;
    border-radius:8px;
    background:transparent;
    cursor:pointer;
  }
  .btn-ghost:hover{border-color:#444;}
  .hero-image{margin-top:60px;width:100%;position:relative;}
  .hero-image img{
    width:100%;
    filter:drop-shadow(0 40px 60px rgba(0,0,0,0.75));
  }
  .hero-fade{
    position:absolute;bottom:0;left:0;right:0;height:120px;
    background:linear-gradient(180deg, transparent, var(--bg));
  }

  /* ---------- MARQUEE ---------- */
  .marquee{
    border-bottom:1px solid var(--line);
    background:var(--bg-raised);
    padding:16px 0;
    overflow:hidden;
    white-space:nowrap;
  }
  .marquee-track{
    display:inline-flex;
    gap:60px;
    animation:scroll 28s linear infinite;
    font-size:13px;
    letter-spacing:2px;
    color:var(--grey-dim);
    font-weight:700;
  }
  .marquee-track span{color:var(--volt);margin:0 10px;}
  @keyframes scroll{
    0%{transform:translateX(0);}
    100%{transform:translateX(-50%);}
  }

  /* ---------- STATS ---------- */
  .stats{
    display:grid;grid-template-columns:repeat(4,1fr);
    border-bottom:1px solid var(--line);
  }
  .stat{padding:36px 20px;text-align:center;border-right:1px solid var(--line);}
  .stat:last-child{border-right:none;}
  .stat .num{font-size:32px;font-weight:800;color:var(--volt);display:block;}
  .stat .lbl{font-size:11.5px;color:var(--grey);margin-top:6px;letter-spacing:1px;}
  @media(max-width:640px){
    .stats{grid-template-columns:repeat(2,1fr);}
    .stat:nth-child(2n){border-right:none;}
    .stat{border-bottom:1px solid var(--line);}
  }

  /* ---------- ABOUT ---------- */
  .about{padding:120px 0;border-bottom:1px solid var(--line);}
  .about-grid{display:grid;grid-template-columns:1fr 1fr;gap:80px;align-items:center;}
  .about h2{font-size:clamp(28px,4vw,44px);line-height:1.15;margin-bottom:22px;}
  .about h2 .hi{color:var(--volt);}
  .about p{color:var(--grey);font-size:15px;line-height:1.85;margin-bottom:18px;}
  .about-list{margin-top:28px;display:flex;flex-direction:column;gap:20px;}
  .about-item{display:flex;gap:16px;align-items:flex-start;}
  .about-item .ico{
    width:38px;height:38px;flex-shrink:0;
    border-radius:10px;
    background:rgba(198,255,26,0.1);
    display:flex;align-items:center;justify-content:center;
  }
  .about-item .ico svg{width:18px;height:18px;stroke:var(--volt);}
  .about-item .t{font-size:14.5px;color:var(--white);font-weight:700;}
  .about-item .d{font-size:13px;color:var(--grey);margin-top:3px;}
  .about-visual{
    position:relative;display:flex;justify-content:center;
    background:radial-gradient(ellipse at center, rgba(198,255,26,0.07), transparent 70%);
    padding:40px;border-radius:24px;
  }
  .about-visual img{max-width:280px;filter:drop-shadow(0 30px 40px rgba(0,0,0,0.6));}
  @media(max-width:860px){ .about-grid{grid-template-columns:1fr;} .about-visual{order:-1;} }

  /* ---------- CATALOG ---------- */
  .catalog{padding:120px 0;border-bottom:1px solid var(--line);}
  .section-head{text-align:center;max-width:600px;margin:0 auto 64px;}
  .section-head h2{font-size:clamp(28px,4vw,44px);line-height:1.15;}
  .section-head p{color:var(--grey);font-size:14.5px;margin-top:16px;line-height:1.6;}

  .filters{
    display:flex;gap:10px;justify-content:center;flex-wrap:wrap;
    margin-bottom:48px;
  }
  .filter-btn{
    background:var(--bg-raised);
    border:1px solid var(--line);
    color:var(--grey);
    font-size:12.5px;
    padding:9px 18px;
    border-radius:20px;
    cursor:pointer;
    transition:all .15s ease;
  }
  .filter-btn.active, .filter-btn:hover{
    background:var(--volt);
    color:#0a0a0a;
    border-color:var(--volt);
    font-weight:700;
  }

  .product-grid{
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:20px;
  }
  .product-card{
    background:var(--bg-card);
    border:1px solid var(--line);
    border-radius:var(--radius);
    padding:26px 22px 22px;
    display:flex;flex-direction:column;
    transition:transform .2s ease, border-color .2s ease;
    position:relative;
    cursor:pointer;
  }
  .product-card:hover{transform:translateY(-4px);border-color:#333;}
  .product-badge{
    position:absolute;top:16px;left:16px;
    background:rgba(198,255,26,0.12);
    color:var(--volt);
    font-size:10px;font-weight:800;letter-spacing:1px;
    padding:5px 10px;border-radius:20px;
    z-index:2;
  }
  .product-img{
    height:170px;display:flex;align-items:flex-end;justify-content:center;
    margin-bottom:18px;
  }
  .product-img img{max-height:170px;width:auto;filter:drop-shadow(0 14px 18px rgba(0,0,0,0.55));}
  .product-name{font-size:16.5px;font-weight:700;}
  .product-tag{font-size:10.5px;color:var(--tag-color,var(--volt));letter-spacing:1.5px;font-weight:700;margin-top:4px;}
  .product-desc{font-size:12.5px;color:var(--grey);margin-top:10px;line-height:1.55;flex-grow:1;}
  .product-footer{
    display:flex;align-items:center;justify-content:space-between;
    margin-top:18px;padding-top:16px;border-top:1px solid var(--line);
  }
  .detail-btn{
    width:100%;background:var(--bg-raised);border:1px solid var(--line);color:var(--white);
    padding:10px;border-radius:8px;font-size:12.5px;font-weight:700;cursor:pointer;
    transition:all .15s ease;
  }
  .detail-btn:hover{background:var(--volt);color:#0a0a0a;border-color:var(--volt);}
  @media(max-width:980px){ .product-grid{grid-template-columns:repeat(2,1fr);} }
  @media(max-width:520px){ .product-grid{grid-template-columns:1fr;} }

  /* ---------- PRODUCT MODAL ---------- */
  .modal-overlay{
    position:fixed;inset:0;background:rgba(0,0,0,0.7);
    z-index:500;opacity:0;pointer-events:none;transition:opacity .25s ease;
    display:flex;align-items:center;justify-content:center;padding:24px;
  }
  .modal-overlay.open{opacity:1;pointer-events:auto;}
  .modal{
    background:var(--bg-raised);border:1px solid var(--line);border-radius:16px;
    max-width:640px;width:100%;max-height:86vh;overflow-y:auto;
    display:grid;grid-template-columns:1fr 1.2fr;
    transform:scale(0.94);transition:transform .25s ease;
  }
  .modal-overlay.open .modal{transform:scale(1);}
  .modal-visual{
    background:radial-gradient(ellipse at center, rgba(198,255,26,0.08), transparent 70%);
    display:flex;align-items:center;justify-content:center;padding:30px;
  }
  .modal-visual img{max-height:280px;filter:drop-shadow(0 20px 30px rgba(0,0,0,0.6));}
  .modal-body{padding:32px 30px 32px 6px;}
  .modal-close{
    position:absolute;top:18px;right:18px;background:none;border:none;color:var(--grey);
    font-size:24px;cursor:pointer;z-index:2;
  }
  .modal-name{font-size:24px;font-weight:800;}
  .modal-tag{font-size:11px;letter-spacing:2px;font-weight:700;margin-top:6px;color:var(--modal-color,var(--volt));}
  .modal-desc{font-size:13.5px;color:var(--grey);line-height:1.7;margin-top:16px;}
  .modal-section{margin-top:22px;}
  .modal-section h4{font-size:11.5px;letter-spacing:1.5px;color:var(--volt);margin-bottom:10px;}
  .modal-ingredients{display:flex;flex-wrap:wrap;gap:8px;}
  .modal-ingredients span{
    background:var(--bg-card);border:1px solid var(--line);padding:6px 12px;
    border-radius:20px;font-size:11.5px;color:var(--white);
  }
  .modal-facts{display:flex;flex-direction:column;gap:8px;}
  .modal-facts .row{display:flex;justify-content:space-between;font-size:12.5px;padding:8px 0;border-bottom:1px solid var(--line);}
  .modal-facts .row span:first-child{color:var(--grey);}
  @media(max-width:600px){ .modal{grid-template-columns:1fr;} }

  /* ---------- INFO / NUTRITION ---------- */
  .info{padding:120px 0;border-bottom:1px solid var(--line);background:var(--bg-raised);}
  .info-grid{display:grid;grid-template-columns:1.1fr 0.9fr;gap:80px;}
  .info h2{font-size:clamp(26px,4vw,40px);line-height:1.15;margin-bottom:18px;}
  .info h2 .hi{color:var(--volt);}
  .info p{color:var(--grey);font-size:14.5px;line-height:1.8;margin-bottom:16px;}
  .nutrition-table{background:var(--bg);border:1px solid var(--line);border-radius:var(--radius);overflow:hidden;}
  .nutrition-table .row{display:flex;justify-content:space-between;padding:17px 24px;border-bottom:1px solid var(--line);font-size:13.5px;}
  .nutrition-table .row:last-child{border-bottom:none;}
  .nutrition-table .row .k{color:var(--grey);}
  .nutrition-table .row .v{font-weight:700;}
  .nutrition-table .head{padding:17px 24px;font-size:11.5px;letter-spacing:2px;color:var(--volt);font-weight:800;border-bottom:1px solid var(--line);background:var(--bg-raised);}
  @media(max-width:860px){ .info-grid{grid-template-columns:1fr;} }

  /* ---------- BUY ---------- */
  .buy{padding:100px 0;border-bottom:1px solid var(--line);text-align:center;}
  .buy h2{font-size:clamp(24px,4vw,36px);margin-bottom:14px;}
  .buy p{color:var(--grey);font-size:14px;max-width:460px;margin:0 auto 40px;}
  .buy-channels{display:grid;grid-template-columns:repeat(3,1fr);gap:16px;max-width:760px;margin:0 auto;}
  .buy-channel{background:var(--bg-card);border:1px solid var(--line);border-radius:var(--radius);padding:30px 20px;font-size:13px;color:var(--grey);}
  .buy-channel b{display:block;color:var(--white);font-size:16px;margin-bottom:6px;}
  @media(max-width:640px){ .buy-channels{grid-template-columns:1fr;} }

  /* ---------- CTA FINAL ---------- */
  .cta-final{
    padding:120px 32px;text-align:center;
    background:radial-gradient(ellipse 900px 420px at 50% 100%, rgba(198,255,26,0.11), transparent 70%), var(--bg);
  }
  .cta-final h2{font-size:clamp(30px,5vw,52px);margin-bottom:20px;}
  .cta-final h2 .hi{color:var(--volt);}
  .cta-final p{color:var(--grey);font-size:14px;margin-bottom:34px;letter-spacing:0.5px;}

  footer{border-top:1px solid var(--line);padding:56px 32px 30px;}
  .footer-grid{max-width:1220px;margin:0 auto;display:flex;justify-content:space-between;flex-wrap:wrap;gap:36px;padding-bottom:36px;}
  .footer-brand{max-width:260px;}
  .footer-brand .display{font-size:19px;}
  .footer-brand .x{color:var(--volt);}
  .footer-brand p{color:var(--grey-dim);font-size:12px;margin-top:12px;line-height:1.6;}
  .footer-col h5{font-size:11.5px;letter-spacing:1.5px;color:var(--grey);margin-bottom:16px;}
  .footer-col a{display:block;font-size:13px;color:var(--white);margin-bottom:11px;}
  .footer-col a:hover{color:var(--volt);}
  .footer-bottom{max-width:1220px;margin:0 auto;border-top:1px solid var(--line);padding-top:24px;font-size:11px;color:var(--grey-dim);letter-spacing:1px;text-align:center;}

  /* ---------- AI ASSISTANT ---------- */
  .ai-toggle{
    position:fixed;bottom:26px;right:26px;z-index:400;
    width:62px;height:62px;border-radius:50%;
    background:linear-gradient(135deg, var(--volt), #7fbf00);
    border:none;cursor:pointer;
    display:flex;align-items:center;justify-content:center;
    box-shadow:0 10px 30px rgba(198,255,26,0.35);
    animation:pulse 2.4s infinite;
  }
  @keyframes pulse{
    0%{box-shadow:0 0 0 0 rgba(198,255,26,0.5);}
    70%{box-shadow:0 0 0 16px rgba(198,255,26,0);}
    100%{box-shadow:0 0 0 0 rgba(198,255,26,0);}
  }
  .ai-toggle svg{width:28px;height:28px;stroke:#0a0a0a;}
  .ai-panel{
    position:fixed;bottom:100px;right:26px;width:360px;max-width:90vw;
    background:var(--bg-raised);border:1px solid var(--line);border-radius:16px;
    z-index:400;box-shadow:0 20px 60px rgba(0,0,0,0.5);
    display:flex;flex-direction:column;height:480px;max-height:70vh;
    opacity:0;pointer-events:none;transform:translateY(20px);
    transition:all .25s ease;
  }
  .ai-panel.open{opacity:1;pointer-events:auto;transform:translateY(0);}
  .ai-head{
    padding:18px 20px;border-bottom:1px solid var(--line);
    display:flex;align-items:center;gap:12px;
  }
  .ai-avatar{
    width:36px;height:36px;border-radius:50%;
    background:linear-gradient(135deg, var(--volt), #7fbf00);
    display:flex;align-items:center;justify-content:center;flex-shrink:0;
  }
  .ai-avatar svg{width:18px;height:18px;stroke:#0a0a0a;}
  .ai-head-info b{font-size:14px;display:block;}
  .ai-head-info span{font-size:11px;color:var(--volt);display:flex;align-items:center;gap:5px;}
  .ai-head-info span::before{content:'';width:6px;height:6px;border-radius:50%;background:var(--volt);display:inline-block;}
  .ai-messages{flex-grow:1;overflow-y:auto;padding:18px 20px;display:flex;flex-direction:column;gap:12px;}
  .msg{max-width:82%;font-size:13px;line-height:1.5;padding:10px 14px;border-radius:12px;}
  .msg.bot{background:var(--bg-card);border:1px solid var(--line);align-self:flex-start;border-bottom-left-radius:2px;}
  .msg.user{background:var(--volt);color:#0a0a0a;font-weight:600;align-self:flex-end;border-bottom-right-radius:2px;}
  .ai-suggestions{display:flex;flex-wrap:wrap;gap:6px;padding:0 20px 14px;}
  .ai-chip{
    background:var(--bg-card);border:1px solid var(--line);color:var(--grey);
    font-size:11px;padding:7px 12px;border-radius:20px;cursor:pointer;
  }
  .ai-chip:hover{border-color:var(--volt);color:var(--volt);}
  .ai-input-row{display:flex;gap:8px;padding:14px 16px;border-top:1px solid var(--line);}
  .ai-input-row input{
    flex-grow:1;background:var(--bg-card);border:1px solid var(--line);color:var(--white);
    padding:11px 14px;border-radius:20px;font-size:13px;outline:none;
  }
  .ai-input-row input:focus{border-color:var(--volt);}
  .ai-send{
    background:var(--volt);border:none;color:#0a0a0a;width:38px;height:38px;border-radius:50%;
    cursor:pointer;display:flex;align-items:center;justify-content:center;flex-shrink:0;
  }
  .ai-send svg{width:16px;height:16px;}
</style>
</head>
<body>

<canvas id="smokeCanvas"></canvas>

<nav>
  <div class="nav-inner">
    <div class="brand">
      <svg viewBox="0 0 100 100" fill="none">
        <path d="M50 8 L18 42 L30 42 L14 92 L58 50 L44 50 L86 8 Z" fill="#c6ff1a"/>
      </svg>
      <div class="name display">VOLTE<span class="x">X</span></div>
    </div>
    <div class="nav-links">
      <a href="#hakkinda">Hakkında</a>
      <a href="#urunler">Ürünler</a>
      <a href="#besin">Besin Değerleri</a>
      <a href="#nerede">Nerede Bulunur</a>
    </div>
    <a class="nav-cta" href="#urunler">Lezzetleri Keşfet</a>
  </div>
</nav>

<section class="hero">
  <div class="eyebrow">VOLTEX ENERGY DRINK</div>
  <h1 class="display">Daha fazlası <span class="hi">senin enerjinde.</span></h1>
  <p class="hero-sub">12 farklı lezzet, tek bir formül felsefesi: odaklan, dayan, sınırlarını zorla. Voltex, gününü yönetmen için tasarlandı.</p>
  <div class="hero-actions">
    <button class="btn-primary" onclick="document.getElementById('urunler').scrollIntoView()">Ürünleri Keşfet</button>
    <button class="btn-ghost" onclick="document.getElementById('besin').scrollIntoView()">Besin Değerleri</button>
  </div>
  <div class="hero-image">
    <img src="images/hero_cans.png" alt="Voltex Energy Drink kutuları">
    <div class="hero-fade"></div>
  </div>
</section>

<div class="marquee">
  <div class="marquee-track">
    <span>•</span> DAHA FAZLA ENERJİ <span>•</span> DAHA İYİ ODAKLANMA <span>•</span> DAHA UZUN DAYANIKLILIK <span>•</span> SINIRLARINI ZORLA
    <span>•</span> DAHA FAZLA ENERJİ <span>•</span> DAHA İYİ ODAKLANMA <span>•</span> DAHA UZUN DAYANIKLILIK <span>•</span> SINIRLARINI ZORLA
  </div>
</div>

<section class="stats">
  <div class="stat"><span class="num">12</span><span class="lbl">FARKLI LEZZET</span></div>
  <div class="stat"><span class="num">500ml</span><span class="lbl">KUTU BOYUTU</span></div>
  <div class="stat"><span class="num">1</span><span class="lbl">ŞEKERSİZ SEÇENEK</span></div>
  <div class="stat"><span class="num">%100</span><span class="lbl">ENERJİ ODAKLI</span></div>
</section>

<section class="about" id="hakkinda">
  <div class="wrap about-grid">
    <div>
      <div class="eyebrow">MARKA HİKAYESİ</div>
      <h2 class="display">Enerji içeceğine <span class="hi">yeni bir bakış.</span></h2>
      <p>Voltex, günün her anında ihtiyaç duyduğun enerjiyi tek formda değil, on iki farklı karakterde sunar. Klasik enerji arayanlar için Classic, şeker almadan performans isteyenler için Zero Sugar, meyveli ve serinletici bir mola isteyenler için Watermelon Ice — her lezzet farklı bir anı için tasarlandı.</p>
      <p>Marka kimliğimizin merkezinde kurt figürü var: keskin, odaklı ve asla sınır tanımayan bir ruh.</p>
      <div class="about-list">
        <div class="about-item">
          <div class="ico"><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M13 2 3 14h7l-1 8 11-14h-7l0-6z"/></svg></div>
          <div><span class="t">Daha Fazla Enerji</span><div class="d">Uzun süreli, dengeli enerji desteği.</div></div>
        </div>
        <div class="about-item">
          <div class="ico"><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="9"/><circle cx="12" cy="12" r="4"/></svg></div>
          <div><span class="t">Daha İyi Odaklanma</span><div class="d">Zihinsel netlik gerektiren anlar için.</div></div>
        </div>
        <div class="about-item">
          <div class="ico"><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M13 4v16M6 8v8M20 8v8"/></svg></div>
          <div><span class="t">Daha Uzun Dayanıklılık</span><div class="d">Antrenmandan mesaiye, günün sonuna kadar.</div></div>
        </div>
      </div>
    </div>
    <div class="about-visual">
      <img src="images/can_mangoblast.png" alt="Voltex Mango Blast kutusu">
    </div>
  </div>
</section>

<section class="catalog" id="urunler">
  <div class="wrap">
    <div class="section-head">
      <div class="eyebrow">TÜM ÇEŞİTLERİMİZ</div>
      <h2 class="display">Bir kutu, <span style="color:var(--volt)">bin fırsat.</span></h2>
      <p>Her lezzet farklı bir ana eşlik etmek için tasarlandı. Detaylarına göz atmak için karta dokun.</p>
    </div>

    <div class="filters" id="filters">
      <button class="filter-btn active" data-filter="all">Tümü</button>
      <button class="filter-btn" data-filter="klasik">Klasik</button>
      <button class="filter-btn" data-filter="meyveli">Meyveli</button>
      <button class="filter-btn" data-filter="ozel">Özel</button>
    </div>

    <div class="product-grid" id="productGrid"></div>
  </div>
</section>

<section class="info" id="besin">
  <div class="wrap info-grid">
    <div>
      <div class="eyebrow">ÜRÜN BİLGİSİ</div>
      <h2 class="display">Kutunun <span class="hi">içindekiler.</span></h2>
      <p>Her Voltex kutusu 500 ml olarak üretilir ve kafein, taurin ve B grubu vitaminlerinin dengeli birleşiminden güç alır. Zero Sugar serisi dışındaki tüm çeşitler standart formülasyonu kullanır; Zero Sugar ise aynı enerji desteğini şeker eklemeden sunar.</p>
      <p>Tüm Voltex ürünleri günlük tüketim için değil, performansın veya odaklanmanın öncelikli olduğu anlar için tasarlanmıştır. Önerilen tüketim: günde 1 kutu, ihtiyaç halinde.</p>
      <p style="font-size:12px;color:var(--grey-dim);margin-top:26px;">*Değerler standart Voltex formülasyonu için genel bir örnektir, çeşide göre küçük farklılıklar gösterebilir.</p>
    </div>
    <div class="nutrition-table">
      <div class="head">100 ML İÇİN ORTALAMA DEĞERLER</div>
      <div class="row"><span class="k">Enerji</span><span class="v">45 kcal</span></div>
      <div class="row"><span class="k">Kafein</span><span class="v">32 mg</span></div>
      <div class="row"><span class="k">Taurin</span><span class="v">400 mg</span></div>
      <div class="row"><span class="k">Şeker</span><span class="v">11 g (Zero Sugar: 0 g)</span></div>
      <div class="row"><span class="k">Vitamin B3, B6, B12</span><span class="v">Günlük referansın %20'si</span></div>
      <div class="row"><span class="k">Ambalaj</span><span class="v">500 ml kutu</span></div>
    </div>
  </div>
</section>

<section class="buy" id="nerede">
  <div class="wrap">
    <h2 class="display">Nerede <span style="color:var(--volt)">bulabilirsin?</span></h2>
    <p>Voltex, Türkiye genelinde market zincirlerinde, bakkallarda ve online marketlerde raflarda yerini alıyor.</p>
    <div class="buy-channels">
      <div class="buy-channel"><b>Marketler</b>Tüm büyük zincir marketlerde</div>
      <div class="buy-channel"><b>Bakkal & Büfe</b>Mahalle noktalarında</div>
      <div class="buy-channel"><b>Online</b>Anlaşmalı e-ticaret platformlarında</div>
    </div>
  </div>
</section>

<section class="cta-final">
  <h2 class="display">Enerjini <span class="hi">şimdi keşfet.</span></h2>
  <p>ENERJİ SENİNLE — 12 LEZZET, TEK MARKA</p>
  <button class="btn-primary" onclick="document.getElementById('urunler').scrollIntoView()">Lezzetleri İncele</button>
</section>

<footer>
  <div class="footer-grid">
    <div class="footer-brand">
      <div class="display">VOLTE<span class="x">X</span></div>
      <p>Daha fazlası senin enerjinde. Voltex Energy Drink, sınırlarını zorlamak isteyenler için tasarlandı.</p>
    </div>
    <div class="footer-col">
      <h5>ÜRÜNLER</h5>
      <a href="#urunler">Tüm Lezzetler</a>
      <a href="#besin">Besin Değerleri</a>
    </div>
    <div class="footer-col">
      <h5>MARKA</h5>
      <a href="#hakkinda">Hakkımızda</a>
      <a href="#nerede">Nerede Bulunur</a>
    </div>
  </div>
  <div class="footer-bottom">VOLTEX ENERGY DRINK · TÜM HAKLARI SAKLIDIR</div>
</footer>

<!-- PRODUCT MODAL -->
<div class="modal-overlay" id="modalOverlay" onclick="closeModalOnOverlay(event)">
  <div class="modal" id="modal">
    <button class="modal-close" onclick="closeModal()">&times;</button>
    <div class="modal-visual"><img id="modalImg" src="" alt=""></div>
    <div class="modal-body">
      <div class="modal-name" id="modalName"></div>
      <div class="modal-tag" id="modalTag"></div>
      <div class="modal-desc" id="modalDesc"></div>
      <div class="modal-section">
        <h4>İÇERİK</h4>
        <div class="modal-ingredients" id="modalIngredients"></div>
      </div>
      <div class="modal-section">
        <h4>100 ML DEĞERLERİ</h4>
        <div class="modal-facts" id="modalFacts"></div>
      </div>
    </div>
  </div>
</div>

<!-- AI ASSISTANT -->
<button class="ai-toggle" onclick="toggleAI()">
  <svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="9" width="18" height="11" rx="2"/><circle cx="8.5" cy="14.5" r="1.5" fill="#0a0a0a"/><circle cx="15.5" cy="14.5" r="1.5" fill="#0a0a0a"/><path d="M12 9V5"/><circle cx="12" cy="3.5" r="1.5" fill="#0a0a0a"/></svg>
</button>
<div class="ai-panel" id="aiPanel">
  <div class="ai-head">
    <div class="ai-avatar"><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="9" width="18" height="11" rx="2"/><circle cx="8.5" cy="14.5" r="1.5" fill="#0a0a0a"/><circle cx="15.5" cy="14.5" r="1.5" fill="#0a0a0a"/><path d="M12 9V5"/><circle cx="12" cy="3.5" r="1.5" fill="#0a0a0a"/></svg></div>
    <div class="ai-head-info">
      <b>Voltex AI</b>
      <span>Çevrimiçi</span>
    </div>
  </div>
  <div class="ai-messages" id="aiMessages">
    <div class="msg bot">Merhaba! Ben Voltex AI 👋 Lezzetler, içerikler veya kutunun içindekiler hakkında sorularını yanıtlayabilirim.</div>
  </div>
  <div class="ai-suggestions" id="aiSuggestions">
    <div class="ai-chip" onclick="askAI('Şekersiz seçenek hangisi?')">Şekersiz seçenek?</div>
    <div class="ai-chip" onclick="askAI('En popüler lezzet hangisi?')">En popüler lezzet?</div>
    <div class="ai-chip" onclick="askAI('Kafein miktarı ne kadar?')">Kafein miktarı?</div>
  </div>
  <div class="ai-input-row">
    <input type="text" id="aiInput" placeholder="Bir şey sor..." onkeydown="if(event.key==='Enter')sendAI()">
    <button class="ai-send" onclick="sendAI()">
      <svg viewBox="0 0 24 24" fill="none" stroke="#0a0a0a" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="22" y1="2" x2="11" y2="13"/><polygon points="22 2 15 22 11 13 2 9 22 2"/></svg>
    </button>
  </div>
</div>

<script>
  /* ================= PRODUCTS ================= */
  const products = [
    { id:'classic', name:'Classic', tag:'KLASİK ENERJİ', desc:"Voltex'in imza tarifi — saf ve klasik enerji lezzeti. Uzun süreli konsantrasyon ve dayanıklılık için tasarlandı.", color:'#d4ff3d', img:'images/can_classic.png', cat:'klasik', badge:'EN ÇOK SATAN',
      ingredients:['Kafein','Taurin','B3 Vitamini','B6 Vitamini','B12 Vitamini','Karbonatlı Su'],
      facts:{Enerji:'45 kcal', Kafein:'32 mg', Taurin:'400 mg', Şeker:'11 g'} },
    { id:'bluerush', name:'Blue Rush', tag:'YABAN MERSİNİ', desc:'Yaban mersini ve frenk üzümü ile ferahlatıcı bir dalga. Zihinsel netlik isteyen anlar için ideal.', color:'#4e8fff', img:'images/can_bluerush.png', cat:'meyveli',
      ingredients:['Kafein','Taurin','Yaban Mersini Aroması','Frenk Üzümü Özütü','B Grubu Vitaminler'],
      facts:{Enerji:'44 kcal', Kafein:'32 mg', Taurin:'400 mg', Şeker:'10 g'} },
    { id:'strawberry', name:'Strawberry Wild', tag:'ÇİLEK & ORMAN MEYVESİ', desc:'Tatlı çilek notaları ve orman meyveleriyle dengelenmiş, dengeli bir enerji deneyimi.', color:'#ff5c6c', img:'images/can_strawberry.png', cat:'meyveli',
      ingredients:['Kafein','Taurin','Çilek Aroması','Orman Meyveleri Özütü','C Vitamini'],
      facts:{Enerji:'46 kcal', Kafein:'32 mg', Taurin:'400 mg', Şeker:'11 g'} },
    { id:'zerosugar', name:'Zero Sugar', tag:'ŞEKERSİZ', desc:'Aynı enerji desteğini şeker eklemeden sunan hafif formül. Kalori bilinciyle enerji arayanlar için.', color:'#e6e6e6', img:'images/can_zerosugar.png', cat:'ozel', badge:'ŞEKERSİZ',
      ingredients:['Kafein','Taurin','Tatlandırıcı (Sükraloz)','B Grubu Vitaminler','Karbonatlı Su'],
      facts:{Enerji:'3 kcal', Kafein:'32 mg', Taurin:'400 mg', Şeker:'0 g'} },
    { id:'purplestorm', name:'Purple Storm', tag:'MÜRDÜM ERİĞİ & BÖĞÜRTLEN', desc:'Yoğun ve karmaşık bir meyve profili, güçlü bir final ile enerji dolu bir deneyim.', color:'#b06bff', img:'images/can_purplestorm.png', cat:'meyveli',
      ingredients:['Kafein','Taurin','Mürdüm Eriği Özütü','Böğürtlen Aroması','B Grubu Vitaminler'],
      facts:{Enerji:'47 kcal', Kafein:'32 mg', Taurin:'400 mg', Şeker:'12 g'} },
    { id:'mangoblast', name:'Mango Blast', tag:'TROPİKAL ENERJİ', desc:'Mango ve tropikal meyvelerin güneşli birleşimi — yaz enerjisini kutuya sığdırdık.', color:'#ffab3d', img:'images/can_mangoblast.png', cat:'meyveli',
      ingredients:['Kafein','Taurin','Mango Özütü','Tropikal Meyve Aroması','B Grubu Vitaminler'],
      facts:{Enerji:'46 kcal', Kafein:'32 mg', Taurin:'400 mg', Şeker:'11 g'} },
    { id:'greenapple', name:'Green Apple', tag:'DOĞAL ENERJİ', desc:'Yeşil elma ve limonun canlandırıcı ekşiliğiyle güne taze bir başlangıç.', color:'#7bec4a', img:'images/can_greenapple.png', cat:'meyveli',
      ingredients:['Kafein','Taurin','Yeşil Elma Özütü','Limon Aroması','B Grubu Vitaminler'],
      facts:{Enerji:'45 kcal', Kafein:'32 mg', Taurin:'400 mg', Şeker:'10 g'} },
    { id:'watermelon', name:'Watermelon Ice', tag:'FERAH ENERJİ', desc:'Karpuz ve buzun serinletici, yaz esintili birlikteliği ile ferahlık dolu bir mola.', color:'#ff4d97', img:'images/can_watermelon.png', cat:'meyveli',
      ingredients:['Kafein','Taurin','Karpuz Özütü','Mentol Aroması','B Grubu Vitaminler'],
      facts:{Enerji:'44 kcal', Kafein:'32 mg', Taurin:'400 mg', Şeker:'10 g'} },
    { id:'tropical', name:'Tropical', tag:'ANANAS & HİNDİSTAN CEVİZİ', desc:'Egzotik bir tatil hissi veren tropikal karışım, gün boyu enerji desteğiyle birleşti.', color:'#3de0d0', img:'images/can_tropical.png', cat:'ozel',
      ingredients:['Kafein','Taurin','Ananas Özütü','Hindistan Cevizi Aroması','B Grubu Vitaminler'],
      facts:{Enerji:'47 kcal', Kafein:'32 mg', Taurin:'400 mg', Şeker:'12 g'} },
    { id:'cola', name:'Cola', tag:'KOLA LEZZETİ', desc:'Tanıdık kola lezzetiyle harmanlanmış klasik enerji desteği, nostaljik ama güçlü.', color:'#e35454', img:'images/can_cola.png', cat:'klasik',
      ingredients:['Kafein','Taurin','Kola Aroması','Karamel Rengi','B Grubu Vitaminler'],
      facts:{Enerji:'45 kcal', Kafein:'32 mg', Taurin:'400 mg', Şeker:'11 g'} },
    { id:'coffee', name:'Coffee', tag:'KAHVE & ENERJİ', desc:'Kahvenin yoğun aromasıyla güçlendirilmiş klasik tarif — sabahın alternatifi.', color:'#c69264', img:'images/can_coffee.png', cat:'ozel', badge:'YENİ',
      ingredients:['Kafein','Taurin','Kahve Özütü','B Grubu Vitaminler','Karbonatlı Su'],
      facts:{Enerji:'48 kcal', Kafein:'45 mg', Taurin:'400 mg', Şeker:'11 g'} },
    { id:'orange', name:'Orange', tag:'PORTAKAL & ENERJİ', desc:'Taze sıkılmış portakal hissi veren canlandırıcı lezzet, C vitamini desteğiyle.', color:'#ff9142', img:'images/can_orange.png', cat:'klasik',
      ingredients:['Kafein','Taurin','Portakal Özütü','C Vitamini','B Grubu Vitaminler'],
      facts:{Enerji:'45 kcal', Kafein:'32 mg', Taurin:'400 mg', Şeker:'11 g'} },
  ];

  function renderProducts(filter='all'){
    const grid = document.getElementById('productGrid');
    grid.innerHTML = '';
    products.filter(p => filter==='all' || p.cat===filter).forEach(p => {
      const card = document.createElement('div');
      card.className = 'product-card';
      card.onclick = () => openModal(p.id);
      card.innerHTML = `
        ${p.badge ? `<div class="product-badge">${p.badge}</div>` : ''}
        <div class="product-img"><img src="${p.img}" alt="Voltex ${p.name}"></div>
        <div class="product-name">${p.name}</div>
        <div class="product-tag" style="--tag-color:${p.color}">${p.tag}</div>
        <div class="product-desc">${p.desc}</div>
        <div class="product-footer">
          <button class="detail-btn">Detayları Gör</button>
        </div>`;
      grid.appendChild(card);
    });
  }

  function openModal(id){
    const p = products.find(x => x.id === id);
    document.getElementById('modalImg').src = p.img;
    document.getElementById('modalImg').alt = p.name;
    document.getElementById('modalName').textContent = p.name;
    const tagEl = document.getElementById('modalTag');
    tagEl.textContent = p.tag;
    tagEl.style.setProperty('--modal-color', p.color);
    document.getElementById('modalDesc').textContent = p.desc;
    document.getElementById('modalIngredients').innerHTML = p.ingredients.map(i => `<span>${i}</span>`).join('');
    document.getElementById('modalFacts').innerHTML = Object.entries(p.facts).map(([k,v]) => `<div class="row"><span>${k}</span><span>${v}</span></div>`).join('');
    document.getElementById('modalOverlay').classList.add('open');
  }
  function closeModal(){ document.getElementById('modalOverlay').classList.remove('open'); }
  function closeModalOnOverlay(e){ if(e.target.id === 'modalOverlay') closeModal(); }

  document.getElementById('filters').addEventListener('click', e => {
    if(e.target.classList.contains('filter-btn')){
      document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
      e.target.classList.add('active');
      renderProducts(e.target.dataset.filter);
    }
  });
  renderProducts();

  /* ================= AI ASSISTANT ================= */
  function toggleAI(){ document.getElementById('aiPanel').classList.toggle('open'); }

  const aiResponses = [
    { keys:['şekersiz','zero','şeker'], reply:'Zero Sugar, sıfır şekerle aynı enerji desteğini sunan tek çeşidimiz. Kafein ve taurin oranı diğer çeşitlerle birebir aynı.' },
    { keys:['popüler','en çok','favori'], reply:'En çok tercih edilen lezzetimiz Classic — Voltex\'in imza tarifi. Yeni çıkan Coffee de hızla yükseliyor!' },
    { keys:['kafein'], reply:'Standart çeşitlerde 100 ml\'de 32 mg kafein bulunur. Coffee çeşidinde bu oran 45 mg\'a çıkar.' },
    { keys:['fiyat','ücret','kaç para'], reply:'Fiyat bilgisi için en yakın market veya online satış noktalarımızı ziyaret edebilirsin — bu site ürünleri tanıtmak için hazırlandı.' },
    { keys:['nerede','satın','market'], reply:'Voltex\'i büyük market zincirlerinde, bakkallarda ve anlaşmalı online platformlarda bulabilirsin.' },
    { keys:['lezzet','çeşit','kaç tane'], reply:'Şu anda 12 farklı Voltex lezzeti var: Classic, Blue Rush, Strawberry Wild, Zero Sugar, Purple Storm, Mango Blast, Green Apple, Watermelon Ice, Tropical, Cola, Coffee ve Orange.' },
    { keys:['taurin'], reply:'Her Voltex kutusunda 100 ml başına 400 mg taurin bulunur — dayanıklılık ve odaklanmayı desteklemek için.' },
    { keys:['vitamin'], reply:'Voltex, B3, B6 ve B12 vitaminleriyle güçlendirilmiştir; günlük referans alımın yaklaşık %20\'sini karşılar.' },
  ];

  function askAI(text){
    document.getElementById('aiInput').value = text;
    sendAI();
  }

  function sendAI(){
    const input = document.getElementById('aiInput');
    const text = input.value.trim();
    if(!text) return;
    const messages = document.getElementById('aiMessages');

    const userMsg = document.createElement('div');
    userMsg.className = 'msg user';
    userMsg.textContent = text;
    messages.appendChild(userMsg);
    input.value = '';
    messages.scrollTop = messages.scrollHeight;

    setTimeout(() => {
      const lower = text.toLowerCase();
      let reply = 'Bu konuda net bir bilgim yok ama sana en yakın Voltex satış noktasını veya "Ürünler" bölümündeki detay kartlarını incelemeni öneririm. Başka bir sorun var mı?';
      for(const r of aiResponses){
        if(r.keys.some(k => lower.includes(k))){ reply = r.reply; break; }
      }
      const botMsg = document.createElement('div');
      botMsg.className = 'msg bot';
      botMsg.textContent = reply;
      messages.appendChild(botMsg);
      messages.scrollTop = messages.scrollHeight;
    }, 500);
  }

  /* ================= SMOKE / PARTICLE EFFECT ================= */
  const canvas = document.getElementById('smokeCanvas');
  const ctx = canvas.getContext('2d');
  let particles = [];

  function resizeCanvas(){
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  }
  resizeCanvas();
  window.addEventListener('resize', resizeCanvas);

  class Smoke{
    constructor(x,y){
      this.x = x; this.y = y;
      this.size = Math.random()*22 + 14;
      this.speedX = (Math.random()-0.5)*1.2;
      this.speedY = -(Math.random()*1.4 + 0.6);
      this.life = 1;
      this.decay = Math.random()*0.012 + 0.012;
      const hueChoice = Math.random();
      this.color = hueChoice > 0.5 ? '198,255,26' : '255,255,255';
    }
    update(){
      this.x += this.speedX;
      this.y += this.speedY;
      this.size += 0.4;
      this.life -= this.decay;
    }
    draw(){
      ctx.beginPath();
      ctx.arc(this.x, this.y, this.size, 0, Math.PI*2);
      ctx.fillStyle = `rgba(${this.color},${Math.max(this.life*0.35,0)})`;
      ctx.filter = 'blur(6px)';
      ctx.fill();
      ctx.filter = 'none';
    }
  }

  function spawnSmoke(x,y){
    for(let i=0;i<10;i++){
      particles.push(new Smoke(x + (Math.random()-0.5)*10, y + (Math.random()-0.5)*10));
    }
  }

  function animate(){
    ctx.clearRect(0,0,canvas.width,canvas.height);
    particles.forEach(p => { p.update(); p.draw(); });
    particles = particles.filter(p => p.life > 0);
    requestAnimationFrame(animate);
  }
  animate();

  window.addEventListener('pointerdown', e => spawnSmoke(e.clientX, e.clientY));
  window.addEventListener('touchstart', e => {
    for(const t of e.touches) spawnSmoke(t.clientX, t.clientY);
  }, {passive:true});
</script>

</body>
</html>
