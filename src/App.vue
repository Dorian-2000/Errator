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
                <router-link to="/" class="logo" @click="closeMenu">
                    <span class="logo-mark">DB</span>
                    <span class="logo-text">Portfolio</span>
                </router-link>

                <button class="menu-toggle" @click="toggleMenu" :aria-expanded="isMenuOpen" aria-label="Menu">
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
    transition: padding var(--transition);
    padding: 1rem 0;
}

.nav {
    max-width: 1140px;
    margin: 0 auto;
    padding: 0.65rem 1.5rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-radius: 9999px;
    border: 1px solid transparent;
    transition: background var(--transition), border-color var(--transition), box-shadow var(--transition), backdrop-filter var(--transition);
}

/* La barre devient une "pilule" flottante en verre une fois scrollé */
.header.scrolled {
    padding: 0.6rem 1.5rem;
}

.header.scrolled .nav {
    background: rgba(8, 10, 8, 0.72);
    -webkit-backdrop-filter: blur(16px) saturate(140%);
    backdrop-filter: blur(16px) saturate(140%);
    border-color: var(--glass-border);
    box-shadow: 0 12px 40px -16px rgba(0, 0, 0, 0.8);
}

.logo {
    display: flex;
    align-items: center;
    gap: 0.6rem;
    text-decoration: none;
}

.logo-mark {
    display: grid;
    place-items: center;
    width: 38px;
    height: 38px;
    border-radius: 11px;
    font-family: var(--font-display);
    font-size: 0.95rem;
    font-weight: 700;
    letter-spacing: 0.02em;
    color: #fff;
    background: var(--gradient-green);
    box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.12), 0 6px 18px -8px rgba(8, 127, 68, 0.8);
    transition: transform var(--transition);
}

.logo:hover .logo-mark {
    transform: rotate(-6deg) scale(1.05);
}

.logo-text {
    font-family: var(--font-display);
    font-size: 1.2rem;
    font-weight: 600;
    letter-spacing: -0.01em;
    color: var(--color-text);
}

.nav-links {
    display: flex;
    gap: 0.4rem;
    list-style: none;
    margin: 0;
    padding: 0;
}

.nav-links a {
    display: block;
    color: var(--color-text-secondary);
    text-decoration: none;
    font-weight: 500;
    font-size: 0.95rem;
    padding: 0.5rem 1rem;
    border-radius: 9999px;
    position: relative;
    transition: color var(--transition-fast), background var(--transition-fast);
}

.nav-links a:hover {
    color: var(--color-text);
    background: var(--glass-bg-hover);
}

.nav-links a.active {
    color: #fff;
    background: rgba(8, 127, 68, 0.18);
    box-shadow: inset 0 0 0 1px rgba(8, 127, 68, 0.45);
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
    margin-top: 84px;
}

.footer {
    border-top: 1px solid var(--glass-border);
    background: rgba(8, 10, 8, 0.4);
    padding: 2.25rem;
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
        background: rgba(5, 6, 5, 0.97);
        -webkit-backdrop-filter: blur(20px);
        backdrop-filter: blur(20px);
        flex-direction: column;
        justify-content: center;
        align-items: center;
        gap: 1rem;
        padding-top: 12vh;
        opacity: 0;
        visibility: hidden;
        transition: opacity 0.3s ease, visibility 0.3s ease;
    }

    .nav-links.open {
        opacity: 1;
        visibility: visible;
    }

    .nav-links a {
        font-size: 1.4rem;
        padding: 0.75rem 1.75rem;
    }
}
</style>
