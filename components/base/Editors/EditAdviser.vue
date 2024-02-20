<template>
                    <v-dialog
                        :value="openDialogLocal"
                        :width="width" 
                        :persistent="$vuetify.breakpoint.smAndUp"
                        :fullscreen="$vuetify.breakpoint.xsOnly" 
                        :hide-overlay="$vuetify.breakpoint.xsOnly">
                        <v-card class="card-border-rounded pa-2">
                        <v-card-title class="text-title pa-6 pb-0">
                            Editar asesor interno
                            <v-spacer />
                            <div class="d-flex align-center">
                                <v-icon
                                    small
                                    color="#4F4F4F"
                                    @click.prevent="closeDialog()">
                                    close
                                </v-icon>
                            </div>
                        </v-card-title>
                        <v-row no-gutters class="pa-6 pb-0">
                            <v-col cols="12" class="pb-0 mt-5">
                                            <v-text-field 
                                                v-model="adviserForm.internal_name" 
                                                outlined 
                                                required
                                                :rules="[v => !!v || 'Este campo es requerido']"
                                                label="Nombre del asesor interno" />
                                        </v-col>
                                        <v-col cols="6" class="pb-0 pt-0">
                                            <v-text-field 
                                                v-model="adviserForm.internal_last_name" 
                                                outlined 
                                                required
                                                :rules="[v => !!v || 'Este campo es requerido']"
                                                label="Apellido paterno" />
                                        </v-col>
                                        <v-col cols="6" class="pb-0 pt-0">
                                            <v-text-field 
                                                v-model="adviserForm.internal_second_last_name" 
                                                outlined 
                                                required
                                                :rules="[v => !!v || 'Este campo es requerido']"
                                                label="Apellido materno" />
                                        </v-col>
                                        <v-col cols="6" class="pb-0 pt-0">
                                            <v-select
                                                v-model="adviserForm.internal_sex_id" 
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
                                                v-model="adviserForm.internal_scholar_grade" 
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
                                                v-model="adviserForm.internal_phone" 
                                                outlined 
                                                required
                                                maxlength="10"
                                                :rules="[v => !!v || 'Este campo es requerido', v => /^[0-9]+$/.test(v) || 'Ingrese un número de teléfono válido']"
                                                label="Teléfono fijo" />
                                        </v-col>
                                        <v-col cols="6" class="pb-0 pt-0">
                                            <v-text-field 
                                                v-model="adviserForm.internal_cel_phone" 
                                                outlined 
                                                required
                                                maxlength="10"
                                                :rules="[v => !!v || 'Este campo es requerido', v => /^[0-9]+$/.test(v) || 'Ingrese un número de teléfono válido']"
                                                label="Teléfono celular" />
                                        </v-col>
                                        <v-col cols="12" class="pb-0 pt-0">
                                            <v-select
                                                v-model="adviserForm.internal_adscription_career" 
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
                                                v-model="adviserForm.internal_email" 
                                                outlined 
                                                required
                                                :rules="[v => !!v || 'Este campo es requerido', v => /.+@.+\..+/.test(v) || 'Ingrese una dirección de correo válida']"
                                                label="Correo institucional" />
                                        </v-col>
                                        <v-col cols="12" class="pb-0 pt-0">
                                            <v-text-field 
                                                v-model="adviserForm.internal_second_email" 
                                                outlined 
                                                required
                                                :rules="[v => !!v || 'Este campo es requerido', v => /.+@.+\..+/.test(v) || 'Ingrese una dirección de correo válida']"
                                                label="Segundo correo" />
                                        </v-col>
                        </v-row>
                        <v-row
                            no-gutters 
                            class="pa-6 pt-3"
                            justify="end">
                            <v-btn
                                tile
                                small
                                color="#2f80ed"
                                class="white--text btn__nxt" 
                                @click.prevent="editFeedback()">
                                Guardar
                            </v-btn>
                        </v-row>
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
    adviser: {
      type: Object,
      required: true
    },
    careers: {
        type: Array,
        required: true,
    },
    genders: {
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
            adviserForm: {}
		}
	},
	watch: {
		isOpenDialog (value) {
			this.openDialogLocal = value
            if(value===true){
                this.adviserForm=this.adviser
            }
		}
	},
    created(){
        // console.log(this.adviser,'holaaa')
        // this.adviserForm=this.adviser
        // console.log(this.adviserForm,'holaaa')
    },
	methods: {}
}
</script>
