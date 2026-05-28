<script setup>
import { ref } from 'vue';

const activeTab = ref('inicial'); // inicial o primaria

const changeTab = (tab) => {
  activeTab.value = tab;
};
</script>

<template>
  <section id="niveles" class="section">
    <div class="container">
      <!-- Encabezado -->
      <div class="section-header text-center">
        <h2>Niveles Educativos</h2>
        <p class="section-subtitle">
          Diseñamos programas de aprendizaje divertidos y significativos según la etapa de crecimiento de tu hijo.
        </p>
      </div>

      <!-- Pestañas de Alternancia -->
      <div class="tabs-container">
        <button 
          :class="['tab-btn', { 'tab-active': activeTab === 'inicial' }]" 
          @click="changeTab('inicial')"
        >
          🎨 Nivel Inicial
        </button>
        <button 
          :class="['tab-btn', { 'tab-active': activeTab === 'primaria' }]" 
          @click="changeTab('primaria')"
        >
          📚 Nivel Primaria
        </button>
      </div>

      <!-- Contenido de las Pestañas con Transiciones -->
      <div class="tab-content">
        <transition name="tab-fade" mode="out-in">
          <!-- NIVEL INICIAL -->
          <div v-if="activeTab === 'inicial'" key="inicial" class="program-grid">
            <div class="program-info">
              <span class="program-age-badge">3 a 5 Años</span>
              <h3>Nivel Inicial: Exploración y Juego</h3>
              <p class="program-intro">
                Nuestra metodología en el nivel inicial se basa en el **juego heurístico**, el aprendizaje socioemocional y la estimulación multisensorial. Creamos un ambiente acogedor donde jugar es aprender.
              </p>
              
              <ul class="program-features">
                <li>
                  <span class="feature-icon">✨</span>
                  <div>
                    <strong>Desarrollo Psicomotriz:</strong> Sesiones diarias de psicomotricidad gruesa y fina para una coordinación excelente.
                  </div>
                </li>
                <li>
                  <span class="feature-icon">🌿</span>
                  <div>
                    <strong>Contacto con la Naturaleza:</strong> Actividades guiadas en nuestro huerto escolar para despertar el sentido de pertenencia y cuidado.
                  </div>
                </li>
                <li>
                  <span class="feature-icon">🗣️</span>
                  <div>
                    <strong>Estimulación del Lenguaje:</strong> Talleres de cuenta-cuentos, cantos y títeres para potenciar su expresión verbal y emocional.
                  </div>
                </li>
                <li>
                  <span class="feature-icon">❤️</span>
                  <div>
                    <strong>Educación en Valores:</strong> Aprenden a compartir, colaborar y expresar su empatía mediante rutinas positivas.
                  </div>
                </li>
              </ul>
              <a href="#admision" class="btn btn-accent">Solicitar Admisión Inicial</a>
            </div>

            <!-- Visual representativa del nivel inicial -->
            <div class="program-visual">
              <div class="visual-wrapper-box box-inicial">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 400 400" class="sub-illustration">
                  <rect x="0" y="0" width="400" height="400" rx="30" fill="var(--accent-light)"/>
                  <!-- Dibujos infantiles estilizados -->
                  <circle cx="200" cy="200" r="100" fill="var(--accent)" opacity="0.2"/>
                  <!-- Mariposa y Flor -->
                  <path d="M150 250 Q160 220 180 250 T210 250" stroke="var(--primary)" stroke-width="4" fill="none"/>
                  <circle cx="150" cy="250" r="10" fill="var(--secondary)"/>
                  <circle cx="210" cy="250" r="10" fill="var(--secondary)"/>
                  <circle cx="180" cy="235" r="12" fill="var(--accent)"/>
                  <line x1="180" y1="247" x2="180" y2="320" stroke="var(--primary)" stroke-width="6" stroke-linecap="round"/>
                  <!-- Solcito feliz -->
                  <circle cx="300" cy="100" r="30" fill="var(--secondary)"/>
                  <path d="M285 105 Q300 115 315 105" stroke="var(--text-dark)" stroke-width="3" fill="none"/>
                  <circle cx="292" cy="95" r="3" fill="var(--text-dark)"/>
                  <circle cx="308" cy="95" r="3" fill="var(--text-dark)"/>
                  <!-- Texto flotante -->
                  <text x="70" y="120" font-family="var(--font-title)" font-size="28" font-weight="bold" fill="var(--primary)">ExpresArte</text>
                  <text x="210" y="350" font-family="var(--font-title)" font-size="24" font-weight="bold" fill="var(--accent)">Jugar</text>
                </svg>
              </div>
            </div>
          </div>

          <!-- NIVEL PRIMARIA -->
          <div v-else-if="activeTab === 'primaria'" key="primaria" class="program-grid">
            <div class="program-info">
              <span class="program-age-badge">6 a 12 Años</span>
              <h3>Nivel Primaria: Pensamiento Crítico</h3>
              <p class="program-intro">
                En el nivel primaria potenciamos el **pensamiento lógico-matemático**, la comprensión lectora reflexiva y el aprendizaje colaborativo. Formamos estudiantes analíticos con capacidad para resolver retos de la vida diaria.
              </p>
              
              <ul class="program-features">
                <li>
                  <span class="feature-icon">🔍</span>
                  <div>
                    <strong>Indagación Científica:</strong> Proyectos vivenciales donde experimentan, prueban hipótesis y descubren la ciencia de forma práctica.
                  </div>
                </li>
                <li>
                  <span class="feature-icon">🇬🇧</span>
                  <div>
                    <strong>Inglés Dinámico:</strong> Clases comunicativas de inglés para sentar las bases de una comunicación global exitosa.
                  </div>
                </li>
                <li>
                  <span class="feature-icon">💻</span>
                  <div>
                    <strong>Tecnología Responsable:</strong> Talleres de robótica y pensamiento computacional adaptados a sus edades para un uso ético del mundo digital.
                  </div>
                </li>
                <li>
                  <span class="feature-icon">🧘</span>
                  <div>
                    <strong>Habilidades Blandas:</strong> Actividades de debate, liderazgo y talleres psicopedagógicos para fortalecer su autoestima.
                  </div>
                </li>
              </ul>
              <a href="#admision" class="btn btn-primary">Solicitar Admisión Primaria</a>
            </div>

            <!-- Visual representativa del nivel primaria -->
            <div class="program-visual">
              <div class="visual-wrapper-box box-primaria">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 400 400" class="sub-illustration">
                  <rect x="0" y="0" width="400" height="400" rx="30" fill="var(--primary-light)"/>
                  <!-- Dibujos interactivos de primaria -->
                  <circle cx="200" cy="200" r="100" fill="var(--primary)" opacity="0.2"/>
                  <!-- Matraz de ciencia -->
                  <path d="M170 120 H230 M185 120 V180 L140 280 H260 L215 180 V120" stroke="var(--primary)" stroke-width="6" stroke-linecap="round" fill="none"/>
                  <path d="M158 240 Q200 220 242 240 L250 260 H150 Z" fill="var(--secondary)" opacity="0.7"/>
                  <circle cx="180" cy="200" r="6" fill="var(--accent)"/>
                  <circle cx="210" cy="170" r="8" fill="var(--accent)"/>
                  <!-- Regla y Lápiz cruzados -->
                  <path d="M80 320 L130 270" stroke="var(--primary)" stroke-width="12" stroke-linecap="round"/>
                  <!-- Fórmulas flotantes -->
                  <text x="60" y="80" font-family="var(--font-title)" font-size="28" font-weight="bold" fill="var(--accent)">E = mc²</text>
                  <text x="250" y="340" font-family="var(--font-title)" font-size="32" font-weight="bold" fill="var(--secondary)">1 + 1 = 3?</text>
                </svg>
              </div>
            </div>
          </div>
        </transition>
      </div>
    </div>
  </section>
