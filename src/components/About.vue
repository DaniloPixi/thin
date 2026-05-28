
<template>
  <section id="about" class="about-section">
    <div class="container">
      <div class="row">
        <div class="content-column">
          <div class="inner-column">
            <figure class="image-1">
              <img src="/images/about2.jpg" alt="A vibrant cocktail being garnished">
            </figure>
            <a href="https://widget.thefork.com/68d9a180-bdef-4ec4-9d71-dae00300ac64" target="_blank" class="book-table-btn">Book a Table</a>
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

.row {
  display: flex;
  justify-content: center;
}

.content-column {
  position: relative;
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
  text-align: center;
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
    border: 1px solid rgba(255, 255, 255, 0.1);
    z-index: 2;
    margin: 0;
}

.image-1 img {
    width: 100%;
    height: auto;
    display: block;
}

.book-table-btn {
  margin-top: 40px;
  font-family: 'Imagine Font', serif;
  font-style: normal;
  font-size: 20px;
  color: #ada1a1;
  background-color: rgba(30, 30, 30, 0.5);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  padding: 14px 40px;
  border-radius: 20px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  text-decoration: none;
  text-transform: uppercase;
  letter-spacing: 2px;
  transition: all 0.4s cubic-bezier(0.23, 1, 0.32, 1);
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2), 0 0 15px rgba(255, 193, 7, 0.25);
  display: inline-block;
}

.book-table-btn:hover {
  background-color: var(--primary-color);
  color: #1a1a1a;
  border-color: transparent;
  transform: translateY(-3px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3), 0 0 25px rgba(255, 193, 7, 0.5);
}

@media (max-width: 768px) {
    .image-1 {
        width: 110%;
    }
}

@media (max-width: 500px) {
    .image-1 {
        width: 100%;
        border-radius: 0;
    }
}

</style>
