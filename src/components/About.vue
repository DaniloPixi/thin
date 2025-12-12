
<template>
  <section id="about" class="about-section">
    <div class="container">
    
      <div class="row">
        <div class="content-column">
          <div class="inner-column">
            <figure class="image-1">
              <img src="/images/about.jpg" alt="A vibrant cocktail being garnished">
            </figure>
            
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
// No script needed for this component
</script>

<style scoped>
.about-section {
    position: relative;
    padding: 120px 0 80px 0;
    background: #0c0c0c;
    overflow-x: hidden;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 15px;
}

.section-title {
  text-align: center;
  margin-bottom: 60px;
}

.section-title h2 {
  font-size: 36px;
  font-weight: 700;
  margin-bottom: 10px;
  font-family: 'Playfair Display', serif;
  color: var(--primary-color);
  text-shadow: 0 2px 4px rgba(255, 223, 150, 0.1);
}

.section-title p {
  font-size: 16px;
  color: var(--secondary-color);
  font-family: 'Poppins', sans-serif;
  margin: 0;
}

.row {
  display: flex;
  justify-content: center;
}

.content-column {
  position: relative;
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
}

.inner-column {
    position: relative;
}

.image-1 {
    position: relative;
    width: 115%;
    left: 50%;
    transform: translateX(-50%);
    border-radius: 12px;
    overflow: hidden;
    box-shadow: 0 20px 50px rgba(0,0,0,0.4);
    border: 3px solid rgba(255, 255, 255, 0.1);
    z-index: 2;
    margin: 0;
}

.image-1 img {
    width: 100%;
    height: auto;
    display: block;
}

.text {
    position: relative;
    width: 90%;
    margin: -40px auto 0;
    z-index: 1;
    padding: 30px 40px;
    font-family: 'Poppins', sans-serif;
    color: var(--secondary-color);
    font-size: 16px;
    line-height: 1.8em;
    background: #1e1e1e;
    border-radius: 12px;
    border: 1px solid rgba(255, 255, 255, 0.1);
}

 .glass-effect {
  background: rgba(30, 30, 30, 0.6);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
} 

.text h3 {
    font-family: 'Playfair Display', serif;
    font-size: 28px;
    font-weight: 700;
    color: var(--primary-color);
    margin-bottom: 20px;
}

.text p {
    margin-bottom: 15px;
}

.text p:last-of-type {
    margin-bottom: 0;
}

@media (max-width: 768px) {
    .text {
        width: 100%;
        margin-top: -60px;
        padding: 25px;
    }

    .image-1 {
        width: 110%;
    }
}

@media (max-width: 500px) {
    .image-1 {
        width: 100%;
        border-radius: 0;
    }

    .text {
        margin-top: -40px;
        border-radius: 0;
    }
}

</style>
