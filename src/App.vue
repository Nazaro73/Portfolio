<script setup lang="ts">
import { onMounted } from 'vue'
import AOS from 'aos'
import 'aos/dist/aos.css'

import Header from './components/Header.vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import Skills from './components/Skills.vue'
import Experience from './components/Experience.vue'
import Projects from './components/Projects.vue'
import Contact from './components/Contact.vue'
import Footer from './components/Footer.vue'

onMounted(() => {
  AOS.init({
    duration: 1000,
    easing: 'ease-out-cubic',
    once: true,
    offset: 50
  })
})
</script>

<template>
  <div id="app">
    <div class="hero-image">
      <img src="/profile-photo.jpg" alt="Photo de profil" class="profile-photo" />
    </div>
    <Header />
    <Hero />
    <About />
    <Skills />
    <Experience />
    <Projects />
    <Contact />
    <Footer />
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  line-height: 1.6;
  color: #334155;
  overflow-x: hidden;
}

#app {
  min-height: 100vh;
  padding-top: 70px;
}

.hero-image {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 100vh;
  z-index: -1;
  overflow: hidden;
}

.profile-photo {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: brightness(0.3);
}

/* Scrollbar personnalisé */
::-webkit-scrollbar {
  width: 8px;
}

::-webkit-scrollbar-track {
  background: #f1f5f9;
}

::-webkit-scrollbar-thumb {
  background: linear-gradient(45deg, #3b82f6, #8b5cf6);
  border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
  background: linear-gradient(45deg, #2563eb, #7c3aed);
}

/* Classes utilitaires pour AOS */
[data-aos="fade-up"] {
  opacity: 0;
  transform: translateY(30px);
  transition-property: opacity, transform;
}

[data-aos="fade-up"].aos-animate {
  opacity: 1;
  transform: translateY(0);
}

[data-aos="fade-left"] {
  opacity: 0;
  transform: translateX(30px);
  transition-property: opacity, transform;
}

[data-aos="fade-left"].aos-animate {
  opacity: 1;
  transform: translateX(0);
}

[data-aos="fade-right"] {
  opacity: 0;
  transform: translateX(-30px);
  transition-property: opacity, transform;
}

[data-aos="fade-right"].aos-animate {
  opacity: 1;
  transform: translateX(0);
}

[data-aos="zoom-in"] {
  opacity: 0;
  transform: scale(0.8);
  transition-property: opacity, transform;
}

[data-aos="zoom-in"].aos-animate {
  opacity: 1;
  transform: scale(1);
}

/* Styles pour le chargement */
.loading-screen {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: #0f172a;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 9999;
  transition: opacity 0.5s ease;
}

.loading-screen.fade-out {
  opacity: 0;
  pointer-events: none;
}

.loader {
  width: 50px;
  height: 50px;
  border: 3px solid rgba(59, 130, 246, 0.3);
  border-top: 3px solid #3b82f6;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

/* Responsive design global */
@media (max-width: 768px) {
  body {
    font-size: 16px;
  }
}

@media (max-width: 480px) {
  body {
    font-size: 14px;
  }
}

/* Focus styles pour l'accessibilité */
button:focus-visible,
a:focus-visible,
input:focus-visible,
textarea:focus-visible,
select:focus-visible {
  outline: 2px solid #3b82f6;
  outline-offset: 2px;
}

/* Styles pour les éléments interactifs */
button,
a {
  cursor: pointer;
}

button:disabled {
  cursor: not-allowed;
}

/* Styles pour les sélections de texte */
::selection {
  background: rgba(59, 130, 246, 0.2);
  color: #1e293b;
}

/* Animations globales */
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.fade-in {
  animation: fadeIn 0.6s ease-out forwards;
}

.fade-in-delay-1 {
  animation: fadeIn 0.6s ease-out 0.1s forwards;
  opacity: 0;
}

.fade-in-delay-2 {
  animation: fadeIn 0.6s ease-out 0.2s forwards;
  opacity: 0;
}

.fade-in-delay-3 {
  animation: fadeIn 0.6s ease-out 0.3s forwards;
  opacity: 0;
}
</style>
