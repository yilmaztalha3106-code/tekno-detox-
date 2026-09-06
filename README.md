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
  .modal-tag{font-size:11px;letter-spacing:2
