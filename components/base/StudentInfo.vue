<template>
    <div class="row-style">
        <v-row align="center" justify="center" class="row-margin">
            <v-col cols="12">
                <v-card>
                    <v-col class="pt-5"> 
                        <h2 class="primaryColor--text font-weight-regular">
                            Datos del estudiante
                        </h2>
                        <v-form ref="form">
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
                                <v-col cols="12" class="pb-0">
                                    <v-text-field
                                        v-model="registerStudentInfo.student_name"  
                                        outlined 
                                        label="Nombre"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="registerStudentInfo.student_last_name"  
                                        outlined 
                                        label="Apellido paterno"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="registerStudentInfo.student_second_last_name"  
                                        outlined 
                                        label="Apellido materno"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="registerStudentInfo.student_control_num"  
                                        outlined 
                                        label="No.Control"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido']" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="registerStudentInfo.student_curp"  
                                        outlined 
                                        label="CURP"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => (/[A-Z]{4}\d{6}[HM]{1}[A-Z]{2}[A-Z]{3}\d{2}$/).test(v) || 'La CURP no tiene el formato válido']" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-select
                                        v-model="registerStudentInfo.student_career_id"  
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
                                        v-model="registerStudentInfo.student_sex_id"  
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
                                        v-model="registerStudentInfo.student_email"  
                                        outlined 
                                        label="Correo institucional"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => /.+@.+\..+/.test(v) || 'Ingrese una dirección de correo válida']" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="registerStudentInfo.student_second_email" 
                                        outlined 
                                        label="Correo personal"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => /.+@.+\..+/.test(v) || 'Ingrese una dirección de correo válida']" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="registerStudentInfo.student_phone" 
                                        outlined 
                                        maxlength="10"
                                        label="Telefono fijo"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => /^[0-9]+$/.test(v) || 'Ingrese un número de teléfono válido']" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="registerStudentInfo.student_cel_phone" 
                                        outlined 
                                        maxlength="10"
                                        label="Telefono celular"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => /^[0-9]+$/.test(v) || 'Ingrese un número de teléfono válido']" />
                                </v-col>
                                <v-col cols="3" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="registerStudentInfo.student_avg" 
                                        outlined 
                                        label="Promedio"
                                        required
                                        maxlength="2"
                                        :rules="[v => !!v || 'Este campo es requerido', v => /^\d+$/.test(v) || 'Este campo solo acepta números']" />
                                </v-col>
                                <v-col cols="3" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="registerStudentInfo.student_credits" 
                                        outlined 
                                        label="Creditos acum"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => /^\d+$/.test(v) || 'Este campo solo acepta números']" />
                                </v-col>
                                <v-col cols="3" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="registerStudentInfo.student_semester" 
                                        outlined 
                                        maxlength="2"
                                        label="Semestre"
                                        required
                                        :rules="[v => !!v || 'Este campo es requerido', v => /^\d+$/.test(v) || 'Este campo solo acepta números']" />
                                </v-col>
                                <v-col cols="3" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="registerStudentInfo.student_studies_code" 
                                        outlined 
                                        label="Clave plan de estudios"
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
import axios from "axios";
export default {
    props: {
        eventNextStep: {
            type: String,
            required: true,
        },
        careers: {
            type: Array,
            required: true,
        },
        genders: {
            type: Array,
            required: true,
        },
    },
    data() {
        return{
            registerStudentInfo:{},
            fotoPerfil: null,
            token: '9260023c-3deb-4b2d-bb8d-bb595bbff9fc',
        }
    },
    methods:{
        nextStep() {
            const valid=this.$refs.form.validate()
            if(valid){
                this.$emit('set-student-info',this.registerStudentInfo)
                
                this.$nuxt.$emit(this.eventNextStep)
            }
            // this.$emit('set-student-info',this.registerStudentInfo)
            //     this.$nuxt.$emit(this.eventNextStep)
        },
        selectImage () {
          this.$refs.fileInput.click()
        },
        pickFile() {
            const input = this.$refs.fileInput;
            const file = input.files;

            if (file && file[0]) {
                const reader = new FileReader();

                reader.onload = (e) => {
                    this.fotoPerfil = e.target.result;
                    this.registerStudentInfo.file_name = file[0].name; // Guardar el nombre del archivo
                };

                reader.readAsDataURL(file[0]);
                this.$emit('input', file[0]);
            }
        },
        async submitFiles(studentId) {
        await console.log(studentId,'llego');
        try {
            const formData = new FormData();
            formData.append('student_id', studentId);

            const fileData = this.fotoPerfil;

            if (fileData) {
                // Convertir los datos base64 en un objeto de tipo Blob
                const blob = await fetch(fileData).then(res => res.blob());

                formData.append('document_type_id', 1);
                formData.append('profile_pic_file_name', this.registerStudentInfo.file_name);
                formData.append('alias', this.registerStudentInfo.file_name);
                formData.append('fotoPerfil', blob, this.registerStudentInfo.file_name);

                console.log(formData);

                // Envía el formData al backend utilizando una solicitud HTTP (por ejemplo, utilizando Axios)
                const response = await axios.post(
                    'http://localhost:3100/api/student_profile_pic',
                    formData,
                    {
                        headers: {
                            authorization: `Bearer ${this.token}`,
                            'content-type': 'multipart/form-data',
                        },
                    }
                );

                if (response.status === 200) {
                    console.log('Archivo subido exitosamente:', response.data);
                } else {
                    console.log('Error al subir archivo:', response.status);
                }
            }
        } catch (error) {
            console.error('Error al subir archivos:', error);
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