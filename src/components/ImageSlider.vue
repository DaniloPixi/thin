<template>
  <section id="gallery" class="gallery-showcase" aria-labelledby="gallery-title">
    <div class="gallery-copy">
      <h2 id="gallery-title">A gallery of moments.</h2>
      <p>
        Discover signature plates, handmade dim sum, and warm evening details from the cottage.
      </p>
    </div>

    <div class="gallery-stage">
      <div class="swiper gallery-swiper" ref="gallerySwiperContainer">
        <div class="swiper-wrapper">
          <article class="swiper-slide gallery-slide" v-for="slide in slides" :key="slide.title">
            <div class="image-frame">
              <img :src="slide.image" :alt="slide.title" />
              <div class="slide-caption">
                <h3>{{ slide.title }}</h3>
                <p>{{ slide.description }}</p>
              </div>
            </div>
          </article>
        </div>
      </div>

      <button class="gallery-nav gallery-nav-prev" type="button" aria-label="Previous gallery image">
        <span aria-hidden="true">←</span>
      </button>
      <button class="gallery-nav gallery-nav-next" type="button" aria-label="Next gallery image">
        <span aria-hidden="true">→</span>
      </button>
    </div>
  </section>
</template>

<script setup>
import { ref, onBeforeUnmount, onMounted } from 'vue';
import Swiper from 'swiper';
import { A11y, Keyboard, Navigation } from 'swiper/modules';
import 'swiper/css';
import 'swiper/css/navigation';

const gallerySwiperContainer = ref(null);
let gallerySwiper = null;

const slides = [
  {
    image: '/images/Beef With Yu.jpg',
    title: 'Beef With Yu',
    description: 'Beef shanks braised in master stock and served in delicate slices.'
  },
  {
    image: '/images/Ha Gao.jpg',
    title: 'Ha Gao',
    description: 'Translucent prawn dumplings with water chestnuts and a gentle bite.'
  },
  {
    image: '/images/Karaage Chicken.jpg',
    title: 'Karaage Chicken',
    description: 'Crisp chicken with sriracha glaze or Ziu-Yim spices and wild garlic-lime mayo.'
  },
  {
    image: '/images/Shrimp & Wild Garlic Gyoza.jpg',
    title: 'Shrimp & Wild Garlic Gyoza',
    description: 'Pan-seared parcels filled with shrimp, water chestnut, and wild garlic.'
  },
  {
    image: '/images/Siu Mai.jpg',
    title: 'Siu Mai',
    description: 'Steamed open dumplings with shrimp, chicken, shiitake, and house seasoning.'
  },
  {
    image: '/images/Sou Gao.jpg',
    title: 'Sou Gao',
    description: 'Vegetable dumplings with peanuts, shiitake, vegan mince, and cottage aromatics.'
  },
  {
    image: '/images/Squid Yu-Style.jpg',
    title: 'Squid Yu-Style',
    description: 'Tender squid braised with green tea and spices, sliced for sharing.'
  },
  {
    image: '/images/Tofu Skin Rolls.jpg',
    title: 'Tofu Skin Rolls',
    description: 'Silky tofu skin wrapped around vegetables, mushrooms, glass noodles, and sauce.'
  },
  {
    image: '/images/Group.jpg',
    title: 'The Yu\'s Cottage Team',
    description: 'The team behind the craft, care, and warm hospitality at Yu\'s Cottage.'
  }
];

onMounted(() => {
  if (!gallerySwiperContainer.value) {
    return;
  }

  gallerySwiper = new Swiper(gallerySwiperContainer.value, {
    modules: [A11y, Keyboard, Navigation],
    loop: true,
    centeredSlides: true,
    grabCursor: true,
    initialSlide: 1,
    slidesPerView: 'auto',
    spaceBetween: 16,
    speed: 850,
    keyboard: {
      enabled: true
    },
    navigation: {
      nextEl: '.gallery-nav-next',
      prevEl: '.gallery-nav-prev'
    },
    a11y: {
      enabled: true,
      slideLabelMessage: '{{index}} of {{slidesLength}}'
    },
    breakpoints: {
      640: {
        spaceBetween: 22
      },
      960: {
        spaceBetween: 30
      }
    }
  });
});

