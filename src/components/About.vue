<template>
  <section id="about" class="about-section">
    <div class="container">
      <div class="row">
        <div class="content-column">
          <div class="inner-column">
            <div class="welcome-copy" aria-label="Welcome to Yu's Cottage, where dim sum and cocktails meet">
              <div class="welcome-panel welcome-panel-primary">
                <span>WELCOME TO</span>
                <h1>YU'S COTTAGE</h1>
              </div>

              <div class="welcome-panel welcome-panel-secondary">
                <p>WHERE DIM SUM</p>
                <p>AND COCKTAILS MEET</p>
              </div>
            </div>

            <figure class="image-1">
              <img src="/images/editedMain.png" alt="A vibrant cocktail being garnished">
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
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@300;400&display=swap');

.about-section {
    position: relative;
    padding: 120px 0 80px 0;
    padding: 3.125rem 0 5rem;
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

.welcome-copy {
  --headline-cycle: 7s;
  --champagne: #d7b67f;
  --champagne-soft: rgba(239, 224, 198, 0.78);
  position: relative;
  z-index: 2;
  isolation: isolate;
  min-height: clamp(6.1rem, 10.8vw, 9rem);
  margin: 0 auto 1.25rem;
  overflow: hidden;
  text-align: center;
  text-transform: uppercase;
  text-rendering: geometricPrecision;
}

.welcome-copy::before {
  content: '';
  position: absolute;
  top: -1.1rem;
  bottom: -0.9rem;
  left: 50%;
  width: min(28rem, 82vw);
  transform: translateX(-50%);
  background:
    radial-gradient(ellipse at center, rgba(215, 182, 127, 0.12), rgba(215, 182, 127, 0.035) 42%, transparent 72%),
    linear-gradient(90deg, transparent, rgba(239, 224, 198, 0.045), transparent);
  opacity: 0.95;
  pointer-events: none;
  mix-blend-mode: screen;
}

.welcome-copy::after {
  content: '';
  position: absolute;
  left: 50%;
  bottom: 0;
  width: min(10.5rem, 38vw);
  height: 1px;
  transform: translateX(-50%);
  background: linear-gradient(
    90deg,
    transparent,
    rgba(215, 182, 127, 0.16),
    rgba(239, 224, 198, 0.6),
    rgba(215, 182, 127, 0.16),
    transparent
  );
  box-shadow: 0 0 10px rgba(215, 182, 127, 0.14);
}

.welcome-panel {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  color: var(--champagne);
  font-family: 'Cormorant Garamond', 'Playfair Display', 'Cinzel', Georgia, serif;
  font-weight: 300;
  line-height: 0.96;
  text-shadow:
    0 0 10px rgba(215, 182, 127, 0.12),
    0 14px 34px rgba(0, 0, 0, 0.42);
  will-change: opacity, transform, filter;
}

.welcome-panel span,
.welcome-panel h1,
.welcome-panel p {
  display: block;
  margin: 0;
  font: inherit;
}

.welcome-panel span {
  margin-bottom: 0.55rem;
  font-size: clamp(0.72rem, 0.95vw, 0.9rem);
  letter-spacing: clamp(0.34em, 0.78vw, 0.46em);
  color: var(--champagne-soft);
}

.welcome-panel h1 {
  font-size: clamp(1.8rem, 5.15vw, 4.45rem);
  letter-spacing: clamp(0.12em, 0.9vw, 0.2em);
}

.welcome-panel-secondary {
  padding-top: clamp(0.35rem, 1.15vw, 0.95rem);
}

.welcome-panel-secondary p {
  font-size: clamp(1.12rem, 2.9vw, 2.55rem);
  letter-spacing: clamp(0.13em, 0.68vw, 0.19em);
}

.welcome-panel-secondary p + p {
  margin-top: 0.45rem;
}

.welcome-panel-primary {
  animation: welcomeTitleCycle var(--headline-cycle) ease-in-out infinite;
}

.welcome-panel-secondary {
  animation: welcomeTaglineCycle var(--headline-cycle) ease-in-out infinite;
}

@keyframes welcomeTitleCycle {
  0%, 33% {
    opacity: 1;
    transform: translateY(0);
    filter: blur(0);
  }

  44%, 88% {
    opacity: 0;
    transform: translateY(-0.24rem);
    filter: blur(0.08rem);
  }

  100% {
    opacity: 1;
    transform: translateY(0);
    filter: blur(0);
  }
}

@keyframes welcomeTaglineCycle {
  0%, 42% {
    opacity: 0;
    transform: translateY(0.24rem);
    filter: blur(0.08rem);
  }

  52%, 84% {
    opacity: 1;
    transform: translateY(0);
    filter: blur(0);
  }

  94%, 100% {
    opacity: 0;
    transform: translateY(-0.22rem);
    filter: blur(0.08rem);
  }
}

.image-1 {
    position: relative;
    width: 115%;
    left: 50%;
    transform: translateX(-50%);
    overflow: hidden;
    box-shadow: 0 20px 50px rgba(0,0,0,0.4);
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
    .welcome-copy {
        margin-bottom: 6px;
    }

    .welcome-panel span {
        letter-spacing: 0.35em;
    }

    .welcome-panel h1 {
        letter-spacing: 0.14em;
    }

    .welcome-panel-secondary p {
        letter-spacing: 0.13em;
    }

    .image-1 {
        width: 110%;
    }
}

@media (max-width: 500px) {
    .welcome-copy {
        margin-bottom: 12px;
    }

    .welcome-panel span {
        letter-spacing: 0.32em;
    }

    .welcome-panel h1 {
        letter-spacing: 0.1em;
    }

    .welcome-panel-secondary p {
        letter-spacing: 0.1em;
    }

    .image-1 {
        width: 100%;
    }
}

</style>