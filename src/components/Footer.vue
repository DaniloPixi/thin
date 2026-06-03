
<template>
  <footer id="footer">
    <img class="footer-motif footer-motif-arc" :src="footerArc" alt="" aria-hidden="true">
    <img class="footer-motif footer-motif-block" :src="distressedBlock" alt="" aria-hidden="true">
    <div class="container">
      <div class="copyright">
        &copy; Copyright <strong><span>Yu's Cottage</span></strong>. All Rights Reserved
      </div>
    </div>
  </footer>
</template>

<script setup>
import footerArc from '../assets/svg/brush-footer-arc.svg';
import distressedBlock from '../assets/svg/brush-footer-distressed-block.svg';
</script>

<style scoped>
#footer {
  position: relative;
  isolation: isolate;
  overflow: hidden;
  background:
    linear-gradient(180deg, #0c0b09, #090908);
  color: var(--secondary-color);
  font-size: 14px;
  text-align: center;
  padding: 30px 0;
}

.footer-motif {
  position: absolute;
  z-index: -1;
  pointer-events: none;
  user-select: none;
  mix-blend-mode: screen;
}

.footer-motif-arc {
  left: max(1rem, calc((100vw - 980px) / 2));
  bottom: -2.4rem;
  width: clamp(4.5rem, 8vw, 6.5rem);
  opacity: 0.18;
  transform: rotate(-8deg);
}

.footer-motif-block {
  top: 0.85rem;
  right: max(1rem, calc((100vw - 980px) / 2));
  width: clamp(5.5rem, 9vw, 8rem);
  opacity: 0.12;
  transform: rotate(3deg);
}

.container {
  position: relative;
  z-index: 1;
}

.copyright strong {
  color: var(--primary-color);
}
</style>