<template>
  <section id="contact" class="contact" ref="contactRef">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title" data-aos="fade-up">Contactez-moi</h2>
        <div class="section-subtitle" data-aos="fade-up" data-aos-delay="100">
          Prêt à concrétiser vos projets ? Discutons ensemble !
        </div>
      </div>

      <div class="contact-content">
        <div class="contact-info" data-aos="fade-right" data-aos-delay="200">
          <div class="info-header">
            <h3>Parlons de votre projet</h3>
            <p>
              Je suis toujours ouvert aux nouvelles opportunités et collaborations.
              N'hésitez pas à me contacter pour discuter de vos idées !
            </p>
          </div>

          <div class="contact-methods">
            <div class="contact-method">
              <div class="method-icon">
                <Mail class="icon" />
              </div>
              <div class="method-content">
                <h4>Email</h4>
                <p>Abdel-Rahim.KHABABA@hotmail.com</p>
                <a href="mailto:Abdel-Rahim.KHABABA@hotmail.com" class="method-action">
                  Envoyer un email
                </a>
              </div>
            </div>

            <div class="contact-method">
              <div class="method-icon">
                <Phone class="icon" />
              </div>
              <div class="method-content">
                <h4>Téléphone</h4>
                <p>07 66 32 40 45</p>
                <a href="tel:0766324045" class="method-action">
                  Appeler maintenant
                </a>
              </div>
            </div>

            <div class="contact-method">
              <div class="method-icon">
                <MapPin class="icon" />
              </div>
              <div class="method-content">
                <h4>Localisation</h4>
                <p>405, Rue du Bertillet<br>73000 Chambéry, France</p>
                <span class="method-action">Disponible en présentiel/distanciel</span>
              </div>
            </div>

            <div class="contact-method">
              <div class="method-icon">
                <Linkedin class="icon" />
              </div>
              <div class="method-content">
                <h4>LinkedIn</h4>
                <p>Connectons-nous professionnellement</p>
                <a href="https://linkedin.com" target="_blank" class="method-action">
                  Voir le profil
                </a>
              </div>
            </div>
          </div>

          <div class="availability">
            <div class="availability-status">
              <div class="status-indicator available"></div>
              <span>Disponible pour de nouvelles missions</span>
            </div>
            <p>Temps de réponse moyen : 24h</p>
          </div>
        </div>

        <div class="contact-form-container" data-aos="fade-left" data-aos-delay="300">
          <form @submit.prevent="submitForm" class="contact-form" ref="formRef">
            <div class="form-header">
              <h3>Envoyez-moi un message</h3>
              <p>Remplissez le formulaire ci-dessous et je vous répondrai rapidement</p>
            </div>

            <div class="form-row">
              <div class="form-group">
                <label for="firstName">Prénom *</label>
                <input
                  type="text"
                  id="firstName"
                  v-model="form.firstName"
                  :class="{ error: errors.firstName }"
                  @blur="validateField('firstName')"
                  @input="clearError('firstName')"
                  required
                />
                <span class="error-message" v-if="errors.firstName">{{ errors.firstName }}</span>
              </div>

              <div class="form-group">
                <label for="lastName">Nom *</label>
                <input
                  type="text"
                  id="lastName"
                  v-model="form.lastName"
                  :class="{ error: errors.lastName }"
                  @blur="validateField('lastName')"
                  @input="clearError('lastName')"
                  required
                />
                <span class="error-message" v-if="errors.lastName">{{ errors.lastName }}</span>
              </div>
            </div>

            <div class="form-group">
              <label for="email">Email *</label>
              <input
                type="email"
                id="email"
                v-model="form.email"
                :class="{ error: errors.email }"
                @blur="validateField('email')"
                @input="clearError('email')"
                required
              />
              <span class="error-message" v-if="errors.email">{{ errors.email }}</span>
            </div>

            <div class="form-group">
              <label for="company">Entreprise</label>
              <input
                type="text"
                id="company"
                v-model="form.company"
                placeholder="Optionnel"
              />
            </div>

            <div class="form-group">
              <label for="projectType">Type de projet *</label>
              <select
                id="projectType"
                v-model="form.projectType"
                :class="{ error: errors.projectType }"
                @change="clearError('projectType')"
                required
              >
                <option value="">Sélectionnez un type de projet</option>
                <option value="website">Site web</option>
                <option value="webapp">Application web</option>
                <option value="mobile">Application mobile</option>
                <option value="api">Développement API</option>
                <option value="consultation">Consultation technique</option>
                <option value="maintenance">Maintenance/Support</option>
                <option value="other">Autre</option>
              </select>
              <span class="error-message" v-if="errors.projectType">{{ errors.projectType }}</span>
            </div>

            <div class="form-group">
              <label for="budget">Budget estimé</label>
              <select id="budget" v-model="form.budget">
                <option value="">Sélectionnez une fourchette</option>
                <option value="<5k">Moins de 5 000€</option>
                <option value="5k-15k">5 000€ - 15 000€</option>
                <option value="15k-30k">15 000€ - 30 000€</option>
                <option value="30k+">Plus de 30 000€</option>
                <option value="discuss">À discuter</option>
              </select>
            </div>

            <div class="form-group">
              <label for="timeline">Timeline souhaitée</label>
              <select id="timeline" v-model="form.timeline">
                <option value="">Sélectionnez une timeline</option>
                <option value="asap">Dès que possible</option>
                <option value="1month">Dans le mois</option>
                <option value="3months">Dans les 3 mois</option>
                <option value="6months">Dans les 6 mois</option>
                <option value="flexible">Flexible</option>
              </select>
            </div>

            <div class="form-group">
              <label for="message">Message *</label>
              <textarea
                id="message"
                v-model="form.message"
                :class="{ error: errors.message }"
                @blur="validateField('message')"
                @input="clearError('message')"
                rows="6"
                placeholder="Décrivez votre projet, vos besoins, vos objectifs..."
                required
              ></textarea>
              <span class="error-message" v-if="errors.message">{{ errors.message }}</span>
            </div>

            <div class="form-actions">
              <button
                type="submit"
                class="submit-btn"
                :disabled="isSubmitting"
                :class="{ loading: isSubmitting }"
              >
                <span v-if="!isSubmitting">
                  <Send class="icon" />
                  Envoyer le message
                </span>
                <span v-else>
                  <div class="spinner"></div>
                  Envoi en cours...
                </span>
              </button>
            </div>
          </form>

          <div class="form-success" v-if="showSuccess">
            <div class="success-animation">
              <div class="success-icon">
                <CheckCircle class="icon" />
              </div>
              <h3>Message envoyé !</h3>
              <p>Merci pour votre message. Je vous répondrai dans les plus brefs délais.</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="contact-background">
      <div class="bg-shapes">
        <div class="shape shape-1"></div>
        <div class="shape shape-2"></div>
        <div class="shape shape-3"></div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, reactive, onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import {
  Mail,
  Phone,
  MapPin,
  Linkedin,
  Send,
  CheckCircle
} from 'lucide-vue-next'

