<script setup>
import { ref, onMounted } from 'vue'

const isVisible = ref(false)

const skills = [
  { category: 'Backend', items: ['.NET', 'C#', 'SignalR'] },
  { category: 'Frontend', items: ['Vue.js', 'React.js', 'TypeScript', 'HTML/CSS', 'Angular.js'] },
  { category: 'Outils', items: ['Git', 'Docker', 'VS', 'Azure', 'WSL', 'Jira', 'Github'] },
  { category: 'Methodologies', items: ['Scrum', 'Kanban', 'lean', 'TDD', 'DDD', 'Microservices', 'CI/CD', 'Clean architecture'] },
  { category: 'Game développement', items: ['Unreal engine', 'C++', 'Unity', 'C#', 'Cmake', 'OpenGl', 'Vulkan', 'Assembleur'] }
]

const timeline = [
  {
    year: '2025',
    title: 'Intervenant C++ et Unreal Engine',
    company: 'Auto-entreprise',
    description: 'Intervention en tant que formateur C++ et Unreal Engine pour des étudiants.'
  },
  {
    year: '2025 - Present',
    title: 'Concepteur logiciel Junior',
    company: 'Madic Group',
    description: 'Participation a la conception et la maintenance d\'une application d\'alerting en temps réel SignalR sur des stations essences, conception de système iot avec communication d\'une station hydrogen avec DOMS via MQTT et évolution d\'un projet Legacy de framework 4.2 en .NET 8 sur une architechture microservice monolithe.',
  },
  {
    year: '2023 - 2025',
    title: 'Developpeur Full-stack Alternant',
    company: 'Peaksys',
    description: 'Developpement et maintenance d\'API b2b avec .NET et d\'applications frontend avec React.js. Participation aux reunions agiles et collaboration avec les equipes produit et design. Résolutin de bugs et optimisation des performances.',
  },
  {
    year: '2023 - 2025',
    title: 'Etudiant en Master Informatique',
    company: 'Ynov Campus',
    description: 'Expertise en développement logiciel et gestion de projets agiles.'
  },
  {
    year: '2020 - 2023',
    title: 'Etudiant en Informatique',
    company: 'Epitech',
    description: 'Apprentissage des fondamentaux et autonomie de projet.'
  }
]

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true
  }, 100)
})
</script>

<template>
  <section class="about section">
    <div class="container">
      <div class="about-header" :class="{ visible: isVisible }">
        <span class="eyebrow">À propos</span>
        <h1 class="section-title">Mon parcours &amp; <span class="gradient-text">compétences</span></h1>
        <p class="section-subtitle">
          Apprenez-en plus sur mon parcours et mes compétences
        </p>
      </div>

      <div class="about-content">
        <div class="about-intro" :class="{ visible: isVisible }">
          <div class="intro-text">
            <h2>Qui suis-je ?</h2>
            <p>
              J’ai choisi la programmation par curiosité, 
              je suis resté par passion. La raison ? Nous façonnons des
              solutions avec nos connaissances.
            </p>
            <p>
              Après 5 ans d’études en informatique, j’ai acquis une solide base dans plusieurs domaines du développement logiciel.
              J'ai pu participer à divers projets, m'aidant à développer mes compétences techniques et ma capacité à travailler en équipe.
              Curieux de nature, j’aime apprendre de nouvelles technologies et relever des défis complexes.
            </p>
            <p>
              En dehors du code, je suis l'heureux papa d'une petite fille qui me pousse chaque jour à devenir une meilleure version de moi-même.
              Je fais également partie d'un collectif qui développe sur leur temps libre des projets jeux vidéo ou applications. Améliorant en continue mes compétences en développement.
            </p>
          </div>
        </div>

        <div class="skills-section" :class="{ visible: isVisible }">
          <h2>Competences</h2>
          <div class="skills-grid">
            <div v-for="skill in skills" :key="skill.category" class="skill-category">
              <h3>{{ skill.category }}</h3>
              <ul>
                <li v-for="item in skill.items" :key="item">
                  <span class="skill-dot"></span>
                  {{ item }}
                </li>
              </ul>
            </div>
          </div>
        </div>

        <div class="timeline-section" :class="{ visible: isVisible }">
          <h2>Parcours</h2>
          <div class="timeline">
            <div v-for="(item, index) in timeline" :key="index" class="timeline-item">
              <div class="timeline-marker"></div>
              <div class="timeline-content">
                <span class="timeline-year">{{ item.year }}</span>
                <h3>{{ item.title }}</h3>
                <span class="timeline-company">{{ item.company }}</span>
                <p>{{ item.description }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about-header {
  text-align: center;
  margin-bottom: 4rem;
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.7s ease, transform 0.7s ease;
}

.about-header.visible {
  opacity: 1;
  transform: translateY(0);
}

.about-content h2 {
  font-family: var(--font-display);
  font-size: 1.6rem;
  font-weight: 600;
  letter-spacing: -0.01em;
  margin-bottom: 1.75rem;
  color: var(--color-text);
}

/* Intro dans une carte verre */
.about-intro {
  margin-bottom: 4rem;
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.7s ease 0.1s, transform 0.7s ease 0.1s;
}

.about-intro.visible {
  opacity: 1;
  transform: translateY(0);
}

.intro-text {
  position: relative;
  padding: 2.5rem;
  border-radius: var(--radius-lg);
  background: var(--glass-bg);
  border: 1px solid var(--glass-border);
  -webkit-backdrop-filter: blur(14px);
  backdrop-filter: blur(14px);
  overflow: hidden;
}

.intro-text::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  width: 3px;
  background: var(--gradient-brand);
}

