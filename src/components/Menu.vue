
<template>
  <section id="menu" class="menu-section">
    <div class="container">
      <div class="section-title">
        <h2>Our Menu</h2>
        <p>From our kitchen to your table, a symphony of flavors awaits.</p>
      </div>

      <!-- Drinks Section -->
      <div class="menu-category-section">
        <h3 class="category-title">Drinks</h3>
        <div class="menu-tabs">
          <button v-for="category in drinksCategories" :key="category" :class="{ active: activeDrinkCategory === category }" @click="activeDrinkCategory = category">
            {{ category }}
          </button>
        </div>
        <transition name="fade" mode="out-in">
          <div :key="activeDrinkCategory">
            <div v-if="useSimpleLayout" class="menu-items-list">
                <div v-for="(item, index) in activeDrinkMenuItems" :key="index" class="menu-item-list-row">
                    <div class="menu-item-list-info">
                        <h3 class="menu-item-name-list">{{ item.name }}</h3>
                        <p v-if="item.description" class="menu-item-description-list">{{ item.description }}</p>
                    </div>
                    <span class="menu-item-price-list">{{ item.price }} €</span>
                </div>
            </div>
            <div v-else class="menu-items-grid">
              <div v-for="(item, index) in activeDrinkMenuItems" :key="index" class="menu-item" :class="{ 'is-centered': !item.name }">
                <div class="menu-item-header">
                  <h3 class="menu-item-name">{{ item.name }}</h3>
                </div>
                <p class="menu-item-description">{{ item.description }}</p>
                <span v-if="item.price" class="menu-item-price">{{ item.price }} €</span>
              </div>
            </div>
          </div>
        </transition>
      </div>

      <!-- Food Section -->
      <div class="menu-category-section">
        <h3 class="category-title">Dumplings and Co</h3>
        <div class="menu-tabs">
          <button v-for="category in foodCategories" :key="category" :class="{ active: activeFoodCategory === category }" @click="activeFoodCategory = category">
            {{ category }}
          </button>
        </div>
        <transition name="fade" mode="out-in" :key="activeFoodCategory">
          <div>
            <div v-if="activeFoodCategory === 'Steamed'" class="info-label">
              served with peach sriracha
            </div>
            <div v-if="activeFoodCategory === 'Fried'" class="info-label">
              served with umami sauce
            </div>
            <div class="menu-items-grid" >
              <div v-for="(item, index) in activeFoodMenuItems" :key="index" class="menu-item" :class="{ 'is-centered': !item.name }">
                <div class="menu-item-header">
                  <h3 class="menu-item-name">{{ item.name }}</h3>
                </div>
                <p class="menu-item-description">{{ item.description }}</p>
                <span v-if="item.price" class="menu-item-price">{{ item.price }} €</span>
              </div>
            </div>
          </div>
        </transition>
      </div>

    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue';

// --- DRINKS --- 
const drinksCategories = ['Signature Cocktails', 'Classic Cocktails', 'Homemade Lemonades', 'Longdrinks', 'Beer', 'Soft Drinks', 'Tea And Coffee', 'Spritz, Aperitif, Digestif'];
const activeDrinkCategory = ref('Signature Cocktails');
const simpleDrinkCategories = ['Beer', 'Soft Drinks', 'Tea And Coffee', 'Spritz, Aperitif, Digestif'];