gsap.registerPlugin(ScrollTrigger)

const contactRef = ref<HTMLElement>()
const formRef = ref<HTMLElement>()
const isSubmitting = ref(false)
const showSuccess = ref(false)

const form = reactive({
  firstName: '',
  lastName: '',
  email: '',
  company: '',
  projectType: '',
  budget: '',
  timeline: '',
  message: ''
})

const errors = reactive({
  firstName: '',
  lastName: '',
  email: '',
  projectType: '',
  message: ''
})

const validateField = (field: string) => {
  switch (field) {
    case 'firstName':
      errors.firstName = form.firstName.trim() === '' ? 'Le prénom est requis' : ''
      break
    case 'lastName':
      errors.lastName = form.lastName.trim() === '' ? 'Le nom est requis' : ''
      break
    case 'email':
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
      if (form.email.trim() === '') {
        errors.email = 'L\'email est requis'
      } else if (!emailRegex.test(form.email)) {
        errors.email = 'Format d\'email invalide'
      } else {
        errors.email = ''
      }
      break
    case 'projectType':
      errors.projectType = form.projectType === '' ? 'Veuillez sélectionner un type de projet' : ''
      break
    case 'message':
      if (form.message.trim() === '') {
        errors.message = 'Le message est requis'
      } else if (form.message.length < 20) {
        errors.message = 'Le message doit contenir au moins 20 caractères'
      } else {
        errors.message = ''
      }
      break
  }
}

const clearError = (field: string) => {
  errors[field] = ''
}

const validateForm = () => {
  validateField('firstName')
  validateField('lastName')
  validateField('email')
  validateField('projectType')
  validateField('message')

  return !Object.values(errors).some(error => error !== '')
}

const resetForm = () => {
  Object.keys(form).forEach(key => {
    form[key] = ''
  })
  Object.keys(errors).forEach(key => {
    errors[key] = ''
  })
}

