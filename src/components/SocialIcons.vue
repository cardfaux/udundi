<script setup>
import FacebookIcon from './icons/Facebook.vue';
import InstagramIcon from './icons/Instagram.vue';
</script>

<template>
  <div class="social-icons">
    <FacebookIcon />
    <InstagramIcon />
  </div>
</template>

<style scoped>
.social-icons {
  position: absolute;
  bottom: 3.9rem;
  right: 3.1rem;
  z-index: 2;
}
svg {
  width: 6.8rem;
  height: 6.8rem;
  filter: drop-shadow(2px 2px 3px rgba(0, 0, 0, 0.5));
}
</style>
