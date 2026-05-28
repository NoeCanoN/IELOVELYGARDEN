<script setup>
import { ref, computed } from 'vue';

const fotos = ref([
  // Festival de Lectura
  { src: '/FestivalLectura/0.jpg', alt: 'Festival de Lectura - Momento de aprendizaje', categoria: 'lectura', titulo: 'Rincón de la Lectura' },
  { src: '/FestivalLectura/00.jpg', alt: 'Festival de Lectura - Descubriendo libros', categoria: 'lectura', titulo: 'Explorando Mundos' },
  { src: '/FestivalLectura/1.jpg', alt: 'Festival de Lectura - Compartiendo historias', categoria: 'lectura', titulo: 'Lectura Compartida' },
  { src: '/FestivalLectura/2.jpg', alt: 'Festival de Lectura - Cuentacuentos', categoria: 'lectura', titulo: 'La Hora del Cuento' },
  { src: '/FestivalLectura/3.jpg', alt: 'Festival de Lectura - Libros y juegos', categoria: 'lectura', titulo: 'Diversión Literaria' },
  
  // Show de Talentos
  { src: '/ShowTalentos/0.jpg', alt: 'Show de Talentos - Actuación especial', categoria: 'talentos', titulo: 'Expresión Artística' },
  { src: '/ShowTalentos/1.jpg', alt: 'Show de Talentos - Pequeños artistas', categoria: 'talentos', titulo: 'Talento y Sonrisas' },
  { src: '/ShowTalentos/2.jpg', alt: 'Show de Talentos - Baile infantil', categoria: 'talentos', titulo: 'Danza y Ritmo' },
  { src: '/ShowTalentos/3.jpg', alt: 'Show de Talentos - Presentación grupal', categoria: 'talentos', titulo: 'Creatividad en el Escenario' },
  
  // Día de la Madre
  { src: '/DiaDeLaMadre/0.jpg', alt: 'Día de la Madre - Celebración familiar', categoria: 'madre', titulo: 'Homenaje a Mamá' },
  { src: '/DiaDeLaMadre/1.jpg', alt: 'Día de la Madre - Regalos y abrazos', categoria: 'madre', titulo: 'Momento Especial con Mamá' },
  { src: '/DiaDeLaMadre/2.jpg', alt: 'Día de la Madre - Sonrisas en su día', categoria: 'madre', titulo: 'Felicidad Familiar' },
  
  // Día del Trabajador
  { src: '/DiaDelTrabajador/0.jpg', alt: 'Día del Trabajador - Nuestro equipo de docentes', categoria: 'trabajador', titulo: 'Nuestro Gran Equipo de Trabajo' }
]);

const categorias = ref([
  { id: 'todos', nombre: '✨ Todos' },
  { id: 'lectura', nombre: '📚 Festival de Lectura' },
  { id: 'talentos', nombre: '🎭 Show de Talentos' },
  { id: 'madre', nombre: '💖 Día de la Madre' },
  { id: 'trabajador', nombre: '👷 Día del Trabajador' }
]);

const filtroActivo = ref('todos');
const indexSeleccionado = ref(null);

const fotosFiltradas = computed(() => {
  if (filtroActivo.value === 'todos') return fotos.value;
  return fotos.value.filter(f => f.categoria === filtroActivo.value);
});

const activePhoto = computed(() => {
  if (indexSeleccionado.value === null) return null;
  return fotosFiltradas.value[indexSeleccionado.value];
});

const abrirLightbox = (index) => {
  indexSeleccionado.value = index;
  document.body.style.overflow = 'hidden'; // Evitar scroll
};

const cerrarLightbox = () => {
  indexSeleccionado.value = null;
  document.body.style.overflow = ''; // Restaurar scroll
};

const fotoSiguiente = () => {
  if (indexSeleccionado.value === null) return;
  indexSeleccionado.value = (indexSeleccionado.value + 1) % fotosFiltradas.value.length;
};

const fotoAnterior = () => {
  if (indexSeleccionado.value === null) return;
  indexSeleccionado.value = (indexSeleccionado.value - 1 + fotosFiltradas.value.length) % fotosFiltradas.value.length;
};
</script>

