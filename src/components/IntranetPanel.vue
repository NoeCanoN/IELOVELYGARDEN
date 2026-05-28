<script setup>
import { ref, computed } from 'vue';

// --- ESTADO GLOBAL SIMULADO DE LA INTRANET ---
// 1. Datos de Admisiones (Dirección)
const admisiones = ref([
  { id: 1, nombre: 'Luciana Belén Rivas', edad: '4 años', nivel: 'Inicial (4 años)', fecha: '28/05/2026', estado: 'Pendiente' },
  { id: 2, nombre: 'Mateo Sebastián Guerrero', edad: '6 años', nivel: 'Primaria (1er Grado)', fecha: '27/05/2026', estado: 'Pendiente' },
  { id: 3, nombre: 'Emma Sofía Castrejón', edad: '3 años', nivel: 'Inicial (3 años)', fecha: '25/05/2026', estado: 'Aprobado' },
  { id: 4, nombre: 'Juan Diego Portilla', edad: '8 años', nivel: 'Primaria (3er Grado)', fecha: '24/05/2026', estado: 'Rechazado' }
]);

// 2. Personal Docente (Dirección)
const profesores = ref([
  { id: 1, nombre: 'Miss Karito Torres', especialidad: 'Tutora de Inicial 3 Años', estado: 'Activo', email: 'k.torres@lovely.edu.pe' },
  { id: 2, nombre: 'Miss Brenda Aguilar', especialidad: 'Tutora de Inicial 5 Años', estado: 'Activo', email: 'b.aguilar@lovely.edu.pe' },
  { id: 3, nombre: 'Prof. Carlos Mendoza', especialidad: 'Educación Física (Primaria)', estado: 'Activo', email: 'c.mendoza@lovely.edu.pe' },
  { id: 4, nombre: 'Miss Sofía Peralta', especialidad: 'Inglés e Innovación', estado: 'Licencia', email: 's.peralta@lovely.edu.pe' }
]);

// 3. Notas y Estudiantes (Profesores)
// Para Inicial usamos escala conceptual (AD, A, B, C) y para Primaria escala numérica (0-20)
const estudiantesInicial = ref([
  { id: 101, nombre: 'Liam Anderson Ruiz', notas: { taller: 'A', participacion: 'AD', proyecto: 'A' } },
  { id: 102, nombre: 'Catalina Paz Díaz', notas: { taller: 'B', participacion: 'A', proyecto: 'B' } },
  { id: 103, nombre: 'Benjamín Morales', notas: { taller: 'AD', participacion: 'AD', proyecto: 'A' } }
]);

const estudiantesPrimaria = ref([
  { id: 201, nombre: 'Mateo Sebastián Guerrero', notas: { matematica: 16, comunicacion: 18, ingles: 14 } },
  { id: 202, nombre: 'Valeria Alexandra Flores', notas: { matematica: 12, comunicacion: 15, ingles: 17 } },
  { id: 203, nombre: 'Santiago Nicolás Castro', notas: { matematica: 10, comunicacion: 11, ingles: 12 } }
]);

// 4. Exámenes Programados (Se comparte con padres)
const examenes = ref([
  { id: 1, grado: 'Primaria (1er Grado)', curso: 'Matemática', tema: 'Sumas y Restas llevando', fecha: '2026-06-03', diasRestantes: 6 },
  { id: 2, grado: 'Primaria (1er Grado)', curso: 'Comunicación', tema: 'Comprensión Lectora - Cuentos Infantiles', fecha: '2026-06-05', diasRestantes: 8 },
  { id: 3, grado: 'Inicial (5 años)', curso: 'Psicomotricidad', tema: 'Coordinación y Equilibrio Dinámico', fecha: '2026-06-02', diasRestantes: 5 }
]);

// 5. Pensiones y Pagos (Padres)
const pensiones = ref([
  { mes: 'Marzo', monto: 450, vencimiento: '31/03/2026', estado: 'Pagado', transaccion: 'TRX-94830' },
  { mes: 'Abril', monto: 450, vencimiento: '30/04/2026', estado: 'Pagado', transaccion: 'TRX-10293' },
  { mes: 'Mayo', monto: 450, vencimiento: '31/05/2026', estado: 'Pendiente', transaccion: null },
  { mes: 'Junio', monto: 450, vencimiento: '30/06/2026', estado: 'Pendiente', transaccion: null },
  { mes: 'Julio', monto: 450, vencimiento: '31/07/2026', estado: 'Pendiente', transaccion: null },
  { mes: 'Agosto', monto: 450, vencimiento: '31/08/2026', estado: 'Pendiente', transaccion: null },
  { mes: 'Septiembre', monto: 450, vencimiento: '30/09/2026', estado: 'Pendiente', transaccion: null },
  { mes: 'Octubre', monto: 450, vencimiento: '31/10/2026', estado: 'Pendiente', transaccion: null },
  { mes: 'Noviembre', monto: 450, vencimiento: '30/11/2026', estado: 'Pendiente', transaccion: null },
  { mes: 'Diciembre', monto: 450, vencimiento: '20/12/2026', estado: 'Pendiente', transaccion: null }
]);

// --- ESTADOS INTERACTIVOS LOCALES ---
const activeRole = ref('padres'); // 'direccion', 'profesores', 'padres'
const padreTab = ref('notas'); // 'notas', 'examenes', 'pagos'

// Dirección interactivo
const totalIngresos = computed(() => {
  const pagadas = pensiones.value.filter(p => p.estado === 'Pagado').length;
  // Supongamos que hay 80 alumnos pagando este monto simuladamente
  return pagadas * 450 * 80;
});

const aprobarAdmision = (id) => {
  const idx = admisiones.value.findIndex(a => a.id === id);
  if (idx !== -1) admisiones.value[idx].estado = 'Aprobado';
};

const rechazarAdmision = (id) => {
  const idx = admisiones.value.findIndex(a => a.id === id);
  if (idx !== -1) admisiones.value[idx].estado = 'Rechazado';
};

