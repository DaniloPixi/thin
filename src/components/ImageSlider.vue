<template>
  <section id="gallery" class="gallery-showcase" aria-labelledby="gallery-title">
    <div class="gallery-copy">
      <p class="eyebrow">Yu's Cottage Gallery</p>
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
    speed: 650,
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
  color: #f8efe2;
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
  position: relative;
  width: min(100%, 118rem);
  margin: 0 auto;
}

.gallery-swiper {
  overflow: visible;
  width: 100%;
  perspective: 72rem;
  perspective-origin: center;
  padding: clamp(1rem, 2vw, 2rem) 0 clamp(2.2rem, 4vw, 3.5rem);
}

.gallery-slide {
  display: flex;
  align-items: center;
  justify-content: center;
  width: min(66vw, 27rem);
  height: clamp(15rem, 32vw, 22rem);
  opacity: 0.34;
  transform: scale(0.82) rotateZ(-5deg) rotateY(-28deg) translateZ(-2rem);
  transform-style: preserve-3d;
  transition: opacity 0.55s ease, transform 0.55s ease, filter 0.55s ease;
  filter: blur(1.5px) saturate(0.78);
}

.gallery-slide.swiper-slide-prev {
  opacity: 0.72;
  transform: translateX(7%) scale(0.9) rotateZ(-5deg) rotateY(-46deg) rotateX(1.5deg) translateZ(-1.5rem);
  transform-origin: center;
  filter: blur(0) saturate(0.9);
}

.gallery-slide.swiper-slide-next {
  opacity: 0.72;
  transform: translateX(-7%) scale(0.9) rotateZ(5deg) rotateY(46deg) rotateX(1.5deg) translateZ(-1.5rem);
  transform-origin: center;
  filter: blur(0) saturate(0.9);
}

.gallery-slide.swiper-slide-active {
  z-index: 3;
  opacity: 1;
  transform: scale(1) rotateZ(0deg) rotateY(0deg) translateZ(1rem);
  filter: none;
}

.image-frame {
  position: relative;
  overflow: hidden;
  width: 100%;
  height: 82%;
  border: 1px solid rgba(255, 255, 255, 0.13);
  border-radius: 1.45rem;
  background: #111;
  box-shadow: 0 1.2rem 3.5rem rgba(0, 0, 0, 0.48), 0 0.2rem 1.1rem rgba(255, 255, 255, 0.08) inset;
  transform-origin: center;
  transform-style: preserve-3d;
  backface-visibility: hidden;
}

.gallery-slide.swiper-slide-active .image-frame {
  width: clamp(15.3rem, 30.6vw, 24.3rem);
  height: clamp(15.3rem, 30.6vw, 24.3rem);
  overflow: visible;
  border: 0;
  border-radius: 50%;
  background: transparent;
  box-shadow: none;
}

.gallery-slide.swiper-slide-active .image-frame::after {
  content: '';
  position: absolute;
  inset: -13%;
  z-index: 2;
  border-radius: 50%;
  pointer-events: none;
  background:
    conic-gradient(from 18deg, transparent 0 8%, rgba(164, 208, 173, 0.72) 10% 15%, transparent 18% 34%, rgba(164, 208, 173, 0.54) 37% 43%, transparent 47% 63%, rgba(230, 192, 133, 0.46) 66% 70%, transparent 73% 100%);
  -webkit-mask: radial-gradient(farthest-side, transparent calc(100% - 0.45rem), #000 calc(100% - 0.42rem));
  mask: radial-gradient(farthest-side, transparent calc(100% - 0.45rem), #000 calc(100% - 0.42rem));
  transform: rotate(9deg);
  opacity: 0.9;
}

.image-frame img {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.75s ease;
}

.gallery-slide.swiper-slide-active .image-frame img {
  overflow: hidden;
  border-radius: 50%;
  box-shadow: 0 1.7rem 5rem rgba(0, 0, 0, 0.85), 0 0 0 1px rgba(255, 255, 255, 0.12);
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
  padding: 0.85rem 1rem;
  border-radius: 1rem;
  background: linear-gradient(180deg, rgba(0, 0, 0, 0.04), rgba(0, 0, 0, 0.38));
  backdrop-filter: blur(3px);
  -webkit-backdrop-filter: blur(3px);
  text-shadow: 0 0.2rem 0.8rem rgba(0, 0, 0, 0.9);
}

.slide-caption h3 {
  margin: 0;
  color: #f6eadb;
  font-family: 'Cormorant Garamond', 'Playfair Display', Georgia, serif;
  font-weight: 300;
  font-size: clamp(1.18rem, 2vw, 2rem);
  line-height: 1;
}

.slide-caption p {
  max-width: 17rem;
  margin: 0.45rem auto 0;
  color: rgba(255, 255, 255, 0.76);
  font-family: 'Poppins', sans-serif;
  font-size: clamp(0.78rem, 1.2vw, 0.95rem);
  line-height: 1.45;
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
  transition: background 0.25s ease, border-color 0.25s ease, transform 0.25s ease;
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

@media (max-width: 760px) {
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
</style>