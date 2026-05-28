<script setup>
import { ref } from 'vue';

const valores = ref([
  {
    titulo: 'Amor & Cuidado',
    descripcion: 'Creamos un entorno afectuoso que simula el hogar, donde cada niño se siente seguro, escuchado y valorado.',
    color: 'var(--secondary)',
    icono: 'M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z'
  },
  {
    titulo: 'Respeto',
    descripcion: 'Promovemos la tolerancia y el respeto mutuo, reconociendo y celebrando las diferencias individuales de cada estudiante.',
    color: 'var(--primary-hover)',
    icono: 'M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm1 17h-2v-2h2v2zm2.07-7.75l-.9.92C13.45 12.9 13 13.5 13 15h-2v-.5c0-1.1.45-2.1 1.17-2.83l1.24-1.26c.37-.36.59-.86.59-1.41 0-1.1-.9-2-2-2s-2 .9-2 2H7c0-2.76 2.24-5 5-5s5 2.24 5 5c0 1.04-.42 1.99-1.07 2.75z'
  },
  {
    titulo: 'Empatía',
    descripcion: 'Fomentamos la inteligencia emocional y la capacidad de comprender y acompañar los sentimientos de los demás en armonía.',
    color: 'var(--accent)',
    icono: 'M16 11c1.66 0 2.99-1.34 2.99-3S17.66 5 16 5c-1.66 0-3 1.34-3 3s1.34 3 3 3zm-8 0c1.66 0 2.99-1.34 2.99-3S9.66 5 8 5C6.34 5 5 6.34 5 8s1.34 3 3 3zm0 2c-2.33 0-7 1.17-7 3.5V19h14v-2.5c0-2.33-4.67-3.5-7-3.5zm8 0c-.29 0-.62.02-.97.05 1.16.84 1.97 1.97 1.97 3.45V19h6v-2.5c0-2.33-4.67-3.5-7-3.5z'
  },
  {
    titulo: 'Creatividad',
    descripcion: 'Estimulamos la libre expresión, el juego heurístico y la búsqueda de soluciones originales e innovadoras.',
    color: 'var(--secondary)',
    icono: 'M12 3c-4.97 0-9 4.03-9 9 0 2.12.74 4.07 1.97 5.61L4.35 19.4c-.39.39-.39 1.02 0 1.41.39.39 1.02.39 1.41 0l1.9-1.9C9.22 19.58 10.57 20 12 20c4.97 0 9-4.03 9-9s-4.03-9-9-9zm0 15c-3.31 0-6-2.69-6-6s2.69-6 6-6 6 2.69 6 6-2.69 6-6 6z'
  }
]);
</script>

<template>
  <section id="nosotros" class="section section-alt">
    <div class="container">
      <!-- Encabezado de Sección -->
      <div class="section-header text-center">
        <h2>Quiénes Somos</h2>
        <p class="section-subtitle">
          Una comunidad educativa cálida y dedicada al desarrollo integral de tus hijos.
        </p>
      </div>

      <!-- Misión & Visión Asimétrica con texto real -->
      <div class="mv-grid">
        <div class="mv-card mission-card">
          <div class="card-icon-decor">✨</div>
          <h3>Nuestro Compromiso</h3>
          <p>
            Somos una institución educativa comprometida con la formación integral de nuestros estudiantes, promoviendo valores, conocimiento y el desarrollo de sus talentos para construir un futuro lleno de oportunidades.
          </p>
        </div>

        <div class="mv-card vision-card">
          <div class="card-icon-decor">🚀</div>
          <h3>Nuestra Propuesta Pedagógica</h3>
          <p>
            Buscamos ser reconocidos en Huancayo por una metodología innovadora donde el juego, la indagación y la educación socioemocional son los pilares fundamentales. Fomentamos la autonomía y el liderazgo temprano en cada uno de nuestros estudiantes.
          </p>
        </div>
      </div>

      <!-- Valores Institucionales -->
      <div class="values-wrapper">
        <h3 class="values-title text-center">Nuestros Valores</h3>
        <div class="values-grid">
          <div v-for="(val, idx) in valores" :key="idx" class="value-card" :style="{ '--val-color': val.color }">
            <div class="value-icon-box">
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
                <path :d="val.icono" />
              </svg>
            </div>
            <h4>{{ val.titulo }}</h4>
            <p>{{ val.descripcion }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.section-header {
  margin-bottom: 4.5rem;
}

.section-subtitle {
  max-width: 600px;
  margin: 0.5rem auto 0;
  font-size: 1.15rem;
}

/* Misión & Visión */
.mv-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2.5rem;
  margin-bottom: 6rem;
}

.mv-card {
  background-color: var(--bg-secondary);
  border-radius: var(--radius-md);
  padding: 3rem;
  box-shadow: var(--shadow-sm);
  border: 1px solid rgba(255, 167, 38, 0.04);
  position: relative;
  overflow: hidden;
  transition: var(--transition);
}

.mv-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 6px;
  height: 100%;
}

.mission-card::before {
  background-color: var(--primary);
}

.vision-card::before {
  background-color: var(--secondary);
}

.mv-card:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-lg);
}

.card-icon-decor {
  position: absolute;
  top: 1.5rem;
  right: 1.5rem;
  font-size: 2.5rem;
  opacity: 0.15;
  transition: var(--transition);
}

.mv-card:hover .card-icon-decor {
  transform: scale(1.2) rotate(10deg);
  opacity: 0.3;
}

.mv-card h3 {
  font-size: 1.75rem;
  margin-bottom: 1.25rem;
  color: var(--text-dark);
}

.mv-card p {
  font-size: 1.05rem;
  line-height: 1.7;
}

/* Valores */
.values-wrapper {
  position: relative;
}

.values-title {
  font-size: 2rem;
  margin-bottom: 3rem;
}

.values-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 2rem;
}

.value-card {
  background-color: var(--bg-secondary);
  border-radius: var(--radius-md);
  padding: 2.25rem 1.75rem;
  text-align: center;
  box-shadow: var(--shadow-sm);
  border: 1px solid rgba(255, 167, 38, 0.04);
  transition: var(--transition);
}

.value-card:hover {
  transform: translateY(-8px);
  box-shadow: var(--shadow-lg);
  border-bottom: 4px solid var(--val-color);
}

.value-icon-box {
  width: 4rem;
  height: 4rem;
  background-color: var(--bg-primary);
  color: var(--val-color);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 1.5rem;
  transition: var(--transition);
}

.value-icon-box svg {
  width: 2rem;
  height: 2rem;
}

.value-card:hover .value-icon-box {
  background-color: var(--val-color);
  color: var(--bg-secondary);
  transform: scale(1.1);
}

.value-card h4 {
  font-size: 1.25rem;
  margin-bottom: 0.85rem;
  color: var(--text-dark);
}

.value-card p {
  font-size: 0.95rem;
  line-height: 1.5;
}

/* Responsividad */
@media (max-width: 992px) {
  .mv-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .values-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 1.5rem;
  }
}

@media (max-width: 576px) {
  .mv-card {
    padding: 2rem 1.5rem;
  }
  
  .values-grid {
    grid-template-columns: 1fr;
  }
}
</style>
