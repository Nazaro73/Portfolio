<template>
  <section id="projects" class="projects" ref="projectsRef">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title" data-aos="fade-up">Mes Projets</h2>
        <div class="section-subtitle" data-aos="fade-up" data-aos-delay="100">
          Découvrez quelques-uns de mes projets les plus significatifs
        </div>
      </div>

      <div class="projects-filter" data-aos="fade-up" data-aos-delay="200">
        <button
          class="filter-btn"
          :class="{ active: activeFilter === 'all' }"
          @click="setFilter('all')"
        >
          Tous
        </button>
        <button
          class="filter-btn"
          :class="{ active: activeFilter === 'frontend' }"
          @click="setFilter('frontend')"
        >
          Frontend
        </button>
        <button
          class="filter-btn"
          :class="{ active: activeFilter === 'fullstack' }"
          @click="setFilter('fullstack')"
        >
          Full Stack
        </button>
        <button
          class="filter-btn"
          :class="{ active: activeFilter === 'mobile' }"
          @click="setFilter('mobile')"
        >
          Mobile
        </button>
      </div>

      <div class="projects-grid" ref="projectsGridRef">
        <div
          class="project-card"
          v-for="project in filteredProjects"
          :key="project.id"
          :data-category="project.category"
          data-aos="fade-up"
          :data-aos-delay="project.delay"
        >
          <div class="project-image">
            <div class="project-overlay">
              <div class="project-actions">
                <button class="action-btn" @click="viewProject(project)">
                  <Eye class="icon" />
                  Voir
                </button>
                <button class="action-btn" v-if="project.github" @click="openGithub(project.github)">
                  <Github class="icon" />
                  Code
                </button>
                <button class="action-btn" v-if="project.demo" @click="openDemo(project.demo)">
                  <ExternalLink class="icon" />
                  Demo
                </button>
              </div>
            </div>
            <div class="project-preview">
              <div class="browser-bar">
                <div class="browser-dots">
                  <span class="dot red"></span>
                  <span class="dot yellow"></span>
                  <span class="dot green"></span>
                </div>
                <div class="browser-url">{{ project.url }}</div>
              </div>
              <div class="project-screenshot">
                <div class="code-preview" v-if="project.category === 'fullstack'">
                  <div class="code-line" v-for="n in 8" :key="n">
                    <span class="line-number">{{ n }}</span>
                    <span class="code-content">{{ getCodeLine(n) }}</span>
                  </div>
                </div>
                <div class="ui-preview" v-else>
                  <div class="ui-header"></div>
                  <div class="ui-content">
                    <div class="ui-card" v-for="n in 3" :key="n"></div>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="project-content">
            <div class="project-category">{{ getCategoryName(project.category) }}</div>
            <h3 class="project-title">{{ project.title }}</h3>
            <p class="project-description">{{ project.description }}</p>

            <div class="project-tech">
              <span
                class="tech-tag"
                v-for="tech in project.technologies"
                :key="tech"
              >
                {{ tech }}
              </span>
            </div>

            <div class="project-stats">
              <div class="stat">
                <Clock class="stat-icon" />
                <span>{{ project.duration }}</span>
              </div>
              <div class="stat" v-if="project.team">
                <Users class="stat-icon" />
                <span>{{ project.team }}</span>
              </div>
              <div class="stat" v-if="project.status">
                <Activity class="stat-icon" />
                <span>{{ project.status }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="projects-cta" data-aos="fade-up" data-aos-delay="800">
        <h3>Intéressé par mon travail ?</h3>
        <p>Contactez-moi pour discuter de vos projets ou collaborer ensemble</p>
        <button class="cta-btn" @click="scrollToContact">
          <MessageCircle class="icon" />
          Discutons de votre projet
        </button>
      </div>
    </div>

    <!-- Modal pour voir les détails du projet -->
    <div class="modal-overlay" v-if="selectedProject" @click="closeModal">
      <div class="modal" @click.stop>
        <button class="modal-close" @click="closeModal">
          <X class="icon" />
        </button>

        <div class="modal-content">
          <div class="modal-header">
            <h2>{{ selectedProject.title }}</h2>
            <div class="modal-category">{{ getCategoryName(selectedProject.category) }}</div>
          </div>

          <div class="modal-description">
            <p>{{ selectedProject.longDescription || selectedProject.description }}</p>
          </div>

          <div class="modal-details">
            <div class="detail-section">
              <h4>Technologies utilisées</h4>
              <div class="tech-list">
                <span
                  class="tech-item"
                  v-for="tech in selectedProject.technologies"
                  :key="tech"
                >
                  {{ tech }}
                </span>
              </div>
            </div>

            <div class="detail-section" v-if="selectedProject.features">
              <h4>Fonctionnalités principales</h4>
              <ul>
                <li v-for="feature in selectedProject.features" :key="feature">
                  {{ feature }}
                </li>
              </ul>
            </div>

            <div class="detail-section" v-if="selectedProject.challenges">
              <h4>Défis techniques</h4>
              <ul>
                <li v-for="challenge in selectedProject.challenges" :key="challenge">
                  {{ challenge }}
                </li>
              </ul>
            </div>
          </div>

          <div class="modal-actions">
            <button v-if="selectedProject.github" @click="openGithub(selectedProject.github)" class="action-btn primary">
              <Github class="icon" />
              Voir le code
            </button>
            <button v-if="selectedProject.demo" @click="openDemo(selectedProject.demo)" class="action-btn">
              <ExternalLink class="icon" />
              Voir la démo
            </button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import {
  Eye,
  Github,
  ExternalLink,
  Clock,
  Users,
  Activity,
  MessageCircle,
  X
} from 'lucide-vue-next'

// Typage des projets
interface Project {
  id: number
  title: string
  description: string
  longDescription?: string
  category: 'frontend' | 'fullstack' | 'mobile' | 'backend'
  technologies: string[]
  duration: string
  status?: string
  team?: string
  url?: string
  github?: string
  demo?: string
  delay?: number
  features?: string[]
  challenges?: string[]
}

gsap.registerPlugin(ScrollTrigger)

const projectsRef = ref<HTMLElement>()
const projectsGridRef = ref<HTMLElement>()
const activeFilter = ref<'all' | Project['category']>('all')
const selectedProject = ref<Project | null>(null)

const projects: Project[] = [
  {
    id: 1,
    title: 'Plateforme E-Learning Biologie',
    description: 'Plateforme complète d\'apprentissage en ligne spécialisée en biologie avec gestion d\'utilisateurs, cours interactifs et suivi de progression.',
    longDescription: 'Une plateforme d\'e-learning moderne développée avec React et Node.js, offrant une expérience d\'apprentissage immersive en biologie. Intégration d\'outils d\'automatisation avec Make et gestion de données avec Airtable.',
    category: 'fullstack',
    technologies: ['React', 'Node.js', 'Express', 'MongoDB', 'Make', 'Airtable'],
    duration: '6 mois',
    status: 'En cours',
    team: 'Équipe de 3',
    url: 'e-learning.360skillvue.com',
    github: 'https://github.com',
    demo: 'https://demo.com',
    delay: 100,
    features: [
      'Système d\'authentification complet',
      'Cours interactifs avec vidéos et quiz',
      'Tableau de bord étudiant et professeur',
      'Suivi de progression en temps réel',
      'Intégration d\'automatisations Make',
      'Gestion de données Airtable'
    ],
    challenges: [
      'Intégration complexe avec des API tierces',
      'Optimisation des performances pour les vidéos',
      'Architecture scalable pour gérer de nombreux utilisateurs',
      'Synchronisation en temps réel des données'
    ]
  },
  {
    id: 2,
    title: 'Dashboard Statistiques LEADS',
    description: 'Application web pour l\'analyse et la visualisation de données clients avec filtres avancés et graphiques interactifs.',
    longDescription: 'Tableau de bord statistique développé avec Vue.js et Express.js pour analyser les données clients. Interface intuitive avec graphiques dynamiques et système de filtrage avancé.',
    category: 'fullstack',
    technologies: ['Vue.js', 'Express.js', 'PostgreSQL', 'Chart.js', 'API REST'],
    duration: '4 mois',
    status: 'Terminé',
    url: 'dashboard.leads.fr',
    github: 'https://github.com',
    delay: 200,
    features: [
      'Visualisation de données en temps réel',
      'Filtres dynamiques et sauvegarde de vues',
      'Graphiques interactifs avec Chart.js',
      'Export de rapports PDF/Excel',
      'Interface responsive et intuitive',
      'Intégration API externe pour les données'
    ],
    challenges: [
      'Optimisation des requêtes complexes PostgreSQL',
      'Gestion de gros volumes de données',
      'Interface utilisateur performante et réactive',
      'Cartographie et intégration de données externes'
    ]
  },
  {
    id: 3,
    title: 'Portfolio Interactif Vue.js',
    description: 'Portfolio personnel développé avec Vue.js, animations GSAP et design responsive moderne.',
    longDescription: 'Portfolio personnel moderne avec des animations sophistiquées utilisant GSAP et ScrollTrigger. Design responsive et performances optimisées.',
    category: 'frontend',
    technologies: ['Vue.js', 'TypeScript', 'GSAP', 'CSS3', 'Responsive Design'],
    duration: '3 semaines',
    status: 'Terminé',
    url: 'abdel-rahim-khababa.com',
    github: 'https://github.com',
    demo: 'https://abdel-rahim-khababa.com',
    delay: 300,
    features: [
      'Animations fluides avec GSAP',
      'Design responsive moderne',
      'Optimisation SEO et performances',
      'Mode sombre/clair',
      'Formulaire de contact fonctionnel',
      'Intégration continue avec Netlify'
    ],
    challenges: [
      'Optimisation des animations pour mobile',
      'Gestion des états et transitions complexes',
      'Performance et chargement rapide',
      'Compatibilité navigateurs'
    ]
  },
  {
    id: 4,
    title: 'Application Flutter E-commerce',
    description: 'Application mobile e-commerce avec panier, paiements intégrés et gestion d\'inventaire.',
    longDescription: 'Application mobile complète développée avec Flutter, offrant une expérience d\'achat fluide avec authentification, panier, paiements et suivi de commandes.',
    category: 'mobile',
    technologies: ['Flutter', 'Dart', 'Firebase', 'Stripe API', 'Provider'],
    duration: '5 mois',
    status: 'Terminé',
    url: 'mobile-shop.app',
    github: 'https://github.com',
    delay: 400,
    features: [
      'Authentification Firebase',
      'Catalogue de produits avec recherche',
      'Panier et gestion de commandes',
      'Paiements sécurisés avec Stripe',
      'Notifications push',
      'Interface utilisateur native'
    ],
    challenges: [
      'Intégration des paiements sécurisés',
      'Optimisation des performances sur différents appareils',
      'Gestion des états complexes avec Provider',
      'Tests unitaires et d\'intégration'
    ]
  },
  {
    id: 5,
    title: 'API REST Node.js',
    description: 'API REST complète avec authentification JWT, documentation Swagger et tests automatisés.',
    longDescription: 'API REST robuste développée avec Node.js et Express, incluant authentification JWT, validation des données, documentation complète et tests automatisés.',
    category: 'fullstack',
    technologies: ['Node.js', 'Express', 'MongoDB', 'JWT', 'Swagger', 'Jest'],
    duration: '2 mois',
    status: 'Terminé',
    url: 'api.example.com',
    github: 'https://github.com',
    delay: 500,
    features: [
      'Authentification JWT sécurisée',
      'CRUD complet pour toutes les ressources',
      'Validation des données avec Joi',
      'Documentation Swagger interactive',
      'Tests unitaires et d\'intégration',
      'Middleware de sécurité et logging'
    ],
    challenges: [
      'Architecture scalable et maintenable',
      'Sécurité et protection contre les attaques',
      'Performance et optimisation des requêtes',
      'Documentation complète et à jour'
    ]
  },
  {
    id: 6,
    title: 'Interface React Dashboard',
    description: 'Tableau de bord administrateur avec gestion d\'utilisateurs, graphiques et exports de données.',
    longDescription: 'Interface d\'administration moderne développée avec React, offrant une gestion complète des utilisateurs, des analyses détaillées et des fonctionnalités d\'export.',
    category: 'frontend',
    technologies: ['React', 'TypeScript', 'Material-UI', 'Redux Toolkit', 'Recharts'],
    duration: '3 mois',
    status: 'Terminé',
    url: 'admin.dashboard.com',
    github: 'https://github.com',
    demo: 'https://demo-dashboard.com',
    delay: 600,
    features: [
      'Interface utilisateur intuitive avec Material-UI',
      'Gestion complète des utilisateurs et rôles',
      'Graphiques et analyses en temps réel',
      'Export de données multiples formats',
      'Recherche et filtrage avancés',
      'Thème sombre/clair personnalisable'
    ],
    challenges: [
      'Gestion d\'état complexe avec Redux',
      'Optimisation des rendus avec React.memo',
      'Interface responsive pour tablettes',
      'Accessibilité et standards WCAG'
    ]
  }
]

const filteredProjects = computed(() => {
  if (activeFilter.value === 'all') {
    return projects
  }
  return projects.filter(project => project.category === activeFilter.value)
})

const setFilter = (filter: Project['category'] | 'all') => {
  activeFilter.value = filter
  animateFilterChange()
}

const animateFilterChange = () => {
  gsap.fromTo('.project-card', {
    opacity: 0,
    y: 30,
    scale: 0.9
  }, {
    opacity: 1,
    y: 0,
    scale: 1,
    duration: 0.6,
    stagger: 0.1,
    ease: 'power2.out'
  })
}

const getCategoryName = (category: Project['category']) => {
  const names: Record<Project['category'], string> = {
    frontend: 'Frontend',
    fullstack: 'Full Stack',
    mobile: 'Mobile',
    backend: 'Backend'
  }
  return names[category] || category
}

const getCodeLine = (n: number) => {
  const lines = [
    'const express = require("express");',
    'const app = express();',
    '',
    'app.get("/api/users", async (req, res) => {',
    '  const users = await User.find();',
    '  res.json(users);',
    '});',
    ''
  ]
  return lines[n - 1] || ''
}

const viewProject = (project: Project) => {
  selectedProject.value = project
}

const closeModal = () => {
  selectedProject.value = null
}

const openGithub = (url: string) => {
  window.open(url, '_blank')
}

const openDemo = (url: string) => {
  window.open(url, '_blank')
}

const scrollToContact = () => {
  const element = document.getElementById('contact')
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

onMounted(() => {
  // Animation des cartes au scroll
  ScrollTrigger.batch('.project-card', {
    onEnter: (elements) => {
      gsap.fromTo(elements, {
        y: 60,
        opacity: 0,
        scale: 0.9
      }, {
        y: 0,
        opacity: 1,
        scale: 1,
        duration: 0.8,
        ease: 'power2.out',
        stagger: 0.1
      })
    }
  })

  // Animation de hover pour les cartes
  document.querySelectorAll('.project-card').forEach(card => {
    card.addEventListener('mouseenter', () => {
      gsap.to(card, {
        y: -10,
        duration: 0.3,
        ease: 'power2.out'
      })
    })

    card.addEventListener('mouseleave', () => {
      gsap.to(card, {
        y: 0,
        duration: 0.3,
        ease: 'power2.out'
      })
    })
  })

  // Parallax pour les éléments de projet
  ScrollTrigger.create({
    trigger: projectsRef.value,
    start: 'top bottom',
    end: 'bottom top',
    scrub: 1,
    onUpdate: (self) => {
      const progress = self.progress
      gsap.to('.project-card:nth-child(odd)', {
        y: progress * 30,
        duration: 0.3
      })
      gsap.to('.project-card:nth-child(even)', {
        y: progress * -30,
        duration: 0.3
      })
    }
  })
})
</script>

<style scoped>
.projects {
  padding: 6rem 0;
  background: #0f172a;
  position: relative;
  overflow: hidden;
}

.projects::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(circle at 30% 70%, rgba(59, 130, 246, 0.1) 0%, transparent 50%),
              radial-gradient(circle at 70% 30%, rgba(139, 92, 246, 0.1) 0%, transparent 50%);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  position: relative;
  z-index: 2;
}

.section-header {
  text-align: center;
  margin-bottom: 3rem;
}

.section-title {
  font-size: 3rem;
  font-weight: bold;
  color: #e2e8f0;
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
  color: #94a3b8;
  font-weight: 300;
}

.projects-filter {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 3rem;
  flex-wrap: wrap;
}

.filter-btn {
  padding: 0.8rem 1.5rem;
  border: 2px solid rgba(59, 130, 246, 0.3);
  background: transparent;
  color: #94a3b8;
  border-radius: 25px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.filter-btn:hover,
.filter-btn.active {
  background: linear-gradient(45deg, #3b82f6, #8b5cf6);
  color: white;
  border-color: transparent;
  transform: translateY(-2px);
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 2rem;
  margin-bottom: 4rem;
}

.project-card {
  background: rgba(30, 41, 59, 0.5);
  backdrop-filter: blur(10px);
  border-radius: 20px;
  overflow: hidden;
  border: 1px solid rgba(148, 163, 184, 0.1);
  transition: all 0.3s ease;
  cursor: pointer;
}

.project-card:hover {
  border-color: rgba(59, 130, 246, 0.3);
  box-shadow: 0 20px 40px rgba(59, 130, 246, 0.1);
}

.project-image {
  position: relative;
  height: 250px;
  overflow: hidden;
}

.project-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
  z-index: 10;
}

.project-card:hover .project-overlay {
  opacity: 1;
}

.project-actions {
  display: flex;
  gap: 1rem;
}

.action-btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.8rem 1.2rem;
  background: rgba(59, 130, 246, 0.9);
  color: white;
  border: none;
  border-radius: 25px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.action-btn:hover {
  background: #3b82f6;
  transform: translateY(-2px);
}

.action-btn.primary {
  background: linear-gradient(45deg, #3b82f6, #8b5cf6);
}

.icon {
  width: 16px;
  height: 16px;
}

.project-preview {
  height: 100%;
  background: #1e293b;
  position: relative;
}

.browser-bar {
  display: flex;
  align-items: center;
  padding: 0.8rem 1rem;
  background: #334155;
  gap: 1rem;
}

.browser-dots {
  display: flex;
  gap: 0.5rem;
}

.dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
}

.dot.red { background: #ef4444; }
.dot.yellow { background: #f59e0b; }
.dot.green { background: #10b981; }

.browser-url {
  font-size: 0.8rem;
  color: #94a3b8;
  font-family: 'Courier New', monospace;
}

.project-screenshot {
  padding: 1rem;
  height: calc(100% - 60px);
}

.code-preview {
  font-family: 'Courier New', monospace;
  font-size: 0.8rem;
  line-height: 1.6;
}

.code-line {
  display: flex;
  align-items: center;
  margin-bottom: 0.3rem;
}

.line-number {
  color: #64748b;
  margin-right: 1rem;
  min-width: 20px;
  text-align: right;
}

.code-content {
  color: #e2e8f0;
}

.ui-preview {
  height: 100%;
}

.ui-header {
  height: 40px;
  background: rgba(59, 130, 246, 0.2);
  border-radius: 8px;
  margin-bottom: 1rem;
}

.ui-content {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.ui-card {
  height: 30px;
  background: rgba(148, 163, 184, 0.2);
  border-radius: 6px;
}

.project-content {
  padding: 2rem;
}

.project-category {
  display: inline-block;
  background: rgba(59, 130, 246, 0.2);
  color: #3b82f6;
  padding: 0.3rem 0.8rem;
  border-radius: 15px;
  font-size: 0.8rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.project-title {
  font-size: 1.5rem;
  font-weight: bold;
  color: #e2e8f0;
  margin: 0 0 1rem 0;
}

.project-description {
  color: #94a3b8;
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.project-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.tech-tag {
  background: rgba(139, 92, 246, 0.2);
  color: #8b5cf6;
  padding: 0.3rem 0.8rem;
  border-radius: 12px;
  font-size: 0.8rem;
  font-weight: 500;
}

.project-stats {
  display: flex;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.stat {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #94a3b8;
  font-size: 0.9rem;
}

.stat-icon {
  width: 16px;
  height: 16px;
}

.projects-cta {
  text-align: center;
  padding: 3rem;
  background: rgba(30, 41, 59, 0.5);
  border-radius: 20px;
  border: 1px solid rgba(148, 163, 184, 0.1);
}

.projects-cta h3 {
  font-size: 2rem;
  font-weight: bold;
  color: #e2e8f0;
  margin: 0 0 1rem 0;
}

.projects-cta p {
  color: #94a3b8;
  margin-bottom: 2rem;
  font-size: 1.1rem;
}

.cta-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 1rem 2rem;
  background: linear-gradient(45deg, #3b82f6, #8b5cf6);
  color: white;
  border: none;
  border-radius: 50px;
  font-weight: 600;
  font-size: 1.1rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

.cta-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 30px rgba(59, 130, 246, 0.3);
}

/* Modal Styles */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  padding: 2rem;
}

.modal {
  background: #1e293b;
  border-radius: 20px;
  max-width: 800px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  position: relative;
  border: 1px solid rgba(148, 163, 184, 0.2);
}

.modal-close {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: rgba(59, 130, 246, 0.2);
  color: #3b82f6;
  border: none;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
}

.modal-close:hover {
  background: #3b82f6;
  color: white;
}

.modal-content {
  padding: 3rem;
}

.modal-header h2 {
  font-size: 2rem;
  font-weight: bold;
  color: #e2e8f0;
  margin: 0 0 0.5rem 0;
}

.modal-category {
  display: inline-block;
  background: rgba(59, 130, 246, 0.2);
  color: #3b82f6;
  padding: 0.3rem 0.8rem;
  border-radius: 15px;
  font-size: 0.9rem;
  font-weight: 600;
  margin-bottom: 2rem;
}

.modal-description {
  color: #94a3b8;
  line-height: 1.7;
  margin-bottom: 2rem;
  font-size: 1.1rem;
}

.modal-details {
  margin-bottom: 2rem;
}

.detail-section {
  margin-bottom: 2rem;
}

.detail-section h4 {
  color: #e2e8f0;
  font-weight: 600;
  margin-bottom: 1rem;
}

.tech-list {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tech-item {
  background: rgba(139, 92, 246, 0.2);
  color: #8b5cf6;
  padding: 0.5rem 1rem;
  border-radius: 15px;
  font-weight: 500;
}

.detail-section ul {
  margin: 0;
  padding-left: 1.5rem;
}

.detail-section li {
  color: #94a3b8;
  margin-bottom: 0.5rem;
  line-height: 1.6;
}

.modal-actions {
  display: flex;
  gap: 1rem;
  justify-content: flex-end;
}

@media (max-width: 768px) {
  .section-title {
    font-size: 2.5rem;
  }

  .projects-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }

  .projects-filter {
    flex-wrap: wrap;
    justify-content: center;
  }

  .filter-btn {
    padding: 0.6rem 1.2rem;
    font-size: 0.9rem;
  }

  .project-card {
    margin-bottom: 1rem;
  }

  .project-image {
    height: 200px;
  }

  .project-content {
    padding: 1.5rem;
  }

  .projects-cta {
    padding: 2rem;
  }

  .projects-cta h3 {
    font-size: 1.5rem;
  }

  .modal {
    margin: 1rem;
  }

  .modal-content {
    padding: 2rem;
  }

  .modal-actions {
    flex-direction: column;
  }

  .action-btn {
    justify-content: center;
  }
}
</style>