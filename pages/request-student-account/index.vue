<template>
  <div class="center-container">
    <v-row class="center-content">
      <v-col cols="12" sm="6">
        <v-card class="card-style elevation-2">
          <v-card-title>
            <h4 class="mt-5 mb-3">
              Favor de contactar con el coordinador de tu carrera para la creación de tu usuario y contraseña.
            </h4>
            <NuxtLink to="/login-student">
              <v-col cols="12">
                <span class="secondaryColor--text" style="cursor:pointer">Regresar</span>
              </v-col>
            </NuxtLink>
          </v-card-title>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<style scoped>
.center-container {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.card-style {
  height: 200px;
}

.center-content {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.secondaryColor--text{
color:#2CA58D;
}

</style>