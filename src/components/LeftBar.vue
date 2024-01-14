<script setup></script>

<template>
  <aside></aside>
</template>

<style scoped>
aside {
  width: 41.3rem;
  height: 100%;
  background-color: #611818;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1;
}

@media (max-width: 480px) {
  aside {
    width: 100%;
    opacity: 0.3;
  }
}
</style>