const drinksData = {
  'Signature Cocktails': [
    { name: 'Yu‘s Oolong Tea', price: '14', description: 'oolong tea infused Tanqueray, sake, yuzu juice, lemon juice, oolong & ginseng syrup, yuzu honey, Foamee' },
    { name: 'Blossom Dance', price: '13', description: 'Tanqueray, Peachtree, lime juice, simple syrup, peach bitters, rose water, Rose‘s Lemonade' },
    { name: 'Thai Basil Smash', price: '12', description: 'Tanqueray, lime juice, simple syrup, thai basil leaves' },
    { name: 'Puschel\'s Brew', price: '14', description: 'Tanqueray, Chambord, rice vinegar, pineapple juice, raspberry & rosemary syrup, Foamee' },
    { name: 'Four Plains Fashioned', price: '14', description: 'sichuan pepper oil fat-washed Jameson, Angostura bitters, rich sugar syrup' },
    { name: 'Jade Sailor', price: '13', description: 'Bacardi, matcha syrup, almond milk, homemade orgeat, Foamee' },
    { name: 'Me-So Salty', price: '13', description: 'sichuan peppercorn infused Finlandia, Cointreau, lemon juice, miso syrup, rich simple syrup' },
  ],
  'Classic Cocktails': [
    { name: '', price: '12', description: 'Please ask our staff for our selection of classic cocktails.' },
  ],
  'Homemade Lemonades': [
    { name: 'Oolong & Ginseng Ice Tea 0,5l', price: '5.5', description: 'oolong tea, ginseng roots, lemon juice' },
    { name: 'Raspberry & Rosemary Lemonade 0,5l', price: '5.5', description: 'raspberries, rosemary, lemon juice' },
  ],
  'Longdrinks': [
    { name: 'Raspberry & Rosemary Tonic', price: '9', description: 'Tanqueray, lime juice, raspberry & rosemary syrup, Kinley tonic' },
    { name: 'Bourbon Iced Tea', price: '9', description: 'bourbon, oolong & ginseng ice tea' },
  ],
  'Beer': [
    { name: 'Stiegl Helles', price: '4,2 | 5,1', description: '0,33l | 0,5l' },
    { name: 'Stiegl Zwickl', price: '4,2 | 5,1', description: '0,33l | 0,5l' },
    { name: 'Tsing Tao', price: '4,9', description: '0,33l' },
    { name: 'Kirin', price: '4,9', description: '0,33l' },
    { name: 'Singha', price: '4,9', description: '0,33l' },
  ],
  'Soft Drinks': [
    { name: 'Fritz Kola zero', price: '4', description: '0,33l' },
    { name: 'Makava', price: '4', description: '0,33l' },
    { name: 'Frucade', price: '4', description: '0,33l' },
    { name: 'Soda / Soda Lemon', price: '3 | 4', description: '' },
    { name: 'Apple Juice „gespritzt“', price: '3 | 4', description: '0,25l | 0,5l' },
  ],
  'Tea And Coffee': [
    { name: 'Oolong tea', price: '4,5', description: '' },
    { name: 'Pu-Erh tea', price: '4,5', description: '' },
    { name: 'Chrysanthemum tea', price: '4,2', description: '' },
    { name: 'Sencha', price: '4,2', description: '' },
    { name: 'Jasmin tea', price: '4,2', description: '' },
    { name: 'Espresso | Doppio/Americano', price: '2 | 4', description: '' },
  ],
  'Spritz, Aperitif, Digestif': [
    { name: 'White wine spritz', price: '4', description: '' },
    { name: 'Yuzu spritz', price: '5', description: '' },
    { name: 'Raspberry & Rosemary spritz', price: '6', description: '' },
    { name: 'Aperol spritz', price: '7', description: '' },
    { name: 'Hugo', price: '7', description: '' },
    { name: 'Gassan no Yuki sake 300ml', price: '21', description: '' },
    { name: 'Soju 360ml', price: '10', description: '' },
    { name: 'Ramazotti 2cl | 4cl', price: '5 | 7', description: '' },
    { name: 'Nonino Grappa 2cl | 4cl', price: '5 | 7', description: '' },
  ],
};

const activeDrinkMenuItems = computed(() => drinksData[activeDrinkCategory.value] || []);
const useSimpleLayout = computed(() => simpleDrinkCategories.includes(activeDrinkCategory.value));

// --- FOOD --- 
const foodCategories = ['Steamed', 'Fried', 'Hot Dishes', 'Cold Dishes', 'Side Dishes', 'Dessert'];
const activeFoodCategory = ref('Steamed');

