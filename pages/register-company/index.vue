<template>
    <div class="container_main" style="height: 100%">
        <v-container>
        <v-row align="center" justify="center" class="margin-row container_main">
            <v-col>
                <v-card>
                    <v-col class="pt-5"> 
                        <h2 class="font-weight-regular">
                            Registro de unidad económica
                        </h2>
                        <v-form>
                            <v-row>
                                <v-col cols="12" class="pb-0 mt-5">
                                    <v-text-field 
                                        v-model="companyForm.company_name"
                                        maxlength="100"
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Nombre de la unidad económica" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_business_name" 
                                        outlined
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Razón social" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_address" 
                                        outlined
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Dirección de la unidad económica" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_postal_code"
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Código postal" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_colony"
                                        outlined
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Colonia" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_location"
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Localidad" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_municipality"
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Municipio" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field
                                        v-model="companyForm.company_state" 
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Estado" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_external_number" 
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Numero exterior" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_country" 
                                        outlined
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="País" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_representative_name" 
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Nombre del representante" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_contact_name" 
                                        outlined
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Nombre del contacto" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-select
                                        v-model="companyForm.company_contact_max_studies" 
                                        :items="studies"
                                        name="grade_name"
                                        item-value="grade_id"
                                        item-text="grade_name"
                                        outlined 
                                        label="Estudios máximos" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_contact_position" 
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Cargo o puesto" />
                                </v-col>
                                <v-col cols="4" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_tel" 
                                        outlined 
                                        maxlength="10"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => /^[0-9]+$/.test(v) || 'Ingrese un número de teléfono válido']"
                                        label="Teléfono fijo" />
                                </v-col>
                                <v-col cols="2" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_tel_ext" 
                                        outlined 
                                        label="Extension" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_cel"  
                                        outlined 
                                        maxlength="10"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => /^[0-9]+$/.test(v) || 'Ingrese un número de teléfono válido']"
                                        label="Teléfono celular" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_email"  
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => /.+@.+\..+/.test(v) || 'Ingrese una dirección de correo válida']"
                                        label="Correo" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_second_email"  
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => /.+@.+\..+/.test(v) || 'Ingrese una dirección de correo válida']"
                                        label="Segundo correo" />
                                </v-col>
                                <v-col :cols="(companyForm.company_agreement_status==2) || (companyForm.company_agreement_status==3)? 3 : 6" class="pb-0 pt-0">
                                    <v-select
                                        v-model="companyForm.company_agreement_status" 
                                        :items="agreement_status"
                                        name="status_name"
                                        item-value="status_id"
                                        item-text="status_name"
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Estatus del convenio" />
                                </v-col>
                                <v-col v-if="(companyForm.company_agreement_status==2) || (companyForm.company_agreement_status==3)" cols="3" class="pb-0 pt-0">
                                    <v-menu
                                        v-model="menu"
                                        :close-on-content-click="false"
                                        transition="scale-transition"
                                        offset-y
                                        min-width="auto"
                                    >
                                        <template v-slot:activator="{ on, attrs }">
                                        <v-text-field
                                            v-model="companyForm.company_agreement_date"  
                                            label="Fecha del convenio"
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
                                        v-model="companyForm.company_agreement_date" 
                                        no-title
                                        @input="menu = false"
                                        >
                                        </v-date-picker>
                                    </v-menu>
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_vacants_number"  
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Número de vacantes" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-textarea 
                                        v-model="companyForm.company_observation_desc"  
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Observaciones" />
                                </v-col>
                            </v-row>
                            <v-btn
                                width="20%"
                                outlined
                                color="#2CA58D"
                                class="border-rounded text-none"
                                @click="saveCompany()">
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
import axios from "axios";
export default {
    layout: "adminLayout",
    data() {
        return{
            token: '9260023c-3deb-4b2d-bb8d-bb595bbff9fc',
            studies:[],
            menu: false,
            agreement_status:[],
            companyForm:{}
        }
    },
    created(){
        axios.get('http://localhost:3100/api/scholar_grades',{
            headers:{
                'authorization':`Bearer ${this.token}`
            }
        }).then((response)=>{
            if(response.status === 200){
                this.studies=response.data
            }
            else{
            	console.log(response.status)
            }
        })

        axios.get('http://localhost:3100/api/agreement_status',{
            headers:{
                'authorization':`Bearer ${this.token}`
            }
        }).then((response)=>{
            if(response.status === 200){
                this.agreement_status=response.data
            }
            else{
            	console.log(response.status)
            }
        })  
    },
    methods:{
        async saveCompany(){
           await axios.post('http://localhost:3100/api/company_info', this.companyForm,{
               headers:{
                   'authorization':`Bearer ${this.token}`,
                   'content-type': 'application/json'
               }
           }).then((response)=>{
               if(response.status==="200"){
                  console.log('Todo bien');
               }
               else{
                console.log(response.status);
               }
           })
        }
    }
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