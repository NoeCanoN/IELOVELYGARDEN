<script setup>
</script>

<template>
  <footer class="footer-section">
    <div class="container footer-grid">
      <!-- Columna 1: Info e Identidad -->
      <div class="footer-brand">
        <a href="#inicio" class="logo">
          <div class="logo-image-container">
            <img src="/logo.webp" alt="Logo de Lovely Garden" class="logo-img" />
          </div>
          <span class="logo-text">Lovely <span class="logo-highlight">Garden</span></span>
        </a>
        <p class="brand-desc">
          Somos una institución educativa comprometida con la formación integral y en valores de nuestros estudiantes, promoviendo un ambiente lúdico, seguro y feliz en Huancayo.
        </p>
        
        <!-- Redes Sociales -->
        <div class="social-links">
          <!-- Facebook real del colegio -->
          <a href="https://www.facebook.com/profile.php?id=100057331814792" target="_blank" aria-label="Facebook de Lovely Garden">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="social-icon">
              <path d="M22 12c0-5.52-4.48-10-10-10S2 6.48 2 12c0 4.84 3.44 8.87 8 9.8V15H8v-3h2V9.5C10 7.57 11.57 6 13.5 6H16v3h-2c-.55 0-1 .45-1 1v2h3v3h-3v6.95c4.56-.93 8-4.96 8-9.75z"/>
            </svg>
          </a>
          <!-- Instagram simulado -->
          <a href="#" aria-label="Instagram de Lovely Garden">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="social-icon">
              <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.051.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 1 0 0 12.324 6.162 6.162 0 0 0 0-12.324zM12 16a4 4 0 1 1 0-8 4 4 0 0 1 0 8zm6.406-11.845a1.44 1.44 0 1 0 0 2.881 1.44 1.44 0 0 0 0-2.881z"/>
            </svg>
          </a>
        </div>
      </div>

      <!-- Columna 2: Enlaces Rápidos -->
      <div class="footer-links">
        <h4>Enlaces Rápidos</h4>
        <ul>
          <li><a href="#inicio">Inicio</a></li>
          <li><a href="#nosotros">Nosotros</a></li>
          <li><a href="#niveles">Niveles Educativos</a></li>
          <li><a href="#beneficios">Propuesta & Beneficios</a></li>
          <li><a href="#galeria">Galería</a></li>
          <li><a href="#admision">Admisión 2026</a></li>
        </ul>
      </div>

      <!-- Columna 3: Niveles -->
      <div class="footer-links">
        <h4>Niveles</h4>
        <ul>
          <li><a href="#niveles">Nivel Inicial (3-5 años)</a></li>
          <li><a href="#niveles">Nivel Primaria (1°-6° grado)</a></li>
          <li><a href="#beneficios">Talleres Creativos</a></li>
          <li><a href="#beneficios">Huerto Ecológico</a></li>
          <li><a href="#beneficios">Apoyo Psicopedagógico</a></li>
        </ul>
      </div>

      <!-- Columna 4: Contacto Real -->
      <div class="footer-contact">
        <h4>Contacto</h4>
        <ul>
          <li class="contact-item">
            <span class="icon">📍</span>
            <span>Calle Los Laureles Mz N Lote 7 - 8 Alto La Merced San Carlos, Huancayo</span>
          </li>
          <li class="contact-item">
            <span class="icon">📞</span>
            <span>+51 981 806 113</span>
          </li>
          <li class="contact-item">
            <span class="icon">✉️</span>
            <span>lovelygardenie@gmail.com</span>
          </li>
          <li class="contact-item">
            <span class="icon">🕒</span>
            <span>Lun a Vie: 8:00 AM - 2:00 PM</span>
          </li>
        </ul>
      </div>
    </div>

    <!-- Copyright -->
    <div class="footer-bottom">
      <div class="container bottom-container">
        <p>&copy; 2026 Lovely Garden. Todos los derechos reservados. Diseñado con amor en Huancayo.</p>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer-section {
  background-color: var(--text-dark);
  color: var(--bg-primary);
  padding: 5rem 0 0;
  border-top: 5px solid var(--primary);
  font-family: var(--font-body);
}

.footer-grid {
  display: grid;
  grid-template-columns: 1.3fr 0.8fr 0.8fr 1.1fr;
  gap: 3.5rem;
  padding-bottom: 4rem;
}

/* Marca */
.footer-brand {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.logo {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.logo-image-container {
  width: 2.5rem;
  height: 2.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  background-color: #FFFFFF;
  padding: 0.15rem;
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
  font-size: 1.5rem;
  color: var(--bg-secondary);
}

.logo-highlight {
  color: var(--primary);
}

.brand-desc {
  color: var(--text-muted);
  font-size: 0.95rem;
  line-height: 1.6;
}

.social-links {
  display: flex;
  gap: 1rem;
}

.social-links a {
  width: 2.5rem;
  height: 2.5rem;
  background-color: rgba(253, 251, 247, 0.08);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: var(--transition);
  color: var(--bg-secondary);
}

.social-links a:hover {
  background-color: var(--secondary);
  transform: translateY(-3px);
}

.social-icon {
  width: 1.25rem;
  height: 1.25rem;
}

/* Enlaces */
.footer-links h4,
.footer-contact h4 {
  font-family: var(--font-title);
  font-size: 1.2rem;
  font-weight: 700;
  color: var(--bg-secondary);
  margin-bottom: 1.5rem;
  position: relative;
}

.footer-links h4::after,
.footer-contact h4::after {
  content: '';
  position: absolute;
  bottom: -6px;
  left: 0;
  width: 35px;
  height: 3px;
  background-color: var(--secondary);
  border-radius: var(--radius-full);
}

.footer-links ul,
.footer-contact ul {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.85rem;
}

.footer-links a {
  color: var(--text-muted);
  font-size: 0.95rem;
  transition: var(--transition);
}

.footer-links a:hover {
  color: var(--secondary);
  padding-left: 5px;
}

/* Contacto */
.contact-item {
  display: flex;
  gap: 0.75rem;
  align-items: flex-start;
  color: var(--text-muted);
  font-size: 0.95rem;
  line-height: 1.4;
}

.contact-item .icon {
  font-size: 1.15rem;
  line-height: 1;
}

/* Bottom Copyright */
.footer-bottom {
  border-top: 1px solid rgba(253, 251, 247, 0.08);
  padding: 1.75rem 0;
  text-align: center;
  font-size: 0.9rem;
  color: var(--text-muted);
}

/* Responsividad */
@media (max-width: 992px) {
  .footer-grid {
    grid-template-columns: 1fr 1fr;
    gap: 3rem;
  }
}

@media (max-width: 576px) {
  .footer-grid {
    grid-template-columns: 1fr;
    gap: 2.5rem;
  }
  
  .footer-brand {
    align-items: center;
    text-align: center;
  }
  
  .social-links {
    justify-content: center;
  }
  
  .footer-links h4::after,
  .footer-contact h4::after {
    left: 50%;
    transform: translateX(-50%);
  }
  
  .footer-links, .footer-contact {
    text-align: center;
  }
  
  .contact-item {
    justify-content: center;
  }
}
</style>
