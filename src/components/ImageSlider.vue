
<template>
  <section id="gallery">
    <div class="section-title">
      <h2>Gallery</h2>
      <p>A glimpse into our world of craft and ambiance.</p>
    </div>
    <div class="gallery-container">
      <!-- Main Swiper -->
      <div class="swiper main-swiper" ref="mainSwiperContainer">
        <div class="swiper-wrapper">
          <div class="swiper-slide" v-for="(slide, index) in slides" :key="index">
            <img :src="slide.image" :alt="slide.title" />
            <div class="slide-caption">
              <h3>{{ slide.title }}</h3>
              <p>{{ slide.description }}</p>
            </div>
          </div>
        </div>
        <div class="swiper-button-prev" role="button" aria-label="Previous slide" tabindex="0"></div>
        <div class="swiper-button-next" role="button" aria-label="Next slide" tabindex="0"></div>
      </div>

      <!-- Thumbs Swiper -->
      <div class="swiper thumbs-swiper" ref="thumbsSwiperContainer">
        <div class="swiper-wrapper">
          <div class="swiper-slide"
               v-for="(slide, index) in slides"
               :key="index"
               role="button"
               tabindex="0"
               :aria-label="`Go to slide ${index + 1}`"
               @keydown.enter.prevent="$event.target.click()"
               @keydown.space.prevent="$event.target.click()">
            <img :src="slide.image" :alt="slide.title" />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import Swiper from 'swiper';
import { Navigation, Thumbs, EffectFade } from 'swiper/modules';
import 'swiper/css';
import 'swiper/css/navigation';
import 'swiper/css/effect-fade';

const mainSwiperContainer = ref(null);
const thumbsSwiperContainer = ref(null);
let mainSwiper = null;
let thumbsSwiper = null;

const slides = [
  {
    image: '/images/Beef With Yu.jpg',
    title: 'Beef With Yu',
    description: 'Beef shanks braised in master stock, served in slices'
  },
  {
    image: '/images/Ha Gao.jpg',
    title: 'Ha Gao',
    description: '4 pieces, shrimps, water chestnuts'
  },
  {
    image: '/images/Karaage Chicken.jpg',
    title: 'Karaage Chicken',
    description: 'available with siracha glaze or Ziu-Yim spices served with wild garlic-lime mayo'
  },
  {
    image: '/images/Shrimp & Wild Garlic Gyoza.jpg',
    title: 'Shrimp & Wild Garlic Gyoza',
    description: '5 pieces, shrimps, water chestnut, wild garlic'
  },
  {
    image: '/images/Siu Mai.jpg',
    title: 'Siu Mai',
    description: '4 pieces, shrimps, chicken, shiitake'
  },
  {
    image: '/images/Sou Gao.jpg',
    title: 'Sou Gao',
    description: '4 pieces, vegetables, peanuts, shiitake, vegan mince'
  },
  {
    image: '/images/Squid Yu-Style.jpg',
    title: 'Squid Yu-Style',
    description: 'squid braised in green tea & spices mixture, served in slices'
  },
  {
    image: '/images/Tofu Skin Rolls.jpg',
    title: 'Tofu Skin Rolls',
    description: '3 pieces, vegetables, mushrooms, glass noodles, vegan mince, mushroom sauce'
  },
  {
    image: '/images/Group.jpg',
    title: 'The Yu\'s Cottage Team',
    description: 'The talented team behind the flavors.'
  }
];

onMounted(() => {
  if (mainSwiperContainer.value && thumbsSwiperContainer.value) {
    thumbsSwiper = new Swiper(thumbsSwiperContainer.value, {
      loop: true,
      spaceBetween: 10,
      slidesPerView: 3,
      freeMode: true,
      watchSlidesProgress: true,
    });

    mainSwiper = new Swiper(mainSwiperContainer.value, {
      modules: [Navigation, Thumbs, EffectFade],
      loop: true,
      effect: 'fade',
      speed: 600,
      fadeEffect: {
        crossFade: true
      },
      spaceBetween: 10,
      navigation: {
        nextEl: '.swiper-button-next',
        prevEl: '.swiper-button-prev',
      },
      thumbs: {
        swiper: thumbsSwiper,
      },
    });
  }
});
</script>

