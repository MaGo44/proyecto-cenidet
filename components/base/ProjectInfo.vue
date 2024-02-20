<template>
    <div class="row-style">
        <v-row align="center" justify="center" class="row-margin">
            <v-col cols="12">
                <v-card>
                    <v-col class="pt-5"> 
                        <h2 class="primaryColor--text font-weight-regular">
                            Datos de educación dual
                        </h2>
                        <v-form ref="form">
                            <v-row>
                                <v-col cols="12" class="pb-0 mt-5">
                                    <v-text-field 
                                        v-model="registerProjectInfo.project_name"  
                                        outlined 
                                        label="Nombre del proyecto"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-select
                                        v-model="registerProjectInfo.project_company_id"  
                                        :items="companies"
                                        item-value="company_id"
                                        item-text="company_name"
                                        outlined 
                                        label="Elige la unidad económica"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-menu
                                        v-model="menu"
                                        :close-on-content-click="false"
                                        transition="scale-transition"
                                        offset-y
                                        min-width="auto"
                                    >
                                        <template #activator="{ on, attrs }">
                                        <v-text-field
                                            v-model="registerProjectInfo.project_start_date"  
                                            label="Fecha de inicio"
                                            prepend-icon="mdi-calendar"
                                            readonly
                                            outlined
                                            required
                                            :rules="[v => !!v || 'Este campo es requerido']"
                                            v-bind="attrs"
                                            v-on="on"
                                        ></v-text-field>
                                        </template>
                                        <v-date-picker
                                        v-model="registerProjectInfo.project_start_date" 
                                        no-title
                                        @input="menu = false"
                                        >
                                        </v-date-picker>
                                    </v-menu>
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-menu
                                        v-model="menu2"
                                        :close-on-content-click="false"
                                        transition="scale-transition"
                                        offset-y
                                        min-width="auto"
                                    >
                                        <template #activator="{ on, attrs }">
                                        <v-text-field
                                            v-model="registerProjectInfo.project_finish_date" 
                                            label="Fecha de finalizacion"
                                            prepend-icon="mdi-calendar"
                                            readonly
                                            outlined
                                            required
                                            :rules="[v => !!v || 'Este campo es requerido']"
                                            v-bind="attrs"
                                            v-on="on"
                                        ></v-text-field>
                                        </template>
                                        <v-date-picker
                                        v-model="registerProjectInfo.project_finish_date" 
                                        no-title
                                        @input="menu2 = false"
                                        >
                                        </v-date-picker>
                                    </v-menu>
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="registerProjectInfo.project_position_name" 
                                        outlined 
                                        label="Puesto a desempenar"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="registerProjectInfo.project_area" 
                                        outlined 
                                        label="Departamento o area asignada"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="registerProjectInfo.project_external_adviser" 
                                        outlined 
                                        label="Nombre del asesor externo"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-select
                                        v-model="registerProjectInfo.project_internal_adviser_id" 
                                        outlined 
                                        :items="advisers"
                                        item-value="internal_adviser_id"
                                        item-text="internal_name"
                                        label="Elige tu asesor interno"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-select
                                        v-model="registerProjectInfo.project_contract_status" 
                                        outlined 
                                        :items="contractStatus"
                                        item-value="status_id"
                                        item-text="status_name"
                                        label="Fuiste contratado por tu empresa?"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-textarea 
                                        v-model="registerProjectInfo.project_objective_desc"
                                        outlined 
                                        label="Objetivo del proyecto"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-textarea 
                                        v-model="registerProjectInfo.project_desc"
                                        outlined 
                                        label="Descripcion del proyecto"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-textarea 
                                        v-model="registerProjectInfo.project_problem_desc"
                                        outlined 
                                        label="Problema que se espera resolver"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-textarea 
                                        v-model="registerProjectInfo.project_results_desc"
                                        outlined 
                                        label="Resultados esperados"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-textarea 
                                        v-model="registerProjectInfo.project_product_desc"
                                        outlined 
                                        label="Producto final"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
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
        companies: {
            type: Array,
            required: true,
        },
        advisers: {
            type: Array,
            required: true,
        },
    },
    data(){
        return{
            registerProjectInfo:{},
            contractStatus:[
                {
                    status_id:0,
                    status_name:'Sí'
                },
                {
                    status_id:1,
                    status_name:'No'
                },
            ],
            menu: false,
            menu2: false,
        }
    },
    methods:{
        nextStep() {
            const valid=this.$refs.form.validate()
            if(valid){
                this.$emit('set-project-info',this.registerProjectInfo)
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
}
.primaryColor--text{
  color:#E07A5F;
}
.secondaryColor--text{
  color:#2CA58D;
}
</style>