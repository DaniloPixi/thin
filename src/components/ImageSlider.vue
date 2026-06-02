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
          <article
            class="swiper-slide gallery-slide"
            v-for="(slide, index) in slides"
            :key="slide.title"
          >
            <div class="image-frame">
              <img :src="slide.image" :alt="slide.title" />
              <span class="image-shine" aria-hidden="true"></span>
            </div>

            <div class="slide-caption">
              <h3>{{ slide.title }}</h3>
              <p>{{ slide.description }}</p>

              <div class="slide-meta" aria-hidden="true">
                <span>{{ formatSlideNumber(index + 1) }}</span>
                <span class="slide-progress">
                  <span :style="{ width: `${((index + 1) / slides.length) * 100}%` }"></span>
                </span>
                <span>{{ formatSlideNumber(slides.length) }}</span>
              </div>
            </div>
          </article>
        </div>
      </div>

      <button class="gallery-nav gallery-nav-prev" type="button" aria-label="Previous gallery image">
        <span class="gallery-nav-orbit" aria-hidden="true"></span>
        <span class="gallery-nav-icon" aria-hidden="true"></span>
      </button>
      <button class="gallery-nav gallery-nav-next" type="button" aria-label="Next gallery image">
        <span class="gallery-nav-orbit" aria-hidden="true"></span>
        <span class="gallery-nav-icon" aria-hidden="true"></span>
      </button>
    </div>
  </section>
</template>

<script setup>
import { ref, onBeforeUnmount, onMounted } from 'vue';
import Swiper from 'swiper';
import { A11y, Autoplay, EffectCreative, Keyboard, Navigation } from 'swiper/modules';
import 'swiper/css';
import 'swiper/css/navigation';
import 'swiper/css/effect-creative';

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

const formatSlideNumber = (number) => String(number).padStart(2, '0');