onBeforeUnmount(() => {
  gallerySwiper?.destroy(true, true);
});
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@300;400&display=swap');

.gallery-showcase {
  position: relative;
  isolation: isolate;
  overflow: hidden;
  padding: clamp(4rem, 8vw, 7rem) 0;
  background:
    radial-gradient(circle at 50% 48%, rgba(159, 197, 166, 0.12), transparent 24rem),
    radial-gradient(circle at 20% 20%, rgba(230, 192, 133, 0.08), transparent 18rem),
    #080908;
  color: #fff;
}

.gallery-showcase::before,
.gallery-showcase::after {
  content: '';
  position: absolute;
  inset: 0;
  z-index: -1;
  pointer-events: none;
}

.gallery-showcase::before {
  background:
    linear-gradient(90deg, #080908 0%, rgba(8, 9, 8, 0.72) 9%, transparent 24%, transparent 76%, rgba(8, 9, 8, 0.72) 91%, #080908 100%),
    radial-gradient(ellipse at center, transparent 42%, rgba(0, 0, 0, 0.7) 100%);
}

.gallery-showcase::after {
  opacity: 0.45;
  background-image:
    linear-gradient(rgba(255, 255, 255, 0.025) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255, 255, 255, 0.02) 1px, transparent 1px);
  background-size: 44px 44px;
  mask-image: radial-gradient(circle at center, black, transparent 76%);
}

.gallery-copy {
  width: min(90vw, 28rem);
  margin: 0 auto clamp(2rem, 4vw, 3.25rem);
  text-align: center;
}

.eyebrow {
  margin: 0 0 0.7rem;
  color: #a4d0ad;
  font-family: 'Poppins', sans-serif;
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 0.35em;
  text-transform: uppercase;
}

.gallery-copy h2 {
  margin: 0;
  color: #29614c;
  font-family: 'Cormorant Garamond', 'Playfair Display', Georgia, serif;
  font-weight: 300;
  font-size: clamp(2rem, 4.8vw, 3.85rem);
  line-height: 0.92;
  text-wrap: balance;
}

.gallery-copy p:not(.eyebrow) {
  max-width: 24rem;
  margin: 1rem auto 0;
  color: rgba(255, 255, 255, 0.68);
  font-family: 'Poppins', sans-serif;
  font-size: clamp(0.9rem, 1.6vw, 1rem);
  line-height: 1.65;
}

.gallery-stage {
  --photo-enter-x: -48vw;
  --caption-enter-x: 86vw;

  position: relative;
  width: min(100%, 118rem);
  margin: 0 auto;
}

.gallery-swiper {
  overflow: visible;
  width: 100%;
  perspective: 54rem;
  perspective-origin: center;
  padding: clamp(1rem, 2vw, 2rem) 0 clamp(2.2rem, 4vw, 3.5rem);
}

.gallery-slide {
  display: flex;
  align-items: center;
  justify-content: center;
  width: min(66vw, 27rem);
  height: clamp(15rem, 32vw, 22rem);
  opacity: 0.28;
  transform: scale(0.78) rotateZ(-7deg) rotateY(-42deg) translateZ(-3rem);
  transform-style: preserve-3d;
  filter: blur(1.5px) saturate(0.72) brightness(0.82);
  backface-visibility: hidden;
  will-change: transform, opacity, filter;
  transition:
    opacity 720ms cubic-bezier(0.22, 1, 0.36, 1),
    transform 900ms cubic-bezier(0.22, 1, 0.36, 1),
    filter 720ms cubic-bezier(0.22, 1, 0.36, 1);
}

.gallery-slide.swiper-slide-prev {
  opacity: 0.68;
  transform: translateX(8%) scale(0.88) rotateZ(-8deg) rotateY(-52deg) rotateX(2deg) translateZ(-2rem);
  transform-origin: center;
  filter: blur(0) saturate(0.88) brightness(0.9);
}

.gallery-slide.swiper-slide-next {
  opacity: 0.68;
  transform: translateX(-8%) scale(0.88) rotateZ(8deg) rotateY(52deg) rotateX(2deg) translateZ(-2rem);
  transform-origin: center;
  filter: blur(0) saturate(0.88) brightness(0.9);
}