</template>

<style scoped>
.section-header {
  margin-bottom: 3.5rem;
}

.tabs-container {
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  margin-bottom: 4rem;
}

.tab-btn {
  padding: 1rem 2.25rem;
  font-family: var(--font-title);
  font-weight: 700;
  font-size: 1.25rem;
  border-radius: var(--radius-full);
  cursor: pointer;
  background-color: var(--bg-secondary);
  color: var(--primary);
  border: 2px solid var(--primary-border);
  box-shadow: var(--shadow-sm);
  transition: var(--transition);
}

.tab-btn:hover {
  transform: translateY(-2px);
  border-color: var(--primary);
  box-shadow: var(--shadow-md);
}

.tab-active {
  background-color: var(--primary);
  color: var(--bg-secondary);
  border-color: var(--primary);
  box-shadow: 0 8px 16px rgba(42, 92, 67, 0.25);
}

.tab-btn:first-child.tab-active {
  background-color: var(--accent);
  border-color: var(--accent);
  box-shadow: var(--shadow-accent);
}

/* Grilla de Contenido de los Programas */
.program-grid {
  display: grid;
  grid-template-columns: 1.2fr 0.8fr;
  gap: 4.5rem;
  align-items: center;
  background-color: var(--bg-secondary);
  border-radius: var(--radius-lg);
  padding: 3.5rem;
  box-shadow: var(--shadow-md);
  border: 1px solid rgba(42, 92, 67, 0.03);
}

