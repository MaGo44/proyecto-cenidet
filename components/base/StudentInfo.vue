<template>
    <div class="row-style">
        <v-row align="center" justify="center" class="row-margin">
            <v-col cols="12">
                <v-card>
                    <v-col class="pt-5"> 
                        <h2 class="primaryColor--text font-weight-regular">
                            Datos del estudiante
                        </h2>
                        <v-form>
                            <v-row>
                                <v-col cols="12" class="text-center pt-5 d-flex align-center">
                                    <v-card
                                        height="100px"
                                        width="100px"
                                        class="elevation-0 grey lighten-2 mx-auto"
                                    >
                                    <div>Subir foto</div>
                                    </v-card>
                                </v-col>
                                <v-col cols="12" class="pb-0">
                                    <v-text-field outlined label="Nombre" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field outlined label="Apellido paterno" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field outlined label="Apellido materno" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field outlined label="No.Control" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field outlined label="CURP" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field outlined label="Carrera" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field outlined label="Sexo" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field outlined label="Correo institucional" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field outlined label="Correo personal" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field outlined label="Telefono fijo" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field outlined label="Telefono celular" />
                                </v-col>
                                <v-col cols="3" class="pb-0 pt-0">
                                    <v-text-field outlined label="Promedio" />
                                </v-col>
                                <v-col cols="3" class="pb-0 pt-0">
                                    <v-text-field outlined label="Creditos acum" />
                                </v-col>
                                <v-col cols="3" class="pb-0 pt-0">
                                    <v-text-field outlined label="Semestre" />
                                </v-col>
                                <v-col cols="3" class="pb-0 pt-0">
                                    <v-text-field outlined label="Clave plan de estudios" />
                                </v-col>
                            </v-row>
                            <v-btn
                                block
                                outlined
                                color="#2CA58D"
                                class="border-rounded text-none"
                                @click="nextStep()">
                                Siguiente
                            </v-btn>
                        </v-form>
                    </v-col>
                </v-card>
            </v-col>
        </v-row>
    </div>
</template>
<script>
export default {
    props: {
        eventNextStep: {
            type: String,
            required: true,
        },
    },
    data() {
        
    },
    methods:{
        nextStep() {
            this.$nuxt.$emit(this.eventNextStep)
        },
    }
}
</script>
<style scoped>
h1 {
  color:#361D2E;
}
.row-style {
  background-color: #F8F7FF;
}
.primaryColor--text{
  color:#E07A5F;
}
.secondaryColor--text{
  color:#2CA58D;
}
</style>