const foodData = {
  'Steamed': [
    { name: 'Ha Gao (B, N)', price: '7', description: '4 pieces, shrimps, water chestnuts' },
    { name: 'Siu Mai (B, N)', price: '7', description: '4 pieces, shrimps, chicken, shiitake' },
    { name: 'Sou Gao (E, N)', price: '7', description: '4 pieces, vegetables, peanuts, shiitake, vegan mince' },
    { name: 'Steamed Mix', price: '10.5', description: '2 pieces each of Ha Gao, Siu Mai and Sou Gao' },
    { name: 'Tofu Skin Rolls (F, L, N)', price: '9', description: '3 pieces, vegetables, mushrooms, glass noodles, vegan mince, mushroom sauce' },
  ],
  'Fried': [
    { name: 'Veggie Gyoza (A, E, F, N)', price: '7', description: '5 pieces, cabbage, morels, shiitake, dried tofu, dried radish, glass noodles, enoki, vegan mince' },
    { name: 'Shrimps Gyoza (A, B, F, N)', price: '9', description: '5 pieces, shrimps, water chestnut, wild garlic' },
  ],
  'Hot Dishes': [
    { name: 'Enoki & Cauliflower Tempura', price: '7', description: 'available with siracha glaze or Ziu-Yim spices served with wild garlic-lime mayo' },
    { name: 'Kaarage Chicken (C, F, H)', price: '10', description: 'available with siracha glaze or Ziu-Yim spices served with wild garlic-lime mayo' },
    { name: 'Fried Tofu with Vegetables (F, N)', price: '8 | 12', description: 'tofu, black beans, seasonal vegetables, lotus root chips. Can be ordered as a large dish.' },
    { name: 'Black Pepper Beef (A, F, N)', price: '12 | 18', description: 'beef slices, seasonal vegetables, black pepper sauce. Can be ordered as a large dish.' },
  ],
  'Cold Dishes': [
    { name: 'Beef with Yu (F)', price: '7', description: 'beef shanks braised in master stock, served in slices' },
    { name: 'Squid Yu-Style (F, R)', price: '8', description: 'squid braised in green tea & spices mixture, served in slices' },
    { name: 'Pidan Doufu (C, F)', price: '6', description: 'silk tofu and century eggs finished with black vinegar & ginger sauce' },
    { name: 'Peanut Noodle Salad (E, F, N)', price: '6', description: 'rice vermicelli mixed with peanut & sesame sauce, topped with cucumber, pickled vegetables and garlic flakes' },
  ],
  'Side Dishes': [
    { name: 'Cucumber Salad (N)', price: '5', description: '' },
    { name: 'Yu‘s Kimchi', price: '5', description: '' },
    { name: 'Pickled Vegetables', price: '5', description: '' },
    { name: 'Rice', price: '2', description: '' },
    { name: 'Siracha, Siracha Mayo, Chili Oil, Wild Garlic-Lime Mayo, Umami Sauce (F)', price: '1', description: '' },
  ],
  'Dessert': [
    { name: 'Steamed Custard Buns (A, C, G)', price: '5', description: '' },
    { name: 'Mini Germlings (A, N)', price: '5', description: 'with powidl and vanilla sauce' },
  ],
};

const activeFoodMenuItems = computed(() => foodData[activeFoodCategory.value] || []);

</script>

<style scoped>
.menu-section {
  padding: 80px 0;
  background: transparent;
  color: #fff;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 15px;
}

.section-title {
  text-align: center;
  margin-bottom: 40px;
}

.section-title h2 {
  font-family: 'Playfair Display', serif;
  font-size: 36px;
  font-weight: 700;
  color: var(--primary-color);
  margin-bottom: 10px;
}

.section-title p {
  font-family: 'Poppins', sans-serif;
  color: var(--secondary-color);
  font-size: 16px;
}

.menu-category-section {
  margin-bottom: 70px;
}

.category-title {
  font-family: 'Playfair Display', serif;
  font-size: 28px;
  font-weight: 600;
  color: #fff;
  text-align: center;
  margin-bottom: 30px;
  position: relative;
}

.category-title::after {
  content: '';
  display: block;
  width: 60px;
  height: 2px;
  background: var(--primary-color);
  margin: 8px auto 0;
}

.menu-tabs {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  margin-bottom: 50px;
  gap: 15px;
}

