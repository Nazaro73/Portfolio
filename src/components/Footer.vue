<template>
  <footer class="footer" ref="footerRef">
    <div class="container">
      <div class="footer-content">
        <div class="footer-main">
          <div class="footer-brand">
            <h3 class="brand-name">Abdel-Rahim KHABABA</h3>
            <p class="brand-tagline">Développeur Full Stack passionné</p>
            <div class="brand-location">
              <MapPin class="location-icon" />
              <span>Chambéry, France</span>
            </div>
          </div>

          <div class="footer-links">
            <div class="link-group">
              <h4>Navigation</h4>
              <nav class="footer-nav">
                <a href="#home" @click="scrollToSection('home')">Accueil</a>
                <a href="#about" @click="scrollToSection('about')">À propos</a>
                <a href="#skills" @click="scrollToSection('skills')">Compétences</a>
                <a href="#experience" @click="scrollToSection('experience')">Expérience</a>
                <a href="#projects" @click="scrollToSection('projects')">Projets</a>
                <a href="#contact" @click="scrollToSection('contact')">Contact</a>
              </nav>
            </div>

            <div class="link-group">
              <h4>Contact</h4>
              <div class="contact-info">
                <a href="mailto:Abdel-Rahim.KHABABA@hotmail.com" class="contact-link">
                  <Mail class="icon" />
                  <span>Email</span>
                </a>
                <a href="tel:0766324045" class="contact-link">
                  <Phone class="icon" />
                  <span>Téléphone</span>
                </a>
                <a href="https://linkedin.com" target="_blank" class="contact-link">
                  <Linkedin class="icon" />
                  <span>LinkedIn</span>
                </a>
                <a href="https://github.com" target="_blank" class="contact-link">
                  <Github class="icon" />
                  <span>GitHub</span>
                </a>
              </div>
            </div>

            <div class="link-group">
              <h4>Compétences</h4>
              <div class="skills-summary">
                <span class="skill-tag">Vue.js</span>
                <span class="skill-tag">React</span>
                <span class="skill-tag">Node.js</span>
                <span class="skill-tag">Python</span>
                <span class="skill-tag">Java</span>
                <span class="skill-tag">PostgreSQL</span>
              </div>
            </div>
          </div>
        </div>

        <div class="footer-bottom">
          <div class="footer-divider"></div>

          <div class="footer-info">
            <div class="copyright">
              <p>&copy; {{ currentYear }} Abdel-Rahim KHABABA. Tous droits réservés.</p>
            </div>

            <div class="footer-meta">
              <span class="status-indicator">
                <div class="status-dot available"></div>
                Disponible pour de nouveaux projets
              </span>
            </div>

            <div class="back-to-top" @click="scrollToTop">
              <div class="back-to-top-btn">
                <ArrowUp class="icon" />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="footer-background">
      <div class="bg-grid"></div>
      <div class="bg-gradient"></div>
    </div>
  </footer>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import {
  MapPin,
  Mail,
  Phone,
  Linkedin,
  Github,
  ArrowUp
} from 'lucide-vue-next'

gsap.registerPlugin(ScrollTrigger)

const footerRef = ref<HTMLElement>()

const currentYear = computed(() => new Date().getFullYear())

const scrollToSection = (sectionId: string) => {
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

onMounted(() => {
  // Animation du footer au scroll
  ScrollTrigger.create({
    trigger: footerRef.value,
    start: 'top 90%',
    onEnter: () => {
      // Animation de la marque
      gsap.fromTo('.footer-brand', {
        y: 30,
        opacity: 0
      }, {
        y: 0,
        opacity: 1,
        duration: 0.8,
        ease: 'power2.out'
      })

      // Animation des groupes de liens
      gsap.fromTo('.link-group', {
        y: 30,
        opacity: 0
      }, {
        y: 0,
        opacity: 1,
        duration: 0.8,
        stagger: 0.2,
        ease: 'power2.out',
        delay: 0.2
      })

      // Animation du footer bottom
      gsap.fromTo('.footer-bottom', {
        y: 20,
        opacity: 0
      }, {
        y: 0,
        opacity: 1,
        duration: 0.8,
        ease: 'power2.out',
        delay: 0.6
      })
    }
  })

  // Animation de hover pour le bouton retour en haut
  const backToTopBtn = document.querySelector('.back-to-top-btn')
  if (backToTopBtn) {
    backToTopBtn.addEventListener('mouseenter', () => {
      gsap.to(backToTopBtn, {
        scale: 1.1,
        rotation: -5,
        duration: 0.3,
        ease: 'power2.out'
      })
    })

    backToTopBtn.addEventListener('mouseleave', () => {
      gsap.to(backToTopBtn, {
        scale: 1,
        rotation: 0,
        duration: 0.3,
        ease: 'power2.out'
      })
    })
  }

  // Animation de pulsation pour le statut disponible
  gsap.to('.status-dot.available', {
    scale: 1.3,
    opacity: 0.7,
    duration: 1.5,
    repeat: -1,
    yoyo: true,
    ease: 'power2.inOut'
  })

  // Afficher le bouton retour en haut seulement quand on scroll
  ScrollTrigger.create({
    start: 'top -100',
    end: 'max',
    onUpdate: (self) => {
      if (self.progress > 0.1) {
        gsap.to('.back-to-top', {
          opacity: 1,
          pointerEvents: 'auto',
          duration: 0.3
        })
      } else {
        gsap.to('.back-to-top', {
          opacity: 0,
          pointerEvents: 'none',
          duration: 0.3
        })
      }
    }
  })
})
</script>

<style scoped>
.footer {
  background: #0f172a;
  color: #e2e8f0;
  padding: 4rem 0 2rem;
  position: relative;
  overflow: hidden;
}

.footer-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 1;
}

