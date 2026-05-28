<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const isMenuOpen = ref(false);
const isScrolled = ref(false);
const currentHash = ref(window.location.hash || '#/');

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

const closeMenu = () => {
  isMenuOpen.value = false;
};

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50;
};

const handleHash = () => {
  currentHash.value = window.location.hash || '#/';
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
  window.addEventListener('hashchange', handleHash);
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
  window.removeEventListener('hashchange', handleHash);
});
</script>

<template>
  <header :class="['header', { 'header-scrolled': isScrolled }]">
    <div class="container header-container">
      <!-- Logo -->
      <a :href="currentHash === '#/intranet' ? '#/' : '#inicio'" class="logo" @click="closeMenu">
        <div class="logo-image-container">
          <!-- Logo real cargado desde public/logo.webp -->
          <img src="/logo.webp" alt="Logo de Lovely Garden" class="logo-img" />
        </div>
        <span class="logo-text">Lovely <span class="logo-highlight">Garden</span></span>
      </a>

      <!-- Menú Desktop -->
      <nav class="nav-desktop">
        <template v-if="currentHash === '#/intranet'">
          <a href="#/" class="nav-link">← Volver al Sitio</a>
          <a href="#/" class="btn btn-outline btn-sm">Web Institucional</a>
        </template>
        <template v-else>
          <a href="#inicio" class="nav-link">Inicio</a>
          <a href="#nosotros" class="nav-link">Nosotros</a>
          <a href="#niveles" class="nav-link">Niveles</a>
          <a href="#beneficios" class="nav-link">Propuesta</a>
          <a href="#galeria" class="nav-link">Galería</a>
          <a href="#/intranet" class="btn btn-primary btn-sm btn-intranet-nav">Intranet 🔐</a>
          <a href="#admision" class="btn btn-accent btn-sm">Admisión 2026</a>
        </template>
      </nav>

      <!-- Botón Menú Móvil -->
      <button class="menu-toggle" @click="toggleMenu" :aria-expanded="isMenuOpen" aria-label="Abrir menú">
        <span :class="['hamburger-line', { 'hamburger-active': isMenuOpen }]"></span>
      </button>
    </div>

    <!-- Menú Móvil desplegable -->
    <transition name="fade-slide">
      <nav v-if="isMenuOpen" class="nav-mobile">
        <div class="nav-mobile-container">
          <template v-if="currentHash === '#/intranet'">
            <a href="#/" class="nav-mobile-link" @click="closeMenu">← Volver al Sitio</a>
            <a href="#/" class="btn btn-outline" @click="closeMenu">Web Institucional</a>
          </template>
          <template v-else>
            <a href="#inicio" class="nav-mobile-link" @click="closeMenu">Inicio</a>
            <a href="#nosotros" class="nav-mobile-link" @click="closeMenu">Nosotros</a>
            <a href="#niveles" class="nav-mobile-link" @click="closeMenu">Niveles</a>
            <a href="#beneficios" class="nav-mobile-link" @click="closeMenu">Propuesta</a>
            <a href="#galeria" class="nav-mobile-link" @click="closeMenu">Galería</a>
            <a href="#/intranet" class="btn btn-primary" @click="closeMenu">Intranet 🔐</a>
            <a href="#admision" class="btn btn-accent" @click="closeMenu">Admisión 2026</a>
          </template>
        </div>
      </nav>
    </transition>
  </header>
</template>

<style scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1000;
  padding: 1.5rem 0;
  transition: var(--transition);
  background-color: transparent;
}

.header-scrolled {
  padding: 0.7rem 0;
  background-color: rgba(253, 251, 247, 0.9);
  backdrop-filter: blur(12px);
  box-shadow: var(--shadow-sm);
  border-bottom: 1px solid rgba(255, 167, 38, 0.08);
}

.header-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

/* Logo */
.logo {
  display: flex;
  align-items: center;
  gap: 0.85rem;
  z-index: 1001;
}

.logo-image-container {
  width: 3.25rem;
  height: 3.25rem;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: var(--transition);
  filter: drop-shadow(0 4px 6px rgba(0, 0, 0, 0.05));
  border-radius: 50%;
  background-color: #FFFFFF;
  padding: 0.25rem;
}

.logo:hover .logo-image-container {
  transform: scale(1.08) rotate(-5deg);
}

.logo-img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  border-radius: 50%;
}

.logo-text {
  font-family: var(--font-title);
  font-weight: 700;
  font-size: 1.7rem;
  color: var(--text-dark);
  letter-spacing: -0.02em;
}

.logo-highlight {
  color: var(--primary-hover);
}

/* Navegación Desktop */
.nav-desktop {
  display: flex;
  align-items: center;
  gap: 2.25rem;
}

.nav-link {
  font-family: var(--font-title);
  font-weight: 600;
  font-size: 1.05rem;
  color: var(--text-dark);
  position: relative;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: -4px;
  left: 0;
  width: 0;
  height: 3px;
  background-color: var(--secondary);
  transition: var(--transition);
  border-radius: var(--radius-full);
}

.nav-link:hover {
  color: var(--secondary);
}

.nav-link:hover::after {
  width: 100%;
}

.btn-sm {
  padding: 0.6rem 1.5rem;
  font-size: 0.95rem;
}

/* Botón Menú Móvil */
.menu-toggle {
  display: none;
  cursor: pointer;
  z-index: 1001;
  width: 2.5rem;
  height: 2.5rem;
  align-items: center;
  justify-content: center;
}

.hamburger-line {
  display: block;
  width: 1.6rem;
  height: 3px;
  background-color: var(--text-dark);
  position: relative;
  transition: var(--transition);
  border-radius: var(--radius-full);
}

.hamburger-line::before,
.hamburger-line::after {
  content: '';
  display: block;
  width: 100%;
  height: 3px;
  background-color: var(--text-dark);
  position: absolute;
  transition: var(--transition);
  border-radius: var(--radius-full);
}

.hamburger-line::before {
  top: -8px;
}

.hamburger-line::after {
  bottom: -8px;
}

.hamburger-active {
  background-color: transparent;
}

.hamburger-active::before {
  transform: rotate(45deg);
  top: 0;
}

.hamburger-active::after {
  transform: rotate(-45deg);
  bottom: 0;
}

/* Navegación Móvil */
.nav-mobile {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background-color: var(--bg-primary);
  z-index: 1000;
  display: flex;
  align-items: center;
  justify-content: center;
}

.nav-mobile-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
  width: 100%;
  padding: 2rem;
}

.nav-mobile-link {
  font-family: var(--font-title);
  font-weight: 700;
  font-size: 1.5rem;
  color: var(--text-dark);
  transition: var(--transition);
}

.nav-mobile-link:hover {
  color: var(--secondary);
}

/* Transiciones de Menú Móvil */
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: var(--transition);
}

.fade-slide-enter-from,
.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}

/* Responsividad */
@media (max-width: 992px) {
  .nav-desktop {
    display: none;
  }
  
  .menu-toggle {
    display: flex;
  }
}
</style>
