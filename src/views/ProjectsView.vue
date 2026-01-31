<script setup>
import { ref, onMounted } from 'vue'
import ProjectCarousel from '../components/ProjectCarousel.vue'
import projectsData from '../data/projects.json'

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
        <h1 class="section-title">Mes Projets</h1>
        <p class="section-subtitle">
          Découvrez une selection de mes realisations.
        </p>
      </div>

      <div class="projects-carousel" :class="{ visible: isLoaded }">
        <ProjectCarousel v-if="projects.length" :projects="projects" />
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

.projects-carousel {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.6s ease 0.2s, transform 0.6s ease 0.2s;
}

.projects-carousel.visible {
  opacity: 1;
  transform: translateY(0);
}
</style>
