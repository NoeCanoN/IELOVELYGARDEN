<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import Header from './components/Header.vue';
import Hero from './components/Hero.vue';
import About from './components/About.vue';
import Programs from './components/Programs.vue';
import Benefits from './components/Benefits.vue';
import Gallery from './components/Gallery.vue';
import AdmissionForm from './components/AdmissionForm.vue';
import Footer from './components/Footer.vue';
import IntranetPanel from './components/IntranetPanel.vue';

// --- SISTEMA DE ENRUTAMIENTO POR HASH SPA ---
const currentHash = ref(window.location.hash || '#/');

const handleHashChange = () => {
  currentHash.value = window.location.hash || '#/';
  // Auto-scroll al inicio de la página al cambiar de ruta
  window.scrollTo({ top: 0, behavior: 'smooth' });
};

onMounted(() => {
  window.addEventListener('hashchange', handleHashChange);
});

onUnmounted(() => {
  window.removeEventListener('hashchange', handleHashChange);
});
</script>

<template>
  <div class="app-wrapper">
    <!-- Barra de Navegación -->
    <Header />

    <!-- RUTA INTRANET: /#/intranet -->
    <template v-if="currentHash === '#/intranet'">
      <IntranetPanel />
    </template>

    <!-- RUTA LANDING PRINCIPAL: /#/ o vacía -->
    <template v-else>
      <!-- Sección Hero (Bienvenida con foto real y lema) -->
      <Hero />

      <!-- Sección Quiénes Somos (Compromiso y Valores) -->
      <About />

      <!-- Sección Niveles Educativos (Inicial y Primaria) -->
      <Programs />

      <!-- Sección Propuesta de Valor / Beneficios -->
      <Benefits />

      <!-- Sección de Galería de Experiencias (Fotos reales agrupadas por eventos) -->
      <Gallery />

      <!-- Sección de Admisión (Formulario reactivo) -->
      <AdmissionForm />
    </template>

    <!-- Pie de página (Contacto y Ubicación real) -->
    <Footer />
  </div>
</template>

<style>
/* Estilos globales y contenedores */
.app-wrapper {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background-color: var(--bg-primary);
}

/* Transiciones de entrada a la página */
.app-wrapper > section {
  animation: pageFadeIn 0.8s ease-out;
}

@keyframes pageFadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
