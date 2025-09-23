<template>
  <section id="experience" class="experience" ref="experienceRef">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title" data-aos="fade-up">Expérience Professionnelle</h2>
        <div class="section-subtitle" data-aos="fade-up" data-aos-delay="100">
          Mon parcours professionnel et académique
        </div>
      </div>

      <div class="timeline-container">
        <div class="timeline-line" ref="timelineLineRef"></div>

        <div class="timeline-items">
          <div
            class="timeline-item"
            v-for="(item, index) in experiences"
            :key="index"
            :class="{ 'timeline-item-right': index % 2 === 1 }"
            data-aos="fade-up"
            :data-aos-delay="index * 100 + 200"
          >
            <div class="timeline-dot" :class="`timeline-dot-${item.type}`">
              <component :is="item.icon" class="timeline-icon" />
            </div>

            <div class="timeline-content">
              <div class="timeline-card">
                <div class="timeline-date">{{ item.date }}</div>
                <h3 class="timeline-title">{{ item.title }}</h3>
                <h4 class="timeline-company">{{ item.company }}</h4>
                <p class="timeline-description">{{ item.description }}</p>

                <div class="timeline-skills" v-if="item.skills">
                  <span
                    class="timeline-skill"
                    v-for="skill in item.skills"
                    :key="skill"
                  >
                    {{ skill }}
                  </span>
                </div>

                <div class="timeline-achievements" v-if="item.achievements">
                  <h5>Réalisations clés :</h5>
                  <ul>
                    <li v-for="achievement in item.achievements" :key="achievement">
                      {{ achievement }}
                    </li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="certifications" data-aos="fade-up" data-aos-delay="800">
        <h3 class="certifications-title">Formations & Certifications</h3>
        <div class="certifications-grid">
          <div
            class="certification-item"
            v-for="cert in certifications"
            :key="cert.name"
            data-aos="zoom-in"
            :data-aos-delay="cert.delay"
          >
            <div class="certification-icon">
              <component :is="cert.icon" class="icon" />
            </div>
            <div class="certification-content">
              <h4>{{ cert.name }}</h4>
              <p class="certification-institution">{{ cert.institution }}</p>
              <p class="certification-year">{{ cert.year }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import {
  Briefcase,
  GraduationCap,
  Award,
  Code,
  Database,
  Globe,
  Smartphone
} from 'lucide-vue-next'

gsap.registerPlugin(ScrollTrigger)

const experienceRef = ref<HTMLElement>()
const timelineLineRef = ref<HTMLElement>()

const experiences = [
  {
    date: '2025 - En cours',
    title: 'Développeur Full Stack',
    company: '360 SKILL VUE',
    description: 'Conception et développement d\'une plateforme d\'e-learning spécialisée en biologie. Utilisation de React et Node.js pour le développement front-end et back-end.',
    type: 'work',
    icon: Briefcase,
    skills: ['React', 'Node.js', 'Make', 'Airtable', 'API REST'],
    achievements: [
      'Développement d\'une plateforme e-learning complète',
      'Intégration d\'automatisations avec Make',
      'Gestion de données complexes avec Airtable',
      'Mise en place d\'une architecture scalable'
    ]
  },
  {
    date: '2023 - 2024',
    title: 'Bachelor Développeur Concepteur d\'Application',
    company: 'MY DIGITAL SCHOOL, Annecy',
    description: 'Formation complète en développement d\'applications avec obtention du titre RNCP Développeur Concepteur d\'Application.',
    type: 'education',
    icon: GraduationCap,
    skills: ['Vue.js', 'React', 'Node.js', 'Gestion de projet', 'UX/UI Design']
  },
  {
    date: '2023 - 2024',
    title: 'Développeur Full Stack',
    company: 'LEADS.FR',
    description: 'Développement d\'un logiciel statistique utilisant Vue.js, Express.js et PostgreSQL pour l\'affichage et le filtrage de statistiques clients.',
    type: 'work',
    icon: Briefcase,
    skills: ['Vue.js', 'Express.js', 'PostgreSQL', 'API REST', 'Intégration de données'],
    achievements: [
      'Développement d\'un tableau de bord statistique interactif',
      'Intégration et cartographie des données client',
      'Optimisation des performances de requêtes complexes',
      'Mise en place de filtres avancés pour l\'analyse de données'
    ]
  },
  {
    date: '2020 - 2022',
    title: 'DUT Informatique',
    company: 'IUT2, Département Informatique, UGA, Grenoble',
    description: 'Formation technique solide en informatique couvrant la programmation, les bases de données, les réseaux et le génie logiciel.',
    type: 'education',
    icon: GraduationCap,
    skills: ['Java', 'C++', 'SQL', 'Algorithmes', 'Génie logiciel', 'Réseaux']
  },
  {
    date: '2020',
    title: 'Baccalauréat SVT',
    company: 'Lycée Louis Armand, Chambéry',
    description: 'Baccalauréat Sciences et Vie de la Terre avec option Physique-Chimie, développant des compétences analytiques et scientifiques.',
    type: 'education',
    icon: Award,
    skills: ['Sciences', 'Physique-Chimie', 'Mathématiques', 'Analyse']
  }
]

const certifications = [
  {
    name: 'Développeur Concepteur d\'Application',
    institution: 'Titre RNCP - My Digital School',
    year: '2024',
    icon: Award,
    delay: 100
  },
  {
    name: 'DUT Informatique',
    institution: 'Université Grenoble Alpes',
    year: '2022',
    icon: GraduationCap,
    delay: 200
  },
  {
    name: 'Vue.js Certification',
    institution: 'Formation continue',
    year: '2023',
    icon: Code,
    delay: 300
  }
]

onMounted(() => {
  // Animation de la ligne de timeline au scroll
  ScrollTrigger.create({
    trigger: '.timeline-container',
    start: 'top 80%',
    end: 'bottom 20%',
    scrub: 1,
    onUpdate: (self) => {
      const progress = self.progress
      if (timelineLineRef.value) {
        gsap.to(timelineLineRef.value, {
          scaleY: progress,
          duration: 0.1,
          ease: 'none'
        })
      }
    }
  })

  // Animation des dots de la timeline
  ScrollTrigger.batch('.timeline-dot', {
    onEnter: (elements) => {
      gsap.fromTo(elements, {
        scale: 0,
        opacity: 0
      }, {
        scale: 1,
        opacity: 1,
        duration: 0.8,
        ease: 'back.out(1.7)',
        stagger: 0.2
      })
    }
  })

  // Animation des cartes de timeline
  ScrollTrigger.batch('.timeline-card', {
    onEnter: (elements) => {
      gsap.fromTo(elements, {
        y: 50,
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

  // Animation des skills tags
  ScrollTrigger.batch('.timeline-skill', {
    onEnter: (elements) => {
      gsap.fromTo(elements, {
        y: 20,
        opacity: 0
      }, {
        y: 0,
        opacity: 1,
        duration: 0.6,
        ease: 'power2.out',
        stagger: 0.1
      })
    }
  })

  // Parallax effect pour les éléments de timeline
  ScrollTrigger.create({
    trigger: experienceRef.value,
    start: 'top bottom',
    end: 'bottom top',
    scrub: true,
    onUpdate: (self) => {
      const progress = self.progress
      gsap.to('.timeline-item:nth-child(odd)', {
        x: progress * 30,
        duration: 0.3
      })
      gsap.to('.timeline-item:nth-child(even)', {
        x: progress * -30,
        duration: 0.3
      })
    }
  })
})
</script>

<style scoped>
.experience {
  padding: 6rem 0;
  background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 100%);
  position: relative;
  overflow: hidden;
}

.experience::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image:
    radial-gradient(circle at 25% 25%, rgba(59, 130, 246, 0.05) 0%, transparent 50%),
    radial-gradient(circle at 75% 75%, rgba(139, 92, 246, 0.05) 0%, transparent 50%);
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

.timeline-container {
  position: relative;
  margin-bottom: 4rem;
}

.timeline-line {
  position: absolute;
  left: 50%;
  top: 0;
  bottom: 0;
  width: 4px;
  background: linear-gradient(to bottom, #3b82f6, #8b5cf6);
  transform: translateX(-50%) scaleY(0);
  transform-origin: top;
  border-radius: 2px;
}

.timeline-items {
  position: relative;
}

.timeline-item {
  position: relative;
  margin-bottom: 4rem;
  display: flex;
  align-items: center;
}

.timeline-item-right {
  flex-direction: row-reverse;
}

.timeline-dot {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  width: 60px;
  height: 60px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  z-index: 10;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
}

.timeline-dot-work {
  background: linear-gradient(45deg, #3b82f6, #1d4ed8);
}

.timeline-dot-education {
  background: linear-gradient(45deg, #8b5cf6, #7c3aed);
}

.timeline-icon {
  width: 24px;
  height: 24px;
}

.timeline-content {
  width: calc(50% - 60px);
  padding: 0 2rem;
}

.timeline-item-right .timeline-content {
  text-align: right;
}

.timeline-card {
  background: white;
  border-radius: 20px;
  padding: 2rem;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.1);
  position: relative;
  transition: all 0.3s ease;
  border: 1px solid rgba(148, 163, 184, 0.1);
}

.timeline-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.15);
}

.timeline-card::before {
  content: '';
  position: absolute;
  top: 50%;
  width: 20px;
  height: 20px;
  background: white;
  border: 1px solid rgba(148, 163, 184, 0.1);
  transform: translateY(-50%) rotate(45deg);
}

.timeline-item:not(.timeline-item-right) .timeline-card::before {
  right: -10px;
}

.timeline-item-right .timeline-card::before {
  left: -10px;
}

.timeline-date {
  display: inline-block;
  background: linear-gradient(45deg, #3b82f6, #8b5cf6);
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.9rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.timeline-title {
  font-size: 1.5rem;
  font-weight: bold;
  color: #1e293b;
  margin: 0 0 0.5rem 0;
}

.timeline-company {
  font-size: 1.1rem;
  color: #3b82f6;
  font-weight: 600;
  margin: 0 0 1rem 0;
}

.timeline-description {
  color: #475569;
  line-height: 1.7;
  margin-bottom: 1.5rem;
}

.timeline-skills {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.timeline-item-right .timeline-skills {
  justify-content: flex-end;
}

.timeline-skill {
  background: rgba(59, 130, 246, 0.1);
  color: #3b82f6;
  padding: 0.3rem 0.8rem;
  border-radius: 15px;
  font-size: 0.85rem;
  font-weight: 500;
  border: 1px solid rgba(59, 130, 246, 0.2);
}

.timeline-achievements {
  margin-top: 1rem;
}

.timeline-achievements h5 {
  color: #1e293b;
  font-weight: 600;
  margin: 0 0 0.5rem 0;
}

.timeline-achievements ul {
  margin: 0;
  padding-left: 1.2rem;
}

.timeline-item-right .timeline-achievements ul {
  padding-left: 0;
  padding-right: 1.2rem;
  text-align: right;
  list-style-position: inside;
}

.timeline-achievements li {
  color: #64748b;
  margin-bottom: 0.3rem;
  line-height: 1.5;
}

.certifications {
  margin-top: 4rem;
}

.certifications-title {
  font-size: 2.5rem;
  font-weight: bold;
  color: #1e293b;
  text-align: center;
  margin-bottom: 3rem;
  position: relative;
}

.certifications-title::after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 50%;
  transform: translateX(-50%);
  width: 80px;
  height: 3px;
  background: linear-gradient(45deg, #3b82f6, #8b5cf6);
  border-radius: 2px;
}

.certifications-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

.certification-item {
  background: white;
  border-radius: 20px;
  padding: 2rem;
  text-align: center;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  border: 1px solid rgba(148, 163, 184, 0.1);
  transition: all 0.3s ease;
}

.certification-item:hover {
  transform: translateY(-10px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
}

.certification-icon {
  width: 80px;
  height: 80px;
  background: linear-gradient(45deg, #3b82f6, #8b5cf6);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 1.5rem auto;
  color: white;
}

.icon {
  width: 32px;
  height: 32px;
}

.certification-content h4 {
  font-size: 1.2rem;
  font-weight: bold;
  color: #1e293b;
  margin: 0 0 0.5rem 0;
}

.certification-institution {
  color: #3b82f6;
  font-weight: 600;
  margin: 0 0 0.5rem 0;
}

.certification-year {
  color: #64748b;
  margin: 0;
}

@media (max-width: 768px) {
  .timeline-line {
    left: 30px;
  }

  .timeline-item,
  .timeline-item-right {
    flex-direction: row;
  }

  .timeline-dot {
    left: 30px;
    width: 50px;
    height: 50px;
  }

  .timeline-content {
    width: calc(100% - 100px);
    margin-left: 70px;
    padding: 0;
  }

  .timeline-item-right .timeline-content {
    text-align: left;
    margin-left: 70px;
  }

  .timeline-card::before {
    left: -10px !important;
  }

  .timeline-skills {
    justify-content: flex-start !important;
  }

  .timeline-achievements ul {
    padding-left: 1.2rem !important;
    text-align: left !important;
    list-style-position: outside !important;
  }

  .section-title {
    font-size: 2.5rem;
  }

  .certifications-title {
    font-size: 2rem;
  }

  .certifications-grid {
    grid-template-columns: 1fr;
    gap: 1rem;
  }

  .certification-item {
    padding: 1.5rem;
  }

  .certification-icon {
    width: 60px;
    height: 60px;
  }
}
</style>