<!-- src/components/Loader.vue -->
<template>
    <div class="loader" v-if="isLoading">
      <img src="../assets/svg/loader.svg" alt="Chargement..." />
    </div>
  </template>
  
  <script>
  export default {
    props: {
      isLoading: {
        type: Boolean,
        required: true
      }
    }
  }
  </script>
  
  <style scoped>
  .loader {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: rgba(0, 0, 0, 1); /* Fond complètement noir */
    z-index: 9999;
  }
  
  img {
    width: 80px;
    height: 80px;
  }
  </style>
  