.program-age-badge {
  display: inline-block;
  background-color: var(--secondary-light);
  color: var(--secondary-hover);
  font-family: var(--font-title);
  font-weight: 700;
  padding: 0.4rem 1rem;
  border-radius: var(--radius-sm);
  font-size: 0.95rem;
  margin-bottom: 1.25rem;
}

.program-info h3 {
  font-size: 2.25rem;
  margin-bottom: 1.25rem;
}

.program-intro {
  font-size: 1.15rem;
  line-height: 1.6;
  margin-bottom: 2rem;
}

.program-features {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  margin-bottom: 2.5rem;
}

.program-features li {
  display: flex;
  gap: 1rem;
  align-items: flex-start;
}

.feature-icon {
  font-size: 1.5rem;
  line-height: 1;
  background-color: var(--bg-primary);
  width: 2.5rem;
  height: 2.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  flex-shrink: 0;
  box-shadow: var(--shadow-sm);
}

.program-features li p {
  font-size: 1.05rem;
  color: var(--text-light);
}

.program-features li strong {
  color: var(--text-dark);
}

.program-visual {
  width: 100%;
}

.visual-wrapper-box {
  width: 100%;
  max-width: 320px;
  margin: 0 auto;
  aspect-ratio: 1;
  border-radius: var(--radius-md);
  overflow: hidden;
  box-shadow: var(--shadow-md);
  transition: var(--transition);
}

.visual-wrapper-box:hover {
  transform: scale(1.03) rotate(2deg);
  box-shadow: var(--shadow-lg);
}

.sub-illustration {
  width: 100%;
  height: auto;
}

/* Transición de las pestañas */
.tab-fade-enter-active,
.tab-fade-leave-active {
  transition: opacity 0.35s ease, transform 0.35s ease;
}

.tab-fade-enter-from {
  opacity: 0;
  transform: translateY(15px);
}

.tab-fade-leave-to {
  opacity: 0;
  transform: translateY(-15px);
}

/* Responsividad */
@media (max-width: 992px) {
  .program-grid {
    grid-template-columns: 1fr;
    gap: 3rem;
    padding: 2.5rem;
  }
  
  .visual-wrapper-box {
    max-width: 280px;
  }
}

@media (max-width: 576px) {
  .tabs-container {
    flex-direction: column;
    gap: 0.75rem;
    align-items: stretch;
  }
  
  .tab-btn {
    text-align: center;
  }
  
  .program-grid {
    padding: 2rem 1.5rem;
  }
  
  .program-info h3 {
    font-size: 1.75rem;
  }
}
</style>
