<script setup>
import { ref } from 'vue';

const form = ref({
  nombrePadre: '',
  correo: '',
  telefono: '',
  nombreEstudiante: '',
  nivelPostula: '',
  comentario: ''
});

const isSubmitting = ref(false);
const showSuccess = ref(false);
const errors = ref({});

const validateForm = () => {
  const tempErrors = {};
  if (!form.value.nombrePadre.trim()) tempErrors.nombrePadre = 'El nombre del padre es obligatorio.';
  if (!form.value.correo.trim()) {
    tempErrors.correo = 'El correo electrónico es obligatorio.';
  } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.value.correo)) {
    tempErrors.correo = 'El formato del correo electrónico no es válido.';
  }
  if (!form.value.telefono.trim()) {
    tempErrors.telefono = 'El teléfono es obligatorio.';
  } else if (!/^\+?[0-9\s-]{7,15}$/.test(form.value.telefono)) {
    tempErrors.telefono = 'El número de teléfono no es válido.';
  }
  if (!form.value.nombreEstudiante.trim()) tempErrors.nombreEstudiante = 'El nombre del estudiante es obligatorio.';
  if (!form.value.nivelPostula) tempErrors.nivelPostula = 'Debes seleccionar el nivel educativo.';

  errors.value = tempErrors;
  return Object.keys(tempErrors).length === 0;
};

const handleSubmit = () => {
  if (!validateForm()) return;
  
  isSubmitting.value = true;
  
  // Simular envío de API
  setTimeout(() => {
    isSubmitting.value = false;
    showSuccess.value = true;
    
    // Resetear formulario
    form.value = {
      nombrePadre: '',
      correo: '',
      telefono: '',
      nombreEstudiante: '',
      nivelPostula: '',
      comentario: ''
    };
    
    // Ocultar mensaje de éxito tras 5 segundos
    setTimeout(() => {
      showSuccess.value = false;
    }, 5000);
  }, 2000);
};
</script>