// Profesores interactivo
const profGrado = ref('primaria'); // 'inicial', 'primaria'
const nuevoExamenCurso = ref('Matemática');
const nuevoExamenTema = ref('');
const nuevoExamenFecha = ref('');

const agregarExamen = () => {
  if (!nuevoExamenTema.value || !nuevoExamenFecha.value) return;
  
  // Calcular días restantes de forma simulada
  const hoy = new Date();
  const examFecha = new Date(nuevoExamenFecha.value);
  const diffTime = Math.abs(examFecha - hoy);
  const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));

  examenes.value.push({
    id: Date.now(),
    grado: profGrado.value === 'inicial' ? 'Inicial (5 años)' : 'Primaria (1er Grado)',
    curso: nuevoExamenCurso.value,
    tema: nuevoExamenTema.value,
    fecha: nuevoExamenFecha.value,
    diasRestantes: diffDays
  });

  nuevoExamenTema.value = '';
  nuevoExamenFecha.value = '';
};

// Calificaciones calculadas
const calcularPromedioPrimaria = (notasObj) => {
  const suma = notasObj.matematica + notasObj.comunicacion + notasObj.ingles;
  return (suma / 3).toFixed(1);
};

const equivalenciaConcepto = (nota) => {
  if (nota === 'AD') return { texto: 'Logro Destacado', clase: 'nota-ad' };
  if (nota === 'A') return { texto: 'Logro Esperado', clase: 'nota-a' };
  if (nota === 'B') return { texto: 'En Proceso', clase: 'nota-b' };
  return { texto: 'En Inicio', clase: 'nota-c' };
};

// Padres e Hijos interactivo
const hijoSeleccionado = ref('Mateo'); // 'Mateo', 'Catalina'

// Modal de pago interactivo
const showPayModal = ref(false);
const selectedMesPago = ref(null);
const cardName = ref('');
const cardNumber = ref('');
const cardExpiry = ref('');
const cardCVV = ref('');
const isProcessingPayment = ref(false);
const paymentSuccess = ref(false);

const openPayment = (mes) => {
  selectedMesPago.value = mes;
  cardName.value = '';
  cardNumber.value = '';
  cardExpiry.value = '';
  cardCVV.value = '';
  paymentSuccess.value = false;
  showPayModal.value = true;
};

const processPayment = () => {
  if (!cardName.value || !cardNumber.value || !cardExpiry.value || !cardCVV.value) {
    alert('Por favor complete todos los datos de la tarjeta.');
    return;
  }
  isProcessingPayment.value = true;
  setTimeout(() => {
    isProcessingPayment.value = false;
    paymentSuccess.value = true;
    
    // Actualizar el estado de la pensión a "Pagado"
    const idx = pensiones.value.findIndex(p => p.mes === selectedMesPago.value.mes);
    if (idx !== -1) {
      pensiones.value[idx].estado = 'Pagado';
      pensiones.value[idx].transaccion = 'TRX-' + Math.floor(10000 + Math.random() * 90000);
    }
  }, 2000);
};

const closePaymentModal = () => {
  showPayModal.value = false;
};
</script>

