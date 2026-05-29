<template>
  <header class="header">
    <div class="header-content">
      <a href="#about" class="brand" aria-label="Yu's Cottage home" @click.prevent="scrollToSection('about')">
        <img :src="logo" alt="Yu's Cottage Logo" class="brand-logo" />
      </a>

      <button
        class="nav-toggle"
        type="button"
        :aria-expanded="isMobileNavOpen"
        aria-label="Toggle navigation"
        @click="isMobileNavOpen = !isMobileNavOpen"
      >
        <span></span>
        <span></span>
        <span></span>
      </button>

      <nav class="main-nav" :class="{ 'is-open': isMobileNavOpen }" aria-label="Primary navigation">
        <ul class="nav-list">
          <li class="nav-item dropdown-container" ref="dropdown">
            <button
              class="nav-link nav-button"
              type="button"
              :aria-expanded="isMenuOpen"
              aria-haspopup="true"
              @click="toggleMenu"
            >
              Menu
            </button>
            <ul v-show="isMenuOpen" class="dropdown-menu" @click="closeAllMenus">
              <li><a href="/Karte-Inhalt.pdf" target="_blank" rel="noopener">Dinner</a></li>
              <li><a href="/IMG-20260509-WA0030.jpg" target="_blank" rel="noopener">Lunch</a></li>
              <li><a href="/chinese-menu.jpg" target="_blank" rel="noopener">午餐</a></li>
              <li><a href="/drinks-menu.pdf" target="_blank" rel="noopener">Drinks</a></li>
            </ul>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/drinks-menu.pdf" target="_blank" rel="noopener" @click="closeAllMenus">Cocktails</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#about" @click.prevent="scrollToSection('about')">Story</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#gallery" @click.prevent="scrollToSection('gallery', 'about')">Gallery</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#contact" @click.prevent="scrollToSection('contact')">Reservations</a>
          </li>
        </ul>
      </nav>

      <a class="book-button" :href="bookingUrl" target="_blank" rel="noopener">
        <span>Book a Table</span>
        <span class="book-arrow" aria-hidden="true">↗</span>
      </a>
    </div>
  </header>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';
import logo from '../assets/black-logo3.png';

const bookingUrl = 'https://widget.thefork.com/68d9a180-bdef-4ec4-9d71-dae00300ac64';
const isMenuOpen = ref(false);
const isMobileNavOpen = ref(false);
const dropdown = ref(null);

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
});

const scrollToSection = (sectionId, fallbackId) => {
  const section = document.getElementById(sectionId) || (fallbackId ? document.getElementById(fallbackId) : null);

  if (section) {
    section.scrollIntoView({ behavior: 'smooth', block: 'start' });
  }

  closeAllMenus();
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
  pointer-events: none;
  opacity: 0.18;
  background-image:
    linear-gradient(90deg, rgba(255, 255, 255, 0.05) 1px, transparent 1px),
    linear-gradient(rgba(255, 255, 255, 0.04) 1px, transparent 1px);
  background-size: 42px 42px;
  mask-image: linear-gradient(90deg, #000, transparent 18%, transparent 82%, #000);
}

.header-content {
  position: relative;
  display: grid;
  grid-template-columns: auto minmax(360px, 1fr) auto;
  align-items: center;
  gap: clamp(28px, 5vw, 76px);
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
  display: flex;
  align-items: center;
  gap: clamp(28px, 4.8vw, 72px);
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

.book-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  justify-self: end;
  gap: 24px;
  min-width: 174px;
  min-height: 38px;
  padding: 0 18px 0 26px;
  border-radius: 999px;
  background: #c9dcbc;
  color: #101310;
  font-family: 'Imagine Font', serif;
  font-size: 12px;
  line-height: 1;
  letter-spacing: 2.4px;
  text-transform: uppercase;
  text-decoration: none;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.45), 0 10px 20px rgba(0, 0, 0, 0.22);
  transition: transform 0.25s ease, background 0.25s ease, box-shadow 0.25s ease;
}

.book-button:hover,
.book-button:focus-visible {
  color: #101310;
  background: #e4efd9;
  transform: translateY(-1px);
  text-shadow: none;
  outline: none;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.55), 0 14px 26px rgba(0, 0, 0, 0.28);
}

.book-arrow {
  font-family: Arial, sans-serif;
  font-size: 15px;
  font-weight: 700;
  line-height: 1;
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
}

@media (max-width: 980px) {
  .header {
    padding: 14px 22px;
  }

  .header-content {
    grid-template-columns: auto 1fr auto;
    gap: 16px;
  }

  .brand-logo {
    width: 62px;
    height: 46px;
  }

  .nav-toggle {
    display: block;
    justify-self: end;
    grid-column: 2;
    grid-row: 1;
  }

  .book-button {
    grid-column: 3;
    grid-row: 1;
    min-width: auto;
    min-height: 36px;
    padding: 0 16px;
    gap: 12px;
  }

  .main-nav {
    display: none;
    grid-column: 1 / -1;
    justify-self: stretch;
    padding-top: 14px;
  }

  .main-nav.is-open {
    display: block;
  }

  .nav-list {
    flex-direction: column;
    align-items: stretch;
    gap: 6px;
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
  .header-content {
    grid-template-columns: auto auto;
  }

  .book-button {
    grid-column: 1 / -1;
    justify-self: stretch;
    width: 100%;
  }
}
</style>