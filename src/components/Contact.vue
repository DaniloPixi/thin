
<template>
  <section id="contact" class="contact-section">
    <div class="container">
      <div class="section-title">
        <h2>Contact & Hours</h2>
        <p>We'd love to host you. Find our details and opening hours below.</p>
      </div>
      <div class="row">
        <div class="contact-info">
          <div class="info-box">
            <h3>Our Address</h3>
            <p>Kettenbrückengasse 3, 1050 Wien</p>
          </div>
          <div class="info-box">
            <h3>Opening Hours</h3>
            <p>Tue - Thu: 11:30-14:30 | 17:00 - 23:00</p>
            <p>Fri - Sat: 11:30-14:30 | 17:00 - 01:00</p>
            <p>Sun: 12:30 - 17:00</p>
          </div>
          <div class="info-box">
            <h3>Contact</h3>
            <p>Email: info@yuscottage.at</p>
            <p>Phone: +43 670 1957515</p>
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
.contact-section {
  padding: 100px 0;
  background: var(--background-color);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 15px;
}

.section-title {
  max-width: 600px;
  margin: 0 auto 60px auto;
  padding: 20px 30px;
  background: rgba(30, 30, 30, 0.6);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3), 0 0 15px rgba(230, 192, 133, 0.1);
  text-align: center;
}

.section-title h2 {
  font-size: 32px;
  font-weight: normal; /* Use the font's natural weight */
  margin-bottom: 20px;
  padding-bottom: 20px;
  position: relative;
  font-family: "Imagine Font", serif;
}

.section-title h2::after {
  content: '';
  position: absolute;
  display: block;
  width: 40px;
  height: 3px;
  background: var(--primary-color);
  bottom: 0;
  left: calc(50% - 20px);
}

.section-title p {
  margin-bottom: 0;
  color: var(--secondary-color);
  font-family: 'Poppins', sans-serif;
}

.row {
  display: flex;
  justify-content: center; 
  align-items: flex-start;
}

.contact-info {
  width: 100%;
  max-width: 500px; 
}

.info-box {
  margin-bottom: 40px;
  text-align: center; 
}

.info-box:last-child {
    margin-bottom: 0;
}

.info-box h3 {
  font-size: 22px;
  color: var(--primary-color);
  margin-bottom: 15px;
  font-family: "Imagine Font", serif;
  font-weight: normal; /* Use the font's natural weight */
  position: relative;
  display: inline-block;
  padding-bottom: 5px;
}

.info-box h3::after {
    content: '';
    position: absolute;
    display: block;
    width: 30px;
    height: 2px;
    background: var(--primary-color);
    bottom: 0;
    left: calc(50% - 15px);
}


.info-box p {
  font-size: 17px;
  line-height: 1.7;
  color: var(--secondary-color);
  margin: 0 0 5px 0;
}

@media (max-width: 768px) {
  .contact-info {
    max-width: 100%;
  }
}
</style>
