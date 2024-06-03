<template>
    <div class="container_main" style="height: 100%">
        <v-container>
        <v-row align="center" justify="center" class="margin-row container_main">
            <v-col>
                <v-card>
                    <v-col class="pt-5"> 
                        <h2 class="primaryColor--text font-weight-regular">
                            Registro de estudiante
                        </h2>
                        <v-form>
                            <v-row>
                                <v-col cols="12" class="text-center pt-5 d-flex align-center">
                                    <v-card
                                        class="elevation-0 grey lighten-2 mx-auto"
                                        style="width: 150px; height: 150px; position: relative;"
                                    >
                                        <div
                                            v-if="fotoPerfil"
                                            :style="{ 'background-image': `url(${fotoPerfil})`, 'background-size': 'cover', 'background-position': 'center', 'width': '100%', 'height': '100%' }"
                                        ></div>
                                        <div v-else style="width: 100%; height: 100%; display: flex; align-items: center; justify-content: center;">
                                            Subir foto
                                        </div>
                                    </v-card>
                                </v-col>
                                <v-col cols="12">
                                    <input ref="fileInput" type="file" @input="pickFile">
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-select
                                        v-model="studentForm.student_period_id" 
                                        :items="periods"
                                        item-value="period_id"
                                        item-text="period_name"
                                        outlined 
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']"
                                        label="Periodo" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field
                                        v-model="studentForm.student_name"  
                                        outlined 
                                        label="Nombre"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="studentForm.student_last_name"  
                                        outlined 
                                        label="Apellido paterno"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="studentForm.student_second_last_name"  
                                        outlined 
                                        label="Apellido materno"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="studentForm.student_control_num"  
                                        outlined 
                                        label="No.Control"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="studentForm.student_curp"  
                                        outlined 
                                        label="CURP"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => (/[A-Z]{4}\d{6}[HM]{1}[A-Z]{2}[A-Z]{3}\d{2}$/).test(v) || 'La CURP no tiene el formato válido']" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-select
                                        v-model="studentForm.student_career_id"  
                                        outlined 
                                        :items="careers"
                                        item-value="career_id"
                                        item-text="career_name"
                                        label="Carrera"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-select
                                        v-model="studentForm.student_sex_id"  
                                        outlined 
                                        :items="genders"
                                        item-value="gender_id"
                                        item-text="gender_name"
                                        label="Sexo"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="studentForm.student_email"  
                                        outlined 
                                        label="Correo institucional"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => /.+@.+\..+/.test(v) || 'Ingrese una dirección de correo válida']" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="studentForm.student_second_email" 
                                        outlined 
                                        label="Correo personal"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => /.+@.+\..+/.test(v) || 'Ingrese una dirección de correo válida']" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="studentForm.student_phone" 
                                        outlined 
                                        maxlength="10"
                                        label="Telefono fijo"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => /^[0-9]+$/.test(v) || 'Ingrese un número de teléfono válido']" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="studentForm.student_cel_phone" 
                                        outlined 
                                        maxlength="10"
                                        label="Telefono celular"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => /^[0-9]+$/.test(v) || 'Ingrese un número de teléfono válido']" />
                                </v-col>
                                <v-col cols="3" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="studentForm.student_avg" 
                                        outlined 
                                        label="Promedio"
                                        required
                                        maxlength="2"
                                        :rules="[v => !!v || 'Este campo es requerido', v => /^\d+$/.test(v) || 'Este campo solo acepta números']" />
                                </v-col>
                                <v-col cols="3" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="studentForm.student_credits" 
                                        outlined 
                                        label="Creditos acum"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => /^\d+$/.test(v) || 'Este campo solo acepta números']" />
                                </v-col>
                                <v-col cols="3" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="studentForm.student_semester" 
                                        outlined 
                                        maxlength="2"
                                        label="Semestre"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => /^\d+$/.test(v) || 'Este campo solo acepta números']" />
                                </v-col>
                                <v-col cols="3" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="studentForm.student_studies_code" 
                                        outlined 
                                        label="Clave plan de estudios"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
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
            periods:[],
            genders:[],
            studies:[],
            careers:[],
            studentForm:{}
        }
    },
    created(){
        axios.get('https://api.render.com/deploy/srv-cpco0pm3e1ms73f15r7g?key=2Nh1yQxD5ag/api/periods',{
            headers:{
                'authorization':`Bearer ${this.token}`
            }
        }).then((response)=>{
            if(response.status === 200){
                this.periods=response.data
            }
            else{
            	console.log(response.status)
            }
        })

        axios.get('http://localhost:3100/api/genders',{
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

        axios.get('http://localhost:3100/api/careers',{
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
           await axios.post('http://localhost:3100/api/internal_adviser_info', this.studentForm,{
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