.menu-tabs button {
  font-family: 'Poppins', sans-serif;
  font-size: 15px;
  font-weight: 600;
  color: var(--secondary-color);
  background: transparent;
  border: 1px solid rgba(255, 255, 255, 0.2);
  padding: 10px 25px;
  cursor: pointer;
  transition: all 0.3s ease;
  border-radius: 50px;
}

.menu-tabs button:hover {
  color: var(--primary-color);
  border-color: var(--primary-color);
  background: rgba(230, 192, 133, 0.05);
}

.menu-tabs button.active {
  color: #121212;
  border-color: var(--primary-color);
  background: var(--primary-color);
  box-shadow: 0 2px 15px rgba(230, 192, 133, 0.2);
}

.menu-items-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 30px 50px;
}

.menu-items-list {
    max-width: 800px;
    margin: 0 auto;
}

.menu-item-list-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px 10px;
    border-bottom: 1px dotted rgba(255, 255, 255, 0.2);
    transition: background-color 0.3s ease;
}

.menu-item-list-row:hover {
    background-color: rgba(230, 192, 133, 0.05);
}

.menu-item-list-row:last-child {
    border-bottom: none;
}

.menu-item-name-list {
    font-family: 'Playfair Display', serif;
    font-size: 19px;
    font-weight: 600;
    color: var(--primary-color);
}

.menu-item-description-list {
    font-family: 'Poppins', sans-serif;
    font-size: 14px;
    color: var(--secondary-color);
    margin: 3px 0 0 0;
    padding-right: 15px;
}

.menu-item-price-list {
    font-family: 'Poppins', sans-serif;
    font-size: 19px;
    font-weight: 600;
    color: #fff;
    white-space: nowrap;
    padding-left: 20px;
}

.menu-item {
  background: rgba(30, 30, 30, 0.3);
  padding: 20px;
  border-radius: 8px;
  border: 1px solid rgba(255, 255, 255, 0.05);
  transition: all 0.4s cubic-bezier(0.25, 0.8, 0.25, 1);
  position: relative;
  overflow: hidden;
}

.menu-item.is-centered {
  text-align: center;
}

.menu-item.is-centered .menu-item-price {
  text-align: center;
}

.menu-item:before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  box-shadow: 0 0 0 0 rgba(230, 192, 133, 0.2);
  border-radius: 8px;
  transition: all 0.4s ease;
  pointer-events: none;
}

.menu-item:hover {
  transform: translateY(-5px);
  border-color: rgba(230, 192, 133, 0.4);
}

.menu-item:hover:before {
  box-shadow: 0 0 20px 5px rgba(230, 192, 133, 0.2);
}

.menu-item-header {
  margin-bottom: 10px;
}

.menu-item-name {
  font-family: 'Playfair Display', serif;
  font-size: 20px;
  font-weight: 600;
  color: var(--primary-color);
  margin: 0;
}

.menu-item-price {
    display: block;
    text-align: right;
    font-family: 'Poppins', sans-serif;
    font-size: 24px;
    font-weight: 700;
    color: var(--secondary-color);
    margin-top: 15px;
}

.menu-item-description {
  font-family: 'Poppins', sans-serif;
  font-size: 14px;
  color: var(--secondary-color);
  margin: 0;
  min-height: 4.2em; /* Ensures consistent card height by reserving space for 3 lines of text */
}

.info-label {
  text-align: center;
  margin-bottom: 20px;
  font-style: italic;
  color: var(--secondary-color);
}


.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.4s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

@media (max-width: 992px) {
  .menu-tabs button {
    font-size: 14px;
    padding: 8px 20px;
  }

  .menu-item-description {
    min-height: 0; /* Disable fixed height on smaller screens */
  }
}

@media (max-width: 768px) {
  .menu-items-grid {
    grid-template-columns: 1fr;
    gap: 25px;
  }
  
  .menu-items-list {
    max-width: 100%;
  }

  .menu-tabs {
    gap: 10px;
  }

  .menu-tabs button {
    font-size: 13px;
    padding: 8px 15px;
  }
}
</style>