.bg-grid {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image:
    linear-gradient(rgba(148, 163, 184, 0.05) 1px, transparent 1px),
    linear-gradient(90deg, rgba(148, 163, 184, 0.05) 1px, transparent 1px);
  background-size: 50px 50px;
  animation: moveGrid 20s linear infinite;
}

@keyframes moveGrid {
  0% { transform: translate(0, 0); }
  100% { transform: translate(50px, 50px); }
}

.bg-gradient {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(circle at 20% 50%, rgba(59, 130, 246, 0.1) 0%, transparent 50%),
              radial-gradient(circle at 80% 50%, rgba(139, 92, 246, 0.1) 0%, transparent 50%);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  position: relative;
  z-index: 2;
}

.footer-content {
  display: flex;
  flex-direction: column;
}

.footer-main {
  display: flex;
  flex-direction: column;
  gap: 4rem;
  margin-bottom: 3rem;
}

.footer-brand {
  display: flex;
  flex-direction: column;
}

.brand-name {
  font-size: 1.8rem;
  font-weight: bold;
  background: linear-gradient(45deg, #3b82f6, #8b5cf6);
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  margin: 0 0 0.5rem 0;
}

.brand-tagline {
  color: #94a3b8;
  margin: 0 0 1rem 0;
  font-size: 1.1rem;
}

.brand-location {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #64748b;
  font-size: 0.9rem;
}

.location-icon {
  width: 16px;
  height: 16px;
}

.footer-links {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 3rem;
}

.link-group {
  display: flex;
  flex-direction: column;
}

.link-group h4 {
  font-size: 1.1rem;
  font-weight: 600;
  color: #e2e8f0;
  margin: 0 0 1rem 0;
  position: relative;
}

.link-group h4::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 30px;
  height: 2px;
  background: linear-gradient(45deg, #3b82f6, #8b5cf6);
  border-radius: 1px;
}

.footer-nav {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.footer-nav a {
  color: #94a3b8;
  text-decoration: none;
  transition: all 0.3s ease;
  padding: 0.3rem 0;
  position: relative;
}

.footer-nav a::before {
  content: '';
  position: absolute;
  left: -15px;
  top: 50%;
  width: 0;
  height: 2px;
  background: #3b82f6;
  transform: translateY(-50%);
  transition: width 0.3s ease;
}

.footer-nav a:hover {
  color: #3b82f6;
  transform: translateX(10px);
}

.footer-nav a:hover::before {
  width: 10px;
}

.contact-info {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.contact-link {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  color: #94a3b8;
  text-decoration: none;
  transition: all 0.3s ease;
  padding: 0.5rem;
  border-radius: 8px;
}

.contact-link:hover {
  color: #3b82f6;
  background: rgba(59, 130, 246, 0.1);
  transform: translateX(5px);
}

.contact-link .icon {
  width: 16px;
  height: 16px;
}

.skills-summary {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.skill-tag {
  background: rgba(59, 130, 246, 0.2);
  color: #3b82f6;
  padding: 0.3rem 0.8rem;
  border-radius: 12px;
  font-size: 0.8rem;
  font-weight: 500;
  border: 1px solid rgba(59, 130, 246, 0.3);
  transition: all 0.3s ease;
}

.skill-tag:hover {
  background: #3b82f6;
  color: white;
  transform: translateY(-2px);
}

.footer-bottom {
  border-top: 1px solid rgba(148, 163, 184, 0.2);
  padding-top: 2rem;
}

.footer-divider {
  width: 100%;
  height: 1px;
  background: linear-gradient(90deg, transparent, rgba(59, 130, 246, 0.5), transparent);
  margin-bottom: 2rem;
}

.footer-info {
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  align-items: center;
  gap: 2rem;
}

.copyright {
  color: #64748b;
  font-size: 0.9rem;
}

.copyright p {
  margin: 0;
}

.footer-meta {
  display: flex;
  justify-content: center;
}

.status-indicator {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #10b981;
  font-size: 0.9rem;
  font-weight: 500;
}

.status-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
}

.status-dot.available {
  background: #10b981;
  box-shadow: 0 0 0 2px rgba(16, 185, 129, 0.3);
}

.back-to-top {
  display: flex;
  justify-content: flex-end;
  opacity: 0;
  pointer-events: none;
}

.back-to-top-btn {
  width: 50px;
  height: 50px;
  background: linear-gradient(45deg, #3b82f6, #8b5cf6);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 20px rgba(59, 130, 246, 0.3);
}

.back-to-top-btn:hover {
  box-shadow: 0 6px 30px rgba(59, 130, 246, 0.4);
}

.back-to-top-btn .icon {
  width: 20px;
  height: 20px;
  color: white;
}

@media (max-width: 768px) {
  .footer {
    padding: 3rem 0 2rem;
  }

  .footer-links {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .footer-info {
    grid-template-columns: 1fr;
    gap: 1rem;
    text-align: center;
  }

  .footer-meta {
    justify-content: center;
  }

  .back-to-top {
    justify-content: center;
  }

  .brand-name {
    font-size: 1.5rem;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 0 1rem;
  }

  .footer-main {
    gap: 2rem;
  }

  .footer-links {
    gap: 1.5rem;
  }

  .contact-link {
    padding: 0.3rem;
  }

  .back-to-top-btn {
    width: 40px;
    height: 40px;
  }

  .back-to-top-btn .icon {
    width: 16px;
    height: 16px;
  }
}
</style>