const submitForm = async () => {
  if (!validateForm()) {
    // Animation d'erreur
    gsap.to(formRef.value, {
      x: -10,
      duration: 0.1,
      repeat: 5,
      yoyo: true,
      ease: 'power2.inOut',
      onComplete: () => {
        gsap.set(formRef.value, { x: 0 })
      }
    })
    return
  }

  isSubmitting.value = true

  // Simulation d'envoi (à remplacer par vraie API)
  try {
    await new Promise(resolve => setTimeout(resolve, 2000))

    // Animation de succès
    showSuccess.value = true
    gsap.fromTo('.success-animation', {
      scale: 0,
      opacity: 0
    }, {
      scale: 1,
      opacity: 1,
      duration: 0.6,
      ease: 'back.out(1.7)'
    })

    // Masquer le formulaire
    gsap.to('.contact-form', {
      opacity: 0,
      y: -30,
      duration: 0.5,
      ease: 'power2.out'
    })

    resetForm()

    // Cacher le message de succès après 5 secondes
    setTimeout(() => {
      showSuccess.value = false
      gsap.to('.contact-form', {
        opacity: 1,
        y: 0,
        duration: 0.5,
        ease: 'power2.out'
      })
    }, 5000)

  } catch (error) {
    console.error('Erreur lors de l\'envoi:', error)
  } finally {
    isSubmitting.value = false
  }
}

onMounted(() => {
  // Animation des éléments de contact au scroll
  ScrollTrigger.create({
    trigger: contactRef.value,
    start: 'top 70%',
    onEnter: () => {
      // Animation des méthodes de contact
      gsap.fromTo('.contact-method', {
        x: -50,
        opacity: 0
      }, {
        x: 0,
        opacity: 1,
        duration: 0.8,
        stagger: 0.2,
        ease: 'power2.out'
      })

      // Animation des champs du formulaire
      gsap.fromTo('.form-group', {
        y: 30,
        opacity: 0
      }, {
        y: 0,
        opacity: 1,
        duration: 0.6,
        stagger: 0.1,
        ease: 'power2.out',
        delay: 0.3
      })
    }
  })

  // Animation des formes de background
  gsap.to('.shape', {
    rotation: 360,
    duration: 20,
    repeat: -1,
    ease: 'none'
  })

  gsap.to('.shape-1', {
    y: -50,
    duration: 4,
    repeat: -1,
    yoyo: true,
    ease: 'power2.inOut'
  })

  gsap.to('.shape-2', {
    x: 30,
    duration: 6,
    repeat: -1,
    yoyo: true,
    ease: 'power2.inOut'
  })

  gsap.to('.shape-3', {
    y: 40,
    duration: 5,
    repeat: -1,
    yoyo: true,
    ease: 'power2.inOut'
  })

  // Animation de focus sur les inputs
  document.querySelectorAll('input, textarea, select').forEach(input => {
    input.addEventListener('focus', () => {
      gsap.to(input.parentElement, {
        scale: 1.02,
        duration: 0.2,
        ease: 'power2.out'
      })
    })

    input.addEventListener('blur', () => {
      gsap.to(input.parentElement, {
        scale: 1,
        duration: 0.2,
        ease: 'power2.out'
      })
    })
  })
})
</script>

<style scoped>
.contact {
  padding: 6rem 0;
  background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 100%);
  position: relative;
  overflow: hidden;
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

.contact-content {
  display: flex;
  flex-direction: column;
  gap: 4rem;
  align-items: stretch;
}

.contact-info {
  background: white;
  border-radius: 20px;
  padding: 2.5rem;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.1);
  border: 1px solid rgba(148, 163, 184, 0.1);
}

.info-header {
  margin-bottom: 3rem;
}

.info-header h3 {
  font-size: 1.8rem;
  font-weight: bold;
  color: #1e293b;
  margin: 0 0 1rem 0;
}

.info-header p {
  color: #64748b;
  line-height: 1.7;
  margin: 0;
}

.contact-methods {
  margin-bottom: 3rem;
}

.contact-method {
  display: flex;
  align-items: flex-start;
  gap: 1.5rem;
  margin-bottom: 2rem;
  padding: 1.5rem;
  border-radius: 15px;
  transition: all 0.3s ease;
}

.contact-method:hover {
  background: rgba(59, 130, 246, 0.05);
  transform: translateX(5px);
}

