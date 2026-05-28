
<template>
  <div id="app">
    <Header @show-map="openMapModal" />
    <main>
      <About />
      <Contact />
    </main>
    <Footer />
    <FloatingButtons />
    <MapModal v-if="showMap" @close="closeMapModal" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Header from './components/Header.vue';
import About from './components/About.vue';
import Contact from './components/Contact.vue';
import Footer from './components/Footer.vue';
import FloatingButtons from './components/FloatingButtons.vue';
import MapModal from './components/MapModal.vue';

const showMap = ref(false);

const openMapModal = () => {
  showMap.value = true;
};

const closeMapModal = () => {
  showMap.value = false;
};
</script>

<style>
:root {
  --primary-color: #e6c085;
  --secondary-color: #b0b0b0;
  --background-color: #1a1a1a;
  --surface-color: #2c2c2c;
  --text-color: #ffffff;
}

body {
  font-family: 'Poppins', sans-serif;
  background-color: var(--background-color);
  color: var(--text-color);
  margin: 0;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

main {
  flex-grow: 1;
  padding-top: 80px; /* Adjust based on header height */
}
</style>
