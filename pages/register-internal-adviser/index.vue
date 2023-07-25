<template>
    <div class="container_main" style="height: 100%">
        <v-container>
        <v-row align="center" justify="center" class="margin-row container_main">
            <v-col>
                <v-card>
                    <v-col class="pt-5"> 
                        <h2 class="primaryColor--text font-weight-regular">
                            Registro de asesor interno
                        </h2>
                        <v-form>
                            <v-row>
                                <v-col cols="12" class="pb-0 mt-5">
                                    <v-text-field outlined label="Nombre del asesor interno" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field outlined label="Apellido paterno" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field outlined label="Apellido materno" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field outlined label="Sexo" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field outlined label="Grado escolar" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field outlined label="Teléfono fijo" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field outlined label="Teléfono celular" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field outlined label="Carrera de adscripción" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field outlined label="Correo institucional" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field outlined label="Segundo correo" />
                                </v-col>
                            </v-row>
                            <v-btn
                                width="20%"
                                outlined
                                color="#2CA58D"
                                class="border-rounded text-none"
                                @click="nextStep()">
                                    Guardar
                            </v-btn>
                        </v-form>
                    </v-col>
                </v-card>
            </v-col>
        </v-row>
    </v-container>
    </div>
</template>
<script>
export default {
    layout: "adminLayout",
    data() {
        return{
            companyForm:{
                
            }
        }
    },
}
</script>
<style scoped>
.margin-row {
  margin: 0 10%;
}
.title-form {
  margin: 0 5%;
}
.textfields-form {
  margin: 0 15%;
}
</style>