<template>
  <section class="intranet-section">
    <div class="container intranet-container">
      
      <!-- Cabecera de la Intranet -->
      <div class="intranet-header card">
        <div class="header-main-info">
          <span class="badge badge-accent">Demo Intranet Interactiva</span>
          <h1>Plataforma Institucional</h1>
          <p>Explora los mockups de gestión escolar interactuando con los distintos perfiles de usuario en tiempo real.</p>
        </div>
        
        <!-- Selectores de Rol Premium -->
        <div class="role-selector">
          <button 
            :class="['role-btn', { active: activeRole === 'direccion' }]" 
            @click="activeRole = 'direccion'"
          >
            <div class="role-icon">🏢</div>
            <div class="role-text-container">
              <span class="role-title">Dirección</span>
              <span class="role-desc">Gestión y control</span>
            </div>
          </button>
          
          <button 
            :class="['role-btn', { active: activeRole === 'profesores' }]" 
            @click="activeRole = 'profesores'"
          >
            <div class="role-icon">👨‍🏫</div>
            <div class="role-text-container">
              <span class="role-title">Profesores</span>
              <span class="role-desc">Notas y evaluaciones</span>
            </div>
          </button>
          
          <button 
            :class="['role-btn', { active: activeRole === 'padres' }]" 
            @click="activeRole = 'padres'"
          >
            <div class="role-icon">👪</div>
            <div class="role-text-container">
              <span class="role-title">Padres de Familia</span>
              <span class="role-desc">Pagos, notas y control</span>
            </div>
          </button>
        </div>
      </div>

      <!-- ============================== -->
      <!-- 🏢 ROL: GESTIÓN DE DIRECCIÓN   -->
      <!-- ============================== -->
      <transition name="fade" mode="out-in">
        <div v-if="activeRole === 'direccion'" class="dashboard-grid" key="direccion">
          
          <!-- Fila de Estadísticas -->
          <div class="stats-row">
            <div class="stat-card card">
              <div class="stat-icon income">💰</div>
              <div class="stat-info">
                <h3>S/. {{ totalIngresos.toLocaleString() }}</h3>
                <p>Ingresos Recaudados</p>
              </div>
            </div>
            
            <div class="stat-card card">
              <div class="stat-icon students">🎒</div>
              <div class="stat-info">
                <h3>240</h3>
                <p>Alumnos Matriculados</p>
              </div>
            </div>
            
            <div class="stat-card card">
              <div class="stat-icon teachers">🏫</div>
              <div class="stat-info">
                <h3>{{ profesores.length }}</h3>
                <p>Docentes Activos</p>
              </div>
            </div>
            
            <div class="stat-card card">
              <div class="stat-icon vacancies">🔑</div>
              <div class="stat-info">
                <h3>35</h3>
                <p>Vacantes Libres</p>
              </div>
            </div>
          </div>

          <!-- Dos Columnas: Admisiones y Profesores -->
          <div class="double-panel-grid">
            
            <!-- Panel de Admisiones -->
            <div class="panel-card card">
              <div class="panel-header">
                <h2>Gestión de Admisiones 2026</h2>
                <span class="badge badge-primary">Solicitudes Pendientes</span>
              </div>
              <p class="panel-desc">Acepta o rechaza postulantes de admisión en tiempo real.</p>
              
              <div class="table-container">
                <table class="premium-table">
                  <thead>
                    <tr>
                      <th>Postulante</th>
                      <th>Edad / Nivel</th>
                      <th>Fecha Solicitud</th>
                      <th>Estado</th>
                      <th>Acciones</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="alumno in admisiones" :key="alumno.id" class="table-row">
                      <td>
                        <span class="font-bold">{{ alumno.nombre }}</span>
                      </td>
                      <td>
                        <div class="text-sm">{{ alumno.nivel }}</div>
                        <div class="text-xs text-muted">{{ alumno.edad }}</div>
                      </td>
                      <td>{{ alumno.fecha }}</td>
                      <td>
                        <span :class="['badge', {
                          'badge-warning': alumno.estado === 'Pendiente',
                          'badge-success': alumno.estado === 'Aprobado',
                          'badge-danger': alumno.estado === 'Rechazado'
                        }]">{{ alumno.estado }}</span>
                      </td>
                      <td>
                        <div v-if="alumno.estado === 'Pendiente'" class="action-buttons">
                          <button class="action-btn approve" @click="aprobarAdmision(alumno.id)" title="Aprobar Admisión">✓</button>
                          <button class="action-btn reject" @click="rechazarAdmision(alumno.id)" title="Rechazar Admisión">✗</button>
                        </div>
                        <span v-else class="text-muted text-xs">Sin acciones</span>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>

            <!-- Panel de Profesores -->
            <div class="panel-card card">
              <div class="panel-header">
                <h2>Cuerpo Docente</h2>
                <span class="badge badge-accent">Personal</span>
              </div>
              <p class="panel-desc">Directorio de profesoras y profesores contratados para el año académico.</p>
              
              <div class="teachers-list">
                <div v-for="teacher in profesores" :key="teacher.id" class="teacher-item">
                  <div class="teacher-avatar">
                    {{ teacher.nombre.split(' ').pop().charAt(0) }}
                  </div>
                  <div class="teacher-details">
                    <h4>{{ teacher.nombre }}</h4>
                    <p class="text-sm text-secondary">{{ teacher.especialidad }}</p>
                    <p class="text-xs text-muted">{{ teacher.email }}</p>
                  </div>
                  <div class="teacher-status">
                    <span :class="['dot-indicator', { 
                      'dot-active': teacher.estado === 'Activo',
                      'dot-license': teacher.estado === 'Licencia'
                    }]"></span>
                    <span class="text-xs">{{ teacher.estado }}</span>
                  </div>
                </div>
              </div>
            </div>

          </div>
        </div>

        <!-- ============================== -->
        <!-- 👨‍🏫 ROL: GESTIÓN DE PROFESORES  -->
        <!-- ============================== -->
        <div v-else-if="activeRole === 'profesores'" class="dashboard-grid" key="profesores">
          
          <div class="double-panel-grid">
            
            <!-- Panel de Ingreso de Calificaciones -->
            <div class="panel-card card">
              <div class="panel-header">
                <h2>Registro de Notas</h2>
                
                <div class="toggle-switch">
                  <button 
                    :class="['switch-btn', { active: profGrado === 'inicial' }]" 
                    @click="profGrado = 'inicial'"
                  >Inicial</button>
                  <button 
                    :class="['switch-btn', { active: profGrado === 'primaria' }]" 
                    @click="profGrado = 'primaria'"
                  >Primaria</button>
                </div>
              </div>
              
              <p class="panel-desc" v-if="profGrado === 'inicial'">
                Nivel Inicial (Aula Creativa - 5 Años). Edita las notas de los niños directamente en la cuadrícula.
              </p>
              <p class="panel-desc" v-else>
                Nivel Primaria (1er Grado - Sección A). Modifica los campos numéricos de 0 a 20 para ver el promedio computado al instante.
              </p>

              <!-- Tabla Notas Inicial -->
              <div v-if="profGrado === 'inicial'" class="table-container">
                <table class="premium-table">
                  <thead>
                    <tr>
                      <th>Estudiante</th>
                      <th class="text-center">Taller Expresivo</th>
                      <th class="text-center">Participación</th>
                      <th class="text-center">Proyecto Grupal</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="niño in estudiantesInicial" :key="niño.id" class="table-row">
                      <td class="font-bold">{{ niño.nombre }}</td>
                      <td class="text-center">
                        <select v-model="niño.notas.taller" class="premium-select">
                          <option value="AD">AD</option>
                          <option value="A">A</option>
                          <option value="B">B</option>
                          <option value="C">C</option>
                        </select>
                      </td>
                      <td class="text-center">
                        <select v-model="niño.notas.participacion" class="premium-select">
                          <option value="AD">AD</option>
                          <option value="A">A</option>
                          <option value="B">B</option>
                          <option value="C">C</option>
                        </select>
                      </td>
                      <td class="text-center">
                        <select v-model="niño.notas.proyecto" class="premium-select">
                          <option value="AD">AD</option>
                          <option value="A">A</option>
                          <option value="B">B</option>
                          <option value="C">C</option>
                        </select>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>

              <!-- Tabla Notas Primaria -->
              <div v-else class="table-container">
                <table class="premium-table">
                  <thead>
                    <tr>
                      <th>Estudiante</th>
                      <th class="text-center">Matemática</th>
                      <th class="text-center">Comunicación</th>
                      <th class="text-center">Inglés</th>
                      <th class="text-center">Promedio</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="est in estudiantesPrimaria" :key="est.id" class="table-row">
                      <td class="font-bold">{{ est.nombre }}</td>
                      <td class="text-center">
                        <input type="number" v-model.number="est.notas.matematica" min="0" max="20" class="premium-input-number" />
                      </td>
                      <td class="text-center">
                        <input type="number" v-model.number="est.notas.comunicacion" min="0" max="20" class="premium-input-number" />
                      </td>
                      <td class="text-center">
                        <input type="number" v-model.number="est.notas.ingles" min="0" max="20" class="premium-input-number" />
                      </td>
                      <td class="text-center">
                        <span :class="['average-badge', {
                          'pass': parseFloat(calcularPromedioPrimaria(est.notas)) >= 13,
                          'fail': parseFloat(calcularPromedioPrimaria(est.notas)) < 13
                        }]">
                          {{ calcularPromedioPrimaria(est.notas) }}
                        </span>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>

            <!-- Panel Programador de Exámenes -->
            <div class="panel-card card">
              <div class="panel-header">
                <h2>Programación de Exámenes</h2>
                <span class="badge badge-secondary">Planificador</span>
              </div>
              <p class="panel-desc">Programa evaluaciones académicas. Los padres recibirán una alerta automática.</p>
              
              <!-- Formulario de Exámenes -->
              <form @submit.prevent="agregarExamen" class="premium-form">
                <div class="form-group">
                  <label>Materia</label>
                  <select v-model="nuevoExamenCurso" class="premium-select w-full">
                    <option value="Matemática">Matemática</option>
                    <option value="Comunicación">Comunicación</option>
                    <option value="Inglés">Inglés</option>
                    <option value="Ciencia y Ambiente">Ciencia y Ambiente</option>
                    <option value="Psicomotricidad">Psicomotricidad</option>
                  </select>
                </div>
                
                <div class="form-group">
                  <label>Tema del Examen</label>
                  <input type="text" v-model="nuevoExamenTema" placeholder="Ej. Tablas de multiplicar del 2 al 5" class="premium-input w-full" required />
                </div>

                <div class="form-group">
                  <label>Fecha de Evaluación</label>
                  <input type="date" v-model="nuevoExamenFecha" class="premium-input w-full" required />
                </div>

                <button type="submit" class="btn btn-secondary w-full">Programar Examen</button>
              </form>

              <!-- Lista de exámenes vigentes -->
              <div class="exam-list-mini">
                <h4>Próximos Exámenes Agendados:</h4>
                <div v-for="ex in examenes" :key="ex.id" class="exam-item-mini">
                  <div class="exam-info">
                    <strong>{{ ex.curso }}</strong> - {{ ex.tema }}
                    <div class="text-xs text-muted">Grado: {{ ex.grado }} | Fecha: {{ ex.fecha }}</div>
                  </div>
                  <span class="badge badge-accent">{{ ex.diasRestantes }} días</span>
                </div>
              </div>
            </div>

          </div>
        </div>

        <!-- ============================== -->
        <!-- 👪 ROL: PORTAL DE PADRES       -->
        <!-- ============================== -->
        <div v-else class="dashboard-grid" key="padres">
          
          <!-- Selector de Hijo y Pestañas -->
          <div class="parents-nav card">
            <div class="student-profile">
              <div class="avatar-large">👨‍👩‍👦</div>
              <div class="profile-details">
                <h3>Portal de la Familia Guerrero</h3>
                <div class="select-child-container">
                  <label for="child-select">Ver datos de: </label>
                  <select id="child-select" v-model="hijoSeleccionado" class="premium-select">
                    <option value="Mateo">Mateo Sebastián Guerrero (Primaria - 1er Grado)</option>
                    <option value="Catalina">Catalina Paz Díaz (Inicial - 5 Años)</option>
                  </select>
                </div>
              </div>
            </div>

            <!-- Pestañas Internas del Portal de Padres -->
            <div class="parents-tabs">
              <button 
                :class="['tab-btn', { active: padreTab === 'notas' }]" 
                @click="padreTab = 'notas'"
              >📊 Notas del Año</button>
              
              <button 
                :class="['tab-btn', { active: padreTab === 'examenes' }]" 
                @click="padreTab = 'examenes'"
              >📝 Exámenes Programados</button>
              
              <button 
                :class="['tab-btn', { active: padreTab === 'pagos' }]" 
                @click="padreTab = 'pagos'"
              >💳 Pagos de Mensualidad</button>
            </div>
          </div>

          <!-- Pestaña de Notas -->
          <transition name="fade" mode="out-in">
            <div v-if="padreTab === 'notas'" class="panel-card card" key="padre-notas">
              <div class="panel-header">
                <h2>Boleta de Calificaciones (Bimestre en Curso)</h2>
                <span class="badge badge-success">Actualizado</span>
              </div>
              <p class="panel-desc">Control de avance del alumno reportado directamente por la docente.</p>
              
              <!-- Si es Mateo (Primaria) -->
              <div v-if="hijoSeleccionado === 'Mateo'" class="grades-box">
                <div class="grade-item-row">
                  <div class="course-name">
                    <h4>Aritmética y Razonamiento</h4>
                    <p class="text-xs text-muted">Docente: Prof. Carlos Mendoza</p>
                  </div>
                  <div class="course-grades-detail">
                    <span class="badge-grade">Tarea: 15</span>
                    <span class="badge-grade">Examen: {{ estudiantesPrimaria[0].notas.matematica }}</span>
                    <span class="badge-grade">Participación: 16</span>
                  </div>
                  <div class="course-average">
                    <span class="avg-label">Promedio</span>
                    <span class="avg-val text-success">{{ estudiantesPrimaria[0].notas.matematica }}</span>
                  </div>
                </div>

                <div class="grade-item-row">
                  <div class="course-name">
                    <h4>Comunicación Integral</h4>
                    <p class="text-xs text-muted">Docente: Miss Karito Torres</p>
                  </div>
                  <div class="course-grades-detail">
                    <span class="badge-grade">Tarea: 18</span>
                    <span class="badge-grade">Examen: {{ estudiantesPrimaria[0].notas.comunicacion }}</span>
                    <span class="badge-grade">Participación: 17</span>
                  </div>
                  <div class="course-average">
                    <span class="avg-label">Promedio</span>
                    <span class="avg-val text-success">{{ estudiantesPrimaria[0].notas.comunicacion }}</span>
                  </div>
                </div>

                <div class="grade-item-row">
                  <div class="course-name">
                    <h4>Inglés Comunicativo</h4>
                    <p class="text-xs text-muted">Docente: Miss Sofía Peralta</p>
                  </div>
                  <div class="course-grades-detail">
                    <span class="badge-grade">Tarea: 14</span>
                    <span class="badge-grade">Examen: {{ estudiantesPrimaria[0].notas.ingles }}</span>
                    <span class="badge-grade">Participación: 15</span>
                  </div>
                  <div class="course-average">
                    <span class="avg-label">Promedio</span>
                    <span class="avg-val text-success">{{ estudiantesPrimaria[0].notas.ingles }}</span>
                  </div>
                </div>

                <!-- Comentario del Tutor -->
                <div class="tutor-feedback card">
                  <h4>💡 Comentario del Tutor:</h4>
                  <p>"Mateo demuestra mucha curiosidad matemática. Se recomienda seguir reforzando el orden en el cuaderno. ¡Excelente avance en comunicación lectoescritora!"</p>
                </div>
              </div>

              <!-- Si es Catalina (Inicial) -->
              <div v-else class="grades-box">
                <div class="grade-item-row" v-for="(nota, area) in estudiantesInicial[1].notas" :key="area">
                  <div class="course-name">
                    <h4 class="capitalize">{{ area === 'taller' ? 'Taller Expresivo Creativo' : area === 'participacion' ? 'Participación y Relaciones' : 'Proyectos de Descubrimiento' }}</h4>
                    <p class="text-xs text-muted">Área Curricular Integrada - Inicial 5 Años</p>
                  </div>
                  <div class="concept-feedback">
                    <span :class="['badge-concept', equivalenciaConcepto(nota).clase]">
                      {{ nota }}
                    </span>
                    <span class="text-sm font-semibold">{{ equivalenciaConcepto(nota).texto }}</span>
                  </div>
                </div>

                <!-- Comentario del Tutor -->
                <div class="tutor-feedback card">
                  <h4>💡 Comentario del Tutor:</h4>
                  <p>"Catalina es sumamente participativa y creativa en los talleres de pintura y moldeado. Demuestra empatía e integración fluida en las actividades de juego grupal."</p>
                </div>
              </div>
            </div>

            <!-- Pestaña de Exámenes -->
            <div v-else-if="padreTab === 'examenes'" class="panel-card card" key="padre-examenes">
              <div class="panel-header">
                <h2>Rol de Evaluaciones y Exámenes</h2>
                <span class="badge badge-accent">Próximos</span>
              </div>
              <p class="panel-desc">Calendario y temarios cargados por el profesor para asegurar el repaso en casa.</p>
              
              <div class="exam-cards-grid">
                <div v-for="ex in examenes.filter(e => hijoSeleccionado === 'Mateo' ? e.grado.includes('Primaria') : e.grado.includes('Inicial'))" :key="ex.id" class="exam-card card">
                  <div class="exam-card-header">
                    <span class="exam-subject">{{ ex.curso }}</span>
                    <span class="badge badge-warning">En {{ ex.diasRestantes }} días</span>
                  </div>
                  <h3>{{ ex.tema }}</h3>
                  <div class="exam-card-footer">
                    <div class="exam-date">📅 Fecha: <strong>{{ ex.fecha }}</strong></div>
                    <div class="exam-recommendation">✍️ Traer cartuchera y colores.</div>
                  </div>
                </div>
                
                <div v-if="examenes.filter(e => hijoSeleccionado === 'Mateo' ? e.grado.includes('Primaria') : e.grado.includes('Inicial')).length === 0" class="no-exams">
                  <p>🎉 No hay exámenes programados para esta semana.</p>
                </div>
              </div>
            </div>

            <!-- Pestaña de Pagos -->
            <div v-else class="panel-card card" key="padre-pagos">
              <div class="panel-header">
                <h2>Control de Pensiones del Año Escolar 2026</h2>
                <span class="badge badge-primary">Pensiones de Marzo - Diciembre</span>
              </div>
              <p class="panel-desc">Mantente al día con las mensualidades del año escolar. Haz clic en "Pagar Ahora" para simular un abono seguro.</p>
              
              <div class="table-container">
                <table class="premium-table">
                  <thead>
                    <tr>
                      <th>Mensualidad</th>
                      <th>Monto</th>
                      <th>Vencimiento</th>
                      <th>Estado de Pago</th>
                      <th>ID de Transacción</th>
                      <th>Acción</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="pensin in pensiones" :key="pensin.mes" class="table-row">
                      <td class="font-bold">{{ pensin.mes }} 2026</td>
                      <td>S/. {{ pensin.monto }}.00</td>
                      <td>{{ pensin.vencimiento }}</td>
                      <td>
                        <span :class="['badge', {
                          'badge-success': pensin.estado === 'Pagado',
                          'badge-warning': pensin.estado === 'Pendiente' && pensin.mes !== 'Mayo',
                          'badge-danger': pensin.estado === 'Pendiente' && pensin.mes === 'Mayo'
                        }]">
                          {{ pensin.estado === 'Pendiente' && pensin.mes === 'Mayo' ? 'Vencido' : pensin.estado }}
                        </span>
                      </td>
                      <td>
                        <span class="text-mono text-xs">{{ pensin.transaccion || '---' }}</span>
                      </td>
                      <td>
                        <button 
                          v-if="pensin.estado === 'Pendiente'" 
                          class="btn btn-accent btn-sm"
                          @click="openPayment(pensin)"
                        >
                          Pagar Ahora
                        </button>
                        <span v-else class="text-success text-sm font-bold">✓ Completado</span>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>
          </transition>
        </div>
      </transition>
    </div>

    <!-- ============================== -->
    <!-- 💳 MODAL PASARELA DE PAGO     -->
    <!-- ============================== -->
    <transition name="modal-fade">
      <div v-if="showPayModal" class="modal-overlay" @click.self="closePaymentModal">
        <div class="modal-card card">
          <button class="close-modal-btn" @click="closePaymentModal">×</button>
          
          <div class="modal-body-content">
            
            <!-- Estado Inicial: Formulario de pago -->
            <div v-if="!paymentSuccess">
              <h2 class="text-center">Pago Seguro de Pensión</h2>
              <p class="text-center text-sm text-muted mb-4">Mes a abonar: <strong>{{ selectedMesPago?.mes }} 2026</strong> | Total: <strong>S/. {{ selectedMesPago?.monto }}.00</strong></p>
              
              <form @submit.prevent="processPayment" class="premium-form">
                <div class="form-group">
                  <label>Nombre del Titular de la Tarjeta</label>
                  <input type="text" v-model="cardName" placeholder="Juan Perez Soto" class="premium-input w-full" required />
                </div>
                
                <div class="form-group">
                  <label>Número de Tarjeta</label>
                  <input type="text" v-model="cardNumber" placeholder="4557 •••• •••• 9382" class="premium-input w-full" required />
                </div>

                <div class="form-row-double">
                  <div class="form-group">
                    <label>Fecha de Exp.</label>
                    <input type="text" v-model="cardExpiry" placeholder="MM/AA" class="premium-input" required />
                  </div>
                  
                  <div class="form-group">
                    <label>CVV / CVC</label>
                    <input type="password" v-model="cardCVV" placeholder="•••" class="premium-input" required />
                  </div>
                </div>

                <div class="payment-security-shield">
                  🔒 Conexión segura con encriptación SSL de 256 bits simulada.
                </div>

                <button type="submit" class="btn btn-accent w-full mt-4" :disabled="isProcessingPayment">
                  <span v-if="isProcessingPayment">Procesando pago seguro... ⏳</span>
                  <span v-else>Pagar S/. {{ selectedMesPago?.monto }}.00</span>
                </button>
              </form>
            </div>

            <!-- Estado Final: Recibo de éxito animado -->
            <div v-else class="payment-success-screen">
              <div class="success-icon-anim">🎉</div>
              <h2>¡Pago Procesado Exitosamente!</h2>
              <p>El recibo correspondiente a la pensión de <strong>{{ selectedMesPago?.mes }} 2026</strong> ha sido emitido y guardado.</p>
              
              <div class="success-receipt card">
                <div class="receipt-row">
                  <span>Concepto:</span>
                  <strong>Pensión Escolar Lovely Garden</strong>
                </div>
                <div class="receipt-row">
                  <span>Estudiante:</span>
                  <strong>{{ hijoSeleccionado === 'Mateo' ? 'Mateo S. Guerrero' : 'Catalina P. Díaz' }}</strong>
                </div>
                <div class="receipt-row">
                  <span>Monto abonado:</span>
                  <strong>S/. {{ selectedMesPago?.monto }}.00</strong>
                </div>
                <div class="receipt-row">
                  <span>Código Operación:</span>
                  <strong class="text-mono">TRX-{{ Math.floor(10000 + Math.random() * 90000) }}</strong>
                </div>
                <div class="receipt-row">
                  <span>Fecha de pago:</span>
                  <strong>{{ new Date().toLocaleDateString() }}</strong>
                </div>
              </div>

              <button class="btn btn-primary w-full mt-4" @click="closePaymentModal">Aceptar y Continuar</button>
            </div>

          </div>
        </div>
      </div>
    </transition>
  </section>
