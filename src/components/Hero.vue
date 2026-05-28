<script setup>
</script>

<template>
  <section id="inicio" class="hero-section">
    <div class="container hero-grid">
      <!-- Texto -->
      <div class="hero-content">
        <span class="hero-badge">Inscripciones Abiertas 2026</span>
        <h1 class="hero-title">
          Un lugar mágico para <span class="highlight-text">crecer</span> y aprender feliz
        </h1>
        <p class="hero-quote">
          ✨ “La educación inicial siembra amor, alegría y los primeros sueños de cada niño.” 💛
        </p>
        <p class="hero-description">
          En <strong>Lovely Garden</strong> en Huancayo, brindamos una educación integral comprometida con el desarrollo de los talentos únicos de cada niño en sus etapas de Inicial y Primaria.
        </p>
        <div class="hero-actions">
          <a href="#admision" class="btn btn-accent">Postular Ahora</a>
          <a href="#nosotros" class="btn btn-outline">Conocer Más</a>
        </div>
      </div>

      <!-- Imagen Real de la Institución con Diseño Premium -->
      <div class="hero-visual">
        <div class="blob-wrapper">
          <!-- Blobs decorativos de fondo basados en la paleta extraída -->
          <div class="visual-blob blob-yellow"></div>
          <div class="visual-blob blob-coral"></div>
          
          <!-- Contenedor de la foto real del colegio con diseño estilo glassmorphism -->
          <div class="visual-card">
            <div class="real-image-frame">
              <!-- Usando la foto real c:\Users\ADMIN\Desktop\App\IEInicialPrimaria\public\institucionales.jpg -->
              <img src="/institucionales.jpg" alt="Estudiantes en Lovely Garden" class="hero-real-img" />
              <!-- Detalles flotantes lúdicos -->
              <div class="floating-badge text-badge">
                👶 Inicial y Primaria
              </div>
              <div class="floating-badge star-badge">
                ⭐ Educación con Valores
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Onda decorativa inferior para conectar con Nosotros -->
    <div class="hero-wave">
      <svg data-name="Layer 1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1200 120" preserveAspectRatio="none">
        <path d="M985.66,92.83C906.67,72,823.78,31,743.84,14.19c-82.26-17.34-168.06-16.33-250.45.39-57.84,11.73-114,31.07-172,41.86A600.21,600.21,0,0,1,0,27.35V120H1200V95.8C1132.19,118.92,1055.71,111.31,985.66,92.83Z" fill="#FFFFFF"></path>
      </svg>
    </div>
  </section>
</template>

<style scoped>
.hero-section {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding-top: 9rem;
  padding-bottom: 8rem;
  background-color: var(--bg-primary);
  overflow: hidden;
}

.hero-grid {
  display: grid;
  grid-template-columns: 1.15fr 0.85fr;
  align-items: center;
  gap: 4rem;
  z-index: 10;
}

/* Textos */
.hero-badge {
  display: inline-block;
  background-color: var(--primary-light);
  color: var(--primary-hover);
  border: 1px solid var(--primary-border);
  padding: 0.5rem 1.25rem;
  border-radius: var(--radius-full);
  font-family: var(--font-title);
  font-weight: 700;
  font-size: 0.95rem;
  margin-bottom: 1.5rem;
  animation: floatBadge 3s ease-in-out infinite;
}

.hero-title {
  font-size: 3.6rem;
  line-height: 1.15;
  color: var(--text-dark);
  margin-bottom: 1.25rem;
}

.hero-title::after {
  display: none;
}

.highlight-text {
  color: var(--secondary);
  position: relative;
  display: inline-block;
}

.highlight-text::after {
  content: '';
  position: absolute;
  bottom: 4px;
  left: 0;
  width: 100%;
  height: 8px;
  background-color: rgba(255, 111, 67, 0.15);
  z-index: -1;
  border-radius: var(--radius-full);
}

.hero-quote {
  font-family: var(--font-title);
  font-size: 1.25rem;
  font-weight: 600;
  color: var(--secondary-hover);
  border-left: 4px solid var(--primary);
  padding-left: 1.25rem;
  margin-bottom: 1.5rem;
  line-height: 1.5;
  max-width: 95%;
}

