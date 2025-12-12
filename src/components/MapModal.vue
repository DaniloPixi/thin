
<template>
  <div class="map-modal-overlay" @click.self="$emit('close')">
    <div class="map-modal-content">
      <button class="close-button" @click="$emit('close')">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
          <path d="M19 6.41L17.59 5 12 10.59 6.41 5 5 6.41 10.59 12 5 17.59 6.41 19 12 13.41 17.59 19 19 17.59 13.41 12z"></path>
        </svg>
      </button>
      <div class="modal-scroll-area">
        <img src="/images/image.png" alt="Map showing the location of Yu's Cottage" class="map-image">
        <a href="https://www.google.com/maps/dir/?api=1&destination=Kettenbr%C3%BCckengasse+3,+1050+Wien" target="_blank" rel="noopener noreferrer" class="directions-button">
          Get Directions
        </a>
      </div>
    </div>
  </div>
</template>

<script setup>
defineEmits(['close']);
</script>

<style scoped>
/* Scrollbar Styling */
::-webkit-scrollbar {
  width: 8px;
}
::-webkit-scrollbar-track {
  background: #1a1a1a;
  border-radius: 10px;
}
::-webkit-scrollbar-thumb {
  background: var(--primary-color);
  border-radius: 10px;
}
::-webkit-scrollbar-thumb:hover {
  background: #fff;
}

.map-modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.85);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  z-index: 2000;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  box-sizing: border-box;
}

.map-modal-content {
  position: relative;
  background: #1e1e1e;
  border-radius: 15px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 15px 50px rgba(0, 0, 0, 0.6);
  width: 100%;
  max-width: 800px;
  max-height: 95vh;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

.close-button {
  position: absolute;
  top: 10px;
  right: 10px;
  background: rgba(0, 0, 0, 0.5);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 50%;
  color: #fff;
  cursor: pointer;
  width: 36px;
  height: 36px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
  z-index: 9999;
}

.close-button:hover {
  background: var(--primary-color);
  transform: rotate(90deg);
}

.close-button svg {
  width: 24px;
  height: 24px;
  fill: currentColor;
}

.modal-scroll-area {
  padding: 25px;
  overflow-y: auto;
  text-align: center;
}

.map-image {
  width: 100%;
  height: auto;
  border-radius: 8px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  display: block;
  margin: 0 auto;
}

.directions-button {
  display: inline-block;
  margin-top: 25px;
  padding: 14px 30px;
  background-image: linear-gradient(to right, var(--primary-color), #e6b985);
  color: #0c0c0c;
  text-decoration: none;
  border-radius: 8px;
  font-weight: bold;
  font-family: 'Poppins', sans-serif;
  font-size: 16px;
  transition: all 0.3s ease;
  box-shadow: 0 4px 20px rgba(230, 192, 133, 0.3);
  border: none;
}

.directions-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 25px rgba(230, 192, 133, 0.4);
}

@media (max-width: 768px) {
  .map-modal-content {
    max-height: 90vh;
  }
  .modal-scroll-area {
    padding: 20px;
  }
  .directions-button {
    padding: 12px 24px;
    font-size: 15px;
    margin-top: 20px;
  }
  .close-button {
    width: 32px;
    height: 32px;
    top: 8px;
    right: 8px;
  }
  .close-button svg {
    width: 20px;
    height: 20px;
  }
}
</style>