</template>

<style scoped>
/* --- ESTILOS DE LA INTRANET --- */
.intranet-section {
  padding: 8rem 0 6rem;
  background-color: var(--bg-primary);
  min-height: 100vh;
  box-sizing: border-box;
}

.intranet-container {
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
}

/* Cabecera */
.intranet-header {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  padding: 3rem;
  background-color: var(--bg-secondary);
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-md);
}

.header-main-info h1 {
  font-size: 2.5rem;
  margin: 0.5rem 0;
  color: var(--primary-hover);
}

.header-main-info p {
  color: var(--text-light);
}

/* Selectores de Rol */
.role-selector {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1.25rem;
  margin-top: 1rem;
}

.role-btn {
  display: flex;
  align-items: center;
  gap: 1.25rem;
  padding: 1.5rem;
  background: var(--bg-primary);
  border: 2px solid transparent;
  border-radius: var(--radius-md);
  cursor: pointer;
  transition: var(--transition);
  text-align: left;
  box-shadow: var(--shadow-sm);
}

.role-btn:hover {
  transform: translateY(-3px);
  border-color: var(--primary-border);
  box-shadow: var(--shadow-md);
}

.role-btn.active {
  border-color: var(--secondary);
  background: rgba(255, 111, 67, 0.05);
}

