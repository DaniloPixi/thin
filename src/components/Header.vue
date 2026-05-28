<template>
  <header class="header">
    <div class="header-inner">
      <!-- Left: compact mark -->
      <a href="#top" class="brand" aria-label="Yu's Cottage home">
        <img :src="logo" alt="Yu's Cottage logo" class="brand-logo" />
      </a>

      <!-- Center: primary nav -->
      <nav class="main-nav" aria-label="Primary navigation">
        <ul>
          <li><a href="#menu">Menu</a></li>
          <li><a href="#cocktails">Cocktails</a></li>
          <li><a href="#story">Story</a></li>
          <li><a href="#gallery">Gallery</a></li>
          <li><a href="#reservations">Reservations</a></li>
        </ul>
      </nav>

      <!-- Right: CTA -->
      <a href="#reservations" class="cta">
        <span>Book a Table</span>
        <span class="arrow" aria-hidden="true">↗</span>
      </a>

      <!-- Mobile toggle -->
      <button
        class="mobile-toggle"
        type="button"
        @click="isMobileOpen = !isMobileOpen"
        :aria-expanded="isMobileOpen"
        aria-controls="mobile-nav"
        aria-label="Toggle menu"
      >
        <span></span><span></span><span></span>
      </button>
    </div>

    <!-- Mobile menu -->
    <nav id="mobile-nav" class="mobile-nav" :class="{ open: isMobileOpen }" aria-label="Mobile navigation">
      <a href="#menu" @click="closeMobile">Menu</a>
      <a href="#cocktails" @click="closeMobile">Cocktails</a>
      <a href="#story" @click="closeMobile">Story</a>
      <a href="#gallery" @click="closeMobile">Gallery</a>
      <a href="#reservations" @click="closeMobile">Reservations</a>
      <a href="#reservations" class="mobile-cta" @click="closeMobile">Book a Table ↗</a>
    </nav>
  </header>
</template>

<script setup>
import { ref } from 'vue';
import logo from '../assets/black-logo.jpg';

const isMobileOpen = ref(false);

const closeMobile = () => {
  isMobileOpen.value = false;
};
</script>

<style scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 200;
  background: rgba(7, 8, 10, 0.84);
  backdrop-filter: blur(6px);
  -webkit-backdrop-filter: blur(6px);
  border-bottom: 1px solid rgba(190, 172, 135, 0.18);
}

.header-inner {
  max-width: 1320px;
  margin: 0 auto;
  min-height: 82px;
  padding: 12px 24px;
  display: grid;
  grid-template-columns: auto 1fr auto;
  align-items: center;
  gap: 20px;
}

/* Brand */
.brand {
  display: inline-flex;
  align-items: center;
  text-decoration: none;
}
.brand-logo {
  width: 56px;
  height: 56px;
  object-fit: cover;
  border-radius: 8px;
  border: 1px solid rgba(255, 255, 255, 0.08);
}

/* Desktop nav */
.main-nav {
  justify-self: center;
}
.main-nav ul {
  list-style: none;
  display: flex;
  gap: clamp(18px, 2.4vw, 42px);
  margin: 0;
  padding: 0;
}
.main-nav a {
  text-decoration: none;
  text-transform: uppercase;
  letter-spacing: 0.14em;
  font-size: 12px;
  color: #e8dfc9;
  opacity: 0.9;
  position: relative;
  transition: opacity 0.22s ease, color 0.22s ease;
}
.main-nav a::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: -8px;
  width: 100%;
  height: 1px;
  background: #c5b78f;
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 0.22s ease;
}
.main-nav a:hover {
  opacity: 1;
  color: #fff3d5;
}
.main-nav a:hover::after {
  transform: scaleX(1);
}

/* CTA */
.cta {
  justify-self: end;
  display: inline-flex;
  align-items: center;
  gap: 10px;
  text-decoration: none;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  font-size: 12px;
  color: #0f1512;
  background: #c5dbb6;
  border-radius: 999px;
  padding: 12px 26px;
  border: 1px solid rgba(15, 21, 18, 0.15);
  transition: transform 0.18s ease, filter 0.18s ease;
}
.cta:hover {
  transform: translateY(-1px);
  filter: brightness(1.02);
}
.arrow {
  font-size: 13px;
  line-height: 1;
}

/* Mobile */
.mobile-toggle {
  display: none;
  justify-self: end;
  background: transparent;
  border: 0;
  cursor: pointer;
  padding: 6px;
}
.mobile-toggle span {
  display: block;
  width: 22px;
  height: 2px;
  background: #e8dfc9;
  margin: 4px 0;
}

.mobile-nav {
  display: none;
}

@media (max-width: 980px) {
  .header-inner {
    grid-template-columns: auto auto;
    min-height: 72px;
  }

  .main-nav,
  .cta {
    display: none;
  }

  .mobile-toggle {
    display: block;
  }

  .mobile-nav {
    display: grid;
    gap: 10px;
    max-height: 0;
    overflow: hidden;
    padding: 0 24px;
    border-top: 1px solid rgba(190, 172, 135, 0.14);
    background: rgba(7, 8, 10, 0.95);
    transition: max-height 0.25s ease, padding 0.25s ease;
  }

  .mobile-nav.open {
    max-height: 340px;
    padding: 14px 24px 18px;
  }

  .mobile-nav a {
    color: #e8dfc9;
    text-decoration: none;
    text-transform: uppercase;
    letter-spacing: 0.12em;
    font-size: 12px;
  }

  .mobile-cta {
    margin-top: 6px;
    color: #c5dbb6 !important;
  }
}

</style>