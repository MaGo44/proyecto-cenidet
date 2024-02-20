<template>
  <v-row class="row-style" align="center">
    <v-col cols="6">
      <div class="text-right" align="center">
          <h1 class="h1-style font-weight-regular">
          Modelo de Educación Dual
          </h1>
      </div>
    </v-col>
    <v-col cols="6">
      <v-card>
        <v-col class="pt-5" style="padding:0 5%; width:100%"> 
          <h2 class="primaryColor--text">
          Accede a la plataforma
          </h2>
          <v-form>
            <v-col class="mr-2">
              <v-text-field outlined label="Nombre de usuario" />
              <v-text-field outlined label="Contraseña" />
              <NuxtLink to="/dashboard">
                <v-btn outlined class="text-none primaryColor--text">
                  Acceder
                </v-btn>
              </NuxtLink>
              <NuxtLink to="/request-student-account">
                <v-col cols="12">
                  <span class="secondaryColor--text" style="cursor:pointer">No tengo una cuenta</span>
                </v-col>
              </NuxtLink>
            </v-col>
        </v-form>
        </v-col>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'IndexPage',
  layout: 'default',
}
</script>

<style scoped>
h1.h1-style {
  font-size: 80px;
  color:#361D2E;
}
.row-style {
  background-color: #F8F7FF;
  height: 100%;
}
.primaryColor--text{
  color:#E07A5F;
}
.secondaryColor--text{
  color:#2CA58D;
}
</style>