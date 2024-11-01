<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import Loader from './components/Loader.vue'
import { ref, onMounted } from 'vue'

const isLoading = ref(true)

// Simuler un chargement (remplacez par un appel API réel si nécessaire)
onMounted(() => {
  setTimeout(() => {
    isLoading.value = false // Cache le loader après le chargement
  }, 2000) // Durée simulée
})
</script>

<template>
  <Loader :isLoading="isLoading" /> <!-- Affiche le loader si isLoading est true -->

  <RouterView v-if="!isLoading" /> <!-- Affiche le contenu une fois le chargement terminé -->
</template>

<style scoped>

</style>