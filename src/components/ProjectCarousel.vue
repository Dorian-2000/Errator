<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  projects: {
    type: Array,
    required: true
  }
})

const currentIndex = ref(0)
const direction = ref('next')

const currentProject = computed(() => props.projects[currentIndex.value])

const totalProjects = computed(() => props.projects.length)

const goToNext = () => {
  direction.value = 'next'
  currentIndex.value = (currentIndex.value + 1) % totalProjects.value
}

const goToPrev = () => {
  direction.value = 'prev'
  currentIndex.value = (currentIndex.value - 1 + totalProjects.value) % totalProjects.value
}

const goToSlide = (index) => {
  direction.value = index > currentIndex.value ? 'next' : 'prev'
  currentIndex.value = index
}
</script>

<template>
  <div class="carousel">
    <div class="carousel-container">
      <button class="carousel-btn prev" @click="goToPrev" aria-label="Projet precedent">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M15 18l-6-6 6-6"/>
        </svg>
      </button>

      <div class="carousel-content">
        <div class="carousel-track">
          <Transition :name="direction === 'next' ? 'slide-next' : 'slide-prev'" mode="out-in">
            <a
              :key="currentProject.id"
              :href="currentProject.link"
              target="_blank"
              rel="noopener noreferrer"
              class="project-card"
            >
              <div class="project-image">
                <img :src="currentProject.image" :alt="currentProject.title" />
              </div>
              <div class="project-info">
                <h3 class="project-title">{{ currentProject.title }}</h3>
                <p class="project-description">{{ currentProject.description }}</p>
                <div class="project-tags">
                  <span v-for="tag in currentProject.tags" :key="tag" class="tag">{{ tag }}</span>
                </div>
                <span class="project-link">
                  Voir le projet
                  <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/>
                    <polyline points="15,3 21,3 21,9"/>
                    <line x1="10" y1="14" x2="21" y2="3"/>
                  </svg>
                </span>
              </div>
            </a>
          </Transition>
        </div>
      </div>

      <button class="carousel-btn next" @click="goToNext" aria-label="Projet suivant">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M9 18l6-6-6-6"/>
        </svg>
      </button>
    </div>

    <div class="carousel-indicators">
      <button
        v-for="(project, index) in projects"
        :key="project.id"
        :class="['indicator', { active: index === currentIndex }]"
        @click="goToSlide(index)"
        :aria-label="`Aller au projet ${index + 1}`"
      ></button>
    </div>

    <div class="carousel-counter">
      {{ currentIndex + 1 }} / {{ totalProjects }}
    </div>
  </div>
</template>

<style scoped>
.carousel {
  width: 100%;
  max-width: 900px;
  margin: 0 auto;
}

.carousel-container {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.carousel-btn {
  flex-shrink: 0;
  width: 48px;
  height: 48px;
  border-radius: 50%;
  background: var(--color-bg-elevated);
  border: 2px solid var(--color-border);
  color: var(--color-text);
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all var(--transition);
}

.carousel-btn:hover {
  background: var(--color-primary);
  border-color: var(--color-primary);
  color: white;
  box-shadow: var(--shadow-colored);
}

.carousel-content {
  flex: 1;
  overflow: hidden;
}

.carousel-track {
  position: relative;
}

.project-card {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
  background: var(--color-bg-elevated);
  border: 1px solid var(--color-border);
  border-radius: var(--radius);
  box-shadow: var(--shadow-lg);
  overflow: hidden;
  text-decoration: none;
  color: inherit;
  transition: transform var(--transition), box-shadow var(--transition), border-color var(--transition);
}

.project-card:hover {
  transform: scale(1.02);
  box-shadow: var(--shadow-colored);
  border-color: var(--color-primary);
}

.project-image {
  height: 300px;
  overflow: hidden;
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
  padding: 2rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.project-title {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
  color: var(--color-text);
}

.project-description {
  color: var(--color-text-secondary);
  line-height: 1.7;
  margin-bottom: 1.5rem;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.project-link {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  color: var(--color-accent);
  font-weight: 500;
  margin-top: auto;
  transition: color var(--transition);
}

.project-card:hover .project-link {
  color: var(--color-primary);
}

.carousel-indicators {
  display: flex;
  justify-content: center;
  gap: 0.5rem;
  margin-top: 2rem;
}

.indicator {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  border: 2px solid var(--color-border);
  background: transparent;
  cursor: pointer;
  transition: all var(--transition);
}

.indicator:hover {
  border-color: var(--color-accent);
  background: var(--color-accent);
}

.indicator.active {
  background: var(--color-primary);
  border-color: var(--color-primary);
}

.carousel-counter {
  text-align: center;
  margin-top: 1rem;
  color: var(--color-text-muted);
  font-size: 0.875rem;
}

/* Slide transitions - Next direction */
.slide-next-enter-active,
.slide-next-leave-active,
.slide-prev-enter-active,
.slide-prev-leave-active {
  transition: opacity 0.25s ease, transform 0.25s ease;
}

.slide-next-enter-from {
  opacity: 0;
  transform: translateX(30px);
}

.slide-next-leave-to {
  opacity: 0;
  transform: translateX(-30px);
}

/* Slide transitions - Prev direction */
.slide-prev-enter-from {
  opacity: 0;
  transform: translateX(-30px);
}

.slide-prev-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

/* Mobile styles */
@media (max-width: 768px) {
  .carousel-container {
    flex-direction: column;
    gap: 1.5rem;
  }

  .carousel-btn {
    display: none;
  }

  .project-card {
    grid-template-columns: 1fr;
  }

  .project-image {
    height: 200px;
  }

  .project-info {
    padding: 1.5rem;
  }

  .project-title {
    font-size: 1.25rem;
  }
}

@media (max-width: 768px) {
  .carousel-container {
    position: relative;
  }

  .carousel-btn {
    display: flex;
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    z-index: 10;
    width: 40px;
    height: 40px;
    background: rgba(255, 255, 255, 0.9);
  }

  .carousel-btn.prev {
    left: 0.5rem;
  }

  .carousel-btn.next {
    right: 0.5rem;
  }
}
</style>
