<script setup>
import { ref } from 'vue';

const beneficios = ref([
  {
    titulo: 'Huerto Escolar Ecológico',
    descripcion: 'Un espacio al aire libre donde los niños siembran, cuidan y cosechan hortalizas, desarrollando conciencia ambiental y paciencia.',
    icono: '🌿',
    bgLight: 'var(--primary-light)',
    badgeColor: 'var(--primary)'
  },
  {
    titulo: 'Apoyo Psicopedagógico',
    descripcion: 'Monitoreamos el desarrollo emocional y de aprendizaje de cada estudiante, brindando orientación a padres y docentes.',
    icono: '🧠',
    bgLight: 'var(--accent-light)',
    badgeColor: 'var(--accent)'
  },
  {
    titulo: 'Talleres Extracurriculares',
    descripcion: 'Fomentamos la expresión corporal y el arte mediante talleres dinámicos de mini-chef, música, danza, teatro y pintura.',
    icono: '🎨',
    bgLight: 'var(--secondary-light)',
    badgeColor: 'var(--secondary-hover)'
  },
  {
    titulo: 'Biblioteca Infantil Lúdica',
    descripcion: 'Ambiente diseñado especialmente para despertar la imaginación y el gusto por la lectura mediante cuentos interactivos.',
    icono: '📚',
    bgLight: 'var(--primary-light)',
    badgeColor: 'var(--primary)'
  }
]);
</script>

<template>
  <section id="beneficios" class="section section-alt">
    <div class="container">
      <!-- Encabezado -->
      <div class="section-header text-center">
        <h2>Nuestra Propuesta</h2>
        <p class="section-subtitle">
          Ofrecemos servicios de alta calidad diseñados para complementar el aprendizaje diario y el bienestar emocional.
        </p>
      </div>

      <!-- Grilla de Beneficios -->
      <div class="benefits-grid">
        <div 
          v-for="(b, idx) in beneficios" 
          :key="idx" 
          class="benefit-card"
        >
          <!-- Icono flotante con fondo personalizado -->
          <div 
            class="benefit-icon-wrapper" 
            :style="{ backgroundColor: b.bgLight, color: b.badgeColor }"
          >
            {{ b.icono }}
          </div>
          
          <h3 class="benefit-card-title">{{ b.titulo }}</h3>
          <p class="benefit-card-desc">{{ b.descripcion }}</p>
        </div>
      </div>

      <!-- Banner de Infraestructura Premium -->
      <div class="infra-banner">
        <div class="infra-content">
          <span class="infra-badge">Entorno Seguro</span>
          <h3>Infraestructura diseñada para su seguridad y felicidad</h3>
          <p>
            Nuestras aulas son amplias, ventiladas e iluminadas de forma natural, con mobiliario ergonómico adaptado a cada edad. Contamos con áreas de juego al aire libre protegidas con piso amortiguante contra caídas y sistemas de seguridad integrales.
          </p>
          <div class="infra-points">
            <span class="point">✔️ Aulas Temáticas</span>
            <span class="point">✔️ Áreas Verdes Libres</span>
            <span class="point">✔️ Control de Accesos</span>
          </div>
        </div>
        <div class="infra-visual">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 500 400" class="infra-illustration">
            <rect x="0" y="0" width="500" height="400" rx="30" fill="var(--bg-primary)" />
            <!-- Casa/Colegio estilizado -->
            <path d="M120 300 H380 V180 L250 80 L120 180 Z" fill="var(--primary)" opacity="0.1" />
            <path d="M120 300 H380 V180 L250 80 L120 180 Z" stroke="var(--primary)" stroke-width="6" stroke-linejoin="round" fill="none" />
            <!-- Puerta y Ventanas -->
            <rect x="220" y="220" width="60" height="80" rx="4" fill="var(--accent)" />
            <circle cx="235" cy="260" r="4" fill="#FFFFFF" />
            <rect x="160" y="190" width="50" height="50" rx="6" fill="var(--secondary)" />
            <rect x="290" y="190" width="50" height="50" rx="6" fill="var(--secondary)" />
            <!-- Nubes y Arbolitos -->
            <circle cx="410" cy="300" r="30" fill="var(--primary)" opacity="0.2"/>
            <path d="M410 300 V340" stroke="var(--primary)" stroke-width="6"/>
            <circle cx="80" cy="100" r="20" fill="var(--secondary)" opacity="0.15" />
          </svg>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.section-header {
  margin-bottom: 4.5rem;
}

