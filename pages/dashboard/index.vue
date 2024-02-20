<template>
    <div style="height: 100%" class="row-style">
      <div class="margin-row">
        <v-row class="mt-5 d-flex align-center">
          <v-col cols="6">
              <h1>Descubre la educación dual para tu futuro profesional</h1>
              <p>
                La educación dual te prepara para enfrentar los retos de la industria con éxito, combinando teoría y
                práctica en empresas, organizaciones y el gobierno.
              </p>
          </v-col>
          <v-col cols="6" class="d-flex justify-center align-center">
              <v-img
                max-height="400"
                max-width="400"
                :src="require('@/assets/png/dashboard.png')" />
          </v-col>
          <!-- [INFO] -->
          <v-row class="mt-5 mb-5" justify="center">
            <p class="font-weight-medium">¿Qué ofrece el modelo de Educación Dual?</p>
          </v-row>
          <v-row style="margin:0 15%">
            <v-col cols="3">
              <div height="100">
                <v-icon size="80">
                  mdi-head-cog
                </v-icon>
              </div>
              <p>Vinculación entre teoría y práctica.</p>
            </v-col>
            <v-col cols="3">
              <v-icon size="60">
                mdi-tools
              </v-icon>
              <p>Desarrollo de nuevas competencias profesionales.</p>
            </v-col>
            <v-col cols="3">
              <v-icon size="80">
                mdi-account-check
              </v-icon>
              <p>Formación en competencias genéricas y específicas de manera efectiva.</p>
            </v-col>
            <v-col cols="3">
              <v-icon size="60">
                mdi-briefcase
              </v-icon>
              <p>Experiencia laboral real para los estudiantes.</p>
            </v-col>
          </v-row>
          <v-row style="margin:0 10%" class="text-center mt-5 mb-5">
            <p>
              Con el Programa de Educación Dual (PED), podrás acreditar las asignaturas de 8vo y 9no semestre,
              incluyendo aquellas del módulo de especialidad y la residencia profesional.
            </p>
            <p class="font-weight-medium">
              Prepárate para un futuro exitoso en el mundo laboral con nuestra educación dual. ¡Únete ahora y forma parte de una formación integral y práctica!
            </p>
          </v-row>
        </v-row>
        <v-row>
          <v-col cols="12" sm="6">
            <v-card class="elevation-0">
              <v-row class="margin-row">
                <h3 style="margin:5% 0">Para ser parte del Proceso de Educación Dual será necesario que proporciones la siguiente
                  documentación al momento de registrarte:</h3>
                <ul class="mb-5">
                  <li>Carta de presentación</li>
                  <li>Carta de aceptación</li>
                  <li>CV</li>
                  <li>Constancia de créditos con promedio</li>
                  <li>Constancia de afiliación al servicio médico vigente</li>
                  <li>Crédito de inglés</li>
                  <li>Servicio social</li>
                  <li>Créditos complementarios</li>
                  <li>Constancia de autorización del jefe de carrera</li>
                  <li>Anexo 1</li>
                </ul>
              </v-row>
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
<script>
  export default {
      layout: 'internalLayout',
  }
</script>
<style scoped>
  .margin-row {
    margin: 5% 5%;
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