
<template>
  <header class="header">
    <div class="header-content">
      <div class="header-left">
        <a href="#" @click.prevent="$emit('show-map')" class="address-link">Kettenbrückengasse 3, 1050 Wien</a>
      </div>
      <div class="logo-container" @click="scrollToAbout">
        <img :src="logo" alt="Yu's Cottage Logo" class="logo" />
        <h1 class="logo-text">Yu's Cottage</h1>
      </div>
      <nav class="main-nav">
        <ul>
          <li><a href="#about">About</a></li>
          <li><a href="/Yus_Speisekarte_11-25_Final.pdf" target="_blank">Menu</a></li>
          <li><a href="#contact">Contact</a></li>
        </ul>
      </nav>
    </div>
  </header>
</template>

<script setup>
import logo from '../assets/black-logo.jpg';

defineEmits(['show-map']);

const scrollToAbout = () => {
  const aboutSection = document.getElementById('about');
  if (aboutSection) {
    aboutSection.scrollIntoView({ behavior: 'smooth' });
  }
};
</script>

<style scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 100;
  padding: 20px 40px;
  background: rgba(12, 12, 12, 0.8);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
  transition: all 0.3s ease;
}

.header-content {
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  align-items: center;
  gap: 60px;
  max-width: 1400px;
  margin: 0 auto;
}

.header-left {
  justify-self: end;
}

.main-nav {
  justify-self: start;
}

.logo-container {
  display: flex;
  align-items: center;
  cursor: pointer;
}

.logo {
  height: 50px;
  margin-right: 15px;
}

.logo-text {
  font-family: 'Playfair Display', serif;
  font-size: 24px;
  font-weight: 700;
  color: #fff;
  margin: 0;
}

.main-nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  gap: 30px;
}

.main-nav a {
  text-decoration: none;
  color: var(--secondary-color);
  font-family: 'Poppins', sans-serif;
  font-size: 16px;
  font-weight: 500;
  position: relative;
  transition: color 0.3s ease;
}

.main-nav a::after {
    content: '';
    position: absolute;
    width: 0;
    height: 2px;
    bottom: -5px;
    left: 50%;
    transform: translateX(-50%);
    background-color: var(--primary-color);
    transition: width 0.4s cubic-bezier(0.23, 1, 0.32, 1);
}

.main-nav a:hover,
.main-nav a.active {
  color: #fff;
}

.main-nav a:hover::after {
    width: 100%;
}

.address-link {
  font-family: 'Poppins', sans-serif;
  font-size: 15px;
  color: var(--secondary-color);
  text-decoration: none;
  transition: color 0.3s ease;
  border-bottom: 1px solid transparent;
}

.address-link:hover {
  color: var(--primary-color);
  border-bottom-color: var(--primary-color);
}


/* Mobile Styles */
@media (max-width: 768px) {
  .header {
    padding: 15px 20px;
  }

  .header-content {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .header-left {
    order: 2; /* Move address to the bottom */
    margin-top: 10px;
  }

  .logo-container {
    order: 1;
  }

  .main-nav {
    order: 1;
  }
  
  .logo-text {
    font-size: 20px;
  }
}
</style>
