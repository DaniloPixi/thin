<template>
  <header ref="header" class="header">
    <img class="navbar-motif navbar-motif-logo" :src="heroDiagonal" alt="" aria-hidden="true">
    <img class="navbar-motif navbar-motif-edge" :src="footerArc" alt="" aria-hidden="true">
    <div class="header-content">
      <a href="#about" class="brand" aria-label="Yu's Cottage home" @click.prevent="scrollToSection('about')">
        <img :src="logo" alt="Yu's Cottage Logo" class="brand-logo" />
      </a>

      <button
        class="nav-toggle"
        type="button"
        :aria-expanded="isMobileNavOpen"
        aria-controls="primary-navigation"
        aria-label="Toggle navigation"
        @click="toggleMobileNav"
      >
        <span></span>
        <span></span>
        <span></span>
      </button>

      <nav
        id="primary-navigation"
        class="main-nav"
        :class="{ 'is-open': isMobileNavOpen }"
        aria-label="Primary navigation"
      >
        <ul class="nav-list">
          <li class="nav-item dropdown-container" ref="dropdown">
            <button
              class="nav-link nav-button"
              type="button"
              :aria-expanded="isMenuOpen"
              aria-controls="menu-dropdown"
              aria-haspopup="true"
              @click="toggleMenu"
            >
              Menu
            </button>
            <ul id="menu-dropdown" v-show="isMenuOpen" class="dropdown-menu" @click="closeAllMenus">
              <li><a href="/Karte-Inhalt.pdf" target="_blank" rel="noopener">Dim Sum & Tapas</a></li>
              <li><a href="/IMG-20260509-WA0030.jpg" target="_blank" rel="noopener">Lunch</a></li>
              <li><a href="/chinese-menu.jpg" target="_blank" rel="noopener">午餐</a></li>
              <li><a href="/drinks-menu.pdf" target="_blank" rel="noopener">Drinks</a></li>
            </ul>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/drinks-menu.pdf" target="_blank" rel="noopener" @click="closeAllMenus">Cocktails</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#specials" @click.prevent="scrollToSection('specials', 'contact')">Specials</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#events" @click.prevent="scrollToSection('events', 'contact')">Events</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#about" @click.prevent="scrollToSection('about')">About</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#gallery" @click.prevent="scrollToSection('gallery', 'about')">Gallery</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#contact" @click.prevent="scrollToSection('contact')">Contact</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#contact" @click.prevent="scrollToSection('contact')">Reservations</a>
          </li>
        </ul>
      </nav>
    </div>
  </header>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';
import logo from '../assets/black-logo3.png';
import heroDiagonal from '../assets/svg/brush-hero-diagonal.svg';
import footerArc from '../assets/svg/brush-footer-arc.svg';

const bookingUrl = 'https://widget.thefork.com/68d9a180-bdef-4ec4-9d71-dae00300ac64';
const isMenuOpen = ref(false);
const isMobileNavOpen = ref(false);
const dropdown = ref(null);
const header = ref(null);
const scrollDuration = 700;
let scrollAnimationFrame = null;

const toggleMobileNav = () => {
  isMobileNavOpen.value = !isMobileNavOpen.value;

  if (!isMobileNavOpen.value) {
    isMenuOpen.value = false;
  }
};

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

const closeAllMenus = () => {
  isMenuOpen.value = false;
  isMobileNavOpen.value = false;
};

const handleClickOutside = (event) => {
  if (dropdown.value && !dropdown.value.contains(event.target)) {
    isMenuOpen.value = false;
  }
};

onMounted(() => {
  document.addEventListener('click', handleClickOutside);
});

onBeforeUnmount(() => {
  document.removeEventListener('click', handleClickOutside);

  if (scrollAnimationFrame) {
    cancelAnimationFrame(scrollAnimationFrame);
  }
});

const easeInOutCubic = (progress) => {
  return progress < 0.5 ? 4 * progress ** 3 : 1 - ((-2 * progress + 2) ** 3) / 2;
};