.hero-description {
  font-size: 1.15rem;
  color: var(--text-light);
  margin-bottom: 2.5rem;
  max-width: 90%;
}

.hero-actions {
  display: flex;
  gap: 1.25rem;
}

/* Visual e Imagen Real */
.hero-visual {
  position: relative;
  width: 100%;
  display: flex;
  justify-content: center;
}

.blob-wrapper {
  position: relative;
  width: 100%;
  max-width: 440px;
  aspect-ratio: 1.05;
}

.visual-blob {
  position: absolute;
  border-radius: 50%;
  filter: blur(40px);
  opacity: 0.45;
  z-index: 1;
}

.blob-yellow {
  width: 260px;
  height: 260px;
  background-color: var(--primary);
  top: -20px;
  right: -20px;
  animation: blobMove 12s ease-in-out infinite alternate;
}

.blob-coral {
  width: 290px;
  height: 290px;
  background-color: var(--secondary);
  bottom: -30px;
  left: -20px;
  animation: blobMove 8s ease-in-out infinite alternate-reverse;
}

.visual-card {
  position: relative;
  z-index: 2;
  width: 100%;
  height: 100%;
  background-color: var(--bg-secondary);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-lg);
  border: 1px solid rgba(255, 167, 38, 0.08);
  padding: 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  transition: var(--transition);
}

.visual-card:hover {
  transform: translateY(-5px) rotate(1deg);
  box-shadow: 0 30px 60px rgba(30, 41, 59, 0.15);
}

.real-image-frame {
  position: relative;
  width: 100%;
  height: 100%;
  border-radius: var(--radius-md);
  overflow: hidden;
  aspect-ratio: 1;
}

.hero-real-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.8s ease;
}

.visual-card:hover .hero-real-img {
  transform: scale(1.05);
}

/* Flotantes */
.floating-badge {
  position: absolute;
  background-color: var(--bg-secondary);
  color: var(--text-dark);
  font-family: var(--font-title);
  font-weight: 700;
  padding: 0.6rem 1.25rem;
  border-radius: var(--radius-sm);
  box-shadow: var(--shadow-md);
  z-index: 5;
  font-size: 0.9rem;
  border: 1px solid rgba(255, 167, 38, 0.1);
  animation: floatElement 4s ease-in-out infinite;
}

.text-badge {
  top: 1.5rem;
  left: 1.5rem;
  border-left: 4px solid var(--accent);
}

.star-badge {
  bottom: 2rem;
  right: 1.5rem;
  border-left: 4px solid var(--secondary);
  animation-delay: -2s;
}

/* Ondas */
.hero-wave {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  line-height: 0;
  transform: rotate(180deg);
}

.hero-wave svg {
  position: relative;
  display: block;
  width: calc(100% + 1.3px);
  height: 80px;
}

/* ANIMACIONES */
@keyframes floatBadge {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-6px); }
}

@keyframes floatElement {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-8px); }
}

@keyframes blobMove {
  0% { transform: translate(0, 0) scale(1); }
  100% { transform: translate(25px, 20px) scale(1.08); }
}

/* Responsividad */
@media (max-width: 992px) {
  .hero-section {
    padding-top: 8rem;
    padding-bottom: 5rem;
    text-align: center;
  }
  
  .hero-grid {
    grid-template-columns: 1fr;
    gap: 3.5rem;
  }
  
  .hero-quote {
    margin-left: auto;
    margin-right: auto;
    text-align: left;
    max-width: 100%;
  }
  
  .hero-description {
    margin-left: auto;
    margin-right: auto;
    max-width: 100%;
  }
  
  .hero-actions {
    justify-content: center;
  }
  
  .blob-wrapper {
    max-width: 340px;
  }
}

@media (max-width: 576px) {
  .hero-title {
    font-size: 2.6rem;
  }
  
  .hero-actions {
    flex-direction: column;
    gap: 1rem;
  }
}
</style>
