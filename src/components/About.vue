<template>
  <section id="about" class="about" ref="aboutRef">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title" data-aos="fade-up">À propos de moi</h2>
        <div class="section-subtitle" data-aos="fade-up" data-aos-delay="100">
          Découvrez mon parcours et mes passions
        </div>
      </div>

      <div class="about-content">
        <div class="about-text" data-aos="fade-right" data-aos-delay="200">
          <div class="intro">
            <p>
              Bonjour ! Je suis <strong>Abdel-Rahim KHABABA</strong>, un développeur full stack
              passionné avec une formation solide en informatique et plusieurs années d'expérience
              dans le développement d'applications web modernes.
            </p>
          </div>

          <div class="description">
            <p>
              Mon parcours m'a permis de maîtriser un large éventail de technologies,
              du développement frontend avec Vue.js et React, au backend avec Node.js,
              Java et Python. J'aime créer des solutions innovantes qui allient
              performance technique et expérience utilisateur exceptionnelle.
            </p>
          </div>

          <div class="highlights">
            <div class="highlight-item" data-aos="fade-up" data-aos-delay="400">
              <div class="highlight-icon">
                <Code class="icon" />
              </div>
              <div class="highlight-content">
                <h3>Développement Full Stack</h3>
                <p>Expertise complète du frontend au backend</p>
              </div>
            </div>

            <div class="highlight-item" data-aos="fade-up" data-aos-delay="500">
              <div class="highlight-icon">
                <Lightbulb class="icon" />
              </div>
              <div class="highlight-content">
                <h3>Innovation</h3>
                <p>Toujours à la recherche de nouvelles solutions</p>
              </div>
            </div>

            <div class="highlight-item" data-aos="fade-up" data-aos-delay="600">
              <div class="highlight-icon">
                <Users class="icon" />
              </div>
              <div class="highlight-content">
                <h3>Collaboration</h3>
                <p>Travail d'équipe et communication efficace</p>
              </div>
            </div>
          </div>
        </div>

        <div class="about-visual" data-aos="fade-left" data-aos-delay="300">
          <div class="visual-container">
            <div class="profile-card">
              <div class="card-header">
                <div class="card-dots">
                  <span class="dot red"></span>
                  <span class="dot yellow"></span>
                  <span class="dot green"></span>
                </div>
                <div class="card-title">developer.profile</div>
              </div>

              <div class="card-content">
                <div class="code-line">
                  <span class="code-key">const</span>
                  <span class="code-variable">developer</span>
                  <span class="code-operator">=</span>
                  <span class="code-bracket">{</span>
                </div>

                <div class="code-line indent">
                  <span class="code-key">name:</span>
                  <span class="code-string">"Abdel-Rahim KHABABA"</span>,
                </div>

                <div class="code-line indent">
                  <span class="code-key">location:</span>
                  <span class="code-string">"Chambéry, France"</span>,
                </div>

                <div class="code-line indent">
                  <span class="code-key">education:</span>
                  <span class="code-string">"DUT Informatique + Bachelor"</span>,
                </div>

                <div class="code-line indent">
                  <span class="code-key">languages:</span>
                  <span class="code-bracket">[</span>
                </div>

                <div class="code-line indent-2">
                  <span class="code-string">"Français (C2)"</span>,
                </div>

                <div class="code-line indent-2">
                  <span class="code-string">"Anglais (B2)"</span>,
                </div>

                <div class="code-line indent-2">
                  <span class="code-string">"Espagnol (B1)"</span>,
                </div>

                <div class="code-line indent-2">
                  <span class="code-string">"Arabe (B2)"</span>
                </div>

                <div class="code-line indent">
                  <span class="code-bracket">]</span>,
                </div>

                <div class="code-line indent">
                  <span class="code-key">passions:</span>
                  <span class="code-bracket">[</span>
                  <span class="code-string">"Code"</span>,
                  <span class="code-string">"Innovation"</span>
                  <span class="code-bracket">]</span>
                </div>

                <div class="code-line">
                  <span class="code-bracket">}</span>
                </div>

                <div class="code-cursor"></div>
              </div>
            </div>

            <div class="floating-elements">
              <div class="floating-element" v-for="n in 6" :key="n">
                <component :is="getRandomIcon()" class="floating-icon" />
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="stats-container" data-aos="fade-up" data-aos-delay="700">
        <div class="stat-item">
          <div class="stat-number" ref="experienceRef">2+</div>
          <div class="stat-label">Années d'expérience</div>
        </div>

        <div class="stat-item">
          <div class="stat-number" ref="projectsRef">15+</div>
          <div class="stat-label">Projets réalisés</div>
        </div>

        <div class="stat-item">
          <div class="stat-number" ref="technologiesRef">10+</div>
          <div class="stat-label">Technologies maîtrisées</div>
        </div>

        <div class="stat-item">
          <div class="stat-number" ref="certificationsRef">3</div>
          <div class="stat-label">Certifications</div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import { Code, Lightbulb, Users, Smartphone, Database, Globe, Zap, Target, Coffee } from 'lucide-vue-next'