onMounted(() => {
  if (!gallerySwiperContainer.value) {
    return;
  }

  gallerySwiper = new Swiper(gallerySwiperContainer.value, {
    modules: [A11y, Autoplay, EffectCreative, Keyboard, Navigation],
    loop: true,
    centeredSlides: true,
    grabCursor: true,
    initialSlide: 1,
    slidesPerView: 'auto',
    spaceBetween: 18,
    speed: 950,
    effect: 'creative',
    creativeEffect: {
      limitProgress: 2,
      prev: {
        translate: ['-42%', 0, -220],
        rotate: [0, 0, -8],
        opacity: 0.42
      },
      next: {
        translate: ['42%', 0, -220],
        rotate: [0, 0, 8],
        opacity: 0.34
      }
    },
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
  padding: clamp(3.35rem, 6.8vw, 5.8rem) 0 clamp(4rem, 7vw, 6rem);
  background:
    radial-gradient(ellipse at 34% 45%, rgba(255, 244, 220, 0.1), transparent 34rem),
    radial-gradient(ellipse at 34% 55%, rgba(231, 140, 3, 0.12), transparent 38rem),
    radial-gradient(ellipse at 50% 43%, rgba(159, 197, 166, 0.12), transparent 30rem),
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
    linear-gradient(90deg, #080908 0%, rgba(8, 9, 8, 0.6) 7%, transparent 22%, transparent 78%, rgba(8, 9, 8, 0.6) 93%, #080908 100%),
    radial-gradient(ellipse at center, transparent 48%, rgba(0, 0, 0, 0.58) 100%);
}

.gallery-showcase::after {
  opacity: 0.36;
  background-image:
    linear-gradient(rgba(255, 255, 255, 0.025) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255, 255, 255, 0.02) 1px, transparent 1px);
  background-size: 44px 44px;
  mask-image: radial-gradient(circle at center, black, transparent 78%);
}

.gallery-copy {
  width: min(90vw, 28rem);
  margin: 0 auto clamp(0.45rem, 1.4vw, 0.95rem);
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
  margin: 0.82rem auto 0;
  color: rgba(255, 255, 255, 0.68);
  font-family: 'Poppins', sans-serif;
  font-size: clamp(0.9rem, 1.6vw, 1rem);
  line-height: 1.65;
}

.gallery-stage {
  --photo-enter-x: -48vw;
  --caption-enter-x: -48vw;
  --caption-panel-delay: 2000ms;
  --caption-title-delay: 2180ms;
  --caption-copy-delay: 2320ms;
  --caption-meta-delay: 2460ms;
  --premium-ease: cubic-bezier(0.16, 1, 0.3, 1);
  --soft-ease: cubic-bezier(0.22, 1, 0.36, 1);

  position: relative;
  width: min(100%, 118rem);
  margin: 0 auto;
}

.gallery-stage::before {
  content: '';
  position: absolute;
  left: 32%;
  top: 48%;
  z-index: -1;
  width: clamp(14rem, 31vw, 31rem);
  height: clamp(30rem, 64vw, 58rem);
  border-radius: 52% 48% 50% 50%;
  background:
    radial-gradient(ellipse at 50% 24%, rgba(255, 244, 220, 0.16), transparent 25%),
    radial-gradient(ellipse at 52% 50%, rgba(230, 192, 133, 0.16), transparent 47%),
    radial-gradient(ellipse at 50% 76%, rgba(164, 208, 173, 0.12), transparent 68%);
  filter: blur(58px);
  opacity: 0.95;
  transform: translate(-50%, -50%);
  pointer-events: none;
}

.gallery-swiper {
  overflow: visible;
  width: 100%;
  perspective: 64rem;
  perspective-origin: center;
  padding: 0 0 clamp(2.8rem, 4vw, 3.8rem);
}

.gallery-slide {
  position: relative;
  display: grid;
  grid-template-columns: minmax(14rem, 24.3rem) minmax(16rem, 24rem);
  align-items: center;
  justify-content: center;
  gap: clamp(1.2rem, 3vw, 3.2rem);
  width: min(88vw, 56rem);
  min-height: clamp(18rem, 34vw, 27rem);
  opacity: 0.18;
  transform-style: preserve-3d;
  filter: blur(2px) saturate(0.48) brightness(0.52);
  backface-visibility: hidden;
  will-change: transform, opacity, filter;
  transition:
    opacity 800ms var(--soft-ease),
    transform 950ms var(--soft-ease),
    filter 800ms var(--soft-ease);
}

.gallery-slide::before {
  content: '';
  position: absolute;
  left: 31.5%;
  top: 50%;
  z-index: -2;
  width: clamp(14rem, 34vw, 32rem);
  height: clamp(34rem, 72vw, 62rem);
  border-radius: 50% 50% 48% 52%;
  opacity: 0;
  filter: blur(54px);
  transform: translate(-50%, -50%) scaleY(0.72) scaleX(0.86);
  transition:
    opacity 900ms var(--soft-ease),
    transform 1200ms var(--soft-ease);
  pointer-events: none;
}

.gallery-slide::after {
  content: '';
  position: absolute;
  left: 31%;
  top: 78%;
  z-index: -1;
  width: clamp(9rem, 20vw, 18rem);
  height: clamp(1.8rem, 4vw, 3.4rem);
  border-radius: 50%;
  background: rgba(0, 0, 0, 0.48);
  opacity: 0;
  filter: blur(18px);
  transform: translate(-50%, -50%) scale(0.72);
  transition:
    opacity 900ms var(--soft-ease),
    transform 1100ms var(--soft-ease);
  pointer-events: none;
}

.gallery-slide.swiper-slide-prev {
  opacity: 0.38;
  filter: blur(0.75px) saturate(0.62) brightness(0.62);
}

.gallery-slide.swiper-slide-next {
  opacity: 0.3;
  filter: blur(1.2px) saturate(0.45) brightness(0.42);
}

.gallery-slide.swiper-slide-next .image-frame {
  transform: scale(0.86);
}

.gallery-slide.swiper-slide-next .image-frame img {
  transform: scale(1.06);
  filter: brightness(0.48) saturate(0.5) contrast(0.92);
}

.gallery-slide.swiper-slide-next .image-frame::before,
.gallery-slide.swiper-slide-next .image-frame::after,
.gallery-slide.swiper-slide-next .image-shine {
  opacity: 0;
}

.gallery-slide.swiper-slide-active {
  z-index: 3;
  opacity: 1;
  filter: none;
}

.gallery-slide.swiper-slide-active::before {
  opacity: 1;
  transform: translate(-50%, -50%) scaleY(1) scaleX(1);
  animation: gallery-aura-breathe 6.5s ease-in-out 1.1s infinite alternate;
}

.gallery-slide.swiper-slide-active::after {
  opacity: 0.78;
  transform: translate(-50%, -50%) scale(1);
}

.image-frame {
  position: relative;
  overflow: visible;
  width: clamp(15.3rem, 30.6vw, 24.3rem);
  height: clamp(15.3rem, 30.6vw, 24.3rem);
  justify-self: end;
  border: 0;
  border-radius: 50%;
  background: transparent;
  transform: scale(0.92);
  transform-origin: center;
  transform-style: preserve-3d;
  backface-visibility: hidden;
  will-change: transform, filter, opacity;
  transition:
    transform 950ms var(--soft-ease),
    filter 800ms ease,
    opacity 800ms ease;
}

.gallery-slide.swiper-slide-active .image-frame {
  animation: gallery-photo-enter-left 1150ms var(--premium-ease) both;
}

.image-frame::after {
  content: '';
  position: absolute;
  inset: -4.4rem -1.2rem;
  z-index: -1;
  border-radius: 52% 48% 50% 50%;
  pointer-events: none;
  opacity: 0;
  filter: blur(38px);
  transform: scaleY(0.72) scaleX(0.9);
  transition:
    opacity 900ms var(--soft-ease),
    transform 1200ms var(--soft-ease);
}

.gallery-slide.swiper-slide-active .image-frame::after {
  opacity: 1;
  transform: scaleY(1.18) scaleX(1);
}

.image-frame::before {
  content: '';
  position: absolute;
  inset: -0.38rem;
  z-index: 2;
  border-radius: 50%;
  pointer-events: none;
  background:
    conic-gradient(
      from 212deg,
      transparent 0 6%,
      rgba(255, 244, 220, 0.82) 10%,
      rgba(230, 192, 133, 0.48) 19%,
      rgba(255, 255, 255, 0.18) 27%,
      transparent 42% 100%
    );
  -webkit-mask:
    radial-gradient(
      farthest-side,
      transparent calc(100% - 0.34rem),
      #000 calc(100% - 0.31rem),
      #000 calc(100% - 0.05rem),
      transparent 100%
    );
  mask:
    radial-gradient(
      farthest-side,
      transparent calc(100% - 0.34rem),
      #000 calc(100% - 0.31rem),
      #000 calc(100% - 0.05rem),
      transparent 100%
    );
  opacity: 0;
  filter:
    blur(0.9px)
    drop-shadow(0 0 0.7rem rgba(255, 244, 220, 0.3))
    drop-shadow(0 0 1.35rem rgba(230, 192, 133, 0.2));
  transform: rotate(-9deg);
  transition:
    opacity 800ms ease,
    transform 1100ms var(--soft-ease);
}

.gallery-slide.swiper-slide-active .image-frame::before {
  opacity: 1;
  transform: rotate(0deg);
}

.image-frame img {
  position: relative;
  z-index: 1;
  display: block;
  width: 100%;
  height: 100%;
  border-radius: inherit;
  object-fit: cover;
  transform: scale(1.08);
  box-shadow:
    0 2rem 5.2rem rgba(0, 0, 0, 0.76),
    0 0 2.6rem rgba(230, 192, 133, 0.16),
    0 0 0 1px rgba(255, 244, 220, 0.22),
    inset 0 0 0 1px rgba(255, 244, 220, 0.18);
  will-change: transform, filter;
  transition:
    transform 1300ms var(--soft-ease),
    filter 900ms ease,
    box-shadow 900ms var(--soft-ease);
}

.gallery-slide.swiper-slide-prev .image-frame img {
  transform: scale(1.045);
  filter: brightness(0.68) saturate(0.68) contrast(0.94);
}

.gallery-slide.swiper-slide-active .image-frame img {
  transform: scale(1.015);
  filter: none;
  animation: gallery-photo-settle 1500ms var(--soft-ease) both;
}

.image-shine {
  position: absolute;
  inset: -0.15rem;
  z-index: 3;
  border-radius: inherit;
  pointer-events: none;
  background:
    radial-gradient(circle at 28% 20%, rgba(255, 255, 255, 0.28), transparent 24%),
    radial-gradient(circle at 40% 32%, rgba(255, 244, 220, 0.16), transparent 36%),
    linear-gradient(
      135deg,
      rgba(255, 244, 220, 0.36) 0%,
      rgba(255, 244, 220, 0.16) 15%,
      transparent 34%,
      transparent 100%
    );
  opacity: 0;
  filter: blur(0.45px);
  mix-blend-mode: screen;
}

.gallery-slide.swiper-slide-active .image-shine {
  animation: gallery-ceramic-highlight 1300ms var(--soft-ease) 300ms both;
}

.gallery-swiper:active .swiper-slide-active .image-frame {
  transform: scale(0.985);
}

.slide-caption {
  position: relative;
  z-index: 4;
  justify-self: start;
  width: min(100%, 24rem);
  color: #fff;
  padding: clamp(1.15rem, 2.5vw, 1.65rem);
  border: 0;
  border-top: 1px solid rgba(255, 255, 255, 0.2);
  border-left: 1px solid rgba(255, 255, 255, 0.18);
  border-radius: 1.3rem;
  background:
    linear-gradient(135deg, rgba(255, 255, 255, 0.12) 0%, rgba(255, 255, 255, 0.045) 42%, rgba(255, 255, 255, 0) 100%),
    linear-gradient(90deg, rgba(7, 12, 10, 0.72) 0%, rgba(7, 12, 10, 0.48) 48%, rgba(7, 12, 10, 0.18) 78%, rgba(7, 12, 10, 0) 100%);
  box-shadow:
    0 1.3rem 3.2rem rgba(0, 0, 0, 0.28),
    inset 1px 1px 0 rgba(255, 255, 255, 0.12);
  backdrop-filter: blur(14px);
  -webkit-backdrop-filter: blur(14px);
  text-shadow: 0 0.2rem 0.8rem rgba(0, 0, 0, 0.9);
  opacity: 0;
  transform: translate3d(-1.2rem, 0.9rem, 0) scale(0.96);
  filter: blur(14px) saturate(0.82) brightness(0.78);
  will-change: opacity, transform, filter;
}

.gallery-slide.swiper-slide-active .slide-caption {
  animation: gallery-caption-enter-left 950ms var(--premium-ease) var(--caption-panel-delay) both;
}

.slide-caption h3 {
  margin: 0;
  color: #78b68e;
  font-family: 'Cormorant Garamond', 'Playfair Display', Georgia, serif;
  font-weight: 300;
  font-size: clamp(1.6rem, 3vw, 2.85rem);
  line-height: 0.92;
  text-wrap: balance;
  opacity: 0;
  transform: translate3d(0, 0.65rem, 0);
  will-change: opacity, transform;
}

.slide-caption p {
  max-width: 19rem;
  margin: 0.7rem 0 0;
  color: rgba(255, 255, 255, 0.76);
  font-family: 'Poppins', sans-serif;
  font-size: clamp(0.82rem, 1vw, 0.95rem);
  line-height: 1.55;
  opacity: 0;
  transform: translate3d(0, 0.65rem, 0);
  will-change: opacity, transform;
}

.gallery-slide.swiper-slide-active .slide-caption h3 {
  animation: gallery-caption-text-enter 650ms var(--premium-ease) var(--caption-title-delay) both;
}

.gallery-slide.swiper-slide-active .slide-caption p {
  animation: gallery-caption-text-enter 650ms var(--premium-ease) var(--caption-copy-delay) both;
}

.slide-meta {
  display: grid;
  grid-template-columns: auto 1fr auto;
  align-items: center;
  gap: 0.85rem;
  margin-top: 1.2rem;
  color: rgba(247, 234, 216, 0.74);
  font-family: 'Poppins', sans-serif;
  font-size: 0.72rem;
  font-weight: 600;
  letter-spacing: 0.18em;
  opacity: 0;
  transform: translateY(0.45rem);
  will-change: opacity, transform;
}

.gallery-slide.swiper-slide-active .slide-meta {
  animation: gallery-caption-text-enter 650ms var(--premium-ease) var(--caption-meta-delay) both;
}

.slide-progress {
  position: relative;
  display: block;
  height: 1px;
  overflow: hidden;
  background: rgba(255, 255, 255, 0.18);
}

.slide-progress span {
  position: absolute;
  inset: 0 auto 0 0;
  display: block;
  background: linear-gradient(90deg, #78b68e, #e6c085);
  transform-origin: left;
}

.gallery-nav {
  --nav-size: 3.45rem;
  --nav-arrow-offset: 0.12rem;

  position: absolute;
  top: 50%;
  z-index: 6;
  display: grid;
  place-items: center;
  width: var(--nav-size);
  height: var(--nav-size);
  border: 0;
  border-radius: 50%;
  background:
    radial-gradient(circle at 32% 24%, rgba(255, 255, 255, 0.16), transparent 34%),
    linear-gradient(145deg, rgba(255, 255, 255, 0.075), rgba(255, 255, 255, 0.018) 48%, rgba(0, 0, 0, 0.16)),
    rgba(5, 8, 7, 0.46);
  color: #fff4df;
  cursor: pointer;
  isolation: isolate;
  transform: translateY(-50%);
  box-shadow:
    0 1rem 2.4rem rgba(0, 0, 0, 0.42),
    0 0 1.7rem rgba(230, 192, 133, 0.09),
    inset 0 0 0 1px rgba(255, 244, 220, 0.1),
    inset 0.18rem 0.18rem 0.75rem rgba(255, 255, 255, 0.045),
    inset -0.35rem -0.4rem 1rem rgba(0, 0, 0, 0.3);
  backdrop-filter: blur(14px);
  -webkit-backdrop-filter: blur(14px);
  transition:
    background 460ms ease,
    box-shadow 520ms ease,
    color 320ms ease,
    filter 520ms ease,
    transform 520ms var(--soft-ease);
}

.gallery-nav-orbit {
  position: absolute;
  inset: -0.42rem;
  z-index: -1;
  border-radius: inherit;
  background:
    conic-gradient(
      from 214deg,
      transparent 0 10%,
      rgba(255, 244, 220, 0.95) 13%,
      rgba(230, 192, 133, 0.78) 22%,
      rgba(164, 208, 173, 0.34) 31%,
      transparent 43% 100%
    );
  -webkit-mask:
    radial-gradient(
      farthest-side,
      transparent calc(100% - 0.12rem),
      #000 calc(100% - 0.1rem),
      #000 calc(100% - 0.015rem),
      transparent 100%
    );
  mask:
    radial-gradient(
      farthest-side,
      transparent calc(100% - 0.12rem),
      #000 calc(100% - 0.1rem),
      #000 calc(100% - 0.015rem),
      transparent 100%
    );
  opacity: 0.72;
  filter:
    blur(0.35px)
    drop-shadow(0 0 0.55rem rgba(230, 192, 133, 0.22));
  transform: rotate(-18deg) scale(0.96);
  transform-origin: 50% 50%;
  pointer-events: none;
  will-change: transform, opacity, filter;
}

.gallery-nav::after {
  content: '';
  position: absolute;
  inset: 0.38rem;
  z-index: -1;
  border-radius: inherit;
  background:
    linear-gradient(135deg, rgba(255, 244, 220, 0.12), transparent 38%),
    radial-gradient(circle at 50% 72%, rgba(164, 208, 173, 0.12), transparent 56%);
  box-shadow:
    inset 0 0 0 1px rgba(230, 192, 133, 0.14),
    inset 0 0 1rem rgba(255, 244, 220, 0.035);
  opacity: 0.9;
  transition:
    opacity 460ms ease,
    transform 640ms var(--soft-ease);
  pointer-events: none;
}

.gallery-nav:hover,
.gallery-nav:focus-visible {
  color: #fffaf0;
  outline: none;
  filter: saturate(1.08) brightness(1.08);
  transform: translateY(-50%) scale(1.045);
  box-shadow:
    0 1.2rem 2.8rem rgba(0, 0, 0, 0.46),
    0 0 2.35rem rgba(230, 192, 133, 0.18),
    0 0 0 1px rgba(255, 244, 220, 0.12),
    inset 0 0 0 1px rgba(255, 244, 220, 0.16),
    inset 0.18rem 0.18rem 0.75rem rgba(255, 255, 255, 0.07),
    inset -0.35rem -0.4rem 1rem rgba(0, 0, 0, 0.32);
}

.gallery-nav:hover .gallery-nav-orbit,
.gallery-nav:focus-visible .gallery-nav-orbit {
  animation: gallery-nav-orbit-sweep 1800ms cubic-bezier(0.16, 1, 0.3, 1) both;
}

.gallery-nav:hover::after,
.gallery-nav:focus-visible::after {
  opacity: 1;
  transform: scale(0.94);
}

.gallery-nav-prev {
  left: max(1rem, calc((100vw - 112rem) / 2 + 1rem));
}

.gallery-nav-next {
  right: max(1rem, calc((100vw - 112rem) / 2 + 1rem));
}

.gallery-nav-icon {
  position: relative;
  z-index: 1;
  display: block;
  width: 0.68rem;
  height: 0.68rem;
  border-top: 1px solid currentColor;
  border-right: 1px solid currentColor;
  filter:
    drop-shadow(0 0 0.3rem rgba(255, 244, 220, 0.28))
    drop-shadow(0 0 0.65rem rgba(230, 192, 133, 0.18));
  transition:
    filter 320ms ease,
    transform 460ms var(--soft-ease);
}

.gallery-nav-prev .gallery-nav-icon {
  transform: translateX(var(--nav-arrow-offset)) rotate(-135deg);
}

.gallery-nav-next .gallery-nav-icon {
  transform: translateX(calc(var(--nav-arrow-offset) * -1)) rotate(45deg);
}

.gallery-nav-prev:hover .gallery-nav-icon,
.gallery-nav-prev:focus-visible .gallery-nav-icon {
  transform: translateX(calc(var(--nav-arrow-offset) - 0.12rem)) rotate(-135deg);
}

.gallery-nav-next:hover .gallery-nav-icon,
.gallery-nav-next:focus-visible .gallery-nav-icon {
  transform: translateX(calc((var(--nav-arrow-offset) * -1) + 0.12rem)) rotate(45deg);
}

.gallery-nav:hover .gallery-nav-icon,
.gallery-nav:focus-visible .gallery-nav-icon {
  filter:
    drop-shadow(0 0 0.42rem rgba(255, 244, 220, 0.45))
    drop-shadow(0 0 0.9rem rgba(230, 192, 133, 0.28));
}

.gallery-nav.swiper-button-disabled {
  opacity: 0.42;
  cursor: default;
  pointer-events: none;
}

@keyframes gallery-nav-orbit-sweep {
  0% {
    opacity: 0.72;
    filter:
      blur(0.35px)
      drop-shadow(0 0 0.55rem rgba(230, 192, 133, 0.22));
    transform: rotate(-18deg) scale(0.96);
  }

  100% {
    opacity: 1;
    filter:
      blur(0.15px)
      drop-shadow(0 0 0.85rem rgba(230, 192, 133, 0.34))
      drop-shadow(0 0 1.35rem rgba(255, 244, 220, 0.16));
    transform: rotate(142deg) scale(1);
  }
}

@keyframes gallery-photo-enter-left {
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

@keyframes gallery-caption-enter-left {
  0% {
    opacity: 0;
    transform: translate3d(-1.2rem, 0.9rem, 0) scale(0.96);
    filter: blur(14px) saturate(0.82) brightness(0.78);
  }

  68% {
    opacity: 1;
    transform: translate3d(0.15rem, -0.05rem, 0) scale(1.012);
    filter: blur(1.5px) saturate(1.03) brightness(1.02);
  }

  100% {
    opacity: 1;
    transform: translate3d(0, 0, 0) scale(1);
    filter: blur(0) saturate(1) brightness(1);
  }
}

@keyframes gallery-photo-settle {
  0% {
    transform: scale(1.18);
    filter: saturate(0.78) contrast(0.9);
  }

  100% {
    transform: scale(1.015);
    filter: saturate(1) contrast(1);
  }
}

@keyframes gallery-caption-text-enter {
  0% {
    opacity: 0;
    transform: translate3d(0, 0.65rem, 0);
  }

  100% {
    opacity: 1;
    transform: translate3d(0, 0, 0);
  }
}

@keyframes gallery-ceramic-highlight {
  0% {
    opacity: 0;
    transform: scale(0.98);
  }

  100% {
    opacity: 0.98;
    transform: scale(1);
  }
}

@keyframes gallery-aura-breathe {
  from {
    opacity: 0.78;
    filter: blur(54px);
  }

  to {
    opacity: 1;
    filter: blur(68px);
  }
}

@media (max-width: 900px) {
  .gallery-slide {
    grid-template-columns: 1fr;
    gap: 0.85rem;
    width: min(82vw, 31rem);
    min-height: 33rem;
  }

  .gallery-stage::before {
    left: 50%;
    top: 31%;
    width: clamp(16rem, 52vw, 32rem);
    height: clamp(30rem, 86vw, 52rem);
  }

  .gallery-slide::before {
    left: 50%;
    top: 31%;
  }

  .gallery-slide::after {
    left: 50%;
    top: 50%;
  }

  .image-frame,
  .slide-caption {
    justify-self: center;
  }

  .slide-caption {
    text-align: center;
  }

  .slide-caption p {
    margin-right: auto;
    margin-left: auto;
  }
}

@media (max-width: 760px) {
  .gallery-stage {
    --photo-enter-x: -40vw;
    --caption-enter-x: -40vw;
  }

  .gallery-showcase {
    padding: 3.5rem 0 3.25rem;
  }

  .gallery-copy {
    margin-bottom: 0.55rem;
  }

  .gallery-slide {
    width: min(84vw, 22rem);
    min-height: 31rem;
    opacity: 0.18;
  }

  .gallery-slide.swiper-slide-prev,
  .gallery-slide.swiper-slide-next {
    opacity: 0.3;
    filter: blur(1.2px) saturate(0.58) brightness(0.52);
  }

  .gallery-slide.swiper-slide-next .image-frame img {
    filter: brightness(0.52) saturate(0.58) contrast(0.92);
  }

  .image-frame {
    width: min(70.2vw, 18.45rem);
    height: min(70.2vw, 18.45rem);
  }

  .slide-caption {
    width: min(100%, 19rem);
    padding: 1rem;
  }

  .slide-caption p {
    max-width: 14rem;
  }

  .gallery-nav {
    --nav-size: 2.9rem;

    top: auto;
    bottom: 0.15rem;
    transform: none;
  }

  .gallery-nav:hover,
  .gallery-nav:focus-visible {
    transform: scale(1.045);
  }

  .gallery-nav-prev {
    left: calc(50% - 3.55rem);
  }

  .gallery-nav-next {
    right: calc(50% - 3.55rem);
  }
}

@media (max-width: 430px) {
  .gallery-stage {
    --photo-enter-x: -34vw;
    --caption-enter-x: -34vw;
  }

  .gallery-slide {
    width: min(86vw, 20rem);
    min-height: 29.5rem;
  }

  .image-frame {
    width: min(73.8vw, 16.2rem);
    height: min(73.8vw, 16.2rem);
  }

  .slide-caption h3 {
    font-size: 1.55rem;
  }

  .slide-caption p {
    font-size: 0.74rem;
  }

  .slide-meta {
    gap: 0.6rem;
    font-size: 0.66rem;
  }
}

@media (prefers-reduced-motion: reduce) {
  .gallery-slide,
  .gallery-slide::before,
  .gallery-slide::after,
  .gallery-stage::before,
  .image-frame,
  .image-frame::before,
  .image-frame::after,
  .image-frame img,
  .image-shine,
  .slide-caption,
  .slide-caption h3,
  .slide-caption p,
  .slide-meta,
  .gallery-nav,
  .gallery-nav::after,
  .gallery-nav-orbit,
  .gallery-nav-icon,
  .gallery-slide.swiper-slide-active .image-frame,
  .gallery-slide.swiper-slide-active .image-frame img,
  .gallery-slide.swiper-slide-active .image-frame::before,
  .gallery-slide.swiper-slide-active .image-frame::after,
  .gallery-slide.swiper-slide-active .image-shine,
  .gallery-slide.swiper-slide-active .slide-caption,
  .gallery-slide.swiper-slide-active .slide-caption h3,
  .gallery-slide.swiper-slide-active .slide-caption p,
  .gallery-slide.swiper-slide-active .slide-meta {
    animation: none;
    transition-duration: 1ms;
  }

  .gallery-slide.swiper-slide-active .image-frame,
  .gallery-slide.swiper-slide-active .slide-caption,
  .gallery-slide.swiper-slide-active .slide-caption h3,
  .gallery-slide.swiper-slide-active .slide-caption p,
  .gallery-slide.swiper-slide-active .slide-meta {
    opacity: 1;
    transform: none;
    filter: none;
  }
}
</style>