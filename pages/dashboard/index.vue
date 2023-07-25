<template>
    <div style="height: 100%" class="row-style">
        <div class="margin-row">
            <v-row class="mt-5">
                [INFO]
            </v-row>
            <v-row>
                <v-col cols="6">
                    <v-card class="elevation-0">
                        <div class="margin-row">
                            <v-row>
                                <h4 class="mt-5 mb-5">
                                    Para ser parte del Proceso de Educación Dual sera necesario que proporciones la siguiente documentación al momento de registrarte:
                                </h4>
                            </v-row>
                            <v-row class="margin-row">
                                <span class="mb-5">
                                    -Carta de presentación<br/>
                                    -Carta de aceptación<br/>
                                    -CV<br/>
                                    -Constancia de creditos con promedio en lugar de kardex<br/>
                                    -Constancia de afiliación al servicio medico vigente<br/>
                                    -Credito de ingles<br/>
                                    -Servicio social<br/>
                                    -Creditos complementarios<br/>
                                    -Constancia de autorización del jefe de carrera<br/>
                                    -Anexo 1
                                </span>
                            </v-row>
                        </div>
                    </v-card>
                </v-col>
                <v-col cols="6">
                    <div class="center-content">
                        <div class="mb-5">
                            Dirigete aqui para descargar los formatos requeridos
                        </div>
                        <div>
                            <NuxtLink to="/downloads">
                                <v-btn outlined class="text-none">
                                    Ir a descargas
                                </v-btn>
                            </NuxtLink>
                        </div>
                    </div>
                </v-col>
            </v-row>
        </div>
    </div>
</template>
<script>
export default {
    layout: 'internalLayout',
    setup() {
        
    },
}
</script>
<style scoped>
.margin-row {
  margin: 0 5%;
}
.row-style{
    background-color: #F8F7FF;
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