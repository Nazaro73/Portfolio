<template>
  <header
    :class="['header', { 'scrolled': isScrolled }]"
    ref="headerRef"
  >
    <nav class="nav">
      <div class="nav-brand">
        <img src="/logo.jpg" alt="Logo AK" class="logo-image" />
      </div>

      <ul class="nav-links" :class="{ active: isMenuOpen }">
        <li><a href="#home" @click="scrollToSection('home')" class="nav-link">Accueil</a></li>
        <li><a href="#about" @click="scrollToSection('about')" class="nav-link">À propos</a></li>
        <li><a href="#skills" @click="scrollToSection('skills')" class="nav-link">Compétences</a></li>
        <li><a href="#experience" @click="scrollToSection('experience')" class="nav-link">Expérience</a></li>
        <li><a href="#projects" @click="scrollToSection('projects')" class="nav-link">Projets</a></li>
        <li><a href="#contact" @click="scrollToSection('contact')" class="nav-link">Contact</a></li>
      </ul>

      <button
        class="menu-toggle"
        @click="toggleMenu"
        :class="{ active: isMenuOpen }"
      >
        <span></span>
        <span></span>
        <span></span>
      </button>
    </nav>
  </header>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import { gsap } from 'gsap'

const headerRef = ref<HTMLElement>()
const isScrolled = ref(false)
const isMenuOpen = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const scrollToSection = (sectionId: string) => {
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
  isMenuOpen.value = false
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)

  // Animation d'entrée du header
  gsap.fromTo(headerRef.value, {
    y: -100,
    opacity: 0
  }, {
    y: 0,
    opacity: 1,
    duration: 1,
    ease: 'power2.out'
  })

  // Animation des liens de navigation
  gsap.fromTo('.nav-link', {
    y: -20,
    opacity: 0
  }, {
    y: 0,
    opacity: 1,
    duration: 0.8,
    stagger: 0.1,
    delay: 0.3,
    ease: 'power2.out'
  })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  background: rgba(15, 23, 42, 0.95);
  backdrop-filter: blur(10px);
  transition: all 0.3s ease;
  border-bottom: 1px solid rgba(148, 163, 184, 0.1);
}

.header.scrolled {
  background: rgba(15, 23, 42, 0.98);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
}

.nav {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 80px;
}

.logo-image {
  height: 50px;
  width: auto;
  border-radius: 50%;
  object-fit: cover;
  transition: all 0.3s ease;
  border: 2px solid transparent;
}

.logo-image:hover {
  border-color: #3b82f6;
  transform: scale(1.05);
}

.nav-links {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
  gap: 2rem;
}

.nav-link {
  color: #e2e8f0;
  text-decoration: none;
  font-weight: 500;
  position: relative;
  transition: all 0.3s ease;
  padding: 0.5rem 0;
}

.nav-link::before {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: linear-gradient(45deg, #3b82f6, #8b5cf6);
  transition: width 0.3s ease;
}

.nav-link:hover {
  color: #3b82f6;
  transform: translateY(-2px);
}

.nav-link:hover::before {
  width: 100%;
}

.menu-toggle {
  display: none;
  flex-direction: column;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0.5rem;
  gap: 4px;
}

.menu-toggle span {
  width: 25px;
  height: 3px;
  background: #e2e8f0;
  transition: all 0.3s ease;
  transform-origin: center;
}

.menu-toggle.active span:nth-child(1) {
  transform: rotate(45deg) translate(6px, 6px);
}

.menu-toggle.active span:nth-child(2) {
  opacity: 0;
}

.menu-toggle.active span:nth-child(3) {
  transform: rotate(-45deg) translate(6px, -6px);
}

@media (max-width: 768px) {
  .nav {
    padding: 0 1rem;
  }

  .menu-toggle {
    display: flex;
  }

  .nav-links {
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    background: rgba(15, 23, 42, 0.98);
    backdrop-filter: blur(10px);
    flex-direction: column;
    padding: 2rem;
    gap: 1rem;
    transform: translateY(-100%);
    opacity: 0;
    visibility: hidden;
    transition: all 0.3s ease;
  }

  .nav-links.active {
    transform: translateY(0);
    opacity: 1;
    visibility: visible;
  }

  .nav-link {
    font-size: 1.1rem;
    padding: 1rem 0;
    border-bottom: 1px solid rgba(148, 163, 184, 0.1);
  }

  .nav-link:last-child {
    border-bottom: none;
  }
}
</style>