gsap.registerPlugin(ScrollTrigger)

const aboutRef = ref<HTMLElement>()
const experienceRef = ref<HTMLElement>()
const projectsRef = ref<HTMLElement>()
const technologiesRef = ref<HTMLElement>()
const certificationsRef = ref<HTMLElement>()

const icons = [Code, Database, Globe, Smartphone, Zap, Target, Coffee, Lightbulb]

const getRandomIcon = () => {
  return icons[Math.floor(Math.random() * icons.length)]
}

const animateCounter = (element: HTMLElement, target: number, suffix = '') => {
  let current = 0
  const increment = target / 100
  const timer = setInterval(() => {
    current += increment
    if (current >= target) {
      current = target
      clearInterval(timer)
    }
    element.textContent = Math.floor(current) + suffix
  }, 20)
}

onMounted(() => {
  // Animation des compteurs
  ScrollTrigger.create({
    trigger: '.stats-container',
    start: 'top 80%',
    onEnter: () => {
      if (experienceRef.value) animateCounter(experienceRef.value, 2, '+')
      if (projectsRef.value) animateCounter(projectsRef.value, 15, '+')
      if (technologiesRef.value) animateCounter(technologiesRef.value, 10, '+')
      if (certificationsRef.value) animateCounter(certificationsRef.value, 3)
    }
  })

  // Animation des éléments flottants
  gsap.to('.floating-element', {
    y: -20,
    duration: 2,
    ease: 'power2.inOut',
    stagger: 0.2,
    repeat: -1,
    yoyo: true
  })

  // Animation du curseur clignotant
  gsap.to('.code-cursor', {
    opacity: 0,
    duration: 0.8,
    repeat: -1,
    yoyo: true,
    ease: 'power2.inOut'
  })

  // Animation des lignes de code
  ScrollTrigger.create({
    trigger: '.profile-card',
    start: 'top 70%',
    onEnter: () => {
      gsap.fromTo('.code-line', {
        opacity: 0,
        x: -20
      }, {
        opacity: 1,
        x: 0,
        duration: 0.6,
        stagger: 0.1,
        ease: 'power2.out'
      })
    }
  })

  // Parallax effect pour les éléments visuels
  ScrollTrigger.create({
    trigger: aboutRef.value,
    start: 'top bottom',
    end: 'bottom top',
    scrub: true,
    onUpdate: self => {
      const progress = self.progress
      gsap.to('.floating-element', {
        y: progress * 50,
        rotation: progress * 360,
        duration: 0.3,
        stagger: 0.1
      })
    }
  })
})
</script>

<style scoped>
.about {
  padding: 6rem 0;
  background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 100%);
  position: relative;
  overflow: hidden;
}

.about::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><circle cx="10" cy="10" r="1" fill="%233b82f6" opacity="0.1"/><circle cx="90" cy="90" r="1" fill="%238b5cf6" opacity="0.1"/></svg>');
  animation: float 20s ease-in-out infinite;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
}

.section-title {
  font-size: 3rem;
  font-weight: bold;
  color: #1e293b;
  margin-bottom: 1rem;
  position: relative;
}

.section-title::after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 50%;
  transform: translateX(-50%);
  width: 100px;
  height: 4px;
  background: linear-gradient(45deg, #3b82f6, #8b5cf6);
  border-radius: 2px;
}

.section-subtitle {
  font-size: 1.2rem;
  color: #64748b;
  font-weight: 300;
}

.about-content {
  display: flex;
  flex-direction: column;
  gap: 4rem;
  align-items: center;
  margin-bottom: 4rem;
}