.method-icon {
  width: 50px;
  height: 50px;
  background: linear-gradient(45deg, #3b82f6, #8b5cf6);
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  flex-shrink: 0;
}

.icon {
  width: 20px;
  height: 20px;
}

.method-content h4 {
  font-size: 1.1rem;
  font-weight: 600;
  color: #1e293b;
  margin: 0 0 0.5rem 0;
}

.method-content p {
  color: #64748b;
  margin: 0 0 0.5rem 0;
  line-height: 1.5;
}

.method-action {
  color: #3b82f6;
  text-decoration: none;
  font-weight: 500;
  font-size: 0.9rem;
  transition: color 0.3s ease;
}

.method-action:hover {
  color: #1d4ed8;
}

.availability {
  padding: 1.5rem;
  background: rgba(16, 185, 129, 0.1);
  border-radius: 15px;
  border: 1px solid rgba(16, 185, 129, 0.2);
}

.availability-status {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  margin-bottom: 0.5rem;
}

.status-indicator {
  width: 12px;
  height: 12px;
  border-radius: 50%;
}

.status-indicator.available {
  background: #10b981;
  box-shadow: 0 0 0 3px rgba(16, 185, 129, 0.3);
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0% { box-shadow: 0 0 0 0 rgba(16, 185, 129, 0.7); }
  70% { box-shadow: 0 0 0 10px rgba(16, 185, 129, 0); }
  100% { box-shadow: 0 0 0 0 rgba(16, 185, 129, 0); }
}

.availability-status span {
  font-weight: 600;
  color: #059669;
}

.availability p {
  color: #64748b;
  margin: 0;
  font-size: 0.9rem;
}

.contact-form-container {
  background: white;
  border-radius: 20px;
  padding: 2.5rem;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.1);
  border: 1px solid rgba(148, 163, 184, 0.1);
  position: relative;
}

.form-header {
  margin-bottom: 2rem;
}

.form-header h3 {
  font-size: 1.8rem;
  font-weight: bold;
  color: #1e293b;
  margin: 0 0 0.5rem 0;
}

.form-header p {
  color: #64748b;
  margin: 0;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.form-group {
  margin-bottom: 1.5rem;
  transition: transform 0.2s ease;
}

.form-group label {
  display: block;
  font-weight: 600;
  color: #374151;
  margin-bottom: 0.5rem;
  font-size: 0.9rem;
}

.form-group input,
.form-group select,
.form-group textarea {
  width: 100%;
  padding: 0.875rem 1rem;
  border: 2px solid #e5e7eb;
  border-radius: 12px;
  font-size: 1rem;
  transition: all 0.3s ease;
  background: white;
  font-family: inherit;
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #3b82f6;
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
}

.form-group input.error,
.form-group select.error,
.form-group textarea.error {
  border-color: #ef4444;
  box-shadow: 0 0 0 3px rgba(239, 68, 68, 0.1);
}

.form-group textarea {
  resize: vertical;
  min-height: 120px;
  line-height: 1.6;
}

.error-message {
  display: block;
  color: #ef4444;
  font-size: 0.8rem;
  margin-top: 0.5rem;
  font-weight: 500;
}

.form-actions {
  margin-top: 2rem;
}

.submit-btn {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
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
  min-height: 56px;
}

.submit-btn:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 10px 30px rgba(59, 130, 246, 0.3);
}

.submit-btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
  transform: none;
}

.submit-btn.loading {
  background: #6b7280;
}

.spinner {
  width: 20px;
  height: 20px;
  border: 2px solid transparent;
  border-top: 2px solid white;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.form-success {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: white;
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.success-animation {
  text-align: center;
}

.success-icon {
  width: 80px;
  height: 80px;
  background: linear-gradient(45deg, #10b981, #059669);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 1.5rem;
  color: white;
}

.success-animation h3 {
  font-size: 1.8rem;
  font-weight: bold;
  color: #1e293b;
  margin: 0 0 1rem 0;
}

.success-animation p {
  color: #64748b;
  margin: 0;
  line-height: 1.6;
}

.contact-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  overflow: hidden;
  z-index: 1;
}

.bg-shapes {
  position: relative;
  width: 100%;
  height: 100%;
}

.shape {
  position: absolute;
  border-radius: 50%;
  opacity: 0.1;
}

.shape-1 {
  width: 200px;
  height: 200px;
  background: linear-gradient(45deg, #3b82f6, #8b5cf6);
  top: 10%;
  right: 10%;
}

.shape-2 {
  width: 150px;
  height: 150px;
  background: linear-gradient(45deg, #8b5cf6, #06b6d4);
  bottom: 20%;
  left: 5%;
}

.shape-3 {
  width: 100px;
  height: 100px;
  background: linear-gradient(45deg, #06b6d4, #10b981);
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

@media (max-width: 768px) {
  .section-title {
    font-size: 2.5rem;
  }

  .contact-info,
  .contact-form-container {
    padding: 2rem;
  }

  .form-row {
    grid-template-columns: 1fr;
    gap: 0;
  }

  .contact-method {
    padding: 1rem;
  }

  .method-icon {
    width: 40px;
    height: 40px;
  }

  .shape-1 {
    width: 120px;
    height: 120px;
  }

  .shape-2 {
    width: 100px;
    height: 100px;
  }

  .shape-3 {
    width: 80px;
    height: 80px;
  }
}
</style>