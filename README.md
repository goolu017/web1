<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Akash General Store</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,500;9..144,600;9..144,700&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root{
    --ink:#22261f;
    --sand:#efe6d1;
    --paper:#fbf7ee;
    --mustard:#c78a2e;
    --rust:#9c4a2f;
    --olive:#4c5a3f;
    --line: rgba(34,38,31,0.14);
    --radius: 4px;
  }

  *{ box-sizing:border-box; }
  html{ scroll-behavior:smooth; }
  body{
    margin:0;
    background:var(--paper);
    color:var(--ink);
    font-family:'Inter', sans-serif;
    line-height:1.5;
    -webkit-font-smoothing:antialiased;
  }
  h1,h2,h3{
    font-family:'Fraunces', serif;
    margin:0;
    color:var(--ink);
  }
  a{ color:inherit; }
  img{ max-width:100%; display:block; }
  button{ font-family:inherit; cursor:pointer; }

  @media (prefers-reduced-motion: reduce){
    html{ scroll-behavior:auto; }
    *{ animation-duration:0.01ms !important; animation-iteration-count:1 !important; scroll-behavior:auto !important; }
  }

  /* ---------- Top bar ---------- */
  .topbar{
    position:fixed; top:0; left:0; right:0; z-index:50;
    display:flex; align-items:center; justify-content:space-between;
    padding:18px 5%;
    background: linear-gradient(to bottom, rgba(0,0,0,0.45), rgba(0,0,0,0));
    color:#fff;
  }
  .topbar .brand{
    font-family:'Fraunces', serif;
    font-weight:600;
    font-size:1.25rem;
    letter-spacing:0.01em;
  }
  .topbar nav a{
    text-decoration:none;
    color:#fff;
    font-size:0.92rem;
    margin-left:26px;
    opacity:0.9;
    border-bottom:1px solid transparent;
    padding-bottom:2px;
    transition:border-color 0.2s ease;
  }
  .topbar nav a:hover{ border-color:#fff; }
  .topbar nav{ display:flex; }
  @media (max-width:640px){
    .topbar nav a:not(.nav-primary){ display:none; }
  }

  /* ---------- Hero ---------- */
  .hero{
    position:relative;
    width:100%;
    min-height:100vh;
    display:flex;
    align-items:flex-end;
    background: #1c1c18 url('hero.jpg') center 30% / cover no-repeat;
  }
  .hero::after{
    content:"";
    position:absolute; inset:0;
    background: linear-gradient(to top, rgba(15,14,10,0.88) 5%, rgba(15,14,10,0.35) 55%, rgba(15,14,10,0.15) 100%);
  }
  .hero-content{
    position:relative;
    z-index:2;
    width:100%;
    padding: 0 5% 9vh;
    color:#fbf7ee;
  }
  .hero-eyebrow{
    color: #e3c98f;
    font-size:0.95rem;
    letter-spacing:0.04em;
    margin-bottom:14px;
  }
  .hero h1{
    font-size: clamp(2.6rem, 7vw, 5.6rem);
    font-weight:600;
    line-height:0.98;
    max-width:16ch;
    margin-bottom:22px;
  }
  .hero p{
    font-size:1.15rem;
    max-width:46ch;
    color:#e9e2cf;
    margin-bottom:34px;
  }
  .btn{
    display:inline-flex;
    align-items:center;
    gap:10px;
    padding:15px 30px;
    background:var(--mustard);
    color:#20200f;
    border:none;
    border-radius:var(--radius);
    font-size:1rem;
    font-weight:600;
    text-decoration:none;
    transition: transform 0.18s ease, background 0.18s ease;
  }
  .btn:hover{ background:#dba143; transform:translateY(-2px); }
  .btn-outline{
    background:transparent;
    border:1.5px solid var(--ink);
    color:var(--ink);
  }
  .btn-outline:hover{ background:var(--ink); color:var(--paper); transform:translateY(-2px); }

  /* ---------- Section shell ---------- */
  section{ padding: 90px 5%; }
  .section-head{
    display:flex;
    justify-content:space-between;
    align-items:flex-end;
    gap:24px;
    margin-bottom:44px;
    flex-wrap:wrap;
  }
  .section-head h2{
    font-size: clamp(1.8rem, 3.4vw, 2.6rem);
    font-weight:600;
    max-width:14ch;
  }
  .section-head p{ max-width:38ch; color:#5c5748; }

  /* ---------- Carousel ---------- */
  .carousel-wrap{
    position:relative;
    background:var(--sand);
  }
  .carousel{
    display:flex;
    gap:22px;
    overflow-x:auto;
    scroll-snap-type:x mandatory;
    padding-bottom:10px;
    scrollbar-width:none;
  }
  .carousel::-webkit-scrollbar{ display:none; }
  .card{
    flex:0 0 auto;
    width:min(320px, 78vw);
    scroll-snap-align:start;
    background:var(--paper);
    border:1px solid var(--line);
    border-radius:var(--radius);
    overflow:hidden;
  }
  .card .card-img{
    width:100%;
    aspect-ratio: 4/3;
    object-fit:cover;
    background:#ddd3b8;
  }
  .card-body{ padding:20px; }
  .card-body h3{ font-size:1.15rem; font-weight:600; margin-bottom:6px; }
  .card-body .price{ color:var(--rust); font-weight:600; margin-bottom:12px; }
  .card-body p{ color:#5c5748; font-size:0.92rem; margin-bottom:16px; }
  .card-body .btn{ padding:10px 18px; font-size:0.9rem; width:100%; justify-content:center; }

  .carousel-controls{
    display:flex; gap:10px; margin-top:22px;
  }
  .carousel-controls button{
    width:42px; height:42px;
    border-radius:50%;
    border:1.5px solid var(--ink);
    background:transparent;
    display:flex; align-items:center; justify-content:center;
    color:var(--ink);
    transition: background 0.18s ease, color 0.18s ease;
  }
  .carousel-controls button:hover{ background:var(--ink); color:var(--paper); }

  /* ---------- About strip ---------- */
  .about{
    display:grid;
    grid-template-columns: 1fr 1fr;
    gap:60px;
    align-items:center;
  }
  .about .tag{
    color:var(--rust);
    font-weight:600;
    margin-bottom:12px;
  }
  .about h2{ font-size:clamp(1.8rem,3vw,2.4rem); margin-bottom:18px; max-width:16ch; }
  .about p{ color:#5c5748; max-width:52ch; margin-bottom:16px; }
  .about-figures{ display:flex; gap:36px; margin-top:28px; }
  .about-figures div strong{ display:block; font-family:'Fraunces',serif; font-size:2rem; color:var(--ink); }
  .about-figures div span{ font-size:0.85rem; color:#6c6656; }
  @media (max-width:820px){ .about{ grid-template-columns:1fr; } }

  /* ---------- Order form ---------- */
  .order{
    background:var(--ink);
    color:var(--paper);
  }
  .order .section-head h2{ color:var(--paper); }
  .order .section-head p{ color:#c9c4b4; }
  .order-grid{
    display:grid;
    grid-template-columns: 1.1fr 0.9fr;
    gap:50px;
  }
  @media (max-width:860px){ .order-grid{ grid-template-columns:1fr; } }

  form{
    background:var(--paper);
    color:var(--ink);
    border-radius:6px;
    padding:34px;
  }
  .field{ margin-bottom:20px; }
  .field label{
    display:block;
    font-size:0.85rem;
    font-weight:600;
    margin-bottom:7px;
    color:#3a3527;
  }
  .row-2{ display:grid; grid-template-columns:1fr 1fr; gap:16px; }
  .field input,
  .field select,
  .field textarea{
    width:100%;
    padding:12px 14px;
    border:1.5px solid var(--line);
    border-radius:var(--radius);
    background:#fff;
    font-family:inherit;
    font-size:0.95rem;
    color:var(--ink);
  }
  .field input:focus,
  .field select:focus,
  .field textarea:focus{
    outline:2px solid var(--mustard);
    outline-offset:1px;
    border-color:var(--mustard);
  }
  .field textarea{ resize:vertical; min-height:90px; }
  form .btn{ width:100%; justify-content:center; margin-top:6px; }

  .order-note{ padding-top:10px; }
  .order-note h3{ color:var(--paper); font-size:1.3rem; margin-bottom:14px; }
  .order-note p{ color:#c9c4b4; margin-bottom:22px; }
  .order-note ul{ list-style:none; padding:0; margin:0 0 26px; }
  .order-note li{
    display:flex; gap:12px;
    padding:14px 0;
    border-top:1px solid rgba(251,247,238,0.15);
    color:#e9e2cf;
    font-size:0.95rem;
  }
  .order-note li:last-child{ border-bottom:1px solid rgba(251,247,238,0.15); }
  .order-note li b{ color:var(--mustard); font-family:'Fraunces',serif; font-weight:600; }

  #confirm-msg{
    display:none;
    margin-top:16px;
    padding:14px 16px;
    background:#e7f1e2;
    border:1px solid #9db98d;
    border-radius:var(--radius);
    color:#2c4322;
    font-size:0.92rem;
  }
  #confirm-msg.show{ display:block; }

  /* ---------- Footer ---------- */
  footer{
    background:#171a13;
    color:#c9c4b4;
    padding:56px 5% 30px;
  }
  .footer-top{
    display:flex;
    justify-content:space-between;
    gap:30px;
    flex-wrap:wrap;
    padding-bottom:34px;
    border-bottom:1px solid rgba(251,247,238,0.12);
    margin-bottom:24px;
  }
  .footer-top h3{ color:var(--paper); font-size:1.4rem; margin-bottom:10px; }
  .footer-top .fcol p{ margin:0 0 6px; font-size:0.92rem; }
  .footer-top .fcol a{ text-decoration:none; color:#e9e2cf; }
  .footer-bottom{ font-size:0.82rem; color:#8b8672; }
</style>
</head>
<body>

  <div class="topbar">
    <div class="brand">Akash General Store</div>
    <nav>
      <a href="#products">Products</a>
      <a href="#about">About</a>
      <a href="#order" class="nav-primary">Order</a>
    </nav>
  </div>

  <!-- HERO -->
  <header class="hero" id="top">
    <div class="hero-content">
      <div class="hero-eyebrow">Your neighbourhood store, since day one</div>
      <h1>Akash General Store</h1>
      <p>Everyday groceries, household essentials and a friendly face behind the counter — run by Akash Singh, for the whole neighbourhood.</p>
      <a href="#products" class="btn" id="shopNowBtn">Shop Now
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M12 5v14M5 12l7 7 7-7"/></svg>
      </a>
    </div>
  </header>

  <!-- CAROUSEL / PRODUCTS -->
  <section class="carousel-wrap" id="products">
    <div class="section-head">
      <h2>What's on the shelf today</h2>
      <p>A quick look at what's stocked and moving fast this week. Scroll through, or let it play on its own.</p>
    </div>

    <div class="carousel" id="carousel">
      <!-- cards are injected by JS from the productData list -->
    </div>

    <div class="carousel-controls">
      <button id="prevBtn" aria-label="Previous">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.3"><path d="M15 18l-6-6 6-6"/></svg>
      </button>
      <button id="nextBtn" aria-label="Next">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.3"><path d="M9 18l6-6-6-6"/></svg>
      </button>
    </div>
  </section>

  <!-- ABOUT -->
  <section class="about" id="about">
    <div>
      <div class="tag">Run by hand, not by chain</div>
      <h2>Owned and run by Akash Singh</h2>
      <p>Akash General Store has been the go-to stop for daily essentials — groceries, snacks, household basics and everything in between. No queues, no fuss, just what you need, restocked every day.</p>
      <p>Have a question about stock or a special request? Reach out directly — Akash reads every message himself.</p>
      <div class="about-figures">
        <div><strong>7</strong><span>Days open a week</span></div>
        <div><strong>100+</strong><span>Everyday items stocked</span></div>
        <div><strong>1:1</strong><span>Direct owner support</span></div>
      </div>
    </div>
    <div>
      <img src="hero.jpg" alt="Inside Akash General Store" style="border-radius:6px; width:100%; height:100%; object-fit:cover; max-height:460px;">
    </div>
  </section>

  <!-- ORDER FORM -->
  <section class="order" id="order">
    <div class="section-head">
      <h2>Place an order</h2>
      <p>Pick an item from today's shelf and send the details straight to Akash — he'll confirm and get it ready.</p>
    </div>

    <div class="order-grid">
      <form id="orderForm">
        <div class="row-2">
          <div class="field">
            <label for="name">Full name</label>
            <input type="text" id="name" name="name" placeholder="Your name" required>
          </div>
          <div class="field">
            <label for="phone">Phone number</label>
            <input type="tel" id="phone" name="phone" placeholder="10-digit mobile number" required>
          </div>
        </div>

        <div class="field">
          <label for="email">Email</label>
          <input type="email" id="email" name="email" placeholder="you@example.com">
        </div>

        <div class="row-2">
          <div class="field">
            <label for="product">Item</label>
            <select id="product" name="product" required>
              <option value="" disabled selected>Choose an item</option>
            </select>
          </div>
          <div class="field">
            <label for="qty">Quantity</label>
            <input type="number" id="qty" name="qty" min="1" value="1" required>
          </div>
        </div>

        <div class="field">
          <label for="address">Delivery / pickup address</label>
          <textarea id="address" name="address" placeholder="House no., street, area, landmark" required></textarea>
        </div>

        <div class="field">
          <label for="note">Note (optional)</label>
          <textarea id="note" name="note" placeholder="Anything else Akash should know"></textarea>
        </div>

        <button type="submit" class="btn">Place Order</button>
        <div id="confirm-msg"></div>
      </form>

      <div class="order-note">
        <h3>How ordering works</h3>
        <p>Orders are sent directly to the shop's inbox — no accounts, no middlemen.</p>
        <ul>
          <li><b>01</b>&nbsp; Fill in your details and pick an item from the shelf.</li>
          <li><b>02</b>&nbsp; Submitting opens an email to the store, pre-filled with your order.</li>
          <li><b>03</b>&nbsp; Akash confirms by phone or email and sets a pickup or delivery time.</li>
        </ul>
        <p style="margin-bottom:4px;">Prefer to skip the form?</p>
        <p style="color:var(--mustard); font-weight:600;">ab7802474@gmail.com</p>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer id="contact">
    <div class="footer-top">
      <div class="fcol">
        <h3>Akash General Store</h3>
        <p>Your everyday shop, stocked and ready.</p>
      </div>
      <div class="fcol">
        <h3 style="font-size:1rem;">Owner</h3>
        <p>Akash Singh</p>
      </div>
      <div class="fcol">
        <h3 style="font-size:1rem;">Contact</h3>
        <p><a href="mailto:ab7802474@gmail.com">ab7802474@gmail.com</a></p>
      </div>
    </div>
    <div class="footer-bottom">&copy; <span id="year"></span> Akash General Store. All rights reserved.</div>
  </footer>

<script>
  // ---------- Product / carousel data ----------
  var productData = [
    {
      name: "Grocery Combo Pack",
      price: "\u20B9 349",
      desc: "A handy mix of daily grocery staples, bundled and ready to go.",
      img: "https://i.ibb.co/vvKz5m6S/Screenshot-2026-08-31-212344.png"
    },
    {
      name: "Daily Essentials Kit",
      price: "\u20B9 219",
      desc: "The everyday basics for the home, restocked fresh each week.",
      img: "https://i.ibb.co/679xmkVR/Screenshot-2026-08-31-212116.png"
    },
    {
      name: "Snacks & Beverages",
      price: "\u20B9 129",
      desc: "A pick of favourite snacks and drinks, always kept in stock.",
      img: "https://i.ibb.co/99qtCkzv/Screenshot-2026-08-31-212540.png"
    }
  ];

  var carousel = document.getElementById('carousel');
  var productSelect = document.getElementById('product');

  function renderCards(){
    var html = '';
    productData.forEach(function(item, i){
      html += ''
        + '<div class="card">'
        + '  <img class="card-img" src="' + item.img + '" alt="' + item.name + '" loading="lazy">'
        + '  <div class="card-body">'
        + '    <h3>' + item.name + '</h3>'
        + '    <div class="price">' + item.price + '</div>'
        + '    <p>' + item.desc + '</p>'
        + '    <button type="button" class="btn order-item" data-index="' + i + '">Order this</button>'
        + '  </div>'
        + '</div>';
    });
    carousel.innerHTML = html;

    var opts = '<option value="" disabled selected>Choose an item</option>';
    productData.forEach(function(item){
      opts += '<option value="' + item.name + '">' + item.name + ' \u2014 ' + item.price + '</option>';
    });
    productSelect.innerHTML = opts;
  }
  renderCards();

  // clicking "Order this" on a card scrolls to the form and pre-selects the item
  carousel.addEventListener('click', function(e){
    var btn = e.target.closest('.order-item');
    if(!btn) return;
    var idx = btn.getAttribute('data-index');
    productSelect.value = productData[idx].name;
    document.getElementById('order').scrollIntoView({behavior:'smooth'});
  });

  // ---------- Shop Now button ----------
  document.getElementById('shopNowBtn').addEventListener('click', function(e){
    e.preventDefault();
    document.getElementById('products').scrollIntoView({behavior:'smooth'});
  });

  // ---------- Auto-sliding carousel ----------
  var autoSlide = setInterval(function(){ stepCarousel(1); }, 3200);

  function cardStep(){
    var card = carousel.querySelector('.card');
    if(!card) return 300;
    var style = getComputedStyle(carousel);
    var gap = parseFloat(style.gap) || 22;
    return card.getBoundingClientRect().width + gap;
  }

  function stepCarousel(dir){
    var maxScroll = carousel.scrollWidth - carousel.clientWidth;
    var next = carousel.scrollLeft + dir * cardStep();
    if(next < 0) next = maxScroll;
    if(next >= maxScroll - 2) next = 0;
    carousel.scrollTo({ left: next, behavior: 'smooth' });
  }

  function pauseAuto(){ clearInterval(autoSlide); }
  function resumeAuto(){
    clearInterval(autoSlide);
    autoSlide = setInterval(function(){ stepCarousel(1); }, 3200);
  }

  carousel.addEventListener('mouseenter', pauseAuto);
  carousel.addEventListener('mouseleave', resumeAuto);
  carousel.addEventListener('touchstart', pauseAuto, {passive:true});
  carousel.addEventListener('touchend', resumeAuto, {passive:true});

  document.getElementById('prevBtn').addEventListener('click', function(){ pauseAuto(); stepCarousel(-1); resumeAuto(); });
  document.getElementById('nextBtn').addEventListener('click', function(){ pauseAuto(); stepCarousel(1); resumeAuto(); });

  // ---------- Order form ----------
  var orderForm = document.getElementById('orderForm');
  var confirmMsg = document.getElementById('confirm-msg');

  orderForm.addEventListener('submit', function(e){
    e.preventDefault();

    var name = document.getElementById('name').value.trim();
    var phone = document.getElementById('phone').value.trim();
    var email = document.getElementById('email').value.trim();
    var product = document.getElementById('product').value;
    var qty = document.getElementById('qty').value;
    var address = document.getElementById('address').value.trim();
    var note = document.getElementById('note').value.trim();

    var subject = 'New order from ' + name + ' - ' + product;
    var body =
      'Item: ' + product + '\n' +
      'Quantity: ' + qty + '\n\n' +
      'Customer: ' + name + '\n' +
      'Phone: ' + phone + '\n' +
      (email ? 'Email: ' + email + '\n' : '') +
      'Delivery / pickup address: ' + address + '\n' +
      (note ? '\nNote: ' + note : '');

    var mailtoLink = 'mailto:ab7802474@gmail.com'
      + '?subject=' + encodeURIComponent(subject)
      + '&body=' + encodeURIComponent(body);

    window.location.href = mailtoLink;

    confirmMsg.textContent = 'Order details ready \u2014 your email app should now open with everything filled in for ab7802474@gmail.com. Send it, and Akash will confirm shortly.';
    confirmMsg.classList.add('show');
    orderForm.reset();
  });

  document.getElementById('year').textContent = new Date().getFullYear();
</script>

</body>
</html>
