<script setup>
import { ref, onMounted } from 'vue'
import projectsData from '../data/projects.json'

// Les cartes avec image ont moins de place : on limite les tags affiches
// et on indique le reste avec une pastille "+N".
const MAX_TAGS_WITH_IMAGE = 4

const visibleTags = (project) =>
  project.image ? project.tags.slice(0, MAX_TAGS_WITH_IMAGE) : project.tags

const hiddenTagsCount = (project) =>
  project.image ? Math.max(0, project.tags.length - MAX_TAGS_WITH_IMAGE) : 0

const projects = ref([])
const isLoaded = ref(false)

onMounted(() => {
  projects.value = projectsData
  setTimeout(() => {
    isLoaded.value = true
  }, 100)
})
</script>

<template>
  <section class="projects section">
    <div class="container">
      <div class="section-header" :class="{ visible: isLoaded }">
        <span class="eyebrow">Réalisations</span>
        <h1 class="section-title">Mes <span class="gradient-text">projets</span></h1>
        <p class="section-subtitle">
          Découvrez une sélection de mes réalisations.
        </p>
      </div>

      <div class="projects-grid" :class="{ visible: isLoaded }">
        <component
          :is="project.link ? 'a' : 'article'"
          v-for="(project, index) in projects"
          :key="project.id"
          :href="project.link"
          :target="project.link ? '_blank' : null"
          :rel="project.link ? 'noopener noreferrer' : null"
          class="project-card"
          :class="{ 'has-image': project.image }"
          :style="{ transitionDelay: `${0.06 * index}s` }"
        >
          <div v-if="project.image" class="project-image">
            <img :src="project.image" :alt="project.title" loading="lazy" />
          </div>

          <span v-if="project.link" class="project-link" aria-hidden="true">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/>
              <polyline points="15,3 21,3 21,9"/>
              <line x1="10" y1="14" x2="21" y2="3"/>
            </svg>
          </span>

          <div class="project-info">
            <h3 class="project-title">{{ project.title }}</h3>
            <p class="project-description">{{ project.description }}</p>
            <div class="project-tags">
              <span v-for="tag in visibleTags(project)" :key="tag" class="tag">{{ tag }}</span>
              <span v-if="hiddenTagsCount(project)" class="tag tag-more">+{{ hiddenTagsCount(project) }}</span>
            </div>
          </div>
        </component>
      </div>
    </div>
  </section>
</template>

<style scoped>
.projects {
  min-height: calc(100vh - 80px);
}

.section-header {
  text-align: center;
  margin-bottom: 3rem;
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}

.section-header.visible {
  opacity: 1;
  transform: translateY(0);
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1.5rem;
}

.project-card {
  position: relative;
  display: flex;
  flex-direction: column;
  aspect-ratio: 1 / 1;
  background: var(--glass-bg);
  border: 1px solid var(--glass-border);
  -webkit-backdrop-filter: blur(16px);
  backdrop-filter: blur(16px);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-lg);
  overflow: hidden;
  text-decoration: none;
  color: inherit;
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.6s ease, transform 0.6s ease, box-shadow var(--transition), border-color var(--transition);
}

.projects-grid.visible .project-card {
  opacity: 1;
  transform: translateY(0);
}

.projects-grid.visible .project-card:hover {
  transform: translateY(-4px);
  box-shadow: var(--glow-green);
  border-color: rgba(8, 127, 68, 0.5);
}

.project-image {
  position: relative;
  flex: 0 0 38%;
  overflow: hidden;
}

.project-image::after {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(180deg, transparent 45%, rgba(17, 19, 17, 0.85) 100%);
  pointer-events: none;
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform var(--transition);
}

.project-card:hover .project-image img {
  transform: scale(1.05);
}

.project-info {
  flex: 1;
  min-height: 0;
  padding: 1.35rem 1.5rem;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

.project-card:not(.has-image) .project-info {
  justify-content: center;
  padding: 2rem;
}

.project-title {
  font-family: var(--font-display);
  font-size: 1.35rem;
  font-weight: 700;
  letter-spacing: -0.01em;
  margin-bottom: 0.5rem;
  color: var(--color-text);
}

.project-description {
  color: var(--color-text-secondary);
  font-size: 0.9rem;
  line-height: 1.55;
  margin-bottom: 0.75rem;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 5;
  line-clamp: 5;
  overflow: hidden;
}

.project-card.has-image .project-description {
  -webkit-line-clamp: 2;
  line-clamp: 2;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  align-content: flex-start;
  gap: 0.5rem;
  margin-top: auto;
  min-height: 0;
  overflow: hidden;
}

.project-link {
  position: absolute;
  top: 0.9rem;
  right: 0.9rem;
  z-index: 2;
  width: 34px;
  height: 34px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(5, 6, 5, 0.6);
  border: 1px solid var(--glass-border);
  -webkit-backdrop-filter: blur(10px);
  backdrop-filter: blur(10px);
  color: var(--color-accent);
  transition: background var(--transition), color var(--transition), border-color var(--transition);
}

.project-card:hover .project-link {
  background: var(--gradient-gold);
  border-color: transparent;
  color: #1a1400;
}

.tag-more {
  background: rgba(255, 255, 255, 0.05);
  color: var(--color-text-muted);
  border-color: var(--glass-border);
}

@media (max-width: 600px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }

  .project-card {
    aspect-ratio: auto;
  }

  .project-image {
    flex: none;
    height: 200px;
  }

  .project-description {
    -webkit-line-clamp: unset;
    line-clamp: unset;
  }

  .project-card.has-image .project-description {
    -webkit-line-clamp: unset;
    line-clamp: unset;
  }
}
</style>
