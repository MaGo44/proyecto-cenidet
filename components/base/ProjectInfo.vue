<template>
    <div class="row-style">
        <v-row align="center" justify="center" class="row-margin">
            <v-col cols="12">
                <v-card>
                    <v-col class="pt-5"> 
                        <h2 class="primaryColor--text font-weight-regular">
                            Datos de educación dual
                        </h2>
                        <v-form>
                            <v-row>
                                <v-col cols="12" class="pb-0 mt-5">
                                    <v-text-field outlined label="Nombre del proyecto" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field outlined label="Elige la unidad económica" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field outlined label="Fecha de inicio" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field outlined label="Fecha de finalizacion" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field outlined label="Puesto a desempenar" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field outlined label="Departamento o area asignada" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field outlined label="Nombre del asesor externo" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field outlined label="Elige tu asesor interno" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field outlined label="Fuiste contratado por tu empresa?" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field outlined label="Periodo" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-textarea outlined label="Objetivo del proyecto" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-textarea outlined label="Descripcion del proyecto" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-textarea outlined label="Problema que se espera resolver" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-textarea outlined label="Resultados esperados" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-textarea outlined label="Producto final" />
                                </v-col>
                            </v-row>
                            <v-btn
                                block
                                color="turquoisePrimary"
                                class="ma-2 white--text border-rounded text-none"
                                @click="nextStep()">
                                <v-icon left dark>
                                    mdi-lock-outline
                                </v-icon>
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