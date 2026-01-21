<script setup>
import { ref, onMounted } from 'vue'

const isVisible = ref(false)

const skills = [
  { category: 'Backend', items: ['.NET 4.2 to 8', 'ASP .NET CORE', 'SQL Server', 'MongoDB', 'REST APIs'] },
  { category: 'Frontend', items: ['Vue.js', 'React', 'TypeScript', 'HTML/CSS', 'Tailwind CSS'] },
  {category: 'Agile', items: ['Scrum', 'Kanban', 'Jira', 'Trello', 'Github project', 'lean'] },
  { category: 'Outils', items: ['Git', 'Docker', 'VS', 'Azure', 'WSL'] },
  { category: 'Methodologies', items: ['TDD', 'DDD', 'Clean Architecture', 'Microservices', 'CI/CD'] },
  { category: 'Frameworks', items: ['Entity Framework', 'AutoMapper', 'SignalR'] },
  { category: 'Langages', items: ['C#', 'JavaScript', 'TypeScript', 'Python', 'C++'] },
]

const timeline = [
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
        <h1 class="section-title">A propos</h1>
        <p class="section-subtitle">
          Apprenez-en plus sur mon parcours et mes competences
        </p>
      </div>

      <div class="about-content">
        <div class="about-intro" :class="{ visible: isVisible }">
          <div class="intro-text">
            <h2>Qui suis-je ?</h2>
            <p>
              J\’ai choisi la programmation par curiosité, 
              je suis resté par passion. La raison ? Nous façonnons des
              solutions avec nos mains.
            </p>
            <p>
              Après 5 ans d\’études en informatique, j\’ai acquis une solide base dans plusieurs domaines du développement logiciel.
              J'ai pue participer a divers projets, m'aidant a developper mes competences techniques et ma capacite a travailler en equipe.
              Curieux de nature, j\’aime apprendre de nouvelles technologies et relever des défis complexes.
            </p>
            <p>
              En dehors du code, je suis l'heureux papa d'une petite fille qui me pousse chaque jour a devenir une meilleure version de moi-meme.
              Je fais également partie d'un collectif qui développe sur leur temps libre des projets fun et innovants. Améliorant en continue mes compétences en développement.
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
  transform: translateY(20px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}

.about-header.visible {
  opacity: 1;
  transform: translateY(0);
}

.about-content h2 {
  font-size: 1.75rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
  color: var(--color-text);
}

.about-intro {
  margin-bottom: 4rem;
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.6s ease 0.1s, transform 0.6s ease 0.1s;
}

.about-intro.visible {
  opacity: 1;
  transform: translateY(0);
}

.intro-text p {
  color: var(--color-text-secondary);
  line-height: 1.8;
  margin-bottom: 1.5rem;
  max-width: 800px;
}

.intro-text p:last-child {
  margin-bottom: 0;
}

.skills-section {
  margin-bottom: 4rem;
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.6s ease 0.2s, transform 0.6s ease 0.2s;
}

.skills-section.visible {
  opacity: 1;
  transform: translateY(0);
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
}

.skill-category {
  background: var(--color-bg-elevated);
  border: 1px solid var(--color-border);
  padding: 2rem;
  border-radius: var(--radius);
  transition: transform var(--transition), border-color var(--transition), box-shadow var(--transition);
}

.skill-category:hover {
  transform: translateY(-4px);
  border-color: var(--color-primary);
  box-shadow: var(--shadow-colored);
}

.skill-category h3 {
  font-size: 1.125rem;
  font-weight: 600;
  margin-bottom: 1rem;
  color: var(--color-accent);
}

.skill-category ul {
  list-style: none;
}

.skill-category li {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.5rem 0;
  color: var(--color-text);
}

.skill-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: var(--color-primary);
}

.timeline-section {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.6s ease 0.3s, transform 0.6s ease 0.3s;
}

.timeline-section.visible {
  opacity: 1;
  transform: translateY(0);
}

.timeline {
  position: relative;
  padding-left: 2rem;
}

.timeline::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  width: 2px;
  background: var(--color-border);
}

.timeline-item {
  position: relative;
  padding-bottom: 2.5rem;
}

.timeline-item:last-child {
  padding-bottom: 0;
}

.timeline-marker {
  position: absolute;
  left: -2rem;
  top: 0;
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: var(--color-accent);
  border: 3px solid var(--color-bg);
  box-shadow: 0 0 0 2px var(--color-border);
  transform: translateX(-5px);
  transition: all var(--transition);
}

.timeline-item:hover .timeline-marker {
  background: var(--color-primary);
  box-shadow: 0 0 0 2px var(--color-primary);
  transform: translateX(-5px) scale(1.2);
}

.timeline-content {
  background: var(--color-bg-elevated);
  border: 1px solid var(--color-border);
  padding: 1.5rem;
  border-radius: var(--radius);
  transition: transform var(--transition), border-color var(--transition), box-shadow var(--transition);
}

.timeline-item:hover .timeline-content {
  transform: translateX(4px);
  border-color: var(--color-primary);
  box-shadow: var(--shadow-colored);
}

.timeline-year {
  display: inline-block;
  padding: 0.25rem 0.75rem;
  background: var(--color-primary);
  color: white;
  font-size: 0.75rem;
  font-weight: 500;
  border-radius: 9999px;
  margin-bottom: 0.75rem;
}

.timeline-content h3 {
  font-size: 1.125rem;
  font-weight: 600;
  margin-bottom: 0.25rem;
}

.timeline-company {
  color: var(--color-text-secondary);
  font-size: 0.875rem;
  display: block;
  margin-bottom: 0.75rem;
}

.timeline-content p {
  color: var(--color-text-secondary);
  font-size: 0.875rem;
  line-height: 1.6;
  margin: 0;
}

@media (max-width: 768px) {
  .about-content h2 {
    font-size: 1.5rem;
  }

  .skills-grid {
    grid-template-columns: 1fr;
  }
}
</style>
