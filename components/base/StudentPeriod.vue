<template>
    <div class="row-style">
        <v-row align="center" justify="center" class="row-margin">
            <v-col cols="12">
                <v-card>
                    <v-col class="pt-5"> 
                        <h2 class="primaryColor--text font-weight-regular">
                            Periodo
                        </h2>
                        <v-form ref="form">
                            <v-row class="mb-2">
                                <v-col cols="12" class="pt-5 pb-0">
                                    <v-select 
                                        v-model="project_period" 
                                        :items="periods"
                                        item-value="period_id"
                                        item-text="period_name"
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Elige el periodo" />
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
    periods: {
            type: Array,
            required: true,
        },
    },
    data() {
        return{
            project_period:null
        }
    },
    methods:{
        nextStep() {
            const valid=this.$refs.form.validate()
            if(valid){
                this.$emit('set-period',this.project_period)
                this.$nuxt.$emit(this.eventNextStep)
            }
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
  height: 500px;
}
.primaryColor--text{
  color:#E07A5F;
}
.secondaryColor--text{
  color:#2CA58D;
}
</style>