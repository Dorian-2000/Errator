<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { useRoute } from 'vue-router'

const isMenuOpen = ref(false)
const isScrolled = ref(false)
const route = useRoute()

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const closeMenu = () => {
  isMenuOpen.value = false
}

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <div class="app">
    <header class="header" :class="{ scrolled: isScrolled }">
      <nav class="nav">
        <router-link to="/" class="logo" @click="closeMenu">Portfolio</router-link>

        <button class="menu-toggle" @click="toggleMenu" :aria-expanded="isMenuOpen">
          <span class="menu-icon" :class="{ open: isMenuOpen }"></span>
        </button>

        <ul class="nav-links" :class="{ open: isMenuOpen }">
          <li>
            <router-link to="/" @click="closeMenu" :class="{ active: route.name === 'home' }">
              Accueil
            </router-link>
          </li>
          <li>
            <router-link to="/projects" @click="closeMenu" :class="{ active: route.name === 'projects' }">
              Projets
            </router-link>
          </li>
          <li>
            <router-link to="/about" @click="closeMenu" :class="{ active: route.name === 'about' }">
              A propos
            </router-link>
          </li>
          <li>
            <router-link to="/contact" @click="closeMenu" :class="{ active: route.name === 'contact' }">
              Contact
            </router-link>
          </li>
        </ul>
      </nav>
    </header>

    <main class="main">
      <router-view v-slot="{ Component }">
        <transition name="fade" mode="out-in">
          <component :is="Component" />
        </transition>
      </router-view>
    </main>

    <footer class="footer">
      <p>&copy; {{ new Date().getFullYear() }} Portfolio. Tous droits reserves.</p>
    </footer>
  </div>
</template>

<style scoped>
.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  background: rgba(0, 0, 0, 0.95);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid var(--color-border);
  transition: box-shadow 0.3s ease, border-color 0.3s ease;
}

.header.scrolled {
  box-shadow: 0 2px 20px rgba(6, 80, 45, 0.2);
  border-color: var(--color-primary);
}

.nav {
  max-width: 1200px;
  margin: 0 auto;
  padding: 1rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--color-accent);
  text-decoration: none;
  transition: color var(--transition);
}

.logo:hover {
  color: var(--color-primary);
}

.nav-links {
  display: flex;
  gap: 2rem;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-links a {
  color: var(--color-text);
  text-decoration: none;
  font-weight: 500;
  padding: 0.5rem 0;
  position: relative;
  transition: color 0.3s ease;
}

.nav-links a::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: var(--color-accent);
  transition: width 0.3s ease;
}

.nav-links a:hover,
.nav-links a.active {
  color: var(--color-accent);
}

.nav-links a.active::after {
  background: var(--color-primary);
}

.nav-links a:hover::after,
.nav-links a.active::after {
  width: 100%;
}

.menu-toggle {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0.5rem;
  z-index: 1001;
}

.menu-icon {
  display: block;
  width: 24px;
  height: 2px;
  background: var(--color-text);
  position: relative;
  transition: background 0.3s ease;
}

.menu-icon::before,
.menu-icon::after {
  content: '';
  position: absolute;
  width: 24px;
  height: 2px;
  background: var(--color-text);
  transition: transform 0.3s ease;
}

.menu-icon::before {
  top: -8px;
}

.menu-icon::after {
  top: 8px;
}

.menu-icon.open {
  background: transparent;
}

.menu-icon.open::before {
  transform: rotate(45deg) translate(5px, 6px);
}

.menu-icon.open::after {
  transform: rotate(-45deg) translate(5px, -6px);
}

.main {
  flex: 1;
  margin-top: 80px;
}

.footer {
  background: var(--color-bg-elevated);
  border-top: 1px solid var(--color-border);
  padding: 2rem;
  text-align: center;
  color: var(--color-text-muted);
  font-size: 0.875rem;
}

/* Page transitions */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* Mobile styles */
@media (max-width: 768px) {
  .menu-toggle {
    display: block;
  }

  .nav-links {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.98);
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 2rem;
    opacity: 0;
    visibility: hidden;
    transition: opacity 0.3s ease, visibility 0.3s ease;
  }

  .nav-links.open {
    opacity: 1;
    visibility: visible;
  }

  .nav-links a {
    font-size: 1.5rem;
  }
}
</style>
