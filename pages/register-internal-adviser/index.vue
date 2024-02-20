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
                                    <v-text-field 
                                        v-model="internalAdviserForm.internal_name" 
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Nombre del asesor interno" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="internalAdviserForm.internal_last_name" 
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Apellido paterno" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="internalAdviserForm.internal_second_last_name" 
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Apellido materno" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-select
                                        v-model="internalAdviserForm.internal_sex_id" 
                                        :items="genders"
                                        item-value="gender_id"
                                        item-text="gender_name"
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Sexo" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-select
                                        v-model="internalAdviserForm.internal_scholar_grade" 
                                        :items="studies"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        name="grade_name"
                                        item-value="grade_id"
                                        item-text="grade_name"
                                        outlined 
                                        label="Grado escolar" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="internalAdviserForm.internal_phone" 
                                        outlined 
                                        required
                                        maxlength="10"
                                        :rules="[v => !!v || 'Este campo es requerido', v => /^[0-9]+$/.test(v) || 'Ingrese un número de teléfono válido']"
                                        label="Teléfono fijo" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="internalAdviserForm.internal_cel_phone" 
                                        outlined 
                                        required
                                        maxlength="10"
                                        :rules="[v => !!v || 'Este campo es requerido', v => /^[0-9]+$/.test(v) || 'Ingrese un número de teléfono válido']"
                                        label="Teléfono celular" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-select
                                        v-model="internalAdviserForm.internal_adscription_career" 
                                        outlined
                                        :items="careers"
                                        item-value="career_id"
                                        item-text="career_name"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" 
                                        label="Carrera de adscripción" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="internalAdviserForm.internal_email" 
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => /.+@.+\..+/.test(v) || 'Ingrese una dirección de correo válida']"
                                        label="Correo institucional" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="internalAdviserForm.internal_second_email" 
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => /.+@.+\..+/.test(v) || 'Ingrese una dirección de correo válida']"
                                        label="Segundo correo" />
                                </v-col>
                            </v-row>
                            <v-btn
                                width="20%"
                                outlined
                                color="#2CA58D"
                                class="border-rounded text-none"
                                @click="saveInternalAdviser()">
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
            genders:[],
            studies:[],
            careers:[],
            internalAdviserForm:{}
        }
    },
    created(){
        axios.get('https://proyecto-cenidet-backend-production.up.railway.app/api/genders',{
            headers:{
                'authorization':`Bearer ${this.token}`
            }
        }).then((response)=>{
            if(response.status === 200){
                this.genders=response.data
            }
            else{
            	console.log(response.status)
            }
        })

        axios.get('https://proyecto-cenidet-backend-production.up.railway.app/api/scholar_grades',{
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

        axios.get('https://proyecto-cenidet-backend-production.up.railway.app/api/careers',{
            headers:{
                'authorization':`Bearer ${this.token}`
            }
        }).then((response)=>{
            if(response.status === 200){
                this.careers=response.data
            }
            else{
            	console.log(response.status)
            }
        })


    },
    methods:{
        async saveInternalAdviser(){
           await axios.post('https://proyecto-cenidet-backend-production.up.railway.app/api/internal_adviser_info', this.internalAdviserForm,{
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