const animateScrollTo = (targetPosition) => {
  if (scrollAnimationFrame) {
    cancelAnimationFrame(scrollAnimationFrame);
  }

  const startPosition = window.scrollY || window.pageYOffset;
  const distance = targetPosition - startPosition;
  const startTime = performance.now();

  const step = (currentTime) => {
    const elapsed = currentTime - startTime;
    const progress = Math.min(elapsed / scrollDuration, 1);
    const easedProgress = easeInOutCubic(progress);

    window.scrollTo(0, startPosition + distance * easedProgress);

    if (progress < 1) {
      scrollAnimationFrame = requestAnimationFrame(step);
    } else {
      scrollAnimationFrame = null;
    }
  };

  scrollAnimationFrame = requestAnimationFrame(step);
};

const scrollToSection = (sectionId, fallbackId) => {
  const section = document.getElementById(sectionId) || (fallbackId ? document.getElementById(fallbackId) : null);

  closeAllMenus();

  if (!section) {
    return;
  }

  requestAnimationFrame(() => {
    const headerOffset = header.value?.offsetHeight || 0;
    const targetPosition = Math.max(
      section.getBoundingClientRect().top + (window.scrollY || window.pageYOffset) - headerOffset,
      0,
    );

    animateScrollTo(targetPosition);
  });
};
</script>

<style scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 100;
  box-sizing: border-box;
  isolation: isolate;
  overflow: hidden;
  padding: 18px 7.2vw;
  background:
    radial-gradient(circle at 0% 50%, rgba(0, 0, 0, 0.18), transparent 13%),
    radial-gradient(circle at 100% 65%, rgba(0, 0, 0, 0.14), transparent 10%),
    linear-gradient(90deg, rgba(0, 0, 0, 0.96), rgba(14, 14, 13, 0.98));
  border-bottom: 1px solid rgba(0, 0, 0, 0.04);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.35);
}

