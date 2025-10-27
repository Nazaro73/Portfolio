<template>
  <section id="home" class="hero" ref="heroRef">
    <div class="hero-bg">
      <div class="particles" ref="particlesRef"></div>
    </div>

    <div class="hero-content">
      <div class="hero-text">
        <div class="logo-container">
          <img src="/logo.jpg" alt="Logo" class="hero-logo" />
        </div>
        <h1 class="hero-title">
          <span class="greeting">Bonjour, je suis</span>
          <span class="name">Abdel-Rahim KHABABA</span>
          <span class="role">Développeur Full Stack</span>
        </h1>

        <p class="hero-description">
          Passionné par le développement web, je crée des applications
          modernes et performantes avec Vue.js, Node.js et bien plus encore.
        </p>

        <div class="hero-buttons">
          <button class="btn btn-primary" @click="scrollToSection('projects')">
            <span>Voir mes projets</span>
            <ArrowRight class="icon" />
          </button>
          <button class="btn btn-secondary" @click="scrollToSection('contact')">
            <span>Me contacter</span>
            <Mail class="icon" />
          </button>
        </div>

        <div class="hero-social">
          <a href="https://github.com" target="_blank" class="social-link">
            <Github class="social-icon" />
          </a>
          <a href="https://linkedin.com" target="_blank" class="social-link">
            <Linkedin class="social-icon" />
          </a>
          <a href="mailto:Abdel-Rahim.KHABABA@hotmail.com" class="social-link">
            <Mail class="social-icon" />
          </a>
        </div>
      </div>

      <div class="hero-visual">
        <div class="avatar-container">
          <div class="avatar">
            <div class="avatar-bg"></div>
            <div class="code-symbols">
              <span>&lt;/&gt;</span>
              <span>{ }</span>
              <span>[ ]</span>
              <span>( )</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="scroll-indicator">
      <div class="scroll-line"></div>
      <ChevronDown class="scroll-icon" />
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'
import { ArrowRight, Mail, Github, Linkedin, ChevronDown } from 'lucide-vue-next'

const heroRef = ref<HTMLElement>()
const particlesRef = ref<HTMLElement>()