<template>
  <section id="galeria" class="section">
    <div class="container">
      <!-- Encabezado de Sección -->
      <div class="section-header text-center">
        <h2>Galería de Experiencias</h2>
        <p class="section-subtitle">
          Capturas reales de los momentos felices, juegos y aprendizajes de nuestros niños durante el año escolar.
        </p>
      </div>

      <!-- Filtros de Eventos -->
      <div class="filters-container">
        <button 
          v-for="cat in categorias" 
          :key="cat.id" 
          :class="['filter-btn', { 'filter-active': filtroActivo === cat.id }]"
          @click="filtroActivo = cat.id"
        >
          {{ cat.nombre }}
        </button>
      </div>

      <!-- Cuadrícula de Fotos -->
      <div class="gallery-grid">
        <transition-group name="gallery-anim">
          <div 
            v-for="(foto, index) in fotosFiltradas" 
            :key="foto.src" 
            class="gallery-item"
            @click="abrirLightbox(index)"
          >
            <div class="image-wrapper">
              <img :src="foto.src" :alt="foto.alt" class="gallery-img" />
              <!-- Hover Overlay -->
              <div class="item-overlay">
                <span class="zoom-icon">🔍</span>
                <span class="item-title">{{ foto.titulo }}</span>
              </div>
            </div>
          </div>
        </transition-group>
      </div>

      <!-- LIGHTBOX DE PANTALLA COMPLETA NATIVO -->
      <transition name="lightbox-anim">
        <div v-if="indexSeleccionado !== null" class="lightbox" @click.self="cerrarLightbox">
          <!-- Botón de Cerrar -->
          <button class="close-btn" @click="cerrarLightbox" aria-label="Cerrar imagen">✕</button>

          <!-- Navegación Izquierda -->
          <button class="nav-btn prev-btn" @click="fotoAnterior" aria-label="Imagen anterior">‹</button>

          <!-- Contenido Central -->
          <div class="lightbox-content">
            <img :src="activePhoto.src" :alt="activePhoto.alt" class="lightbox-img" />
            <div class="lightbox-info">
              <span class="lightbox-category">📍 {{ activePhoto.alt }}</span>
              <h4 class="lightbox-title">{{ activePhoto.titulo }}</h4>
            </div>
          </div>

          <!-- Navegación Derecha -->
          <button class="nav-btn next-btn" @click="fotoSiguiente" aria-label="Siguiente imagen">›</button>
        </div>
      </transition>
    </div>
  </section>
</template>

<style scoped>
.section-header {
  margin-bottom: 3.5rem;
}

/* Filtros */
.filters-container {
  display: flex;
  justify-content: center;
  gap: 1rem;
  flex-wrap: wrap;
  margin-bottom: 3.5rem;
}

.filter-btn {
  padding: 0.65rem 1.5rem;
  font-family: var(--font-title);
  font-weight: 700;
  font-size: 1rem;
  border-radius: var(--radius-full);
  cursor: pointer;
  background-color: var(--bg-secondary);
  color: var(--text-dark);
  border: 2px solid var(--border-color);
  box-shadow: var(--shadow-sm);
  transition: var(--transition);
}

.filter-btn:hover {
  border-color: var(--primary);
  transform: translateY(-2px);
}

.filter-active {
  background-color: var(--primary);
  color: var(--bg-secondary);
  border-color: var(--primary);
  box-shadow: 0 8px 16px rgba(255, 167, 38, 0.25);
}

/* Cuadrícula de la Galería */
.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 1.5rem;
  min-height: 400px;
}

.gallery-item {
  cursor: pointer;
  border-radius: var(--radius-md);
  overflow: hidden;
  box-shadow: var(--shadow-sm);
  background-color: var(--bg-secondary);
  transition: var(--transition);
  border: 1px solid rgba(255, 167, 38, 0.04);
}

.gallery-item:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-lg);
}