.header::before {
  content: '';
  position: absolute;
  inset: 0;
  z-index: 0;
  pointer-events: none;
  opacity: 0.18;
  background-image:
    linear-gradient(90deg, rgba(255, 255, 255, 0.05) 1px, transparent 1px),
    linear-gradient(rgba(255, 255, 255, 0.04) 1px, transparent 1px);
  background-size: 42px 42px;
  mask-image: linear-gradient(90deg, #000, transparent 18%, transparent 82%, #000);
}

.navbar-motif {
  position: absolute;
  z-index: 1;
  pointer-events: none;
  user-select: none;
  mix-blend-mode: screen;
  filter: drop-shadow(0 0 18px rgba(184, 215, 184, 0.14));
}

.navbar-motif-logo {
  top: 50%;
  left: clamp(1.1rem, 5.4vw, 5.9rem);
  width: clamp(5.3rem, 8vw, 7.7rem);
  opacity: 0.18;
  transform: translate(-18%, -50%) rotate(-12deg);
}

.navbar-motif-edge {
  top: 50%;
  right: clamp(0.75rem, 2.2vw, 2.3rem);
  width: clamp(4.6rem, 6.5vw, 6.8rem);
  opacity: 0.14;
  transform: translateY(-50%) rotate(18deg);
}

.header-content {
  position: relative;
  z-index: 2;
  display: grid;
  grid-template-columns: auto minmax(520px, 1fr);
  align-items: center;
  gap: clamp(30px, 5vw, 82px);
  max-width: 1320px;
  margin: 0 auto;
}

.brand {
  display: inline-flex;
  align-items: center;
  justify-self: start;
  border-radius: 14px;
}

.brand-logo {
  display: block;
  width: 90px;
  height: 80px;
  object-fit: cover;
  border-radius: 8px;
  box-shadow: 0 0 0 1px rgba(255, 255, 255, 0.08), 0 10px 25px rgba(0, 0, 0, 0.45);
}

.main-nav {
  justify-self: center;
}

.nav-list,
.dropdown-menu {
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-list {
  display: grid;
  grid-template-columns: repeat(4, max-content);
  align-items: center;
  justify-content: center;
  row-gap: 16px;
  column-gap: clamp(34px, 4.4vw, 72px);
}

.nav-item {
  position: relative;
}

.nav-link {
  position: relative;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-height: 32px;
  padding: 0;
  border: 0;
  background: transparent;
  color: #f3efe2;
  cursor: pointer;
  font-family: 'Imagine Font', serif;
  font-size: 12px;
  line-height: 1;
  font-weight: 400;
  letter-spacing: 2.7px;
  text-transform: uppercase;
  text-decoration: none;
  white-space: nowrap;
  transition: color 0.25s ease, opacity 0.25s ease;
}

.nav-link::after {
  content: '';
  position: absolute;
  left: 50%;
  bottom: 2px;
  width: 0;
  height: 1px;
  transform: translateX(-50%);
  background: #c9dcbc;
  transition: width 0.25s ease;
}

.nav-link:hover,
.nav-link:focus-visible {
  color: #c9dcbc;
  outline: none;
  text-shadow: none;
}

.nav-link:hover::after,
.nav-link:focus-visible::after {
  width: 100%;
}

.dropdown-menu {
  position: absolute;
  top: calc(100% + 14px);
  left: 50%;
  min-width: 150px;
  padding: 14px 0;
  transform: translateX(-50%);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 14px;
  background: rgba(10, 10, 9, 0.96);
  box-shadow: 0 18px 36px rgba(0, 0, 0, 0.35);
}

.dropdown-menu a {
  display: block;
  padding: 10px 20px;
  color: #f3efe2;
  font-family: 'Imagine Font', serif;
  font-size: 12px;
  letter-spacing: 2px;
  text-transform: uppercase;
  text-decoration: none;
  white-space: nowrap;
  transition: background 0.25s ease, color 0.25s ease;
}

.dropdown-menu a:hover,
.dropdown-menu a:focus-visible {
  color: #0b0c0b;
  background: #c9dcbc;
  text-shadow: none;
  outline: none;
}

.nav-toggle {
  display: none;
  width: 42px;
  height: 42px;
  padding: 0;
  border: 1px solid rgba(255, 255, 255, 0.12);
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.05);
  cursor: pointer;
}

.nav-toggle span {
  display: block;
  width: 18px;
  height: 2px;
  margin: 4px auto;
  border-radius: 2px;
  background: #f3efe2;
  transition: transform 0.25s ease, opacity 0.25s ease;
}

.nav-toggle[aria-expanded="true"] span:nth-child(1) {
  transform: translateY(6px) rotate(45deg);
}

.nav-toggle[aria-expanded="true"] span:nth-child(2) {
  opacity: 0;
}

.nav-toggle[aria-expanded="true"] span:nth-child(3) {
  transform: translateY(-6px) rotate(-45deg);
}

@media (max-width: 980px) {
  .header {
    padding: 14px 22px;
  }

  .navbar-motif-logo {
    left: 1.35rem;
    width: 5.25rem;
    opacity: 0.13;
  }

  .navbar-motif-edge {
    right: 0.75rem;
    width: 4.8rem;
    opacity: 0.1;
  }

  .header-content {
    grid-template-columns: auto 1fr auto;
    grid-template-areas:
      "brand spacer toggle"
      "book book book"
      "nav nav nav";
    gap: 12px 16px;
  }

  .brand {
    grid-area: brand;
  }

  .brand-logo {
    width: 62px;
    height: 46px;
  }

  .nav-toggle {
    grid-area: toggle;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    justify-self: end;
  }

  .main-nav {
    grid-area: nav;
    display: none;
    justify-self: stretch;
    padding-top: 0;
  }

  .main-nav.is-open {
    display: block;
  }

  .nav-list {
    display: flex;
    flex-direction: column;
    align-items: stretch;
    gap: 10px;
    padding: 14px;
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 18px;
    background: rgba(9, 10, 10, 0.96);
  }

  .nav-link {
    justify-content: flex-start;
    width: 100%;
    min-height: 42px;
  }

  .dropdown-menu {
    position: static;
    min-width: 100%;
    margin: 4px 0 8px;
    padding: 6px 0;
    transform: none;
  }
}

@media (max-width: 560px) {
  .header {
    padding: 12px 20px;
  }

  .navbar-motif-edge {
    opacity: 0.07;
    transform: translate(28%, -50%) rotate(18deg);
  }

  .header-content {
    grid-template-columns: auto 1fr auto;
    gap: 10px 14px;
  }
}
</style>