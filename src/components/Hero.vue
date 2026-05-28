
<template>
    <section class="hero" id="top">
      <div class="hero-vignette"></div>
  
      <div class="hero-inner">
        <!-- 1/4 COPY -->
        <div class="hero-copy">
          <h2 class="hero-title">
            Giving authentic
            flavours a modern
            stage
          </h2>
  
          <div class="hero-brush" aria-hidden="true">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 700 300" width="100%" height="100%" style="overflow: visible;">
              <defs>
                <filter id="realistic-paper-disp" x="-10%" y="-10%" width="120%" height="120%">
                  <feTurbulence type="fractalNoise" baseFrequency="0.015 0.15" numOctaves="4" result="noise" />
                  <feColorMatrix type="matrix" values="1 0 0 0 0 0 1 0 0 0 0 0 1 0 0 0 0 0 8 -2.2" result="sharpNoise" />
                  <feDisplacementMap in="SourceGraphic" in2="noise" scale="3.5" xChannelSelector="R" yChannelSelector="G" result="displaced" />
                  <feComposite operator="in" in2="sharpNoise" in="displaced" />
                </filter>
              </defs>
  
              <g transform="rotate(0, 350, 150)" filter="url(#realistic-paper-disp)">
                <path d="M 72.3,152.9 Q 192.6,158.4 313.0,147.9 T 553.7,152.9" stroke="#627f6a" stroke-width="1.61" opacity="1" fill="none" stroke-linecap="round" />
                <path d="M 80.4,148.6 Q 204.4,146.3 328.4,154.4 T 576.5,148.6" stroke="#627f6a" stroke-width="2.24" opacity="1" fill="none" stroke-linecap="round" />
                <path d="M 66.1,146.0 Q 188.4,144.4 310.7,151.8 T 555.3,146.0" stroke="#627f6a" stroke-width="1.65" opacity="0.97" fill="none" stroke-linecap="round" />
                <path d="M 75.7,147.1 Q 202.7,152.6 329.7,146.2 T 583.7,147.1" stroke="#627f6a" stroke-width="1.35" opacity="0.96" fill="none" stroke-linecap="round" />
                <path d="M 92.0,150.8 Q 213.7,155.6 335.5,146.8 T 578.9,150.8" stroke="#627f6a" stroke-width="0.63" opacity="1.04" fill="none" stroke-linecap="round" />
              </g>
            </svg>
          </div>
  
          <p class="hero-subtitle">
            Where time slows, flavours linger,
            and every detail is crafted with care.
            Welcome to Yu’s Cottage.
          </p>
  
          <div class="hero-actions">
            <a href="#reservations" class="hero-btn hero-btn--primary">
              <span>Book a Table</span><span aria-hidden="true">↗</span>
            </a>
            <a href="#menu" class="hero-btn hero-btn--text">View Menu</a>
          </div>
        </div>
  
        <!-- 3/4 MEDIA -->
        <div class="hero-media">
          <img src="/images/Group.jpg" alt="Featured dish presentation" class="hero-image" />
        </div>
      </div>
    </section>
  </template>
  
  <script setup>
  </script>
  
  <style scoped>
  .hero {
    position: relative;
    background: #000;
    padding-top: 88px;
    min-height: 420px;
    border-bottom: 1px solid rgba(170, 151, 115, 0.18);
    overflow: hidden;
  }
  
  .hero-vignette {
    position: absolute;
    inset: 0;
    pointer-events: none;
    z-index: 0;
    background:
      radial-gradient(72% 95% at 58% 50%, rgba(0,0,0,0.05) 0%, rgba(0,0,0,0.50) 65%, rgba(0,0,0,0.88) 100%),
      linear-gradient(90deg, rgba(0,0,0,0.90) 0%, rgba(0,0,0,0.28) 34%, rgba(0,0,0,0.22) 66%, rgba(0,0,0,0.90) 100%);
  }
  
  .hero-inner {
    position: relative;
    z-index: 1;
    max-width: 1320px;
    margin: 0 auto;
    padding: 24px 34px 22px;
    display: grid;
    grid-template-columns: 1fr 3fr;
    gap: 18px;
    align-items: center;
  }
  
  .hero-copy {
    justify-self: end;
    max-width: 320px;
    text-align: center;
  }
  
  .hero-title {
    margin: 0;
    font-family: "Cormorant Garamond", "Times New Roman", serif;
    font-size: clamp(34px, 3.2vw, 58px);
    font-weight: 400;
    line-height: 0.96;
    letter-spacing: 0.01em;
    color: #cdba88d1;
  }
  
  .hero-brush {
    margin: 8px auto 12px;
    width: 260px;
    height: 30px;
  }
  
  .hero-brush svg {
    display: block;
    width: 100%;
    height: 100%;
  }
  
  .hero-subtitle {
    margin: 0 auto 14px;
    max-width: 290px;
    font-size: 14px;
    line-height: 1.45;
    color: #cdba88d1;
  }
  
  .hero-actions {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 12px;
    flex-wrap: wrap;
  }
  
  .hero-btn {
    text-decoration: none;
    text-transform: uppercase;
    letter-spacing: 0.14em;
    font-size: 10px;
  }
  
  .hero-btn--primary {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 9px 18px;
    border-radius: 999px;
    background: #c5dbb6;
    color: #101510;
    border: 1px solid rgba(16, 21, 16, 0.24);
  }
  
  .hero-btn--text {
    color: #cdba88d1;
    border-bottom: 1px solid #cdba88d1;
    padding-bottom: 1px;
  }
  
  .hero-media {
    position: relative;
    min-height: 300px;
  }
  
  .hero-image {
    width: 100%;
    height: 100%;
    max-height: 360px;
    object-fit: cover;
    filter: brightness(0.88) contrast(1.03) saturate(0.95);
  }
  
  .hero-media::before,
  .hero-media::after {
    content: "";
    position: absolute;
    top: 0;
    bottom: 0;
    width: 12%;
    pointer-events: none;
  }
  
  .hero-media::before {
    left: 0;
    background: linear-gradient(90deg, rgba(0,0,0,0.70), rgba(0,0,0,0));
  }
  
  .hero-media::after {
    right: 0;
    background: linear-gradient(270deg, rgba(0,0,0,0.82), rgba(0,0,0,0));
  }
  
  @media (max-width: 980px) {
    .hero-inner {
      grid-template-columns: 1fr;
      padding: 20px 20px;
      gap: 14px;
    }
  
    .hero-copy {
      justify-self: center;
      max-width: 520px;
    }
  
    .hero-subtitle {
      max-width: 100%;
    }
  
    .hero-media {
      min-height: 240px;
    }
  
    .hero-image {
      max-height: 300px;
    }
  }
  </style>