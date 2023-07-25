<template>
    <div class="container_main" style="height: 100%">
        <v-container>
        <v-row align="center" justify="center" class="margin-row container_main">
            <v-col>
                <v-card>
                    <v-col class="pt-5"> 
                        <h2 class="font-weight-regular">
                            Registro de unidad economica
                        </h2>
                        <v-form>
                            <v-row>
                                <v-col cols="12" class="pb-0 mt-5">
                                    <v-text-field 
                                        v-model="companyForm.company_name" 
                                        outlined 
                                        label="Nombre de la unidad economica" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_business_name" 
                                        outlined 
                                        label="Razón social" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_address" 
                                        outlined 
                                        label="Dirección de la unidad economica" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_postal_code"
                                        outlined 
                                        label="Código postal" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_colony"
                                        outlined 
                                        label="Colonia" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_location"
                                        outlined 
                                        label="Localidad" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_municipality"
                                        outlined 
                                        label="Municipio" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field
                                        v-model="companyForm.company_state" 
                                        outlined 
                                        label="Estado" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_external_number" 
                                        outlined 
                                        label="Numero exterior" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_country" 
                                        outlined 
                                        label="País" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_representative_name" 
                                        outlined 
                                        label="Nombre del representante" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_contact_name" 
                                        outlined 
                                        label="Nombre del contacto" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_contact_max_studies" 
                                        outlined 
                                        label="Estudios máximos" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_contact_position" 
                                        outlined 
                                        label="Cargo o puesto" />
                                </v-col>
                                <v-col cols="4" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_tel" 
                                        outlined 
                                        label="Teléfono fijo" />
                                </v-col>
                                <v-col cols="2" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_tel" 
                                        outlined 
                                        label="Extension" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_cel"  
                                        outlined 
                                        label="Teléfono celular" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_email"  
                                        outlined 
                                        label="Correo" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_second_email"  
                                        outlined 
                                        label="Segundo correo" />
                                </v-col>
                                <v-col :cols="companyForm.company_agreement_status=='true'? 3 : 6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_agreement_status"  
                                        outlined 
                                        label="Tiene convenio?" />
                                </v-col>
                                <v-col v-if="companyForm.company_agreement_status=='true'" cols="3" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_agreement_status"  
                                        outlined 
                                        label="Fecha de convenio" />
                                </v-col>
                                <v-col cols="6" class="pb-0 pt-0">
                                    <v-text-field 
                                        v-model="companyForm.company_vacants_number"  
                                        outlined 
                                        label="Número de vacantes" />
                                </v-col>
                                <v-col cols="12" class="pb-0 pt-0">
                                    <v-textarea 
                                        v-model="companyForm.company_observation_desc"  
                                        outlined 
                                        label="Observaciones" />
                                </v-col>
                            </v-row>
                            <v-btn
                                width="20%"
                                outlined
                                color="#2CA58D"
                                class="border-rounded text-none"
                                @click="nextStep()">
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
export default {
    layout: "adminLayout",
    data() {
        return{
            companyForm:{
                
            }
        }
    },
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