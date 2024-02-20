<template>
    <v-row class="row-style">
        <v-row align="center" justify="center" class="row-margin">
            <v-col cols="12">
                <h1 class="primaryColor--text mb-5" align="center">
                    Modelo de Educación Dual
                </h1>
                <v-card>
                    <v-col class="pt-5"> 
                        <h2 class="primaryColor--text font-weight-regular" align="center">
                            Acceso de administrador
                        </h2>
                        <v-form>
                            <v-row>
                                <v-col cols="12" class="pb-0 mt-5">
                                    <v-text-field outlined label="Correo" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field outlined label="Contrasena" />
                                </v-col>
                            </v-row>
                            <NuxtLink to="/admin-dash">
                                <v-btn outlined class="text-none secondaryColor--text" align="center">
                                    Acceder
                                </v-btn>
                            </NuxtLink>
                        </v-form>
                    </v-col>
                </v-card>
            </v-col>
        </v-row>
    </v-row>
</template>
<style scoped>
.row-margin{
    margin: 0 25%
}
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