<template>
  <section id="admision" class="section">
    <div class="container admission-container">
      <!-- Info e Invitación -->
      <div class="admission-info">
        <span class="admission-badge">Proceso 2026</span>
        <h2>Inicia la postulación de tu hijo hoy</h2>
        <p class="admission-text">
          Queremos que conozcas nuestro proyecto educativo de cerca. Completa el formulario de contacto para reservar una vacante, programar una visita guiada o recibir atención personalizada de nuestro equipo de admisiones en Huancayo.
        </p>
        
        <div class="steps-list">
          <div class="step-item">
            <span class="step-num">1</span>
            <div>
              <strong>Registra tus datos:</strong> Completa este sencillo formulario en línea con información básica.
            </div>
          </div>
          <div class="step-item">
            <span class="step-num">2</span>
            <div>
              <strong>Contacto personalizado:</strong> Nuestro equipo te llamará o enviará un WhatsApp en menos de 24 horas hábiles.
            </div>
          </div>
          <div class="step-item">
            <span class="step-num">3</span>
            <div>
              <strong>Entrevista y Visita:</strong> Ven a conocer nuestras hermosas aulas y el huerto ecológico con tu pequeño.
            </div>
          </div>
        </div>
      </div>

      <!-- Formulario de Admisión -->
      <div class="admission-form-wrapper">
        <!-- Banner de éxito -->
        <transition name="fade">
          <div v-if="showSuccess" class="success-banner text-center">
            <div class="success-icon">🎉</div>
            <h3>¡Solicitud Recibida!</h3>
            <p>
              Muchas gracias por tu interés en **Lovely Garden**. Nuestro equipo de admisiones se comunicará contigo muy pronto.
            </p>
          </div>
        </transition>

        <form v-if="!showSuccess" @submit.prevent="handleSubmit" class="admission-form">
          <h3 class="form-title">Formulario de Contacto</h3>
          
          <!-- Padre/Apoderado -->
          <div class="form-group">
            <label for="nombrePadre">Nombre del Padre o Tutor</label>
            <input 
              type="text" 
              id="nombrePadre" 
              v-model="form.nombrePadre" 
              placeholder="Ej. Juan Pérez"
              :class="{ 'input-error': errors.nombrePadre }"
            />
            <span v-if="errors.nombrePadre" class="error-msg">{{ errors.nombrePadre }}</span>
          </div>

          <!-- Correo & Teléfono -->
          <div class="form-row">
            <div class="form-group">
              <label for="correo">Correo Electrónico</label>
              <input 
                type="email" 
                id="correo" 
                v-model="form.correo" 
                placeholder="ejemplo@correo.com"
                :class="{ 'input-error': errors.correo }"
              />
              <span v-if="errors.correo" class="error-msg">{{ errors.correo }}</span>
            </div>

            <div class="form-group">
              <label for="telefono">Teléfono / WhatsApp</label>
              <input 
                type="tel" 
                id="telefono" 
                v-model="form.telefono" 
                placeholder="Ej. 987654321"
                :class="{ 'input-error': errors.telefono }"
              />
              <span v-if="errors.telefono" class="error-msg">{{ errors.telefono }}</span>
            </div>
          </div>

          <!-- Estudiante & Nivel -->
          <div class="form-row">
            <div class="form-group">
              <label for="nombreEstudiante">Nombre del Estudiante</label>
              <input 
                type="text" 
                id="nombreEstudiante" 
                v-model="form.nombreEstudiante" 
                placeholder="Nombre completo"
                :class="{ 'input-error': errors.nombreEstudiante }"
              />
              <span v-if="errors.nombreEstudiante" class="error-msg">{{ errors.nombreEstudiante }}</span>
            </div>

            <div class="form-group">
              <label for="nivelPostula">Nivel al que Postula</label>
              <select 
                id="nivelPostula" 
                v-model="form.nivelPostula"
                :class="{ 'input-error': errors.nivelPostula }"
              >
                <option value="" disabled>Seleccione un nivel</option>
                <optgroup label="Nivel Inicial">
                  <option value="inicial-3">Inicial - 3 Años</option>
                  <option value="inicial-4">Inicial - 4 Años</option>
                  <option value="inicial-5">Inicial - 5 Años</option>
                </optgroup>
                <optgroup label="Nivel Primaria">
                  <option value="primaria-1">Primaria - 1° Grado</option>
                  <option value="primaria-2">Primaria - 2° Grado</option>
                  <option value="primaria-3">Primaria - 3° Grado</option>
                  <option value="primaria-4">Primaria - 4° Grado</option>
                  <option value="primaria-5">Primaria - 5° Grado</option>
                  <option value="primaria-6">Primaria - 6° Grado</option>
                </optgroup>
              </select>
              <span v-if="errors.nivelPostula" class="error-msg">{{ errors.nivelPostula }}</span>
            </div>
          </div>

          <!-- Comentario -->
          <div class="form-group">
            <label for="comentario">Mensaje o Consultas Adicionales</label>
            <textarea 
              id="comentario" 
              v-model="form.comentario" 
              rows="3" 
              placeholder="¿Tienes alguna consulta en especial?"
            ></textarea>
          </div>

          <button 
            type="submit" 
            class="btn btn-accent btn-full" 
            :disabled="isSubmitting"
          >
            <span v-if="isSubmitting" class="spinner"></span>
            <span v-else>Enviar Solicitud de Información</span>
          </button>
        </form>
      </div>
    </div>
  </section>
</template>

<style scoped>
.admission-container {
  display: grid;
  grid-template-columns: 1fr 1.1fr;
  gap: 5rem;
  align-items: center;
}

/* Info */
.admission-badge {
  display: inline-block;
  background-color: var(--accent-light);
  color: var(--accent);
  border: 1px solid rgba(231, 122, 109, 0.2);
  font-family: var(--font-title);
  font-weight: 700;
  font-size: 0.9rem;
  padding: 0.35rem 1rem;
  border-radius: var(--radius-full);
  margin-bottom: 1.25rem;
}