.benefits-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 2rem;
  margin-bottom: 6.5rem;
}

.benefit-card {
  background-color: var(--bg-secondary);
  border-radius: var(--radius-md);
  padding: 2.5rem 1.85rem;
  box-shadow: var(--shadow-sm);
  border: 1px solid rgba(42, 92, 67, 0.02);
  transition: var(--transition);
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.benefit-card:hover {
  transform: translateY(-8px);
  box-shadow: var(--shadow-lg);
  border-color: var(--primary-border);
}

.benefit-icon-wrapper {
  width: 3.5rem;
  height: 3.5rem;
  font-size: 1.75rem;
  border-radius: var(--radius-sm);
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 1.5rem;
  transition: var(--transition);
  box-shadow: var(--shadow-sm);
}

.benefit-card:hover .benefit-icon-wrapper {
  transform: scale(1.1) rotate(6deg);
}

.benefit-card-title {
  font-size: 1.35rem;
  color: var(--primary);
  margin-bottom: 0.85rem;
}

.benefit-card-title::after {
  display: none;
}

.benefit-card-desc {
  font-size: 0.95rem;
  line-height: 1.6;
}

/* Banner de Infraestructura */
.infra-banner {
  display: grid;
  grid-template-columns: 1.15fr 0.85fr;
  gap: 4rem;
  align-items: center;
  background-color: var(--bg-secondary);
  border-radius: var(--radius-lg);
  padding: 4rem;
  box-shadow: var(--shadow-md);
  border: 1px solid rgba(42, 92, 67, 0.03);
}

.infra-badge {
  display: inline-block;
  background-color: var(--primary-light);
  color: var(--primary);
  border: 1px solid var(--primary-border);
  font-family: var(--font-title);
  font-weight: 600;
  font-size: 0.9rem;
  padding: 0.35rem 1rem;
  border-radius: var(--radius-full);
  margin-bottom: 1.25rem;
}

.infra-content h3 {
  font-size: 2.25rem;
  margin-bottom: 1.25rem;
}

.infra-content p {
  font-size: 1.1rem;
  margin-bottom: 2rem;
}

.infra-points {
  display: flex;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.infra-points .point {
  font-family: var(--font-title);
  font-weight: 600;
  font-size: 1.05rem;
  color: var(--primary);
  background-color: var(--bg-primary);
  padding: 0.5rem 1.25rem;
  border-radius: var(--radius-sm);
  box-shadow: var(--shadow-sm);
}

.infra-visual {
  width: 100%;
}

.infra-illustration {
  width: 100%;
  height: auto;
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-sm);
  transition: var(--transition);
}

.infra-illustration:hover {
  transform: scale(1.02);
  box-shadow: var(--shadow-md);
}

/* Responsividad */
@media (max-width: 1200px) {
  .benefits-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 1.5rem;
  }
}

@media (max-width: 992px) {
  .infra-banner {
    grid-template-columns: 1fr;
    gap: 3rem;
    padding: 2.5rem;
  }
}

@media (max-width: 576px) {
  .benefits-grid {
    grid-template-columns: 1fr;
  }
  
  .benefit-card {
    padding: 2rem 1.5rem;
  }
  
  .infra-banner {
    padding: 2rem 1.5rem;
  }
  
  .infra-content h3 {
    font-size: 1.75rem;
  }
  
  .infra-points {
    flex-direction: column;
    gap: 0.75rem;
  }
}
</style>
