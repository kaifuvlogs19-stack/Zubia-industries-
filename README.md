# Zubia-industries-
🏛️ Zubia Industry — Handicrafts &amp; Artisanal Creations | Responsive business website with 3D card animations, scroll effects, image lightbox &amp; WhatsApp integration. Pure HTML/CSS/JS. No frameworks.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Luxury Fountains | Premium Collection</title>
    
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>
    
    <style>
        :root {
            --bg-color: #fbfbfd;
            --text-color: #1d1d1f;
            --accent-color: #86868b;
            --gold: #c9a84c;
            --shadow: 0 20px 60px rgba(0,0,0,0.12);
            --shadow-hover: 0 40px 80px rgba(0,0,0,0.2);
            --transition-smooth: all 0.6s cubic-bezier(0.23, 1, 0.32, 1);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            overflow-x: hidden;
        }

        /* ── Noise texture overlay ── */
        body::before {
            content: '';
            position: fixed;
            inset: 0;
            background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E");
            pointer-events: none;
            z-index: 9999;
        }

        /* ── Navbar ── */
        nav {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            z-index: 100;
            padding: 20px 6vw;
            display: flex;
            align-items: center;
            justify-content: space-between;
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            background: rgba(251,251,253,0.72);
            border-bottom: 1px solid rgba(0,0,0,0.06);
        }

        .nav-logo {
            font-size: 1.1rem;
            font-weight: 600;
            letter-spacing: 0.08em;
            color: var(--text-color);
            text-decoration: none;
        }

        .nav-logo span {
            color: var(--gold);
        }

        .nav-links {
            display: flex;
            gap: 32px;
            list-style: none;
        }

        .nav-links a {
            font-size: 0.85rem;
            color: var(--accent-color);
            text-decoration: none;
            letter-spacing: 0.04em;
            transition: color 0.3s;
        }

        .nav-links a:hover { color: var(--text-color); }

        /* ── Hero / Header ── */
        header {
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 120px 20px 60px;
            position: relative;
            overflow: hidden;
        }

        .hero-eyebrow {
            font-size: 0.78rem;
            letter-spacing: 0.25em;
            text-transform: uppercase;
            color: var(--gold);
            margin-bottom: 22px;
            opacity: 0;
        }

        header h1 {
            font-size: clamp(2.8rem, 6vw, 5.5rem);
            font-weight: 700;
            letter-spacing: -0.03em;
            line-height: 1.08;
            margin-bottom: 22px;
            opacity: 0;
        }

        header h1 em {
            font-style: normal;
            color: var(--gold);
        }

        header p {
            font-size: clamp(1rem, 2vw, 1.25rem);
            color: var(--accent-color);
            max-width: 540px;
            line-height: 1.65;
            opacity: 0;
        }

        .hero-scroll-hint {
            position: absolute;
            bottom: 42px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 8px;
            opacity: 0;
        }

        .scroll-line {
            width: 1px;
            height: 60px;
            background: linear-gradient(to bottom, var(--gold), transparent);
            animation: scrollPulse 2s ease-in-out infinite;
        }

        .scroll-label {
            font-size: 0.7rem;
            letter-spacing: 0.2em;
            text-transform: uppercase;
            color: var(--accent-color);
        }

        @keyframes scrollPulse {
            0%, 100% { opacity: 0.4; transform: scaleY(1); }
            50%       { opacity: 1;   transform: scaleY(1.15); }
        }

        /* ── Decorative background circles ── */
        .hero-bg-circle {
            position: absolute;
            border-radius: 50%;
            filter: blur(80px);
            pointer-events: none;
            opacity: 0.18;
        }

        .circle-1 {
            width: 600px; height: 600px;
            background: radial-gradient(circle, #d4af6a, transparent 70%);
            top: -100px; right: -150px;
        }

        .circle-2 {
            width: 400px; height: 400px;
            background: radial-gradient(circle, #a8c5da, transparent 70%);
            bottom: 0; left: -100px;
        }

        /* ── Gallery ── */
        .gallery-container {
            padding: 0 6vw;
            padding-bottom: 12vh;
        }

        /* Section divider label */
        .section-label {
            text-align: center;
            margin-bottom: 8vh;
            opacity: 0;
        }

        .section-label h2 {
            font-size: clamp(1.6rem, 3vw, 2.4rem);
            font-weight: 600;
            letter-spacing: -0.02em;
        }

        .section-label p {
            font-size: 1rem;
            color: var(--accent-color);
            margin-top: 10px;
        }

        .gold-rule {
            width: 60px;
            height: 2px;
            background: var(--gold);
            margin: 16px auto 0;
            border-radius: 2px;
        }

        /* ── Card ── */
        .section {
            display: flex;
            align-items: center;
            justify-content: center;
            min-height: 90vh;
            margin-bottom: 14vh;
            perspective: 1200px;
        }

        .card {
            position: relative;
            width: 100%;
            max-width: 960px;
            opacity: 0;
            transform: translateY(80px) scale(0.96);
        }

        .image-wrapper {
            position: relative;
            width: 100%;
            border-radius: 28px;
            overflow: hidden;
            box-shadow: var(--shadow);
            cursor: pointer;
            transition: box-shadow 0.5s ease;
            will-change: transform;
        }

        .image-wrapper:hover {
            box-shadow: var(--shadow-hover);
        }

        .image-wrapper img {
            width: 100%;
            height: auto;
            display: block;
            transition: transform 1.4s cubic-bezier(0.2, 0, 0.2, 1);
        }

        .image-wrapper:hover img {
            transform: scale(1.06);
        }

        /* Gradient overlay on image */
        .image-wrapper::after {
            content: '';
            position: absolute;
            inset: 0;
            background: linear-gradient(
                to top,
                rgba(10,10,20,0.55) 0%,
                rgba(10,10,20,0.12) 40%,
                transparent 70%
            );
            pointer-events: none;
            transition: opacity 0.5s ease;
        }

        /* ── Caption ── */
        .caption {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            padding: 36px 36px 32px;
            z-index: 2;
            transform: translateY(6px);
            transition: transform 0.5s cubic-bezier(0.23,1,0.32,1);
        }

        .image-wrapper:hover .caption {
            transform: translateY(0);
        }

        .caption-tag {
            display: inline-block;
            font-size: 0.68rem;
            letter-spacing: 0.22em;
            text-transform: uppercase;
            color: var(--gold);
            background: rgba(201,168,76,0.12);
            border: 1px solid rgba(201,168,76,0.4);
            padding: 4px 12px;
            border-radius: 40px;
            margin-bottom: 10px;
        }

        .caption h3 {
            font-size: clamp(1.3rem, 2.5vw, 1.8rem);
            font-weight: 600;
            color: #fff;
            letter-spacing: -0.01em;
            line-height: 1.2;
            margin-bottom: 8px;
        }

        .caption p {
            font-size: 0.9rem;
            color: rgba(255,255,255,0.72);
            line-height: 1.55;
            max-width: 560px;
        }

        /* ── Number badge ── */
        .card-number {
            position: absolute;
            top: 28px;
            right: 28px;
            width: 48px;
            height: 48px;
            border-radius: 50%;
            background: rgba(255,255,255,0.15);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255,255,255,0.25);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.78rem;
            font-weight: 600;
            color: #fff;
            letter-spacing: 0.04em;
            z-index: 3;
        }

        /* ── Footer ── */
        footer {
            text-align: center;
            padding: 60px 20px;
            border-top: 1px solid rgba(0,0,0,0.07);
        }

        footer p {
            font-size: 0.85rem;
            color: var(--accent-color);
            letter-spacing: 0.04em;
        }

        footer .footer-logo {
            font-size: 1.3rem;
            font-weight: 700;
            letter-spacing: -0.01em;
            margin-bottom: 12px;
        }

        footer .footer-logo span { color: var(--gold); }

        /* ── Cursor dot ── */
        .cursor-dot {
            position: fixed;
            width: 10px;
            height: 10px;
            border-radius: 50%;
            background: var(--gold);
            pointer-events: none;
            z-index: 10000;
            transform: translate(-50%, -50%);
            transition: transform 0.15s ease, width 0.3s ease, height 0.3s ease, opacity 0.3s ease;
            opacity: 0;
        }

        .cursor-ring {
            position: fixed;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            border: 1.5px solid rgba(201,168,76,0.6);
            pointer-events: none;
            z-index: 9999;
            transform: translate(-50%, -50%);
            transition: transform 0.4s cubic-bezier(0.23,1,0.32,1),
                        width 0.4s ease, height 0.4s ease, opacity 0.3s ease;
            opacity: 0;
        }

        /* ── Responsive ── */
        @media (max-width: 768px) {
            .nav-links { display: none; }
            .caption { padding: 24px 20px 20px; }
            .card-number { top: 16px; right: 16px; width: 38px; height: 38px; }
            .section { min-height: auto; margin-bottom: 10vh; }
        }
    </style>
</head>
<body>

    <!-- Custom cursor -->
    <div class="cursor-dot" id="cursorDot"></div>
    <div class="cursor-ring" id="cursorRing"></div>

    <!-- Navbar -->
    <nav>
        <a href="#" class="nav-logo">AQUA<span>LUXE</span></a>
        <ul class="nav-links">
            <li><a href="#">Collection</a></li>
            <li><a href="#">Craftsmanship</a></li>
            <li><a href="#">Materials</a></li>
            <li><a href="#">Bespoke</a></li>
            <li><a href="#">Contact</a></li>
        </ul>
    </nav>

    <!-- Hero Header -->
    <header>
        <div class="hero-bg-circle circle-1"></div>
        <div class="hero-bg-circle circle-2"></div>

        <p class="hero-eyebrow">Est. 1987 · Handcrafted Excellence</p>

        <h1>
            The Art of<br>
            <em>Living Water</em>
        </h1>

        <p>
            Each piece in our collection is a testament to centuries-old craftsmanship — 
            carved from the finest marbles, cast in enduring stone, and destined to become 
            the soul of your space.
        </p>

        <div class="hero-scroll-hint" id="scrollHint">
            <span class="scroll-label">Scroll</span>
            <div class="scroll-line"></div>
        </div>
    </header>

    <!-- Gallery -->
    <div class="gallery-container">

        <!-- Section intro label -->
        <div class="section-label" id="sectionLabel">
            <h2>Premium Collection</h2>
            <p>Eleven masterworks — each one unique, each one timeless.</p>
            <div class="gold-rule"></div>
        </div>

        <!-- Card 01 -->
        <div class="section">
            <div class="card" data-index="1">
                <div class="image-wrapper">
                    <img 
                        src="https://i.imgur.com/8RkIxmJ.jpeg" 
                        alt="Carrara Elegance Fountain"
                        loading="lazy"
                    >
                    <div class="card-number">01</div>
                    <div class="caption">
                        <span class="caption-tag">White Marble · Outdoor</span>
                        <h3>Carrara Elegance</h3>
                        <p>A two-tier masterpiece in pure Carrara marble, installed at a Florida estate. The scalloped basins echo centuries of European fountain design.</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Card 02 -->
        <div class="section">
            <div class="card" data-index="2">
                <div class="image-wrapper">
                    <img 
                        src="https://i.imgur.com/QkLm2Nw.jpeg" 
                        alt="Garden Serenity Fountain"
                        loading="lazy"
                    >
                    <div class="card-number">02</div>
                    <div class="caption">
                        <span class="caption-tag">White Marble · Garden</span>
                        <h3>Garden Serenity</h3>
                        <p>Set within a lush private garden, this three-tier fountain features intricate rope-edge detailing and a tall finial centerpiece in pristine white marble.</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Card 03 -->
        <div class="section">
            <div class="card" data-index="3">
                <div class="image-wrapper">
                    <img 
                        src="https://i.imgur.com/bWpJlKv.jpeg" 
                        alt="Versailles Grand Fountain"
                        loading="lazy"
                    >
                    <div class="card-number">03</div>
                    <div class="caption">
                        <span class="caption-tag">Stone Cast · Classic</span>
                        <h3>Versailles Grand</h3>
                        <p>Inspired by the grandeur of French palatial gardens, this four-tier beauty captures the romance of old-world mastery — with cascading water from every level.</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Card 04 -->
        <div class="section">
            <div class="card" data-index="4">
                <div class="image-wrapper">
                    <img 
                        src="https://i.imgur.com/6tZkP1Y.jpeg" 
                        alt="Atelier Workshop Fountain"
                        loading="lazy"
                    >
                    <div class="card-number">04</div>
                    <div class="caption">
                        <span class="caption-tag">White Marble · Bespoke</span>
                        <h3>Atelier Series No. 4</h3>
                        <p>Photographed at our Rajasthan workshop, this lotus-carved two-tier fountain with a polished sphere finial is a study in geometric harmony and balance.</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Card 05 -->
        <div class="section">
            <div class="card" data-index="5">
                <div class="image-wrapper">
                    <img 
                        src="https://i.imgur.com/mFz7dLs.jpeg" 
                        alt="Imperial Plaza Fountain"
                        loading="lazy"
                    >
                    <div class="card-number">05</div>
                    <div class="caption">
                        <span class="caption-tag">Cast Stone · Urban</span>
                        <h3>Imperial Plaza</h3>
                        <p>A bold three-tier fountain gracing a city courtyard, its ornate basin wall bearing egg-and-dart mouldings and Ionic scroll corbels — civic art at its finest.</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Card 06 -->
        <div class="section">
            <div class="card" data-index="6">
                <div class="image-wrapper">
                    <img 
                        src="https://i.imgur.com/nV3XWQJ.jpeg" 
                        alt="Pegasus Grandeur Fountain"
                        loading="lazy"
                    >
                    <div class="card-number">06</div>
                    <div class="caption">
                        <span class="caption-tag">Beige Marble · Sculptural</span>
                        <h3>Pegasus Grandeur</h3>
                        <p>Three winged-horse sculptures rise from a hexagonal basin, supporting a cascading two-tier crown. A mythological statement in warm beige marble.</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Card 07 -->
        <div class="section">
            <div class="card" data-index="7">
                <div class="image-wrapper">
                    <img 
                        src="https://i.imgur.com/LRpT8aH.jpeg" 
                        alt="Twilight Estate Fountain"
                        loading="lazy"
                    >
                    <div class="card-number">07</div>
                    <div class="caption">
                        <span class="caption-tag">White Marble · Residential</span>
                        <h3>Twilight Estate</h3>
                        <p>Photographed at dusk, this winged-horse fountain commands the forecourt of a private residence — its pale marble luminous against the fading evening sky.</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Card 08 -->
        <div class="section">
            <div class="card" data-index="8">
                <div class="image-wrapper">
                    <img 
                        src="https://i.imgur.com/Jt2pKbZ.jpeg" 
                        alt="Saxon Park Fountain"
                        loading="lazy"
                    >
                    <div class="card-number">08</div>
                    <div class="caption">
                        <span class="caption-tag">Limestone · Park</span>
                        <h3>Saxon Park</h3>
                        <p>A classic single-basin fountain with dramatic multi-jet water display, flanked by bronze animal sculptures and surrounded by manicured English lawns.</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Card 09 -->
        <div class="section">
            <div class="card" data-index="9">
                <div class="image-wrapper">
                    <img 
                        src="https://i.imgur.com/Hk4mD9c.jpeg" 
                        alt="Noir Pegasus Fountain"
                        loading="lazy"
                    >
                    <div class="card-number">09</div>
                    <div class="caption">
                        <span class="caption-tag">Black Granite · Statement</span>
                        <h3>Noir Pegasus</h3>
                        <p>In dramatic black granite, this Pegasus-base fountain exudes power and gravitas. A bold counterpoint to our white marble range — equally breathtaking.</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Card 10 -->
        <div class="section">
            <div class="card" data-index="10">
                <div class="image-wrapper">
                    <img 
                        src="https://i.imgur.com/VpNs7kM.jpeg" 
                        alt="Saffron Spiral Fountain"
                        loading="lazy"
                    >
                    <div class="card-number">10</div>
                    <div class="caption">
                        <span class="caption-tag">Yellow Sandstone · Tropical</span>
                        <h3>Saffron Spiral</h3>
                        <p>Carved from warm Rajasthani sandstone, the spiral-fluted central column and ruffled basins contrast beautifully against the mosaic tile base in vibrant blue.</p>
                    </div>
                </div>
            </div>
        </div>

    </div><!-- /gallery-container -->

    <!-- Footer -->
    <footer>
        <div class="footer-logo">AQUA<span>LUXE</span></div>
        <p>© 2025 AquaLuxe Fountains. All rights reserved. · Crafted with passion.</p>
    </footer>


    <script>
    /* ─────────────────────────────────────────
       GSAP + ScrollTrigger Setup
    ───────────────────────────────────────── */
    gsap.registerPlugin(ScrollTrigger);

    /* ── 1. Hero entrance animations ── */
    const heroTl = gsap.timeline({ defaults: { ease: 'power3.out' } });

    heroTl
        .to('.hero-eyebrow', { opacity: 1, y: 0, duration: 1, delay: 0.3 })
        .to('header h1',      { opacity: 1, y: 0, duration: 1.1 }, '-=0.6')
        .to('header p',       { opacity: 1, y: 0, duration: 1   }, '-=0.7')
        .to('#scrollHint',    { opacity: 1, duration: 0.8         }, '-=0.4');

    /* Ensure initial Y offset for hero elements */
    gsap.set(['.hero-eyebrow', 'header h1', 'header p'], { y: 30 });

    /* ── 2. Section label reveal ── */
    ScrollTrigger.create({
        trigger: '#sectionLabel',
        start: 'top 82%',
        onEnter: () => {
            gsap.to('#sectionLabel', {
                opacity: 1,
                y: 0,
                duration: 1,
                ease: 'power3.out'
            });
        }
    });

    gsap.set('#sectionLabel', { y: 40 });

    /* ── 3. Card scroll-reveal animations ── */
    document.querySelectorAll('.card').forEach((card, i) => {
        const direction = i % 2 === 0 ? 60 : -60;

        gsap.set(card, { opacity: 0, y: 80, x: direction * 0.3, scale: 0.96 });

        ScrollTrigger.create({
            trigger: card,
            start: 'top 85%',
            onEnter: () => {
                gsap.to(card, {
                    opacity: 1,
                    y: 0,
                    x: 0,
                    scale: 1,
                    duration: 1.1,
                    ease: 'power3.out',
                    delay: 0.05
                });
            }
        });
    });

    /* ── 4. Parallax on image inside card ── */
    document.querySelectorAll('.image-wrapper img').forEach(img => {
        gsap.to(img, {
            yPercent: -8,
            ease: 'none',
            scrollTrigger: {
                trigger: img.closest('.card'),
                start: 'top bottom',
                end: 'bottom top',
                scrub: true
            }
        });
    });

    /* ── 5. 3-D Tilt effect on hover ── */
    document.querySelectorAll('.image-wrapper').forEach(wrapper => {
        wrapper.addEventListener('mousemove', (e) => {
            const rect   = wrapper.getBoundingClientRect();
            const centerX = rect.left + rect.width  / 2;
            const centerY = rect.top  + rect.height / 2;
            const dx = (e.clientX - centerX) / (rect.width  / 2);
            const dy = (e.clientY - centerY) / (rect.height / 2);
            const rotY =  dx * 8;  // max ±8°
            const rotX = -dy * 5;  // max ±5°

            gsap.to(wrapper, {
                rotateY: rotY,
                rotateX: rotX,
                transformPerspective: 1000,
                duration: 0.4,
                ease: 'power2.out'
            });
        });

        wrapper.addEventListener('mouseleave', () => {
            gsap.to(wrapper, {
                rotateY: 0,
                rotateX: 0,
                duration: 0.8,
                ease: 'elastic.out(1, 0.5)'
            });
        });
    });

    /* ── 6. Custom cursor ── */
    const dot  = document.getElementById('cursorDot');
    const ring = document.getElementById('cursorRing');
    let mx = window.innerWidth / 2,
        my = window.innerHeight / 2;

    document.addEventListener('mousemove', e => {
        mx = e.clientX;
        my = e.clientY;
        gsap.to(dot, { x: mx, y: my, duration: 0.1, opacity: 1 });
        gsap.to(ring, { x: mx, y: my, duration: 0.45, opacity: 1, ease: 'power2.out' });
    });

    /* Cursor expand on hover over image wrappers */
    document.querySelectorAll('.image-wrapper').forEach(el => {
        el.addEventListener('mouseenter', () => {
            gsap.to(dot,  { scale: 2.5, duration: 0.3 });
            gsap.to(ring, { scale: 1.8, opacity: 0.5, duration: 0.3 });
        });
        el.addEventListener('mouseleave', () => {
            gsap.to(dot,  { scale: 1, duration: 0.3 });
            gsap.to(ring, { scale: 1, opacity: 1, duration: 0.3 });
        });
    });

    document.addEventListener('mouseleave', () => {
        gsap.to([dot, ring], { opacity: 0, duration: 0.3 });
    });

    /* ── 7. Navbar background on scroll ── */
    ScrollTrigger.create({
        start: 100,
        onUpdate: self => {
            const nav = document.querySelector('nav');
            if (self.progress > 0) {
                nav.style.borderBottomColor = 'rgba(0,0,0,0.1)';
            } else {
                nav.style.borderBottomColor = 'rgba(0,0,0,0.06)';
            }
        }
    });

    /* ── 8. Stagger card numbers on scroll ── */
    document.querySelectorAll('.card-number').forEach((num, i) => {
        gsap.from(num, {
            opacity: 0,
            scale: 0.5,
            duration: 0.6,
            ease: 'back.out(1.7)',
            scrollTrigger: {
                trigger: num.closest('.card'),
                start: 'top 80%'
            }
        });
    });

    </script>
</body>
</html>