.admission-info h2 {
  font-size: 2.5rem;
  line-height: 1.2;
  margin-bottom: 1.5rem;
}

.admission-info h2::after {
  display: none;
}

.admission-text {
  font-size: 1.15rem;
  margin-bottom: 2.5rem;
}

.steps-list {
  display: flex;
  flex-direction: column;
  gap: 1.75rem;
}

.step-item {
  display: flex;
  gap: 1.25rem;
  align-items: flex-start;
}

.step-num {
  width: 2.5rem;
  height: 2.5rem;
  background-color: var(--primary);
  color: var(--bg-secondary);
  font-family: var(--font-title);
  font-weight: 700;
  font-size: 1.25rem;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  box-shadow: var(--shadow-sm);
}

.step-item strong {
  color: var(--text-dark);
}

.step-item div {
  font-size: 1.05rem;
  color: var(--text-light);
  line-height: 1.5;
}

/* Formulario Wrapper */
.admission-form-wrapper {
  background-color: var(--bg-secondary);
  border-radius: var(--radius-lg);
  padding: 3.5rem;
  box-shadow: var(--shadow-lg);
  border: 1px solid rgba(42, 92, 67, 0.04);
  position: relative;
  min-height: 480px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.form-title {
  font-size: 1.75rem;
  color: var(--primary);
  margin-bottom: 2rem;
  text-align: center;
}

.form-title::after {
  display: none;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
  width: 100%;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.5rem;
}

label {
  font-family: var(--font-title);
  font-weight: 600;
  font-size: 0.95rem;
  color: var(--text-dark);
}

input, select, textarea {
  width: 100%;
  padding: 0.85rem 1.25rem;
  border-radius: var(--radius-sm);
  border: 2px solid var(--border-color);
  background-color: var(--bg-primary);
  color: var(--text-dark);
  font-family: var(--font-body);
  font-size: 1rem;
  transition: var(--transition);
}

input:focus, select:focus, textarea:focus {
  border-color: var(--primary);
  background-color: var(--bg-secondary);
  box-shadow: var(--shadow-sm);
}

.input-error {
  border-color: var(--accent);
  background-color: rgba(231, 122, 109, 0.03);
}

.error-msg {
  color: var(--accent);
  font-size: 0.85rem;
  font-weight: 500;
  margin-top: 0.25rem;
}

.btn-full {
  width: 100%;
  margin-top: 1rem;
}

/* Spinner de carga */
.spinner {
  width: 1.5rem;
  height: 1.5rem;
  border: 3px solid rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  border-top-color: #FFFFFF;
  animation: spin 1s ease-in-out infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

/* Banner de éxito */
.success-banner {
  animation: bounceIn 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.success-icon {
  font-size: 4rem;
  margin-bottom: 1.5rem;
}

.success-banner h3 {
  font-size: 2rem;
  margin-bottom: 1rem;
  color: var(--primary);
}

.success-banner h3::after {
  display: none;
}

.success-banner p {
  font-size: 1.15rem;
  line-height: 1.6;
}

@keyframes bounceIn {
  from { opacity: 0; transform: scale(0.8); }
  to { opacity: 1; transform: scale(1); }
}

/* Transición simple */
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}

/* Responsividad */
@media (max-width: 992px) {
  .admission-container {
    grid-template-columns: 1fr;
    gap: 4rem;
  }
  
  .admission-form-wrapper {
    padding: 2.5rem;
  }
}

@media (max-width: 576px) {
  .admission-form-wrapper {
    padding: 2rem 1.5rem;
  }
  
  .form-row {
    grid-template-columns: 1fr;
    gap: 0;
  }
  
  .admission-info h2 {
    font-size: 2rem;
  }
}
</style>
