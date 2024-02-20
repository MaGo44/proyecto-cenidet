<template>
    <v-dialog
        :value="openDialogLocal"
        :width="width" 
        :persistent="$vuetify.breakpoint.smAndUp"
        :fullscreen="$vuetify.breakpoint.xsOnly" 
        :hide-overlay="$vuetify.breakpoint.xsOnly">
        <v-card class="card-border-rounded pa-2">
            <v-row justify="center" align="center" class="mt-5 mb-3">
                <v-icon color="green" size="100px">
                mdi-check-circle-outline
                </v-icon>
            </v-row>
            <v-card-title v-if="$slots.sectionContent">
                <v-row align="center" justify="center" class="text-title pa-4">
                    <slot name="sectionContent" />
                </v-row>
            </v-card-title>
            <v-card-actions>
                <v-spacer></v-spacer>
				        <v-btn 
                  width="20%"
                  outlined
                  color="#2CA58D"
                  class="border-rounded text-none"
                  @click.prevent="$emit('close')">Cerrar</v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
</template>
<script>
export default {
  props: {
    // title: {
    //   type: String,
    //   required: true
    // },
    width: {
      type: String,
      required: true
    },
    isOpenDialog: {
      type: Boolean,
      required: false,
      default: false,
    },
  },
  data () {
		return {
			openDialogLocal: this.isOpenDialog
		}
	},
	watch: {
		isOpenDialog (value) {
			this.openDialogLocal = value
		}
	},
	methods: {}
}
</script>