.about-text {
  color: #334155;
}

.intro {
  font-size: 1.2rem;
  line-height: 1.8;
  margin-bottom: 2rem;
}

.intro strong {
  color: #3b82f6;
  font-weight: 600;
}

.description {
  font-size: 1.1rem;
  line-height: 1.7;
  margin-bottom: 3rem;
  color: #475569;
}

.highlights {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.highlight-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1.5rem;
  background: white;
  border-radius: 15px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.highlight-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.15);
}

.highlight-icon {
  width: 60px;
  height: 60px;
  background: linear-gradient(45deg, #3b82f6, #8b5cf6);
  border-radius: 15px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  flex-shrink: 0;
}

.icon {
  width: 24px;
  height: 24px;
}

.highlight-content h3 {
  font-size: 1.2rem;
  font-weight: 600;
  color: #1e293b;
  margin: 0 0 0.5rem 0;
}

.highlight-content p {
  color: #64748b;
  margin: 0;
}

.about-visual {
  display: flex;
  justify-content: center;
  align-items: center;
}

.visual-container {
  position: relative;
  width: 100%;
  max-width: 500px;
}

.profile-card {
  background: #1e293b;
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
  position: relative;
  z-index: 2;
}

.card-header {
  background: #334155;
  padding: 1rem 1.5rem;
  display: flex;
  align-items: center;
  gap: 1rem;
}

.card-dots {
  display: flex;
  gap: 0.5rem;
}

.dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
}

.dot.red { background: #ef4444; }
.dot.yellow { background: #f59e0b; }
.dot.green { background: #10b981; }

.card-title {
  color: #e2e8f0;
  font-size: 0.9rem;
  font-family: 'Courier New', monospace;
}

.card-content {
  padding: 2rem;
  font-family: 'Courier New', monospace;
  font-size: 0.9rem;
  line-height: 1.6;
}

.code-line {
  margin-bottom: 0.5rem;
  position: relative;
}

.indent { padding-left: 2rem; }
.indent-2 { padding-left: 4rem; }

.code-key { color: #f59e0b; }
.code-variable { color: #06b6d4; }
.code-operator { color: #e2e8f0; }
.code-string { color: #10b981; }
.code-bracket { color: #8b5cf6; }

.code-cursor {
  display: inline-block;
  width: 2px;
  height: 20px;
  background: #3b82f6;
  margin-left: 5px;
  vertical-align: middle;
}

.floating-elements {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  pointer-events: none;
  z-index: 1;
}

.floating-element {
  position: absolute;
  width: 40px;
  height: 40px;
  background: rgba(59, 130, 246, 0.1);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #3b82f6;
}

.floating-element:nth-child(1) { top: 10%; left: 10%; }
.floating-element:nth-child(2) { top: 20%; right: 10%; }
.floating-element:nth-child(3) { top: 50%; left: 5%; }
.floating-element:nth-child(4) { bottom: 30%; right: 5%; }
.floating-element:nth-child(5) { bottom: 10%; left: 15%; }
.floating-element:nth-child(6) { top: 70%; right: 20%; }

.floating-icon {
  width: 20px;
  height: 20px;
}

.stats-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 2rem;
  margin-top: 4rem;
}

.stat-item {
  text-align: center;
  padding: 2rem;
  background: white;
  border-radius: 20px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.stat-item:hover {
  transform: translateY(-10px);
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.15);
}

.stat-number {
  font-size: 3rem;
  font-weight: bold;
  color: #3b82f6;
  margin-bottom: 0.5rem;
}

.stat-label {
  color: #64748b;
  font-weight: 500;
}

@media (max-width: 768px) {
  .section-title {
    font-size: 2.5rem;
  }

  .stats-container {
    grid-template-columns: repeat(2, 1fr);
    gap: 1rem;
  }

  .stat-item {
    padding: 1.5rem;
  }

  .stat-number {
    font-size: 2.5rem;
  }

  .profile-card {
    max-width: 350px;
  }

  .card-content {
    padding: 1.5rem;
    font-size: 0.8rem;
  }
}

@media (max-width: 480px) {
  .about-content {
    gap: 2rem;
  }

  .stats-container {
    grid-template-columns: 1fr;
    gap: 1rem;
  }
}

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-20px); }
}
</style>