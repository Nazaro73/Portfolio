<template>
  <section id="skills" class="skills" ref="skillsRef">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title" data-aos="fade-up">Compétences Techniques</h2>
        <div class="section-subtitle" data-aos="fade-up" data-aos-delay="100">
          Technologies que je maîtrise et utilise au quotidien
        </div>
      </div>

      <div class="skills-content">
        <div class="skills-categories">
          <div class="category" data-aos="fade-up" data-aos-delay="200">
            <div class="category-header">
              <div class="category-icon">
                <Code class="icon" />
              </div>
              <h3 class="category-title">Frontend</h3>
            </div>

            <div class="skills-grid">
              <div class="skill-item" v-for="skill in frontendSkills" :key="skill.name">
                <div class="skill-header">
                  <span class="skill-name">{{ skill.name }}</span>
                  <span class="skill-percentage">{{ skill.percentage }}%</span>
                </div>
                <div class="skill-bar">
                  <div
                    class="skill-progress"
                    :style="{ width: skillProgressWidth(skill.percentage) }"
                    :data-percentage="skill.percentage"
                  ></div>
                </div>
              </div>
            </div>
          </div>

          <div class="category" data-aos="fade-up" data-aos-delay="300">
            <div class="category-header">
              <div class="category-icon">
                <Server class="icon" />
              </div>
              <h3 class="category-title">Backend</h3>
            </div>

            <div class="skills-grid">
              <div class="skill-item" v-for="skill in backendSkills" :key="skill.name">
                <div class="skill-header">
                  <span class="skill-name">{{ skill.name }}</span>
                  <span class="skill-percentage">{{ skill.percentage }}%</span>
                </div>
                <div class="skill-bar">
                  <div
                    class="skill-progress"
                    :style="{ width: skillProgressWidth(skill.percentage) }"
                    :data-percentage="skill.percentage"
                  ></div>
                </div>
              </div>
            </div>
          </div>

          <div class="category" data-aos="fade-up" data-aos-delay="400">
            <div class="category-header">
              <div class="category-icon">
                <Database class="icon" />
              </div>
              <h3 class="category-title">Base de données</h3>
            </div>

            <div class="skills-grid">
              <div class="skill-item" v-for="skill in databaseSkills" :key="skill.name">
                <div class="skill-header">
                  <span class="skill-name">{{ skill.name }}</span>
                  <span class="skill-percentage">{{ skill.percentage }}%</span>
                </div>
                <div class="skill-bar">
                  <div
                    class="skill-progress"
                    :style="{ width: skillProgressWidth(skill.percentage) }"
                    :data-percentage="skill.percentage"
                  ></div>
                </div>
              </div>
            </div>
          </div>

          <div class="category" data-aos="fade-up" data-aos-delay="500">
            <div class="category-header">
              <div class="category-icon">
                <Settings class="icon" />
              </div>
              <h3 class="category-title">Outils & DevOps</h3>
            </div>

            <div class="skills-grid">
              <div class="skill-item" v-for="skill in toolsSkills" :key="skill.name">
                <div class="skill-header">
                  <span class="skill-name">{{ skill.name }}</span>
                  <span class="skill-percentage">{{ skill.percentage }}%</span>
                </div>
                <div class="skill-bar">
                  <div
                    class="skill-progress"
                    :style="{ width: skillProgressWidth(skill.percentage) }"
                    :data-percentage="skill.percentage"
                  ></div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="skills-visual" data-aos="fade-left" data-aos-delay="600">
          <div class="radar-chart">
            <div class="radar-background">
              <div class="radar-line" v-for="n in 5" :key="n"></div>
              <div class="radar-axis" v-for="n in 6" :key="n"></div>
            </div>

            <div class="radar-labels">
              <div class="radar-label frontend">Frontend</div>
              <div class="radar-label backend">Backend</div>
              <div class="radar-label database">Database</div>
              <div class="radar-label mobile">Mobile</div>
              <div class="radar-label devops">DevOps</div>
              <div class="radar-label design">Design</div>
            </div>

            <svg class="radar-polygon" viewBox="0 0 200 200">
              <polygon
                :points="radarPoints"
                fill="rgba(59, 130, 246, 0.2)"
                stroke="#3b82f6"
                stroke-width="2"
                ref="polygonRef"
              />
            </svg>
          </div>

          <div class="tech-icons">
            <div
              class="tech-icon"
              v-for="(tech, index) in technologies"
              :key="tech.name"
              :style="{ animationDelay: (index * 0.1) + 's' }"
            >
              <div class="tech-logo">{{ tech.icon }}</div>
              <div class="tech-name">{{ tech.name }}</div>
            </div>
          </div>
        </div>
      </div>

      <div class="soft-skills" data-aos="fade-up" data-aos-delay="700">
        <h3 class="soft-skills-title">Compétences humaines</h3>
        <div class="soft-skills-grid">
          <div
            class="soft-skill-item"
            v-for="skill in softSkills"
            :key="skill.name"
            data-aos="zoom-in"
            :data-aos-delay="skill.delay"
          >
            <div class="soft-skill-icon">
              <component :is="skill.icon" class="icon" />
            </div>
            <div class="soft-skill-content">
              <h4>{{ skill.name }}</h4>
              <p>{{ skill.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted, computed } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import {
  Code,
  Server,
  Database,
  Settings,
  Users,
  MessageSquare,
  Target,
  Zap,
  Heart,
  BookOpen
} from 'lucide-vue-next'

gsap.registerPlugin(ScrollTrigger)

const skillsRef = ref<HTMLElement>()
const polygonRef = ref<SVGPolygonElement>()
const animationStarted = ref(false)

const frontendSkills = [
  { name: 'Vue.js', percentage: 90 },
  { name: 'React', percentage: 75 },
  { name: 'JavaScript', percentage: 95 },
  { name: 'TypeScript', percentage: 85 },
  { name: 'HTML/CSS', percentage: 95 },
  { name: 'Nuxt.js', percentage: 80 },
  { name: 'Bootstrap', percentage: 90 },
  { name: 'Flutter', percentage: 70 }
]

const backendSkills = [
  { name: 'Node.js', percentage: 85 },
  { name: 'Express.js', percentage: 90 },
  { name: 'Java', percentage: 80 },
  { name: 'Python', percentage: 75 },
  { name: 'PHP', percentage: 70 },
  { name: 'C++', percentage: 65 },
  { name: 'C#', percentage: 60 }
]

const databaseSkills = [
  { name: 'MySQL', percentage: 85 },
  { name: 'PostgreSQL', percentage: 80 },
  { name: 'MongoDB', percentage: 70 },
  { name: 'Sequelize ORM', percentage: 85 }
]

const toolsSkills = [
  { name: 'Git/GitHub', percentage: 90 },
  { name: 'GitLab', percentage: 80 },
  { name: 'JIRA', percentage: 75 },
  { name: 'Docker', percentage: 65 },
  { name: 'API REST', percentage: 90 }
]

const technologies = [
  { name: 'Vue', icon: 'V' },
  { name: 'React', icon: 'R' },
  { name: 'Node', icon: 'N' },
  { name: 'Java', icon: 'J' },
  { name: 'Python', icon: 'P' },
  { name: 'Git', icon: 'G' },
  { name: 'Docker', icon: 'D' },
  { name: 'MySQL', icon: 'M' }
]

const softSkills = [
  {
    name: 'Leadership',
    description: 'Capacité à guider et motiver une équipe',
    icon: Users,
    delay: 100
  },
  {
    name: 'Communication',
    description: 'Excellentes compétences relationnelles',
    icon: MessageSquare,
    delay: 200
  },
  {
    name: 'Résolution de problèmes',
    description: 'Approche analytique et créative',
    icon: Target,
    delay: 300
  },
  {
    name: 'Adaptabilité',
    description: 'Capacité à s\'adapter rapidement',
    icon: Zap,
    delay: 400
  },
  {
    name: 'Passion',
    description: 'Passion pour la technologie',
    icon: Heart,
    delay: 500
  },
  {
    name: 'Apprentissage',
    description: 'Apprendre continuellement',
    icon: BookOpen,
    delay: 600
  }
]

const skillProgressWidth = (percentage: number) => {
  return animationStarted.value ? `${percentage}%` : '0%'
}

const radarPoints = computed(() => {
  const values = [90, 85, 82, 70, 65, 75] // Frontend, Backend, DB, Mobile, DevOps, Design
  const center = 100
  const maxRadius = 80

  return values.map((value, index) => {
    const angle = (index * 60 - 90) * (Math.PI / 180)
    const radius = (value / 100) * maxRadius
    const x = center + radius * Math.cos(angle)
    const y = center + radius * Math.sin(angle)
    return `${x},${y}`
  }).join(' ')
})

onMounted(() => {
  ScrollTrigger.create({
    trigger: skillsRef.value,
    start: 'top 60%',
    onEnter: () => {
      animationStarted.value = true

      // Animation des barres de progression
      gsap.fromTo('.skill-progress', {
        width: '0%',
        opacity: 0
      }, {
        width: (index, element) => element.dataset.percentage + '%',
        opacity: 1,
        duration: 1.5,
        ease: 'power2.out',
        stagger: 0.1
      })

      // Animation du polygone radar
      if (polygonRef.value) {
        gsap.fromTo(polygonRef.value, {
          scale: 0,
          opacity: 0
        }, {
          scale: 1,
          opacity: 1,
          duration: 2,
          ease: 'back.out(1.7)'
        })
      }
    }
  })

  // Animation continue des icônes technologiques
  gsap.to('.tech-icon', {
    y: -10,
    duration: 2,
    ease: 'power2.inOut',
    stagger: 0.2,
    repeat: -1,
    yoyo: true
  })
})
</script>

<style scoped>
.skills {
  padding: 6rem 0;
  background: #0f172a;
  position: relative;
  overflow: hidden;
}

.skills::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(circle at 20% 50%, rgba(59, 130, 246, 0.1) 0%, transparent 50%),
              radial-gradient(circle at 80% 20%, rgba(139, 92, 246, 0.1) 0%, transparent 50%);
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

.skills-content {
  display: flex;
  flex-direction: column;
  gap: 4rem;
  margin-bottom: 4rem;
}

.skills-categories {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 2rem;
}

.category {
  background: rgba(30, 41, 59, 0.5);
  backdrop-filter: blur(10px);
  border-radius: 20px;
  padding: 2rem;
  border: 1px solid rgba(148, 163, 184, 0.1);
  transition: all 0.3s ease;
}

.category:hover {
  transform: translateY(-5px);
  border-color: rgba(59, 130, 246, 0.3);
  box-shadow: 0 10px 30px rgba(59, 130, 246, 0.1);
}

.category-header {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 2rem;
}

.category-icon {
  width: 50px;
  height: 50px;
  background: linear-gradient(45deg, #3b82f6, #8b5cf6);
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
}

.icon {
  width: 24px;
  height: 24px;
}

.category-title {
  font-size: 1.5rem;
  font-weight: bold;
  color: #e2e8f0;
  margin: 0;
}

.skills-grid {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.skill-item {
  transition: all 0.3s ease;
}

.skill-item:hover {
  transform: translateX(5px);
}

.skill-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5rem;
}

.skill-name {
  font-weight: 600;
  color: #e2e8f0;
}

.skill-percentage {
  font-weight: bold;
  color: #3b82f6;
  font-size: 0.9rem;
}

.skill-bar {
  height: 8px;
  background: rgba(148, 163, 184, 0.2);
  border-radius: 10px;
  overflow: hidden;
}

.skill-progress {
  height: 100%;
  background: linear-gradient(45deg, #3b82f6, #8b5cf6);
  border-radius: 10px;
  transition: width 1.5s ease-out;
  position: relative;
}

.skill-progress::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
  animation: shimmer 2s infinite;
}

@keyframes shimmer {
  0% { transform: translateX(-100%); }
  100% { transform: translateX(100%); }
}

.skills-visual {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
}

.radar-chart {
  width: 300px;
  height: 300px;
  position: relative;
  background: radial-gradient(circle, rgba(59, 130, 246, 0.1) 0%, transparent 70%);
  border-radius: 50%;
}

.radar-background {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 260px;
  height: 260px;
}

.radar-line {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100%;
  height: 100%;
  border: 1px solid rgba(148, 163, 184, 0.2);
  border-radius: 50%;
}

.radar-line:nth-child(1) { width: 20%; height: 20%; }
.radar-line:nth-child(2) { width: 40%; height: 40%; }
.radar-line:nth-child(3) { width: 60%; height: 60%; }
.radar-line:nth-child(4) { width: 80%; height: 80%; }
.radar-line:nth-child(5) { width: 100%; height: 100%; }

.radar-axis {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 1px;
  height: 50%;
  background: rgba(148, 163, 184, 0.2);
  transform-origin: bottom center;
}

.radar-axis:nth-child(1) { transform: translate(-50%, -100%) rotate(0deg); }
.radar-axis:nth-child(2) { transform: translate(-50%, -100%) rotate(60deg); }
.radar-axis:nth-child(3) { transform: translate(-50%, -100%) rotate(120deg); }
.radar-axis:nth-child(4) { transform: translate(-50%, -100%) rotate(180deg); }
.radar-axis:nth-child(5) { transform: translate(-50%, -100%) rotate(240deg); }
.radar-axis:nth-child(6) { transform: translate(-50%, -100%) rotate(300deg); }

.radar-labels {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

.radar-label {
  position: absolute;
  color: #94a3b8;
  font-size: 0.9rem;
  font-weight: 600;
  transform: translate(-50%, -50%);
}

.radar-label.frontend { top: 10%; left: 50%; }
.radar-label.backend { top: 25%; right: 15%; }
.radar-label.database { bottom: 25%; right: 15%; }
.radar-label.mobile { bottom: 10%; left: 50%; }
.radar-label.devops { bottom: 25%; left: 15%; }
.radar-label.design { top: 25%; left: 15%; }

.radar-polygon {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 260px;
  height: 260px;
}

.tech-icons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1rem;
  width: 100%;
}

.tech-icon {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  padding: 1rem;
  background: rgba(30, 41, 59, 0.5);
  border-radius: 12px;
  border: 1px solid rgba(148, 163, 184, 0.1);
  transition: all 0.3s ease;
}

.tech-icon:hover {
  border-color: rgba(59, 130, 246, 0.5);
  transform: translateY(-5px);
}

.tech-logo {
  width: 40px;
  height: 40px;
  background: linear-gradient(45deg, #3b82f6, #8b5cf6);
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-weight: bold;
  font-size: 1.2rem;
}

.tech-name {
  font-size: 0.8rem;
  color: #94a3b8;
  text-align: center;
}

.soft-skills {
  margin-top: 4rem;
}

.soft-skills-title {
  font-size: 2rem;
  font-weight: bold;
  color: #e2e8f0;
  text-align: center;
  margin-bottom: 3rem;
}

.soft-skills-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

.soft-skill-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 2rem;
  background: rgba(30, 41, 59, 0.5);
  backdrop-filter: blur(10px);
  border-radius: 15px;
  border: 1px solid rgba(148, 163, 184, 0.1);
  transition: all 0.3s ease;
}

.soft-skill-item:hover {
  transform: translateY(-5px);
  border-color: rgba(59, 130, 246, 0.3);
  box-shadow: 0 10px 30px rgba(59, 130, 246, 0.1);
}

.soft-skill-icon {
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

.soft-skill-content h4 {
  font-size: 1.1rem;
  font-weight: 600;
  color: #e2e8f0;
  margin: 0 0 0.5rem 0;
}

.soft-skill-content p {
  color: #94a3b8;
  margin: 0;
  font-size: 0.9rem;
  line-height: 1.4;
}

@media (max-width: 768px) {
  .skills-categories {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 768px) {
  .section-title {
    font-size: 2.5rem;
  }

  .soft-skills-grid {
    grid-template-columns: 1fr;
    gap: 1rem;
  }

  .soft-skill-item {
    padding: 1.5rem;
  }

  .tech-icons {
    grid-template-columns: repeat(2, 1fr);
  }

  .radar-chart {
    width: 250px;
    height: 250px;
  }
}
</style>