.role-icon {
  font-size: 2.25rem;
}

.role-text-container {
  display: flex;
  flex-direction: column;
}

.role-title {
  font-family: var(--font-title);
  font-weight: 700;
  font-size: 1.2rem;
  color: var(--text-dark);
}

.role-desc {
  font-size: 0.85rem;
  color: var(--text-muted);
}

/* Estadísticas de Dirección */
.stats-row {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1.5rem;
}

.stat-card {
  display: flex;
  align-items: center;
  gap: 1.5rem;
  padding: 2rem;
  background-color: var(--bg-secondary);
}

.stat-icon {
  font-size: 2.25rem;
  width: 4rem;
  height: 4rem;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.stat-icon.income { background-color: rgba(59, 164, 229, 0.12); color: var(--accent); }
.stat-icon.students { background-color: rgba(255, 167, 38, 0.12); color: var(--primary); }
.stat-icon.teachers { background-color: rgba(255, 111, 67, 0.12); color: var(--secondary); }
.stat-icon.vacancies { background-color: rgba(76, 175, 80, 0.12); color: #4CAF50; }

.stat-info h3 {
  font-size: 1.75rem;
  color: var(--text-dark);
}

.stat-info p {
  font-size: 0.95rem;
  color: var(--text-muted);
}

/* Doble Panel (Dirección y Profesores) */
.double-panel-grid {
  display: grid;
  grid-template-columns: 1.4fr 1fr;
  gap: 2rem;
}

@media (max-width: 992px) {
  .double-panel-grid {
    grid-template-columns: 1fr;
  }
}

.panel-card {
  padding: 2.5rem;
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.panel-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 2px dashed rgba(255, 167, 38, 0.15);
  padding-bottom: 1rem;
}

.panel-desc {
  font-size: 0.95rem;
  color: var(--text-light);
}

/* Tablas Premium */
.table-container {
  overflow-x: auto;
  border-radius: var(--radius-sm);
  border: 1px solid var(--border-color);
}

.premium-table {
  width: 100%;
  border-collapse: collapse;
  text-align: left;
}

.premium-table th {
  background-color: var(--bg-primary);
  padding: 1rem 1.25rem;
  font-weight: 600;
  color: var(--text-dark);
  font-size: 0.95rem;
}

.premium-table td {
  padding: 1.25rem;
  border-bottom: 1px solid var(--border-color);
  color: var(--text-light);
  font-size: 0.95rem;
}

.table-row:hover {
  background-color: rgba(255, 167, 38, 0.02);
}

.font-bold { font-weight: 700; color: var(--text-dark); }
.text-sm { font-size: 0.85rem; }
.text-xs { font-size: 0.75rem; }
.text-mono { font-family: monospace; }
.capitalize { text-transform: capitalize; }
.mb-4 { margin-bottom: 1rem; }

/* Botones de acción tabla */
.action-buttons {
  display: flex;
  gap: 0.5rem;
}

.action-btn {
  width: 2rem;
  height: 2rem;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  cursor: pointer;
  transition: var(--transition);
}

.action-btn.approve {
  background-color: rgba(76, 175, 80, 0.12);
  color: #4CAF50;
}

.action-btn.approve:hover {
  background-color: #4CAF50;
  color: #FFFFFF;
}

.action-btn.reject {
  background-color: rgba(244, 67, 54, 0.12);
  color: #F44336;
}

.action-btn.reject:hover {
  background-color: #F44336;
  color: #FFFFFF;
}

/* Directorio Profesores */
.teachers-list {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.teacher-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1rem 0;
  border-bottom: 1px solid var(--border-color);
}

.teacher-item:last-child {
  border-bottom: none;
}

.teacher-avatar {
  width: 3rem;
  height: 3rem;
  border-radius: 50%;
  background-color: var(--primary-light);
  color: var(--primary-hover);
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: var(--font-title);
  font-weight: 700;
  font-size: 1.25rem;
}

.teacher-details {
  flex-grow: 1;
}

.teacher-details h4 {
  color: var(--text-dark);
  font-size: 1.05rem;
}

.teacher-status {
  display: flex;
  align-items: center;
  gap: 0.35rem;
}

.dot-indicator {
  width: 8px;
  height: 8px;
  border-radius: 50%;
}

.dot-active { background-color: #4CAF50; }
.dot-license { background-color: var(--primary); }

/* Switch Toggle en Profesores */
.toggle-switch {
  display: flex;
  background-color: var(--bg-primary);
  border-radius: var(--radius-full);
  padding: 0.25rem;
  border: 1px solid var(--border-color);
}

.switch-btn {
  padding: 0.4rem 1.25rem;
  border-radius: var(--radius-full);
  font-family: var(--font-title);
  font-weight: 700;
  font-size: 0.9rem;
  cursor: pointer;
  transition: var(--transition);
}

.switch-btn.active {
  background-color: var(--secondary);
  color: var(--bg-secondary);
}

/* Inputs de Notas y Formularios */
.premium-select {
  padding: 0.6rem 1rem;
  border-radius: var(--radius-sm);
  border: 1.5px solid var(--border-color);
  background-color: var(--bg-secondary);
  font-family: var(--font-body);
  transition: var(--transition);
  cursor: pointer;
}

.premium-select:focus {
  border-color: var(--primary);
}

.premium-input-number {
  width: 4rem;
  padding: 0.5rem;
  border-radius: var(--radius-sm);
  border: 1.5px solid var(--border-color);
  text-align: center;
  font-weight: 700;
  transition: var(--transition);
}

.premium-input-number:focus {
  border-color: var(--primary);
  box-shadow: 0 0 5px rgba(255, 167, 38, 0.2);
}

.average-badge {
  padding: 0.35rem 0.85rem;
  border-radius: var(--radius-full);
  font-weight: 700;
  font-size: 0.9rem;
}

.average-badge.pass { background-color: rgba(76, 175, 80, 0.12); color: #4CAF50; }
.average-badge.fail { background-color: rgba(244, 67, 54, 0.12); color: #F44336; }

/* Formulario */
.premium-form {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.form-group label {
  font-family: var(--font-title);
  font-weight: 700;
  color: var(--text-dark);
  font-size: 0.95rem;
}

.premium-input {
  padding: 0.85rem 1.25rem;
  border-radius: var(--radius-sm);
  border: 1.5px solid var(--border-color);
  transition: var(--transition);
  font-family: var(--font-body);
}

.premium-input:focus {
  border-color: var(--primary);
}

.w-full { width: 100%; }

/* Exámenes Programador */
.exam-list-mini {
  margin-top: 1.5rem;
  display: flex;
  flex-direction: column;
  gap: 0.85rem;
}

.exam-item-mini {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.85rem;
  background-color: var(--bg-primary);
  border-radius: var(--radius-sm);
  border-left: 4px solid var(--accent);
}

.exam-info {
  font-size: 0.9rem;
}

/* =============================== */
/* Portal Padres Estilos           */
/* =============================== */
.parents-nav {
  padding: 2.5rem;
}

.student-profile {
  display: flex;
  align-items: center;
  gap: 2rem;
  border-bottom: 2px dashed var(--border-color);
  padding-bottom: 1.5rem;
}

@media (max-width: 768px) {
  .student-profile {
    flex-direction: column;
    text-align: center;
  }
}

.avatar-large {
  font-size: 3.5rem;
  width: 6rem;
  height: 6rem;
  border-radius: 50%;
  background: var(--primary-light);
  display: flex;
  align-items: center;
  justify-content: center;
  border: 3px solid var(--primary-border);
}

.select-child-container {
  margin-top: 0.75rem;
  font-size: 1rem;
}

.parents-tabs {
  display: flex;
  gap: 1rem;
  margin-top: 2rem;
  flex-wrap: wrap;
}

.tab-btn {
  padding: 0.85rem 1.75rem;
  border-radius: var(--radius-full);
  font-family: var(--font-title);
  font-weight: 700;
  cursor: pointer;
  transition: var(--transition);
  background-color: var(--bg-primary);
  border: 1px solid var(--border-color);
  color: var(--text-light);
}

.tab-btn.active {
  background-color: var(--accent);
  color: var(--bg-secondary);
  border-color: var(--accent);
  box-shadow: var(--shadow-accent);
}

/* Boleta Notas Padres */
.grades-box {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.grade-item-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem;
  background-color: var(--bg-primary);
  border-radius: var(--radius-sm);
  border-left: 5px solid var(--primary);
  gap: 1rem;
}

@media (max-width: 768px) {
  .grade-item-row {
    flex-direction: column;
    text-align: center;
  }
}

.course-grades-detail {
  display: flex;
  gap: 1rem;
}

.badge-grade {
  background-color: var(--bg-secondary);
  padding: 0.5rem 1rem;
  border-radius: var(--radius-full);
  font-size: 0.85rem;
  font-weight: 600;
  border: 1px solid var(--border-color);
}

.course-average {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.avg-label {
  font-size: 0.75rem;
  text-transform: uppercase;
  color: var(--text-muted);
}

.avg-val {
  font-size: 1.5rem;
  font-weight: 700;
}

.text-success { color: #4CAF50; }

.badge-concept {
  padding: 0.4rem 1rem;
  border-radius: var(--radius-full);
  font-weight: 700;
  color: #FFFFFF;
}

.nota-ad { background-color: #4CAF50; }
.nota-a { background-color: var(--accent); }
.nota-b { background-color: var(--primary); }
.nota-c { background-color: #F44336; }

.concept-feedback {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.tutor-feedback {
  background-color: rgba(255, 167, 38, 0.05);
  border: 1.5px dashed var(--primary-border);
  padding: 2rem;
  margin-top: 1rem;
}

/* Tarjetas Exámenes Padres */
.exam-cards-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
  margin-top: 1rem;
}

.exam-card {
  border-left: 6px solid var(--secondary);
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.exam-card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.exam-subject {
  font-family: var(--font-title);
  font-weight: 700;
  font-size: 1.1rem;
  color: var(--secondary);
}

.exam-card-footer {
  border-top: 1px solid var(--border-color);
  padding-top: 0.75rem;
  margin-top: 0.5rem;
  font-size: 0.85rem;
}

.no-exams {
  grid-column: 1 / -1;
  text-align: center;
  padding: 3rem;
  color: var(--text-muted);
}

/* Badges y Decorados */
.badge {
  display: inline-block;
  padding: 0.35rem 0.85rem;
  font-size: 0.8rem;
  font-weight: 700;
  border-radius: var(--radius-full);
  font-family: var(--font-title);
}

.badge-primary { background-color: var(--primary-light); color: var(--primary-hover); }
.badge-secondary { background-color: var(--secondary-light); color: var(--secondary-hover); }
.badge-accent { background-color: var(--accent-light); color: var(--accent-hover); }
.badge-success { background-color: rgba(76, 175, 80, 0.12); color: #4CAF50; }
.badge-warning { background-color: rgba(255, 167, 38, 0.12); color: var(--primary-hover); }
.badge-danger { background-color: rgba(244, 67, 54, 0.12); color: #F44336; }

/* MODAL DE PAGO */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(30, 41, 59, 0.6);
  backdrop-filter: blur(8px);
  z-index: 10000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1.5rem;
}

.modal-overlay .modal-card {
  width: 100%;
  max-width: 520px;
  position: relative;
  box-shadow: var(--shadow-lg);
  border: 1px solid rgba(255, 255, 255, 0.2);
  animation: modalScaleUp 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
  padding: 3rem;
}

@keyframes modalScaleUp {
  from { transform: scale(0.9); opacity: 0; }
  to { transform: scale(1); opacity: 1; }
}

.close-modal-btn {
  position: absolute;
  top: 1.25rem;
  right: 1.25rem;
  font-size: 2.25rem;
  color: var(--text-muted);
  cursor: pointer;
  transition: var(--transition);
}

.close-modal-btn:hover {
  color: var(--text-dark);
  transform: rotate(90deg);
}

.form-row-double {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}

.payment-security-shield {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  font-size: 0.8rem;
  color: var(--text-muted);
  background-color: var(--bg-primary);
  padding: 0.75rem;
  border-radius: var(--radius-sm);
  margin-top: 1rem;
  border: 1.5px solid var(--border-color);
}

.payment-success-screen {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: 1rem;
}

.success-icon-anim {
  font-size: 4rem;
  animation: pulseRotate 1s ease-in-out infinite alternate;
}

@keyframes pulseRotate {
  from { transform: scale(1) rotate(-5deg); }
  to { transform: scale(1.1) rotate(5deg); }
}

.success-receipt {
  width: 100%;
  padding: 1.5rem;
  background-color: var(--bg-primary);
  border: 1px dashed var(--border-color);
  margin-top: 1rem;
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.receipt-row {
  display: flex;
  justify-content: space-between;
  font-size: 0.9rem;
  border-bottom: 1px solid var(--border-color);
  padding-bottom: 0.5rem;
}

.receipt-row:last-child {
  border-bottom: none;
}

.mt-4 { margin-top: 1.5rem; }

/* Transiciones */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.25s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
