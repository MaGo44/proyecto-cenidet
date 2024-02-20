<template>
                    <v-dialog
                        :value="openDialogLocal"
                        :width="width" 
                        :persistent="$vuetify.breakpoint.smAndUp"
                        :fullscreen="$vuetify.breakpoint.xsOnly" 
                        :hide-overlay="$vuetify.breakpoint.xsOnly">
                        <v-card class="card-border-rounded pa-2">
                        <v-card-title class="text-title pa-6 pb-0">
                            Editar unidad económica
                            <v-spacer />
                            <div class="d-flex align-center">
                                <v-icon
                                    small
                                    color="#4F4F4F"
                                    @click.prevent="closeDialog()">
                                    mdi-close
                                </v-icon>
                            </div>
                        </v-card-title>
                            <v-row no-gutters class="pa-6 pb-0">
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
                                        label="Número exterior" />
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
                                        v-model.number="companyForm.company_tel_ext" 
                                        outlined 
                                        label="Extensión" />
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
                                        v-model.number="companyForm.company_vacants_number"  
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
                            <v-card-actions>
                                <v-spacer></v-spacer>
                                <v-btn
                                    width="20%"
                                    outlined
                                    color="#2CA58D"
                                    class="border-rounded text-none"
                                    @click="editCompany()">
                                        Guardar
                                </v-btn>
                            </v-card-actions>
                    </v-card>
                </v-dialog>
</template>
<script>
export default {
  props: {
    title: {
      type: String,
      required: true
    },
    width: {
      type: String,
      required: true
    },
    company: {
      type: Object,
      required: true
    },
    careers: {
        type: Array,
        required: true,
    },
    agreement_status: {
        type: Array,
        required: true,
    },
   studies: {
        type: Array,
        required: true,
    },
    isOpenDialog: {
      type: Boolean,
      required: false,
      default: false,
    },
  },
  data () {
		return {
			openDialogLocal: this.isOpenDialog,
            companyForm: {},
		}
	},
	watch: {
		isOpenDialog (value) {
			this.openDialogLocal = value
            if(value===true){
                this.companyForm=this.company
            }
		}
	},
    created(){
        // console.log(this.adviser,'holaaa')
        // this.adviserForm=this.adviser
        // console.log(this.adviserForm,'holaaa')
    },
	methods: {
        editCompany(){
            // Clonar el objeto companyForm para evitar modificar el original
            const editedCompanyForm = Object.assign({}, this.companyForm);
            // Convertir el formato de la fecha si es necesario
            if (editedCompanyForm.company_agreement_date) {
                const fecha = new Date(editedCompanyForm.company_agreement_date);
                editedCompanyForm.company_agreement_date = fecha.toISOString().split('T')[0];
            }
            // Emitir el objeto modificado
            this.$emit('edit-company', editedCompanyForm);
            this.closeDialog();
        },
        closeDialog(){
            this.openDialogLocal = false
            this.$emit('close-dialog')
            this.companyForm={}
        }
    }
}
</script>
