<script setup>
import { onMounted, ref } from 'vue'

const isVisible = ref(false)

const stack = ['.NET', 'C#', 'Azure', 'Vue.js', 'C++']

onMounted(() => {
    setTimeout(() => {
        isVisible.value = true
    }, 100)
})
</script>

<template>
    <section class="home">
        <div class="container">
            <div class="hero reveal" :class="{ visible: isVisible }">
                <div class="hero-content">
                    <span class="eyebrow">Développeur logiciel</span>
                    <h1 class="hero-title">
                        Bonjour, je suis <span class="gradient-text">Dorian</span>
                    </h1>
                    <p class="hero-tagline">
                        Développeur logiciel spécialisé en <strong>.NET</strong> et
                        environnement <strong>Azure</strong>. Je conçois des solutions
                        robustes, du backend temps réel aux interfaces modernes.
                    </p>

                    <ul class="hero-stack" aria-label="Technologies">
                        <li v-for="tech in stack" :key="tech">{{ tech }}</li>
                    </ul>

                    <div class="hero-actions">
                        <router-link to="/projects" class="btn btn-primary">
                            Voir mes projets
                            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24"
                                fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                stroke-linejoin="round">
                                <path d="M5 12h14M12 5l7 7-7 7" />
                            </svg>
                        </router-link>
                        <a href="/CV_DORIAN_BARAT.pdf" download class="btn btn-accent">
                            Télécharger mon CV
                            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24"
                                fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                stroke-linejoin="round">
                                <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4" />
                                <polyline points="7 10 12 15 17 10" />
                                <line x1="12" y1="15" x2="12" y2="3" />
                            </svg>
                        </a>
                        <router-link to="/contact" class="btn btn-secondary">
                            Me contacter
                        </router-link>
                    </div>
                </div>

                <div class="hero-image">
                    <div class="image-ring">
                        <img src="/me.JPG" alt="Photo de profil" />
                    </div>
                    <span class="status-badge">
                        <span class="status-dot"></span>
                        Disponible
                    </span>
                </div>
            </div>
        </div>
    </section>
</template>

<style scoped>
.home {
    min-height: calc(100vh - 84px);
    display: flex;
    align-items: center;
    padding: 3rem 0;
}

.hero {
    display: grid;
    grid-template-columns: 1.1fr auto;
    gap: clamp(2rem, 6vw, 5rem);
    align-items: center;
    width: 100%;
}

.hero-title {
    font-family: var(--font-display);
    font-size: clamp(2.4rem, 6vw, 4rem);
    font-weight: 700;
    letter-spacing: -0.025em;
    line-height: 1.05;
    margin-bottom: 1.5rem;
}

.hero-tagline {
    font-size: clamp(1.05rem, 2vw, 1.25rem);
    color: var(--color-text-secondary);
    line-height: 1.75;
    margin-bottom: 2rem;
    max-width: 560px;
}

.hero-tagline strong {
    color: var(--color-text);
    font-weight: 600;
}

.hero-stack {
    display: flex;
    flex-wrap: wrap;
    gap: 0.6rem;
    list-style: none;
    margin: 0 0 2.5rem;
    padding: 0;
}

.hero-stack li {
    font-family: var(--font-display);
    font-size: 0.82rem;
    font-weight: 500;
    padding: 0.4rem 0.9rem;
    border-radius: 9999px;
    color: var(--color-text-secondary);
    background: var(--glass-bg);
    border: 1px solid var(--glass-border);
    transition: color var(--transition-fast), border-color var(--transition-fast), transform var(--transition-fast);
}

.hero-stack li:hover {
    color: var(--color-accent);
    border-color: rgba(212, 175, 55, 0.4);
    transform: translateY(-2px);
}

.hero-actions {
    display: flex;
    gap: 0.9rem;
    flex-wrap: wrap;
}

/* Image avec anneau lumineux en dégradé */
.hero-image {
    position: relative;
    justify-self: center;
}

.image-ring {
    position: relative;
    width: clamp(240px, 30vw, 320px);
    height: clamp(240px, 30vw, 320px);
    border-radius: 50%;
    padding: 5px;
    background: var(--gradient-brand);
    box-shadow: var(--glow-green);
    animation: float 6s ease-in-out infinite;
}

.image-ring::before {
    content: '';
    position: absolute;
    inset: -22px;
    border-radius: 50%;
    background: conic-gradient(from 0deg, rgba(8, 127, 68, 0.35), rgba(212, 175, 55, 0.3), rgba(8, 127, 68, 0.35));
    filter: blur(28px);
    opacity: 0.7;
    z-index: -1;
}

.image-ring img {
    width: 100%;
    height: 100%;
    border-radius: 50%;
    object-fit: cover;
    border: 4px solid var(--color-bg);
}

.status-badge {
    position: absolute;
    bottom: 14px;
    right: -6px;
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    font-size: 0.82rem;
    font-weight: 600;
    color: var(--color-text);
    padding: 0.5rem 0.95rem;
    border-radius: 9999px;
    background: rgba(8, 10, 8, 0.85);
    -webkit-backdrop-filter: blur(10px);
    backdrop-filter: blur(10px);
    border: 1px solid var(--glass-border);
    box-shadow: var(--shadow);
}

.status-dot {
    width: 9px;
    height: 9px;
    border-radius: 50%;
    background: #2ec27e;
    box-shadow: 0 0 0 0 rgba(46, 194, 126, 0.6);
    animation: pulse 2s infinite;
}

@keyframes float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-12px); }
}

@keyframes pulse {
    0% { box-shadow: 0 0 0 0 rgba(46, 194, 126, 0.55); }
    70% { box-shadow: 0 0 0 10px rgba(46, 194, 126, 0); }
    100% { box-shadow: 0 0 0 0 rgba(46, 194, 126, 0); }
}

@media (max-width: 900px) {
    .hero {
        grid-template-columns: 1fr;
        text-align: center;
        gap: 2.5rem;
    }

    .hero-image {
        grid-row: 1;
    }

    .eyebrow {
        justify-content: center;
    }

    .hero-tagline {
        margin-left: auto;
        margin-right: auto;
    }

    .hero-stack,
    .hero-actions {
        justify-content: center;
    }
}

@media (max-width: 480px) {
    .hero-actions {
        flex-direction: column;
    }

    .hero-actions .btn {
        width: 100%;
    }
}
</style>
