
<template>
  <section id="hero">
    <div class="hero-container">
      <img src="/YusCottageLogoBig.png" alt="Yu's Cottage Logo" class="hero-logo">
    </div>
  </section>
</template>

<script setup>
</script>

<style scoped>
#hero {
  width: 100%;
  height: 100vh;
  background: url('/images/hero-bg.jpg') top center;
  background-size: cover;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}

#hero:before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.6);
  z-index: 1;
}

.hero-container {
  position: relative;
  text-align: center;
  z-index: 2;
  padding: 0 20px;
}

.hero-logo {
  max-width: 98%;
  max-height: 85vh;
  height: auto;
  filter: drop-shadow(0 8px 20px rgba(0,0,0,0.7));
}

@media (max-width: 768px) {
  .hero-logo {
    max-width: 95%;
  }
}
</style>