<style scoped>
#gallery {
  padding: 60px 0;
  background: #0c0c0c;
  background-image: url('/noise.png');
}

.section-title {
  max-width: 500px;
  margin: 0 auto 40px auto;
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
  font-weight: bold;
  margin-bottom: 20px;
  padding-bottom: 20px;
  position: relative;
  font-family: "Playfair Display", serif;
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

.gallery-container {
  width: 90%;
  max-width: 1200px;
  margin: auto;
  position: relative;
}

.main-swiper {
  width: 100%;
  height: 60vh;
  border-radius: 15px;
  overflow: hidden;
}

.main-swiper .swiper-slide-active .slide-caption {
  opacity: 1;
  transform: translateY(0);
  transition-delay: 0.5s;
}

.main-swiper .swiper-slide img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 1s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  transform: scale(1.1);
}

.main-swiper .swiper-slide-active img {
    transform: scale(1);
}

.slide-caption {
  position: absolute;
  bottom: 30px;
  left: 30px;
  width: auto;
  max-width: 60%;
  background: rgba(30, 30, 30, 0.6);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3), 0 0 15px rgba(230, 192, 133, 0.1);
  color: white;
  padding: 20px 25px;
  text-align: left;
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.4s ease, transform 0.4s ease;
}

.slide-caption h3 {
  font-family: 'Playfair Display', serif;
  font-size: 22px;
  margin: 0 0 5px 0;
  color: var(--primary-color);
  font-weight: 700;
}

.slide-caption p {
  font-family: 'Poppins', sans-serif;
  font-size: 14px;
  margin: 0;
  color: var(--secondary-color);
}

.swiper-button-next,
.swiper-button-prev {
  width: 44px;
  height: 44px;
  background: rgba(30, 30, 30, 0.6);
  backdrop-filter: blur(5px);
  -webkit-backdrop-filter: blur(5px);
  border-radius: 50%;
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
  transition: all 0.3s ease;
  color: var(--primary-color);
}

.swiper-button-next:hover,
.swiper-button-prev:hover {
  background: rgba(230, 192, 133, 0.2);
  transform: scale(1.1);
}

.swiper-button-next::after,
.swiper-button-prev::after {
  font-size: 18px;
  font-weight: 900;
}

.swiper-button-prev {
  left: 20px;
}

.swiper-button-next {
  right: 20px;
}

.thumbs-swiper {
  position: absolute;
  right: 20px;
  bottom: 20px;
  width: 260px;
  height: 80px;
  z-index: 10;
}

.thumbs-swiper .swiper-slide {
  width: 80px;
  height: 80px;
  border-radius: 6px;
  overflow: hidden;
  cursor: pointer;
  opacity: 0.5;
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.thumbs-swiper .swiper-slide:nth-of-type(3n+1) { transform: scale(1); }
.thumbs-swiper .swiper-slide:nth-of-type(3n+2) { transform: scale(0.9); }
.thumbs-swiper .swiper-slide:nth-of-type(3n+3) { transform: scale(0.8); }

.thumbs-swiper .swiper-slide-thumb-active {
  opacity: 1;
  border: 2px solid var(--primary-color);
  transform: scale(1.1);
}

.thumbs-swiper .swiper-slide img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

@media (max-width: 768px) {
  .main-swiper {
    height: 50vh;
  }

  .swiper-button-next,
  .swiper-button-prev {
    display: none;
  }

  .slide-caption {
    opacity: 1; 
    transform: translateY(0);
    position: absolute;
    left: 0;
    bottom: 0;
    max-width: 100%;
    border-radius: 0;
    background: rgba(0,0,0,0.6);
    backdrop-filter: none;
    box-shadow: none;
    padding: 15px;
  }

  .thumbs-swiper {
    position: relative;
    right: auto;
    bottom: auto;
    width: 100%;
    height: auto;
    margin-top: 15px;
    padding: 0 10px;
  }

  .thumbs-swiper .swiper-slide {
    height: 100px;
  }
}
</style>
