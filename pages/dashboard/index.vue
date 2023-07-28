<template>
    <div style="height: 100%" class="row-style">
      <div class="margin-row">
        <v-row class="mt-5">
          <!-- [INFO] -->
          <h2>¡Descubre la educación dual para tu futuro profesional!</h2>
          <p>
            Nuestra educación dual te prepara para enfrentar los retos de la industria con éxito, combinando teoría y
            práctica en empresas, organizaciones y el gobierno.
          </p>
          <p>¿Qué ofrece nuestro modelo de Educación Dual?</p>
          <div>
            <ul>
            <li>Vinculación entre teoría y práctica.</li>
            <li>Desarrollo de nuevas competencias profesionales.</li>
            <li>Flexibilidad en acciones y recursos.</li>
            <li>Integración entre el TecNM y empresas u organizaciones gubernamentales.</li>
            <li>Formación en competencias genéricas y específicas de manera efectiva.</li>
            <li>Experiencia laboral real para los estudiantes.</li>
          </ul>
          </div>

          <p>
            ¡Con nuestro Programa de Educación Dual (PED), podrás acreditar las asignaturas de 8vo y 9no semestre,
            incluyendo aquellas del módulo de especialidad y la residencia profesional!
          </p>
          <p>
            Prepárate para un futuro exitoso en el mundo laboral con nuestra educación dual. ¡Únete ahora y forma parte de una formación integral y práctica!
          </p>
        </v-row>
        <v-row>
          <v-col cols="12" sm="6">
            <v-card class="elevation-0">
              <div class="margin-row">
                <h3 class="mt-5 mb-3">Para ser parte del Proceso de Educación Dual será necesario que proporciones la siguiente
                  documentación al momento de registrarte:</h3>
                <ul class="mb-5">
                  <li>Carta de presentación</li>
                  <li>Carta de aceptación</li>
                  <li>CV</li>
                  <li>Constancia de créditos con promedio en lugar de kardex</li>
                  <li>Constancia de afiliación al servicio médico vigente</li>
                  <li>Crédito de inglés</li>
                  <li>Servicio social</li>
                  <li>Créditos complementarios</li>
                  <li>Constancia de autorización del jefe de carrera</li>
                  <li>Anexo 1</li>
                </ul>
              </div>
            </v-card>
          </v-col>
          <v-col cols="12" sm="6">
            <div class="center-content">
              <div class="mb-5">
                Dirígete aquí para descargar los formatos requeridos
              </div>
              <router-link to="/downloads">
                <v-btn outlined class="text-none">
                  Ir a descargas
                </v-btn>
              </router-link>
            </div>
          </v-col>
        </v-row>
      </div>
    </div>
  </template>
  
  <style scoped>
  .margin-row {
    margin: 0 5%;
  }
  
  .row-style {
    background-color: #f8f7ff;
  }
  
  .card-style {
    height: 200px;
  }
  
  .center-content {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100%;
  }
  </style>