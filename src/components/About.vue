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
              <div class="welcome-panel welcome-panel-secondary" aria-hidden="true">
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
  --headline-cycle: 17s;
  position: relative;
  z-index: 2;
  isolation: isolate;
  min-height: clamp(5.5rem, 11vw, 9rem);
  margin: 0 auto 1.25rem;
  overflow: hidden;
  text-align: center;
  text-transform: uppercase;
  animation: welcomeReveal 1.1s cubic-bezier(0.22, 1, 0.36, 1) both;
}

.welcome-panel {
  position: absolute;
  inset: 0 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  margin: 0;
  color: #c9a063;
  font-family: 'Cormorant Garamond', 'Playfair Display', 'Cinzel', Georgia, serif;
  font-weight: 300;
  line-height: 0.95;
  text-shadow:
    0 0 12px rgba(201, 160, 99, 0.16),
    0 10px 28px rgba(170, 94, 43, 0.12);
  clip-path: inset(0 50% 0 50%);
  opacity: 0;
  will-change: opacity, transform, filter, clip-path;
}

.welcome-panel::before {
  content: '';
  position: absolute;
  top: -0.7rem;
  bottom: -0.7rem;
  left: 50%;
  width: min(28rem, 82vw);
  transform: translateX(-50%) scaleX(0);
  transform-origin: center;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(201, 160, 99, 0.08),
    rgba(232, 214, 184, 0.2),
    rgba(201, 160, 99, 0.08),
    transparent
  );
  opacity: 0;
  pointer-events: none;
  mix-blend-mode: screen;
}

.welcome-panel-primary {
  animation: welcomePanelPrimary var(--headline-cycle) cubic-bezier(0.22, 1, 0.36, 1) infinite;
}

.welcome-panel-secondary {
  animation: welcomePanelSecondary var(--headline-cycle) cubic-bezier(0.22, 1, 0.36, 1) infinite;
}

.welcome-panel-primary::before {
  animation: welcomeAperturePrimary var(--headline-cycle) cubic-bezier(0.22, 1, 0.36, 1) infinite;
}

.welcome-panel-secondary::before {
  animation: welcomeApertureSecondary var(--headline-cycle) cubic-bezier(0.22, 1, 0.36, 1) infinite;
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
  font-size: clamp(0.75rem, 1vw, 0.95rem);
  letter-spacing: clamp(0.35em, 0.85vw, 0.5em);
  opacity: 0.82;
}

.welcome-panel h1 {
  font-size: clamp(1.85rem, 5.4vw, 4.75rem);
  letter-spacing: clamp(0.12em, 1vw, 0.22em);
}

.welcome-panel-secondary {
  padding-top: clamp(0.3rem, 1.1vw, 0.9rem);
}

.welcome-panel-secondary p {
  font-size: clamp(1.15rem, 3.15vw, 2.75rem);
  letter-spacing: clamp(0.12em, 0.75vw, 0.2em);
}

.welcome-panel-secondary p + p {
  margin-top: 0.45rem;
}

.welcome-copy::after {
  content: '';
  position: absolute;
  left: 50%;
  bottom: 0;
  width: min(12rem, 42vw);
  height: 1px;
  transform: translateX(-50%);
  background: linear-gradient(
    90deg,
    transparent,
    rgba(201, 160, 99, 0.26),
    rgba(232, 214, 184, 0.82),
    rgba(201, 160, 99, 0.26),
    transparent
  );
  box-shadow: 0 0 12px rgba(201, 160, 99, 0.34);
}

@keyframes welcomeReveal {
  from {
    opacity: 0;
    transform: translateY(24px);
    filter: blur(8px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
    filter: blur(0);
  }
}

@keyframes welcomePanelPrimary {
  0%, 4% {
    clip-path: inset(0 50% 0 50%);
    opacity: 0;
    transform: translateY(0.35rem) scale(0.985);
    filter: blur(0.35rem);
  }

  12%, 23% {
    clip-path: inset(0 0 0 0);
    opacity: 1;
    transform: translateY(0) scale(1);
    filter: blur(0);
  }

  31%, 100% {
    clip-path: inset(0 50% 0 50%);
    opacity: 0;
    transform: translateY(-0.3rem) scale(0.99);
    filter: blur(0.28rem);
  }
}

@keyframes welcomePanelSecondary {
  0%, 30% {
    clip-path: inset(0 50% 0 50%);
    opacity: 0;
    transform: translateY(0.35rem) scale(0.985);
    filter: blur(0.35rem);
  }

  39%, 96% {
    clip-path: inset(0 0 0 0);
    opacity: 1;
    transform: translateY(0) scale(1);
    filter: blur(0);
  }

  100% {
    clip-path: inset(0 50% 0 50%);
    opacity: 0;
    transform: translateY(-0.3rem) scale(0.99);
    filter: blur(0.28rem);
  }
}

@keyframes welcomeAperturePrimary {
  0%, 4%, 31%, 100% {
    opacity: 0;
    transform: translateX(-50%) scaleX(0);
  }

  10%, 22% {
    opacity: 0.58;
    transform: translateX(-50%) scaleX(1);
  }

  27% {
    opacity: 0;
    transform: translateX(-50%) scaleX(0.18);
  }
}

@keyframes welcomeApertureSecondary {
  0%, 30%, 100% {
    opacity: 0;
    transform: translateX(-50%) scaleX(0);
  }

  37%, 91% {
    opacity: 0.46;
    transform: translateX(-50%) scaleX(1);
  }

  96% {
    opacity: 0;
    transform: translateX(-50%) scaleX(0.18);
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