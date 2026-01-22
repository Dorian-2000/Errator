<script setup>
import { onMounted, ref } from 'vue'

const isVisible = ref(false)

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true
  }, 100)
})
</script>

<template>
  <section class="home">
    <div class="container">
      <div class="hero" :class="{ visible: isVisible }">
        <div class="hero-image">
          <img src="/me.jpg" alt="Photo de profil" />
        </div>

        <div class="hero-content">
          <h1 class="hero-title">Bonjour, je suis <span>Dorian</span></h1>
          <p class="hero-tagline">
            Développeur logiciel junior,  Je suis spécialisé dans le .NET et environnement Azure.
          </p>

          <div class="hero-actions">
            <router-link to="/projects" class="btn btn-primary">
              Voir mes projets
              <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <path d="M5 12h14M12 5l7 7-7 7"/>
              </svg>
            </router-link>
            <router-link to="/contact" class="btn btn-secondary">
              Me contacter
            </router-link>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.home {
  min-height: calc(100vh - 80px);
  display: flex;
  align-items: center;
}

.hero {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 4rem;
  align-items: center;
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}

.hero.visible {
  opacity: 1;
  transform: translateY(0);
}

.hero-image {
  width: 280px;
  height: 280px;
  border-radius: 50%;
  overflow: hidden;
  box-shadow: var(--shadow-lg);
  border: 4px solid var(--color-primary);
}

.hero-image img {
  width: 100%;
  object-fit: cover;
}

.hero-title {
  font-size: 3rem;
  font-weight: 700;
  line-height: 1.2;
  margin-bottom: 1.5rem;
}

.hero-title span {
  color: var(--color-primary);
}

.hero-tagline {
  font-size: 1.25rem;
  color: var(--color-text-secondary);
  line-height: 1.7;
  margin-bottom: 2.5rem;
  max-width: 600px;
}

.hero-actions {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}

.hero-actions .btn {
  gap: 0.5rem;
}

@media (max-width: 900px) {
  .hero {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 2rem;
  }

  .hero-image {
    width: 200px;
    height: 200px;
    margin: 0 auto;
  }

  .hero-title {
    font-size: 2.25rem;
  }

  .hero-tagline {
    font-size: 1.125rem;
    margin-left: auto;
    margin-right: auto;
  }

  .hero-actions {
    justify-content: center;
  }
}

@media (max-width: 480px) {
  .hero-title {
    font-size: 1.875rem;
  }

  .hero-actions {
    flex-direction: column;
  }

  .hero-actions .btn {
    width: 100%;
  }
}
</style>
