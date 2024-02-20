<template>
    <div style="height: 100%" class="row-style">
        <div class="margin-row">
            <v-row class="mt-10 mb-10 justify-center text-center">
                <h2>Encuentra los documentos requeridos para el proceso de educacion dual</h2>
            </v-row>
            <v-row>
                <v-col cols="4">
                    <div class="mb-10 justify-center text-center">
                        Inicio al PED
                    </div>
                    <v-card class="card-style elevation-0">
                        <v-row class="margin-content mt-5">
                            <v-col cols="9">
                                Anexo 1
                            </v-col>
                            <v-col cols="3">
                                <v-btn outlined small>
                                    <v-icon size="20px" class="ma-0">
                                        mdi-tray-arrow-down
                                    </v-icon>
                                </v-btn>
                            </v-col>
                        </v-row>
                        <v-row class="margin-content">
                            <v-col cols="9">
                                Lineamiento de educación dual
                            </v-col>
                            <v-col cols="3">
                                <v-btn outlined small>
                                    <v-icon size="20px" class="ma-0">
                                        mdi-tray-arrow-down
                                    </v-icon>
                                </v-btn>
                            </v-col>
                        </v-row>
                        <v-row class="margin-content">
                            <v-col cols="9">
                                Anexo 3
                            </v-col>
                            <v-col cols="3">
                                <v-btn outlined small>
                                    <v-icon size="20px" class="ma-0">
                                        mdi-tray-arrow-down
                                    </v-icon>
                                </v-btn>
                            </v-col>
                        </v-row>
                    </v-card>
                </v-col>
                <v-col cols="4">
                    <div class="mb-10 justify-center text-center">
                        Durante el proceso
                    </div>
                    <v-card class="card-style elevation-0 margin-row">
                        <div class="mt-5">
                            <v-row class="margin-content">
                                <v-col cols="9">
                                    Formato de reportes mensuales
                                </v-col>
                                <v-col cols="3">
                                    <v-btn outlined small>
                                        <v-icon size="20px" class="ma-0">
                                            mdi-tray-arrow-down
                                        </v-icon>
                                    </v-btn>
                                </v-col>
                            </v-row>
                            <v-row class="margin-content">
                                <v-col cols="9">
                                    Guia para la elaboracion del reporte final
                                </v-col>
                                <v-col cols="3">
                                    <v-btn outlined small>
                                        <v-icon size="20px" class="ma-0">
                                            mdi-tray-arrow-down
                                        </v-icon>
                                    </v-btn>
                                </v-col>
                            </v-row>
                        </div>
                    </v-card>
                </v-col>
                <v-col cols="4">
                    <div class="mb-10 justify-center text-center">
                        Finalización
                    </div>
                    <v-card class="card-style elevation-0 margin-row">
                        <v-row class="margin-content">
                                <v-col cols="9">
                                    Carta de liberación
                                </v-col>
                                <v-col cols="3">
                                    <v-btn outlined small>
                                        <v-icon size="20px" class="ma-0">
                                            mdi-tray-arrow-down
                                        </v-icon>
                                    </v-btn>
                                </v-col>
                            </v-row>
                    </v-card>
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
  margin: 0 5%;
}
.margin-content {
  margin: 0 10%;
}
.row-style{
    background-color: #F8F7FF;
}
.card-style {
  height: 200px;
}
</style>