.gallery-slide.swiper-slide-active {
  z-index: 3;
  opacity: 1;
  transform: scale(1) rotateZ(0deg) rotateY(0deg) translateZ(1rem);
  filter: drop-shadow(0 1.5rem 3rem rgba(0, 0, 0, 0.48));
}

.image-frame {
  position: relative;
  overflow: hidden;
  width: 100%;
  height: 82%;
  border: 1px solid rgba(255, 255, 255, 0.13);
  border-radius: 1.45rem;
  background: #111;
  box-shadow:
    0 1.2rem 3.5rem rgba(0, 0, 0, 0.48),
    0 0.2rem 1.1rem rgba(255, 255, 255, 0.08) inset;
  transform: scale(0.96);
  transform-origin: center;
  transform-style: preserve-3d;
  backface-visibility: hidden;
  will-change: transform, border-radius, box-shadow, filter, opacity;
  transition:
    transform 900ms cubic-bezier(0.22, 1, 0.36, 1),
    border-radius 900ms cubic-bezier(0.22, 1, 0.36, 1),
    box-shadow 900ms cubic-bezier(0.22, 1, 0.36, 1),
    filter 700ms ease,
    opacity 700ms ease;
}

.gallery-slide.swiper-slide-active .image-frame {
  width: clamp(15.3rem, 30.6vw, 24.3rem);
  height: clamp(15.3rem, 30.6vw, 24.3rem);
  overflow: visible;
  border: 0;
  border-radius: 50%;
  background: transparent;
  box-shadow: none;
  transform: scale(1);
  animation: gallery-photo-enter-left-strong 1150ms cubic-bezier(0.16, 1, 0.3, 1) both;
}

