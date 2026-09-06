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

  /* ---------- NAV ---------- */
  nav{
    position:sticky;top:0;z-index:200;
    background:rgba(8,9,10,0.82);
    backdrop-filter:blur(14px);
    -webkit-backdrop-filter:blur(14px);
    border-bottom:1px solid var(--line);
  }
  .nav-inner{
    max-width:1220px;margin:0 auto;padding:18px 32px;
    display:flex;align-items:center;justify-content:space-between;
  }
  .nav-logo{font-size:21px;display:flex;align-items:center;gap:8px;}
  .nav-logo .x{color:var(--volt);}
  .nav-links{display:flex;gap:36px;font-size:13.5px;color:var(--grey);}
  .nav-links a{transition:color .15s ease;}
  .nav-links a:hover{color:var(--white);}
  .nav-right{display:flex;align-items:center;gap:20px;}
  .cart-btn{
    position:relative;
    display:flex;align-items:center;gap:8px;
    background:var(--bg-raised);
    border:1px solid var(--line);
    padding:10px 16px;
    border-radius:30px;
    font-size:13px;
    cursor:pointer;
  }
  .cart-btn svg{width:16px;height:16px;stroke:var(--white);}
  .cart-count{
    background:var(--volt);
    color:#0a0a0a;
    font-size:11px;
    font-weight:800;
    min-width:18px;height:18px;
    border-radius:50%;
    display:flex;align-items:center;justify-content:center;
    padding:0 4px;
  }
  @media(max-width:820px){ .nav-links{display:none;} }

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
  }
  .product-card:hover{transform:translateY(-4px);border-color:#333;}
  .product-badge{
    position:absolute;top:16px;left:16px;
    background:rgba(198,255,26,0.12);
    color:var(--volt);
    font-size:10px;font-weight:800;letter-spacing:1px;
    padding:5px 10px;border-radius:20px;
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
  .product-price{font-size:17px;font-weight:800;}
  .product-price small{font-size:11px;color:var(--grey);font-weight:400;}
  .add-btn{
    background:var(--bg-raised);
    border:1px solid var(--line);
    color:var(--white);
    width:38px;height:38px;
    border-radius:8px;
    font-size:18px;
    cursor:pointer;
    transition:all .15s ease;
    display:flex;align-items:center;justify-content:center;
  }
  .add-btn:hover{background:var(--volt);color:#0a0a0a;border-color:var(--volt);}
  @media(max-width:980px){ .product-grid{grid-template-columns:repeat(2,1fr);} }
  @media(max-width:520px){ .product-grid{grid-template-columns:1fr;} }

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

  /* ---------- CART DRAWER ---------- */
  .overlay{
    position:fixed;inset:0;background:rgba(0,0,0,0.6);
    z-index:300;opacity:0;pointer-events:none;transition:opacity .25s ease;
  }
  .overlay.open{opacity:1;pointer-events:auto;}
  .cart-drawer{
    position:fixed;top:0;right:-420px;width:400px;max-width:90vw;height:100%;
    background:var(--bg-raised);border-left:1px solid var(--line);
    z-index:301;transition:right .3s ease;
    display:flex;flex-direction:column;
  }
  .cart-drawer.open{right:0;}
  .cart-head{
    padding:24px;border-bottom:1px solid var(--line);
    display:flex;justify-content:space-between;align-items:center;
  }
  .cart-head h3{font-size:17px;}
  .cart-close{background:none;border:none;color:var(--grey);font-size:22px;cursor:pointer;}
  .cart-items{flex-grow:1;overflow-y:auto;padding:16px 24px;}
  .cart-empty{color:var(--grey);font-size:13.5px;text-align:center;margin-top:60px;}
  .cart-item{display:flex;gap:14px;padding:16px 0;border-bottom:1px solid var(--line);align-items:center;}
  .cart-item img{width:44px;height:70px;object-fit:contain;}
  .cart-item-info{flex-grow:1;}
  .cart-item-name{font-size:13.5px;font-weight:700;}
  .cart-item-price{font-size:12px;color:var(--grey);margin-top:2px;}
  .qty-control{display:flex;align-items:center;gap:10px;margin-top:8px;}
  .qty-control button{
    width:22px;height:22px;border-radius:5px;border:1px solid var(--line);
    background:var(--bg-card);color:var(--white);cursor:pointer;font-size:13px;
  }
  .qty-control span{font-size:12.5px;min-width:14px;text-align:center;}
  .cart-remove{background:none;border:none;color:var(--grey-dim);font-size:11px;cursor:pointer;margin-top:8px;text-decoration:underline;}
  .cart-foot{padding:22px 24px;border-top:1px solid var(--line);}
  .cart-total-row{display:flex;justify-content:space-between;font-size:14.5px;margin-bottom:16px;}
  .cart-total-row b{font-size:19px;color:var(--volt);}
  .checkout-btn{
    width:100%;background:var(--volt);color:#0a0a0a;border:none;
    padding:16px;border-radius:8px;font-weight:800;font-size:14px;cursor:pointer;
  }

  .toast{
    position:fixed;bottom:26px;left:50%;transform:translateX(-50%) translateY(20px);
    background:var(--volt);color:#0a0a0a;font-weight:700;font-size:13px;
    padding:14px 26px;border-radius:30px;z-index:400;
    opacity:0;transition:all .3s ease;pointer-events:none;
  }
  .toast.show{opacity:1;transform:translateX(-50%) translateY(0);}
</style>
</head>
<body>

<nav>
  <div class="nav-inner">
    <div class="nav-logo display">VOLTE<span class="x">X</span></div>
    <div class="nav-links">
      <a href="#hakkinda">Hakkında</a>
      <a href="#urunler">Ürünler</a>
      <a href="#besin">Besin Değerleri</a>
      <a href="#nerede">Nerede Bulunur</a>
    </div>
    <div class="nav-right">
      <button class="cart-btn" onclick="toggleCart(true)">
        <svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="9" cy="21" r="1"/><circle cx="20" cy="21" r="1"/><path d="M1 1h4l2.68 13.39a2 2 0 0 0 2 1.61h9.72a2 2 0 0 0 2-1.61L23 6H6"/></svg>
        <span>Sepet</span>
        <span class="cart-count" id="cartCount">0</span>
      </button>
    </div>
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
      <p>Her lezzet farklı bir ana eşlik etmek için tasarlandı. Sana uygun olanı seç, sepete ekle.</p>
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
      <div class="buy-channel"><b>Online</b>Bu sitede sepete ekleyerek</div>
    </div>
  </div>
</section>

<section class="cta-final">
  <h2 class="display">Enerjini <span class="hi">şimdi keşfet.</span></h2>
  <p>ENERJİ SENİNLE — 12 LEZZET, TEK MARKA</p>
  <button class="btn-primary" onclick="document.getElementById('urunler').scrollIntoView()">Ürünleri İncele</button>
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

<div class="overlay" id="overlay" onclick="toggleCart(false)"></div>
<div class="cart-drawer" id="cartDrawer">
  <div class="cart-head">
    <h3>Sepetim</h3>
    <button class="cart-close" onclick="toggleCart(false)">&times;</button>
  </div>
  <div class="cart-items" id="cartItems"></div>
  <div class="cart-foot">
    <div class="cart-total-row"><span>Toplam</span><b id="cartTotal">0,00 ₺</b></div>
    <button class="checkout-btn" onclick="checkout()">Siparişi Tamamla</button>
  </div>
</div>

<div class="toast" id="toast">Sepete eklendi</div>

<script>
  const products = [
    { id:'classic', name:'Classic', tag:'KLASİK ENERJİ', desc:"Voltex'in imza tarifi — saf ve klasik enerji lezzeti.", price:44.90, color:'#d4ff3d', img:'images/can_classic.png', cat:'klasik', badge:'EN ÇOK SATAN' },
    { id:'bluerush', name:'Blue Rush', tag:'YABAN MERSİNİ', desc:'Yaban mersini ve frenk üzümü ile ferahlatıcı bir dalga.', price:46.90, color:'#4e8fff', img:'images/can_bluerush.png', cat:'meyveli' },
    { id:'strawberry', name:'Strawberry Wild', tag:'ÇİLEK & ORMAN MEYVESİ', desc:'Tatlı çilek notaları ve orman meyveleriyle dengelenmiş lezzet.', price:46.90, color:'#ff5c6c', img:'images/can_strawberry.png', cat:'meyveli' },
    { id:'zerosugar', name:'Zero Sugar', tag:'ŞEKERSİZ', desc:'Aynı enerji, sıfır şeker. Klasik lezzetin hafif versiyonu.', price:44.90, color:'#e6e6e6', img:'images/can_zerosugar.png', cat:'ozel', badge:'ŞEKERSİZ' },
    { id:'purplestorm', name:'Purple Storm', tag:'MÜRDÜM ERİĞİ & BÖĞÜRTLEN', desc:'Yoğun ve karmaşık bir meyve profili, güçlü bir final.', price:47.90, color:'#b06bff', img:'images/can_purplestorm.png', cat:'meyveli' },
    { id:'mangoblast', name:'Mango Blast', tag:'TROPİKAL ENERJİ', desc:'Mango ve tropikal meyvelerin güneşli birleşimi.', price:46.90, color:'#ffab3d', img:'images/can_mangoblast.png', cat:'meyveli' },
    { id:'greenapple', name:'Green Apple', tag:'DOĞAL ENERJİ', desc:'Yeşil elma ve limonun canlandırıcı ekşiliği.', price:45.90, color:'#7bec4a', img:'images/can_greenapple.png', cat:'meyveli' },
    { id:'watermelon', name:'Watermelon Ice', tag:'FERAH ENERJİ', desc:'Karpuz ve buzun serinletici, yaz esintili birlikteliği.', price:46.90, color:'#ff4d97', img:'images/can_watermelon.png', cat:'meyveli' },
    { id:'tropical', name:'Tropical', tag:'ANANAS & HİNDİSTAN CEVİZİ', desc:'Egzotik bir tatil hissi veren tropikal karışım.', price:47.90, color:'#3de0d0', img:'images/can_tropical.png', cat:'ozel' },
    { id:'cola', name:'Cola', tag:'KOLA LEZZETİ', desc:'Tanıdık kola lezzetiyle harmanlanmış enerji desteği.', price:45.90, color:'#e35454', img:'images/can_cola.png', cat:'klasik' },
    { id:'coffee', name:'Coffee', tag:'KAHVE & ENERJİ', desc:'Kahvenin yoğun aromasıyla güçlendirilmiş klasik tarif.', price:48.90, color:'#c69264', img:'images/can_coffee.png', cat:'ozel', badge:'YENİ' },
    { id:'orange', name:'Orange', tag:'PORTAKAL & ENERJİ', desc:'Taze sıkılmış portakal hissi veren canlandırıcı lezzet.', price:45.90, color:'#ff9142', img:'images/can_orange.png', cat:'klasik' },
  ];

  let cart = {};

  function renderProducts(filter='all'){
    const grid = document.getElementById('productGrid');
    grid.innerHTML = '';
    products.filter(p => filter==='all' || p.cat===filter).forEach(p => {
      const card = document.createElement('div');
      card.className = 'product-card';
      card.innerHTML = `
        ${p.badge ? `<div class="product-badge">${p.badge}</div>` : ''}
        <div class="product-img"><img src="${p.img}" alt="Voltex ${p.name}"></div>
        <div class="product-name">${p.name}</div>
        <div class="product-tag" style="--tag-color:${p.color}">${p.tag}</div>
        <div class="product-desc">${p.desc}</div>
        <div class="product-footer">
          <div class="product-price">${p.price.toFixed(2).replace('.',',')} ₺<br><small>500 ml</small></div>
          <button class="add-btn" onclick="addToCart('${p.id}')">+</button>
        </div>`;
      grid.appendChild(card);
    });
  }

  function addToCart(id){
    cart[id] = (cart[id] || 0) + 1;
    updateCartUI();
    showToast('Sepete eklendi');
  }
  function changeQty(id, delta){
    if(!cart[id]) return;
    cart[id] += delta;
    if(cart[id] <= 0) delete cart[id];
    updateCartUI();
  }
  function removeFromCart(id){
    delete cart[id];
    updateCartUI();
  }

  function updateCartUI(){
    const itemsEl = document.getElementById('cartItems');
    const countEl = document.getElementById('cartCount');
    const totalEl = document.getElementById('cartTotal');
    const ids = Object.keys(cart);
    let totalCount = 0, totalPrice = 0;

    if(ids.length === 0){
      itemsEl.innerHTML = '<div class="cart-empty">Sepetin şu an boş.<br>Bir lezzet seç ve enerjini keşfet.</div>';
    } else {
      itemsEl.innerHTML = ids.map(id => {
        const p = products.find(x => x.id === id);
        const qty = cart[id];
        totalCount += qty;
        totalPrice += qty * p.price;
        return `
          <div class="cart-item">
            <img src="${p.img}" alt="${p.name}">
            <div class="cart-item-info">
              <div class="cart-item-name">${p.name}</div>
              <div class="cart-item-price">${p.price.toFixed(2).replace('.',',')} ₺ / adet</div>
              <div class="qty-control">
                <button onclick="changeQty('${id}',-1)">-</button>
                <span>${qty}</span>
                <button onclick="changeQty('${id}',1)">+</button>
              </div>
              <button class="cart-remove" onclick="removeFromCart('${id}')">Kaldır</button>
            </div>
          </div>`;
      }).join('');
    }
    countEl.textContent = totalCount;
    totalEl.textContent = totalPrice.toFixed(2).replace('.',',') + ' ₺';
  }

  function toggleCart(open){
    document.getElementById('cartDrawer').classList.toggle('open', open);
    document.getElementById('overlay').classList.toggle('open', open);
  }

  function showToast(msg){
    const t = document.getElementById('toast');
    t.textContent = msg;
    t.classList.add('show');
    setTimeout(() => t.classList.remove('show'), 1800);
  }

  function checkout(){
    if(Object.keys(cart).length === 0){
      showToast('Sepetin boş');
      return;
    }
    showToast('Siparişin alındı, teşekkürler!');
    cart = {};
    updateCartUI();
    setTimeout(() => toggleCart(false), 900);
  }

  document.getElementById('filters').addEventListener('click', e => {
    if(e.target.classList.contains('filter-btn')){
      document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
      e.target.classList.add('active');
      renderProducts(e.target.dataset.filter);
    }
  });

  renderProducts();
  updateCartUI();
</script>

</body>
</html>
