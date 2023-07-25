<template>
    <div class="row-style">
        <v-row align="center" justify="center" class="row-margin">
            <v-col cols="12">
                <v-card>
                    <v-col class="pt-5"> 
                        <h2 class=" font-weight-regular">
                            Subir reporte
                        </h2>
                        <v-form>
                            <v-row>
                                <v-col cols="12" class="pt-5 pb-0">
                                    <VueFileAgent v-model="fileRecords"></VueFileAgent>
                                    <v-file-input
                                        height="100"
                                        solo
                                        color="grey"
                                        class="elevation-0"
                                        accept="image/*"
                                        label="Selecciona el archivo pdf"
                                    ></v-file-input>
                                </v-col>
                            </v-row>
                            <v-btn
                                block
                                outlined
                                color="#2CA58D"
                                class="border-rounded text-none btn-style"
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
import VueFileAgent from 'vue-file-agent'
export default {
    components:{
        VueFileAgent
    },
    props: {
        eventNextStep: {
            type: String,
            required: true,
        },
    },
    data() {
        return {
            fileRecords:''
        }
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
  height: 300px;
}
.primaryColor--text{
  color:#E07A5F;
}
.secondaryColor--text{
  color:#2CA58D;
}
.btn-style{
    width: 80px;
}
</style>