const scrollToSection = (sectionId: string) => {
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

const createParticles = () => {
  const particlesContainer = particlesRef.value
  if (!particlesContainer) return

  for (let i = 0; i < 50; i++) {
    const particle = document.createElement('div')
    particle.classList.add('particle')
    particle.style.left = Math.random() * 100 + '%'
    particle.style.top = Math.random() * 100 + '%'
    particle.style.animationDelay = Math.random() * 2 + 's'
    particlesContainer.appendChild(particle)
  }
}

onMounted(() => {
  createParticles()

  // Timeline principale
  const tl = gsap.timeline()

  // Animation du background
  tl.fromTo('.hero-bg', {
    opacity: 0
  }, {
    opacity: 1,
    duration: 1.5
  })

  // Animation du logo
  tl.fromTo('.hero-logo', {
    scale: 0,
    opacity: 0,
    rotation: -180
  }, {
    scale: 1,
    opacity: 1,
    rotation: 0,
    duration: 1,
    ease: 'back.out(1.7)'
  }, 0.3)

  // Animation du texte
  tl.fromTo('.greeting', {
    y: 50,
    opacity: 0
  }, {
    y: 0,
    opacity: 1,
    duration: 0.8,
    ease: 'power2.out'
  }, 0.3)

  tl.fromTo('.name', {
    y: 50,
    opacity: 0,
    scale: 0.9
  }, {
    y: 0,
    opacity: 1,
    scale: 1,
    duration: 1,
    ease: 'back.out(1.7)'
  }, 0.6)

  tl.fromTo('.role', {
    y: 50,
    opacity: 0
  }, {
    y: 0,
    opacity: 1,
    duration: 0.8,
    ease: 'power2.out'
  }, 0.9)

  tl.fromTo('.hero-description', {
    y: 30,
    opacity: 0
  }, {
    y: 0,
    opacity: 1,
    duration: 0.8,
    ease: 'power2.out'
  }, 1.2)

  tl.fromTo('.hero-buttons .btn', {
    y: 30,
    opacity: 0
  }, {
    y: 0,
    opacity: 1,
    duration: 0.6,
    stagger: 0.2,
    ease: 'power2.out'
  }, 1.4)

  tl.fromTo('.hero-social .social-link', {
    y: 30,
    opacity: 0,
    scale: 0
  }, {
    y: 0,
    opacity: 1,
    scale: 1,
    duration: 0.6,
    stagger: 0.1,
    ease: 'back.out(1.7)'
  }, 1.6)

  // Animation du visual
  tl.fromTo('.avatar-container', {
    scale: 0,
    opacity: 0,
    rotation: -180
  }, {
    scale: 1,
    opacity: 1,
    rotation: 0,
    duration: 1.2,
    ease: 'back.out(1.7)'
  }, 0.8)

  tl.fromTo('.code-symbols span', {
    scale: 0,
    opacity: 0,
    rotation: 180
  }, {
    scale: 1,
    opacity: 1,
    rotation: 0,
    duration: 0.8,
    stagger: 0.1,
    ease: 'back.out(1.7)'
  }, 1.5)

  // Animation de l'indicateur de scroll
  tl.fromTo('.scroll-indicator', {
    y: 30,
    opacity: 0
  }, {
    y: 0,
    opacity: 1,
    duration: 0.8,
    ease: 'power2.out'
  }, 2)

  // Animation continue des particules
  gsap.to('.particle', {
    y: '-100vh',
    duration: 3,
    repeat: -1,
    ease: 'none',
    stagger: {
      each: 0.1,
      repeat: -1
    }
  })
})
</script>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  position: relative;
  overflow: hidden;
  background: linear-gradient(135deg, #0f172a 0%, #1e293b 50%, #334155 100%);
}

.hero-bg {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 1;
}

.particles {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  overflow: hidden;
}

.particle {
  position: absolute;
  width: 2px;
  height: 2px;
  background: #3b82f6;
  border-radius: 50%;
  opacity: 0.6;
}

.particle::before {
  content: '';
  position: absolute;
  top: -1px;
  left: -1px;
  width: 4px;
  height: 4px;
  background: radial-gradient(circle, #3b82f6 0%, transparent 70%);
  border-radius: 50%;
}

.hero-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: flex;
  flex-direction: column;
  gap: 4rem;
  align-items: center;
  z-index: 2;
  position: relative;
  text-align: center;
}

.hero-text {
  color: white;
}

.logo-container {
  display: flex;
  justify-content: center;
  margin-top: 3rem;
  margin-bottom: 2rem;
}

.hero-logo {
  width: 120px;
  height: 120px;
  object-fit: cover;
  border-radius: 50%;
  border: 3px solid rgba(59, 130, 246, 0.3);
  box-shadow: 0 0 30px rgba(59, 130, 246, 0.3);
  transition: all 0.3s ease;
}

.hero-logo:hover {
  transform: scale(1.05);
  border-color: #3b82f6;
  box-shadow: 0 0 40px rgba(59, 130, 246, 0.5);
}

.hero-title {
  margin: 0 0 2rem 0;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.greeting {
  font-size: 1.2rem;
  color: #94a3b8;
  font-weight: 400;
}

.name {
  font-size: 3.5rem;
  font-weight: bold;
  background: linear-gradient(45deg, #3b82f6, #8b5cf6, #06b6d4);
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-size: 200% 200%;
  animation: gradient 3s ease infinite;
}

@keyframes gradient {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

.role {
  font-size: 1.8rem;
  color: #e2e8f0;
  font-weight: 300;
}

.hero-description {
  font-size: 1.1rem;
  line-height: 1.8;
  color: #94a3b8;
  margin-bottom: 3rem;
}

.hero-buttons {
  display: flex;
  gap: 1rem;
  margin-bottom: 3rem;
}

.btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 1rem 2rem;
  border: none;
  border-radius: 50px;
  font-weight: 600;
  text-decoration: none;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transition: left 0.5s;
}

.btn:hover::before {
  left: 100%;
}

.btn-primary {
  background: linear-gradient(45deg, #3b82f6, #8b5cf6);
  color: white;
  transform: translateY(0);
}

.btn-primary:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 30px rgba(59, 130, 246, 0.3);
}

.btn-secondary {
  background: transparent;
  color: #e2e8f0;
  border: 2px solid #3b82f6;
}

.btn-secondary:hover {
  background: #3b82f6;
  transform: translateY(-3px);
  box-shadow: 0 10px 30px rgba(59, 130, 246, 0.2);
}

.icon {
  width: 18px;
  height: 18px;
}

.hero-social {
  display: flex;
  gap: 1rem;
}

.social-link {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background: rgba(59, 130, 246, 0.1);
  color: #3b82f6;
  text-decoration: none;
  transition: all 0.3s ease;
  border: 2px solid rgba(59, 130, 246, 0.2);
}

.social-link:hover {
  background: #3b82f6;
  color: white;
  transform: translateY(-3px);
  box-shadow: 0 10px 30px rgba(59, 130, 246, 0.3);
}

.social-icon {
  width: 20px;
  height: 20px;
}

.hero-visual {
  display: flex;
  justify-content: center;
  align-items: center;
}

.avatar-container {
  position: relative;
}

.avatar {
  width: 300px;
  height: 300px;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}

.avatar-bg {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(45deg, #3b82f6, #8b5cf6, #06b6d4);
  border-radius: 50%;
  animation: rotate 10s linear infinite;
}

.avatar-bg::before {
  content: '';
  position: absolute;
  inset: 10px;
  background: #0f172a;
  border-radius: 50%;
}

@keyframes rotate {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.code-symbols {
  position: relative;
  z-index: 2;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  gap: 2rem;
  font-size: 2rem;
  font-weight: bold;
  color: #3b82f6;
}

.code-symbols span {
  animation: float 3s ease-in-out infinite;
}

.code-symbols span:nth-child(2) {
  animation-delay: -0.5s;
}

.code-symbols span:nth-child(3) {
  animation-delay: -1s;
}

.code-symbols span:nth-child(4) {
  animation-delay: -1.5s;
}

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}

.scroll-indicator {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  color: #94a3b8;
  cursor: pointer;
  z-index: 2;
}

.scroll-line {
  width: 1px;
  height: 50px;
  background: linear-gradient(to bottom, transparent, #3b82f6);
  margin-bottom: 0.5rem;
}

.scroll-icon {
  width: 20px;
  height: 20px;
  animation: bounce 2s infinite;
}

@keyframes bounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}

@media (max-width: 768px) {
  .hero-content {
    padding: 2rem 1rem;
    gap: 2rem;
  }

  .hero-logo {
    width: 100px;
    height: 100px;
  }

  .name {
    font-size: 2.5rem;
  }

  .role {
    font-size: 1.4rem;
  }

  .hero-buttons {
    flex-direction: column;
    align-items: center;
  }

  .btn {
    width: 100%;
    max-width: 300px;
  }

  .avatar {
    width: 250px;
    height: 250px;
  }

  .code-symbols {
    font-size: 1.5rem;
  }
}
</style>