.intro-text p {
  color: var(--color-text-secondary);
  line-height: 1.85;
  margin-bottom: 1.25rem;
  max-width: 760px;
}

.intro-text p:last-child {
  margin-bottom: 0;
}

/* Compétences */
.skills-section {
  margin-bottom: 4rem;
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.7s ease 0.2s, transform 0.7s ease 0.2s;
}

.skills-section.visible {
  opacity: 1;
  transform: translateY(0);
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1.25rem;
}

.skill-category {
  position: relative;
  background: var(--glass-bg);
  border: 1px solid var(--glass-border);
  padding: 1.75rem;
  border-radius: var(--radius);
  -webkit-backdrop-filter: blur(12px);
  backdrop-filter: blur(12px);
  transition: transform var(--transition), border-color var(--transition), box-shadow var(--transition), background var(--transition);
}

.skill-category:hover {
  transform: translateY(-5px);
  background: var(--glass-bg-hover);
  border-color: rgba(8, 127, 68, 0.5);
  box-shadow: var(--glow-green);
}

.skill-category h3 {
  font-family: var(--font-display);
  font-size: 1.05rem;
  font-weight: 600;
  margin-bottom: 1.1rem;
  color: var(--color-accent);
}

.skill-category ul {
  list-style: none;
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.skill-category li {
  display: inline-flex;
  align-items: center;
  gap: 0.45rem;
  padding: 0.35rem 0.7rem;
  font-size: 0.84rem;
  border-radius: 8px;
  color: var(--color-text-secondary);
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid var(--glass-border);
  transition: color var(--transition-fast), border-color var(--transition-fast);
}

.skill-category li:hover {
  color: var(--color-text);
  border-color: rgba(8, 127, 68, 0.5);
}

.skill-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: var(--color-primary-light);
}

/* Timeline */
.timeline-section {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.7s ease 0.3s, transform 0.7s ease 0.3s;
}

.timeline-section.visible {
  opacity: 1;
  transform: translateY(0);
}

.timeline {
  position: relative;
  padding-left: 2.25rem;
}

.timeline::before {
  content: '';
  position: absolute;
  left: 5px;
  top: 6px;
  bottom: 6px;
  width: 2px;
  background: linear-gradient(to bottom, var(--color-primary-light), rgba(212, 175, 55, 0.5), transparent);
}

.timeline-item {
  position: relative;
  padding-bottom: 1.5rem;
}

.timeline-item:last-child {
  padding-bottom: 0;
}

.timeline-marker {
  position: absolute;
  left: -2.25rem;
  top: 8px;
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: var(--color-accent);
  box-shadow: 0 0 0 4px var(--color-bg), 0 0 12px rgba(212, 175, 55, 0.5);
  transition: all var(--transition);
}

.timeline-item:hover .timeline-marker {
  background: var(--color-primary-light);
  box-shadow: 0 0 0 4px var(--color-bg), 0 0 16px rgba(8, 127, 68, 0.7);
  transform: scale(1.3);
}

.timeline-content {
  background: var(--glass-bg);
  border: 1px solid var(--glass-border);
  padding: 1.5rem;
  border-radius: var(--radius);
  -webkit-backdrop-filter: blur(12px);
  backdrop-filter: blur(12px);
  transition: transform var(--transition), border-color var(--transition), box-shadow var(--transition), background var(--transition);
}

.timeline-item:hover .timeline-content {
  transform: translateX(6px);
  background: var(--glass-bg-hover);
  border-color: rgba(8, 127, 68, 0.45);
  box-shadow: var(--shadow);
}

.timeline-year {
  display: inline-block;
  padding: 0.28rem 0.8rem;
  background: rgba(8, 127, 68, 0.18);
  border: 1px solid rgba(8, 127, 68, 0.4);
  color: #7fdca7;
  font-family: var(--font-display);
  font-size: 0.74rem;
  font-weight: 600;
  border-radius: 9999px;
  margin-bottom: 0.85rem;
}

.timeline-content h3 {
  font-family: var(--font-display);
  font-size: 1.1rem;
  font-weight: 600;
  margin-bottom: 0.2rem;
}

.timeline-company {
  color: var(--color-accent);
  font-size: 0.85rem;
  font-weight: 500;
  display: block;
  margin-bottom: 0.75rem;
}

.timeline-content p {
  color: var(--color-text-secondary);
  font-size: 0.9rem;
  line-height: 1.65;
  margin: 0;
}

@media (max-width: 768px) {
  .about-content h2 {
    font-size: 1.4rem;
  }

  .skills-grid {
    grid-template-columns: 1fr;
  }

  .intro-text {
    padding: 1.75rem;
  }
}
</style>