.image-wrapper {
  position: relative;
  width: 100%;
  aspect-ratio: 1.33; /* Forzar aspecto 4:3 para orden */
  overflow: hidden;
}

.gallery-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.6s ease;
}

.gallery-item:hover .gallery-img {
  transform: scale(1.08);
}

/* Hover Overlay */
.item-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(30, 41, 59, 0.7);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: var(--transition);
  padding: 1.5rem;
  text-align: center;
}

.gallery-item:hover .item-overlay {
  opacity: 1;
}

.zoom-icon {
  font-size: 2.25rem;
  color: #FFFFFF;
  margin-bottom: 0.5rem;
  transform: scale(0.8);
  transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.gallery-item:hover .zoom-icon {
  transform: scale(1);
}

.item-title {
  font-family: var(--font-title);
  font-weight: 700;
  font-size: 1.2rem;
  color: #FFFFFF;
}

/* LIGHTBOX PANTALLA COMPLETA */
.lightbox {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(15, 23, 42, 0.95);
  z-index: 2000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
}

.close-btn {
  position: absolute;
  top: 1.5rem;
  right: 1.5rem;
  width: 3.5rem;
  height: 3.5rem;
  border-radius: 50%;
  background-color: rgba(255, 255, 255, 0.1);
  color: #FFFFFF;
  font-size: 1.75rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: var(--transition);
}

.close-btn:hover {
  background-color: var(--accent);
  transform: scale(1.1);
}

.nav-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 4rem;
  height: 4rem;
  border-radius: 50%;
  background-color: rgba(255, 255, 255, 0.15);
  color: #FFFFFF;
  font-size: 2.5rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: var(--transition);
  z-index: 2100;
}

.nav-btn:hover {
  background-color: var(--accent);
  transform: translateY(-50%) scale(1.08);
}

.prev-btn {
  left: 2rem;
}

.next-btn {
  right: 2rem;
}

.lightbox-content {
  max-width: 900px;
  width: 100%;
  display: flex;
  flex-direction: column;
  background-color: var(--bg-secondary);
  border-radius: var(--radius-md);
  overflow: hidden;
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.5);
  animation: scaleUp 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.lightbox-img {
  width: 100%;
  max-height: 70vh;
  object-fit: contain;
  background-color: #000000;
}

.lightbox-info {
  padding: 1.75rem 2.5rem;
}

.lightbox-category {
  font-size: 0.95rem;
  color: var(--text-light);
  font-weight: 500;
  display: block;
  margin-bottom: 0.35rem;
}

.lightbox-title {
  font-size: 1.5rem;
  color: var(--primary-hover);
}

/* ANIMACIONES */
@keyframes scaleUp {
  from { transform: scale(0.9); opacity: 0; }
  to { transform: scale(1); opacity: 1; }
}

/* Transiciones */
.gallery-anim-move {
  transition: transform 0.5s ease;
}

.gallery-anim-enter-active,
.gallery-anim-leave-active {
  transition: all 0.5s ease;
}

.gallery-anim-enter-from,
.gallery-anim-leave-to {
  opacity: 0;
  transform: scale(0.8) translateY(20px);
}

.gallery-anim-leave-active {
  position: absolute;
}

.lightbox-anim-enter-active,
.lightbox-anim-leave-active {
  transition: opacity 0.35s ease;
}

.lightbox-anim-enter-from,
.lightbox-anim-leave-to {
  opacity: 0;
}

/* Responsividad */
@media (max-width: 992px) {
  .nav-btn {
    width: 3.25rem;
    height: 3.25rem;
    font-size: 2rem;
  }
  
  .prev-btn { left: 0.5rem; }
  .next-btn { right: 0.5rem; }
  
  .lightbox-content {
    max-width: 90%;
  }
}

@media (max-width: 576px) {
  .lightbox {
    padding: 1rem;
  }
  
  .nav-btn {
    display: none; /* Ocultar botones de navegación en móviles y permitir gestos */
  }
  
  .lightbox-info {
    padding: 1.25rem 1.5rem;
  }
  
  .lightbox-title {
    font-size: 1.2rem;
  }
}
</style>
