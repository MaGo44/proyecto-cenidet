<template>
    <div class="row-style">
        <v-row align="center" justify="center" class="row-margin">
            <v-col cols="12">
                <v-card>
                    <v-col class="pt-5"> 
                        <h2 class="primaryColor--text font-weight-regular">
                            Documentos
                        </h2>
                        <v-form ref="form">
                            <v-row class="mb-2">
                                <v-col cols="12" class="pt-5 pb-0">
                                    <v-file-input
                                        v-model="cartaPresentacion"
                                        label="Carta de presentación"
                                        required
                                        outlined 
                                        :rules="[v => !!v || 'Este campo es requerido']" 
                                        variant="outlined" />
                                    <v-file-input 
                                        v-model="cartaAceptacion"
                                        label="Carta de aceptación"
                                        required
                                        outlined 
                                        :rules="[v => !!v || 'Este campo es requerido']" 
                                        variant="outlined" />
                                    <v-file-input 
                                        v-model="cv"
                                        label="CV"
                                        required
                                        outlined 
                                        :rules="[v => !!v || 'Este campo es requerido']" 
                                        variant="outlined" />
                                    <v-file-input 
                                        v-model="constanciaCreditos"
                                        label="Constancia de créditos con promedio"
                                        required
                                        outlined 
                                        :rules="[v => !!v || 'Este campo es requerido']" 
                                        variant="outlined" />
                                    <v-file-input
                                        v-model="constanciaMedico"
                                        label="Constancia de afiliación al servicio médico vigente"
                                        required
                                        outlined 
                                        :rules="[v => !!v || 'Este campo es requerido']" 
                                        variant="outlined" />
                                    <v-file-input 
                                        v-model="creditoIngles"
                                        label="Crédito de inglés"
                                        required
                                        outlined 
                                        :rules="[v => !!v || 'Este campo es requerido']" 
                                        variant="outlined" />
                                    <v-file-input
                                        v-model="servicioSocial" 
                                        label="Servicio social"
                                        required
                                        outlined 
                                        :rules="[v => !!v || 'Este campo es requerido']" 
                                        variant="outlined"/>
                                    <v-file-input
                                        v-model="creditosComplementarios"  
                                        label="Créditos complementarios"
                                        required
                                        outlined 
                                        :rules="[v => !!v || 'Este campo es requerido']" 
                                        variant="outlined" />
                                    <v-file-input
                                        v-model="constanciaAutorizacion"  
                                        label="Constancia de autorización del jefe de carrera"
                                        required
                                        outlined 
                                        :rules="[v => !!v || 'Este campo es requerido']" 
                                        variant="outlined" />
                                    <v-file-input
                                        v-model="anexo1"   
                                        label="Anexo 1"
                                        required
                                        outlined 
                                        :rules="[v => !!v || 'Este campo es requerido']" 
                                        variant="outlined" />
                                    <v-file-input
                                        v-model="anexo3"  
                                        label="Anexo 3"
                                        required
                                        outlined 
                                        :rules="[v => !!v || 'Este campo es requerido']" 
                                        variant="outlined" />
                                </v-col>
                            </v-row>
                            <v-btn
                                block
                                outlined
                                color="#2CA58D"
                                class="border-rounded text-none"
                                @click="submitFiles()">
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
        studentId: {
            type: String,
            required: true,
        },
    },
    data() {
        return{
            token: '9260023c-3deb-4b2d-bb8d-bb595bbff9fc',
            cartaPresentacion: null,
            cartaAceptacion: null,
            cv: null,
            constanciaCreditos: null,
            constanciaAfiliacion: null,
            creditoIngles: null,
            servicioSocial: null,
            creditosComplementarios: null,
            constanciaAutorizacion: null,
            anexo1: null,
            anexo3: null,
        }
    },
    methods:{
    async submitFiles() {
        try {
            const fileProps = ['cartaPresentacion', 'cartaAceptacion', 'cv', 'constanciaCreditos', 'constanciaAfiliacion', 'creditoIngles', 'servicioSocial', 'creditosComplementarios', 'constanciaAutorizacion', 'anexo1', 'anexo3'];

            for (let i = 0; i < fileProps.length; i++) {
            const formData = new FormData();
            formData.append('student_id', this.studentId);

            const propName = fileProps[i];
            const file = this[propName];
            if (file) {
                formData.append('document_type_id', i + 1);
                formData.append('document_file_name', file.name);
                formData.append('alias', file.name);
                formData.append('document_desc', propName);

                formData.append(propName, file);

                console.log(formData);

                // Envía el formData al backend utilizando una solicitud HTTP (por ejemplo, utilizando Axios)
                const response = await axios.post(
                'http://localhost:3100/api/student_documents',
                formData,
                {
                    headers: {
                    authorization: `Bearer ${this.token}`,
                    'content-type': 'multipart/form-data',
                    },
                }
                );

                if (response.status === 200) {
                    console.log(`Archivo ${propName} subido exitosamente:`, response.data);
                    this.$router.push('/dashboard');
                } else {
                    console.log(`Error al subir archivo ${propName}:`, response.status);
                }
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
  /* height: 500px; */
}
.primaryColor--text{
  color:#E07A5F;
}
.secondaryColor--text{
  color:#2CA58D;
}
</style>