.gallery-slide.swiper-slide-active .image-frame::after {
  content: '';
  position: absolute;
  inset: -13%;
  z-index: 2;
  border-radius: 50%;
  pointer-events: none;
  background:
    conic-gradient(
      from 18deg,
      transparent 0 8%,
      rgba(164, 208, 173, 0.72) 10% 15%,
      transparent 18% 34%,
      rgba(164, 208, 173, 0.54) 37% 43%,
      transparent 47% 63%,
      rgba(230, 192, 133, 0.46) 66% 70%,
      transparent 73% 100%
    );
  -webkit-mask: radial-gradient(farthest-side, transparent calc(100% - 0.45rem), #000 calc(100% - 0.42rem));
  mask: radial-gradient(farthest-side, transparent calc(100% - 0.45rem), #000 calc(100% - 0.42rem));
  opacity: 0.9;
  transform: rotate(9deg);
  animation: gallery-ring-drift 7s linear infinite;
  will-change: transform;
}

.image-frame img {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
  transform: scale(1.08);
  will-change: transform, filter;
  transition:
    transform 1200ms cubic-bezier(0.22, 1, 0.36, 1),
    filter 900ms ease;
}

.gallery-slide.swiper-slide-prev .image-frame img,
.gallery-slide.swiper-slide-next .image-frame img {
  transform: scale(1.045);
}

.gallery-slide.swiper-slide-active .image-frame img {
  overflow: hidden;
  border-radius: 50%;
  box-shadow:
    0 1.7rem 5rem rgba(0, 0, 0, 0.85),
    0 0 0 1px rgba(255, 255, 255, 0.12);
  transform: scale(1.015);
  animation: gallery-photo-settle-left 1500ms cubic-bezier(0.22, 1, 0.36, 1) both;
}

.image-frame::before {
  content: '';
  position: absolute;
  inset: 0;
  z-index: 1;
  border-radius: inherit;
  pointer-events: none;
  background:
    radial-gradient(circle at center, transparent 34%, rgba(0, 0, 0, 0.38) 72%, rgba(0, 0, 0, 0.93) 100%),
    linear-gradient(180deg, transparent 42%, rgba(0, 0, 0, 0.86) 100%);
}

.gallery-slide.swiper-slide-active .image-frame::before {
  background:
    radial-gradient(circle at center, transparent 42%, rgba(0, 0, 0, 0.28) 70%, rgba(0, 0, 0, 0.78) 100%),
    linear-gradient(180deg, transparent 44%, rgba(0, 0, 0, 0.76) 100%);
  clip-path: none;
  border: 0;
  filter: none;
  transform: none;
}

.slide-caption {
  position: absolute;
  right: 1rem;
  bottom: 1rem;
  left: 1rem;
  z-index: 3;
  color: #fff;
  text-align: center;
  padding: 0.55rem 0.9rem;
  border-radius: 0.95rem;
  background:
    linear-gradient(180deg, rgba(7, 12, 10, 0.1), rgba(7, 12, 10, 0.72));
  box-shadow:
    0 0.8rem 2rem rgba(0, 0, 0, 0.3),
    inset 0 1px 0 rgba(255, 255, 255, 0.12);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  text-shadow: 0 0.2rem 0.8rem rgba(0, 0, 0, 0.9);
  opacity: 0;
  transform: translate3d(var(--caption-enter-x), 0.7rem, 0) scale(0.88);
  filter: blur(16px);
  will-change: opacity, transform, filter;
}

.gallery-slide.swiper-slide-active .slide-caption {
  animation: gallery-caption-enter-right-strong 1050ms cubic-bezier(0.16, 1, 0.3, 1) 180ms both;
}

.slide-caption h3 {
  margin: 0;
  color: #78b68e;
  font-family: 'Cormorant Garamond', 'Playfair Display', Georgia, serif;
  font-weight: 300;
  font-size: clamp(1.05rem, 1.7vw, 1.7rem);
  line-height: 0.95;
  opacity: 0;
  transform: translate3d(1.8rem, 0.2rem, 0);
  will-change: opacity, transform;
}

.slide-caption p {
  max-width: 17rem;
  margin: 0.28rem auto 0;
  color: rgba(255, 255, 255, 0.78);
  font-family: 'Poppins', sans-serif;
  font-size: clamp(0.72rem, 1vw, 0.84rem);
  line-height: 1.28;
  opacity: 0;
  transform: translate3d(1.8rem, 0.2rem, 0);
  will-change: opacity, transform;
}

.gallery-slide.swiper-slide-active .slide-caption h3 {
  animation: gallery-caption-text-enter 700ms cubic-bezier(0.16, 1, 0.3, 1) 560ms both;
}

.gallery-slide.swiper-slide-active .slide-caption p {
  animation: gallery-caption-text-enter 700ms cubic-bezier(0.16, 1, 0.3, 1) 680ms both;
}

.gallery-nav {
  position: absolute;
  top: 50%;
  z-index: 6;
  display: grid;
  place-items: center;
  width: 3.1rem;
  height: 3.1rem;
  border: 1px solid rgba(255, 255, 255, 0.28);
  border-radius: 50%;
  background: rgba(0, 0, 0, 0.42);
  color: #f7ead8;
  cursor: pointer;
  transform: translateY(-50%);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  transition:
    background 0.25s ease,
    border-color 0.25s ease,
    transform 0.25s ease;
}

.gallery-nav:hover,
.gallery-nav:focus-visible {
  border-color: rgba(230, 192, 133, 0.75);
  background: rgba(230, 192, 133, 0.17);
  outline: none;
  transform: translateY(-50%) scale(1.08);
}

.gallery-nav-prev {
  left: max(1rem, calc((100vw - 112rem) / 2 + 1rem));
}

.gallery-nav-next {
  right: max(1rem, calc((100vw - 112rem) / 2 + 1rem));
}

.gallery-nav span {
  font-size: 1.35rem;
  line-height: 1;
}

@keyframes gallery-photo-enter-left-strong {
  0% {
    opacity: 0;
    transform: translate3d(var(--photo-enter-x), 0.9rem, 0) scale(0.74) rotateZ(-8deg);
    filter: blur(18px) saturate(0.6) brightness(0.7);
  }

  52% {
    opacity: 1;
    transform: translate3d(1.8rem, 0, 0) scale(1.055) rotateZ(1.5deg);
    filter: blur(0) saturate(1.05) brightness(1.04);
  }

  100% {
    opacity: 1;
    transform: translate3d(0, 0, 0) scale(1) rotateZ(0deg);
    filter: blur(0) saturate(1) brightness(1);
  }
}

@keyframes gallery-photo-settle-left {
  0% {
    transform: scale(1.18);
    filter: saturate(0.78) contrast(0.9);
  }

  100% {
    transform: scale(1.015);
    filter: saturate(1) contrast(1);
  }
}

@keyframes gallery-caption-enter-right-strong {
  0% {
    opacity: 0;
    transform: translate3d(var(--caption-enter-x), 0.7rem, 0) scale(0.88);
    filter: blur(16px);
  }

  58% {
    opacity: 1;
    transform: translate3d(-1rem, 0, 0) scale(1.025);
    filter: blur(0);
  }

  100% {
    opacity: 1;
    transform: translate3d(0, 0, 0) scale(1);
    filter: blur(0);
  }
}

@keyframes gallery-caption-text-enter {
  0% {
    opacity: 0;
    transform: translate3d(1.8rem, 0.2rem, 0);
  }

  100% {
    opacity: 1;
    transform: translate3d(0, 0, 0);
  }
}

@keyframes gallery-ring-drift {
  from {
    transform: rotate(9deg);
  }

  to {
    transform: rotate(369deg);
  }
}

@media (max-width: 760px) {
  .gallery-stage {
    --photo-enter-x: -40vw;
    --caption-enter-x: 72vw;
  }

  .gallery-showcase {
    padding: 4rem 0 3.25rem;
  }

  .gallery-copy {
    margin-bottom: 1rem;
  }

  .gallery-slide {
    width: min(73.8vw, 19.8rem);
    height: 25.2rem;
    opacity: 0.2;
  }

  .gallery-slide.swiper-slide-prev,
  .gallery-slide.swiper-slide-next {
    opacity: 0.46;
    transform: scale(0.82) rotateZ(0deg) rotateY(0deg) translateZ(0);
    transform-origin: center;
  }

  .gallery-slide.swiper-slide-active .image-frame {
    width: min(70.2vw, 18.45rem);
    height: min(70.2vw, 18.45rem);
  }

  .slide-caption {
    right: 1.25rem;
    bottom: 1.25rem;
    left: 1.25rem;
    padding: 0.45rem 0.75rem;
  }

  .slide-caption p {
    max-width: 14rem;
  }

  .gallery-nav {
    top: auto;
    bottom: 0.15rem;
    width: 2.75rem;
    height: 2.75rem;
    transform: none;
  }

  .gallery-nav:hover,
  .gallery-nav:focus-visible {
    transform: scale(1.06);
  }

  .gallery-nav-prev {
    left: calc(50% - 3.4rem);
  }

  .gallery-nav-next {
    right: calc(50% - 3.4rem);
  }
}

@media (max-width: 430px) {
  .gallery-stage {
    --photo-enter-x: -36vw;
    --caption-enter-x: 64vw;
  }

  .gallery-slide {
    height: 21.6rem;
  }

  .gallery-slide.swiper-slide-active .image-frame {
    width: min(73.8vw, 16.2rem);
    height: min(73.8vw, 16.2rem);
  }

  .slide-caption h3 {
    font-size: 1.22rem;
  }

  .slide-caption p {
    font-size: 0.74rem;
  }
}

@media (prefers-reduced-motion: reduce) {
  .gallery-slide,
  .image-frame,
  .image-frame img,
  .slide-caption,
  .slide-caption h3,
  .slide-caption p,
  .gallery-slide.swiper-slide-active .image-frame,
  .gallery-slide.swiper-slide-active .image-frame img,
  .gallery-slide.swiper-slide-active .image-frame::after {
    animation: none;
    transition-duration: 1ms;
  }

  .gallery-slide.swiper-slide-active .image-frame,
  .gallery-slide.swiper-slide-active .slide-caption,
  .gallery-slide.swiper-slide-active .slide-caption h3,
  .gallery-slide.swiper-slide-active .slide-caption p {
    opacity: 1;
    transform: none;
    filter: none;
  }
}
</style>