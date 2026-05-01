<script setup lang="ts">
import { ref, watch, onUnmounted } from 'vue'

defineProps<{
  currentPage: string
}>()

const emit = defineEmits<{
  navigate: [page: string]
}>()

const isOpen = ref(false)

const handleNavigate = (page: string) => {
  emit('navigate', page)
  isOpen.value = false
  window.scrollTo(0, 0)
}

const closeMenu = () => {
  isOpen.value = false
}

watch(isOpen, (open) => {
  if (open) {
    document.body.style.overflow = 'hidden'
    document.body.style.position = 'fixed'
    document.body.style.width = '100%'
  } else {
    document.body.style.overflow = ''
    document.body.style.position = ''
    document.body.style.width = ''
  }
})

onUnmounted(() => {
  document.body.style.overflow = ''
})
</script>

<template>
  <nav class="site-nav" :class="{ 'site-nav--transparent': currentPage === 'home' }">
    <div class="nav-container">
      <a
        v-if="currentPage !== 'home'"
        class="nav-logo"
        href="javascript:void(0)"
        @click="handleNavigate('home')"
      >
        <img src="/logo.png" alt="Ri.Crea" />
      </a>
      <div class="nav-menu" :class="{ 'is-open': isOpen }" @click.self="closeMenu">
        <button v-if="isOpen" class="nav-close" @click="closeMenu" aria-label="Close menu">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M18 6L6 18"></path>
            <path d="M6 6l12 12"></path>
          </svg>
        </button>
        <a
          class="nav-link"
          :class="{ 'is-active': currentPage === 'home' }"
          href="javascript:void(0)"
          @click="handleNavigate('home')"
        >
          Home
        </a>
        <a
          class="nav-link"
          :class="{ 'is-active': currentPage === 'portfolio' }"
          href="javascript:void(0)"
          @click="handleNavigate('portfolio')"
        >
          Portfolio
        </a>
        <a
          class="nav-link"
          :class="{ 'is-active': currentPage.startsWith('gallery-') }"
          href="javascript:void(0)"
        >
          Gallerie
        </a>
        <a
          class="nav-link"
          :class="{ 'is-active': currentPage === 'services' }"
          href="javascript:void(0)"
          @click="handleNavigate('services')"
        >
          Servizi
        </a>
        <a class="nav-link" href="mailto:hello@example.com">Contatti</a>
      </div>
      <button class="nav-toggle" @click="isOpen = !isOpen" aria-label="Toggle menu">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="nav-icon">
          <circle cx="12" cy="12" r="10"></circle>
          <path d="m14.31 8 5.74 9.94"></path>
          <path d="M9.69 8h11.48"></path>
          <path d="m7.38 12 5.74-9.94"></path>
          <path d="M9.69 16 3.95 6.06"></path>
          <path d="M14.31 16H2.83"></path>
          <path d="m16.62 12-5.74 9.94"></path>
        </svg>
      </button>
    </div>
  </nav>
</template>

<style scoped>
.site-nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;

  backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
}

.site-nav--transparent {
  background: linear-gradient(180deg, rgba(2, 2, 3, 0.30), rgba(2, 2, 3, 0.1));
  border-bottom: none;
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 72px;
}

.nav-menu {
  margin-left: auto;
  display: flex;
  align-items: center;
  gap: 28px;
}

.nav-logo {
  flex-shrink: 0;
  width: 120px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
  border-radius: 9px;
}

.nav-logo::after {
  content: '';
  position: absolute;
  top: 12%;
  bottom: 12%;
  left: 0;
  width: 2px;
  border-radius: 999px;
  background: linear-gradient(180deg, var(--accent), var(--accent-dark), var(--accent-warm));
  box-shadow: 0 0 22px rgba(0, 180, 200, 0.72), 0 0 34px rgba(240, 40, 100, 0.42);
  animation:
    logoCursor 2.4s steps(18, end) 0.2s both,
    cursorBlink 0.62s steps(1, end) 0.2s 4;
}

.nav-logo img {
  width: 100%;
  height: auto;
  clip-path: inset(0 100% 0 0);
  animation: logoTypeReveal 2.4s steps(18, end) 0.2s both;
}

.nav-menu {
  display: flex;
  align-items: center;
  gap: 28px;
}

.nav-link {
  color: var(--text);
  font-family: 'Doto', cursive;
  font-size: 0.88rem;
  font-weight: 800;
  text-transform: uppercase;
  text-decoration: none;
  transition: all 0.3s ease;
  position: relative;
}

.nav-link:hover {
  color: var(--accent);
}

.nav-link.is-active {
  color: var(--accent);
}

.nav-link.is-active::after {
  content: '';
  position: absolute;
  bottom: -6px;
  left: 0;
  right: 0;
  height: 2px;
  background: var(--accent);
}

.nav-toggle {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
  padding: 8px;
}

.nav-icon {
  width: 24px;
  height: 24px;
  color: var(--text);
  transition: color 0.3s ease;
}

.nav-close {
  position: absolute;
  top: 20px;
  right: 20px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 8px;
  color: var(--text);
  z-index: 101;
}

.nav-close svg {
  width: 24px;
  height: 24px;
}

@media (max-width: 768px) {
  .nav-container {
    height: 64px;
  }

  .nav-toggle {
    display: flex;
  }

  .nav-menu {
    position: fixed;
    inset: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 24px;
    padding: 120px 28px 32px;
    background: rgba(5, 5, 6, 0.96);
    backdrop-filter: blur(24px);
    transform: translateY(-100%);
    opacity: 0;
    pointer-events: none;
    transition: transform 0.3s ease, opacity 0.3s ease;
    z-index: 150;
    height: 100vh;
  }

  .nav-menu.is-open {
    transform: translateY(0);
    opacity: 1;
    pointer-events: auto;
  }

  .nav-link {
    padding: 0;
    width: auto;
    border: none;
    font-size: 1.1rem;
  }

  .nav-link.is-active::after {
    display: none;
  }

  .nav-link.is-active {
    background: none;
  }
}
</style>
