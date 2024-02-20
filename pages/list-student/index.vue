<template>
	<v-container fluid>
		<v-row>
			<v-col cols="12">
				<v-row class="mb-3">
					<h1>Estudiantes inscritos en {{ periodSelected.period_name }}</h1>
					<v-spacer/>
					<v-menu offset-y>
						<template v-slot:activator="{ on, attrs }">
							<v-btn
							outlined
							v-bind="attrs"
							v-on="on"
							>
							Filtros
							</v-btn>
						</template>
						<v-list>
							<v-list-item>
            					<v-list-item-action>
									<v-select 
										v-model="careerSelected"
										:items="careers"
										item-value="career_id"
										item-text="career_name"
										label="Carrera"
										style="max-width:206px"
										:menu-props="{ openOnHover: true }"
										dense
										outlined
										single-line>
									</v-select>
									<v-select 
										v-model="periodSelected"
										:items="periods"
										item-text="period_name"
										label="Periodo"
										return-object
										class="mt-0 pt0"
										style="max-width:206px"
										:menu-props="{ openOnHover: true }"
										dense
										outlined
										single-line>
									</v-select>
									<v-select 
										v-model="genderSelected"
										:items="genders"
										item-value="gender_id"
										item-text="gender_name"
										label="Sexo"
										style="max-width:206px"
										:menu-props="{ openOnHover: true }"
										dense
										outlined
										single-line>
									</v-select>
								</v-list-item-action>
							</v-list-item>
						</v-list>
					</v-menu>
				</v-row>
			</v-col>
			<v-col cols="12" class="pt-0">
				<BaseDataTable
					:headers="headers"
					:items="filteredStudents"
					:search="search"
					:show-pagination="true"
					:is-loading="loadingData"
					:is-enabled="isEnabled"
					:total-pages="totalPages"
					:current-page.sync="currentPage" 
					title-export="Listado de personas"
					:per-page="perPage"
					download-csv="EVENT_DOWNLOAD_CSV_PERSONS"
					download-pdf="EVENT_DOWNLOAD_PDF_PERSONS"
					height="calc(100vh - 300px)">
					<template #[`item.profile_pic`]="{ item }">
						<div class="d-flex align-center py-2">
							<span>
								<span>
									<img :src="'/Users/owner/Downloads/' + item.alias" alt="Profile Image">
								</span>
								<!-- <v-chip v-if="getDays(item) && (item.attended == 0 || item.attended == null)" class="ma-0 px-2 chip-new" x-small color="turquoisePrimary">
									Nuevo
								</v-chip> -->
							</span>
						</div>
					</template>
					<template #[`item.name`]="{ item }">
						<div class="d-flex align-center py-2">
							<span>
								<span>
									{{ item.name }}
								</span>
								<!-- <v-chip v-if="getDays(item) && (item.attended == 0 || item.attended == null)" class="ma-0 px-2 chip-new" x-small color="turquoisePrimary">
									Nuevo
								</v-chip> -->
							</span>
						</div>
					</template>
					<template #[`item.student_last_name`]="{ item }">
						<div class="d-flex align-center py-2">
							<span>
								<span>
									{{ item.student_last_name }} {{ item.student_second_last_name }}
								</span>
								<!-- <v-chip v-if="getDays(item) && (item.attended == 0 || item.attended == null)" class="ma-0 px-2 chip-new" x-small color="turquoisePrimary">
									Nuevo
								</v-chip> -->
							</span>
						</div>
					</template>
					<template #[`item.student_sex_id`]="{ item }">
						<div class="d-flex align-center py-2">
							<span>
								<span v-if="item.student_sex_id===1">
									Hombre
								</span>
								<span v-else>
									Mujer
								</span>
								<!-- <v-chip v-if="getDays(item) && (item.attended == 0 || item.attended == null)" class="ma-0 px-2 chip-new" x-small color="turquoisePrimary">
									Nuevo
								</v-chip> -->
							</span>
						</div>
					</template>
					<template #[`item.student_career`]="{ item }">
						<div class="d-flex align-center py-2">
								<span>
									{{ item.career_name }}
								</span>
						</div>
					</template>
					<template #[`item.project_name`]="{ item }">
						<div class="d-flex align-center py-2">
							<span>
								<span>
									{{ item.project_name }}
								</span>
							</span>
						</div>
					</template>
					<template #[`item.company_name`]="{ item }">
						<div class="d-flex align-center py-2">
							<span>
								<span>
									{{ item.company_name }}
								</span>
							</span>
						</div>
					</template>
					<!-- <template v-slot:[`item.createdAt`]="{ item }">
						<span>{{ getDate(item.createdAt) }}</span>
					</template> -->
					<template #[`item.email`]="{ item }">
						<div class="d-flex align-center py-2">
							<span>{{ item.email == '' || item.email == null ? 'Correo no proporcionado' : item.email }}</span>
						</div>
					</template>
					<template #[`item.emailVerified`]="{ item }">
						<div class="d-flex align-center py-2">
							<v-chip 
								class="border-rounded px14 font-weight-medium"
								outlined
								:color="item.emailVerified == 1 ? 'success' : 'neutral1Primary'">
								{{ item.emailVerified == 1 ? 'Verificado' : 'No verificado' }}
							</v-chip>
						</div>
					</template>
					<template #[`item.phone`]="{ item }">
						<span>{{ item.phone }}</span>
					</template>
					<template #[`item.adminAccountId`]="{ item }">
						<div class="d-flex align-center py-2">
							<v-avatar
								v-if="item.adminAccountId != null && item.adminName != ''"
								tile
								:size="30"
								class="mr-2">
								<v-img
									:src="profilePicturePath + item.adminProfilePicture" />
							</v-avatar>
							<span 
								v-if="item.adminAccountId != null && item.adminName != ''">
								{{ item.adminName }}
							</span>
							<span v-else>Registro propio</span>
						</div>
					</template>
					<template #[`item.subaccount`]="{ item }">
						<div 
							v-if="item.assignedAdmin != null && !item.callApiSubaccount && item.assignedAdmin.id ==
								$store.getters['auth/getAdministratorId']" 
							class="d-flex align-center py-2">
							<v-avatar
								tile
								:size="30"
								class="mr-2">
								<v-img
									:src="profilePicturePath + item.subaccountImage" />
							</v-avatar>
							{{ item.subaccountName }}
						</div>
						<div v-else>
							<div v-if="!item.callApiSubaccount" class="pa-3">
								<span 
									v-if="$store.getters['auth/getAdministratorTypeId'] == 1"
									class="link-hover"
									@click.prevent="changeSubaccount(item)">
									Asignarme
								</span>
								<v-select
									v-else-if="$store.getters['auth/getAdministratorTypeId'] == null"
									v-model="item.assignedAdmin"
									:items="subaccounts"
									hide-details
									item-value="id"
									return-object
									dense
									hide-selected
									append-icon="expand_more"
									item-text="name"
									class="br-0"
									@input="changeSubaccount(item)">
									<template #selection="{ item }">
										<div class="d-flex align-center py-2">
											<v-avatar
												tile
												:size="30"
												class="mr-2">
												<v-img
													:src="profilePicturePath + item.profilePicture" />
											</v-avatar>
											<span class="px14 font-weight-medium">{{ item.name }}</span>
										</div>
									</template>
									<template #item="{ item }">
										<template>
											<v-list-item-content>
												<v-list-item-title>
													<div class="d-flex align-center py-2">
														<v-avatar
															tile
															:size="30"
															class="mr-2">
															<v-img
																:src="profilePicturePath + item.profilePicture" />
														</v-avatar>
														<span class="px14 font-weight-medium">{{ item.name }}</span>
													</div>
												</v-list-item-title>
											</v-list-item-content>
										</template>
									</template>
								</v-select>
							</div>
							<v-icon 
								v-else
								small>
								fas fa-circle-notch fa-spin
							</v-icon>
						</div>
					</template>
					<template #[`item.status`]="{ item }">
						<div v-if="!item.callApiAttended" class="text-center pa-3 pt-6">
							<v-select
								v-if="(item.attended != null && $store.getters['auth/getAccountIdOriginal'] == null) || (item.attended != null && item.assignedAdmin.id == $store.getters['auth/getAdministratorId'])"
								v-model="item.attended"
								:items="attendedItems"
								hide-details
								item-value="id"
								dense
								hide-selected
								color="colorPrimary"
								append-icon="expand_more"
								item-text="text"
								class="br-0"
								@input="changeAttended(item)">
								<template #selection="{ item }">
									<span class="px14 font-weight-medium">{{ item.text }}</span>
								</template>
							</v-select>
							<span
								v-else-if="item.attended != null"
								class="px14 font-weight-medium">
								{{ item.attended == 1 ? 'Atendido' : 'Por atender' }}
							</span>
						</div>
						<v-icon 
							v-else
							small>
							fas fa-circle-notch fa-spin
						</v-icon>
					</template>
					<template #[`item.action`]="{ item }">
						<div class="align-center d-flex">
							<v-tooltip 
								top
								class="mr-2"
								content-class="custom-tooltip">
								<template #activator="{ on }">
									<v-icon 
										v-on="on"
										@click.prevent="open(item)">
										mdi-pencil
									</v-icon>
								</template>
								<span>Editar</span>
							</v-tooltip>
							<v-tooltip 
								top 
								content-class="custom-tooltip">
								<template #activator="{ on }">
									<v-icon 
										v-on="on"
										@click.prevent="deleteDialog=true">
										mdi-trash-can
									</v-icon>
								</template>
								<span>Eliminar</span>
							</v-tooltip>
						</div>
					</template>
				</BaseDataTable>
			</v-col>
		</v-row>
		<v-dialog
			v-model="deleteDialog"
			width="30%"
			>
			<v-card>
				<v-card-title>
					¿Desea continuar?
				</v-card-title>
				<v-row justify="center" align="center" class="mt-3 mb-3">
					<v-icon color="yellow" size="100px">
					mdi-alert-circle-outline
					</v-icon>
				</v-row>
				<v-card-actions>
					<v-spacer></v-spacer>
					<v-btn color="primary" text @click="deleteDialog = false">Cancelar</v-btn>
					<v-btn color="primary" @click="closeDownloadInfoDialog()">Eliminar</v-btn>
				</v-card-actions>
			</v-card>
		</v-dialog>
		<base-dialog 
			:is-open-dialog="downloadInfoDialog"
			:title="titleDialog" 
			width="350"
			@close="closeDownloadInfoDialog()">
			<template #sectionContent>
				<v-row no-gutters justify="center">
					<v-progress-circular
						indeterminate
						color="colorPrimary" />
				</v-row>
				<v-row no-gutters justify="center" class="pt-3">
					<span class="item-text" style="text-align: center;">
						Procesando información. La descarga comenzará automáticamente
					</span>
				</v-row>
				<v-row no-gutters justify="center" class="pt-3">
					<v-btn
						color="colorPrimary"
						small
						class="font-weight-light text-none px14 px-2 whitePrimary--text"
						@click.prevent="closeDownloadInfoDialog()">
						Aceptar
					</v-btn>
				</v-row>
			</template>
			<template #sectionActions />
		</base-dialog>
		<v-dialog
			v-model="feedbackDialog"
			max-width="500"
			@input="closeFeedbackDialog()">
			<v-card v-if="feedbackInfo != undefined" tile>
				<v-card-title class="text-title pa-6 pb-0">
					Comentarios
					<v-spacer />
					<div class="d-flex align-center">
						<v-icon
							small
							color="#4F4F4F"
							@click.prevent="closeFeedbackDialog()">
							close
						</v-icon>
					</div>
				</v-card-title>
				<v-row no-gutters class="pa-6 pb-0">
					<span>
						<span class="contact-info-text">
							Comentarios sobre
						</span> 
						<span 
							:style="{ color: primaryColor }"
							class="contact-info-text">
							{{ feedbackInfo.personName }}
						</span>
					</span>
				</v-row>
				<div v-if="!isCreateFeedback && !isEditFeedback">
					<v-row 
						v-for="(item, index) in feedbackInfo.feedback" 
						:key="index"
						no-gutters 
						class="pa-6 pb-0">
						<v-col 
							:cols="isEditFeedback || item.feedback == '' ? 12 : 11">
							<v-row 
								no-gutters
								class="contact-info-feedback pt-1">
								<span class="date-text">{{ getDateFeedback(item.createdAt) }} - {{ item.fullName }}</span>
								<span v-if="!isEditFeedback && item.feedback != ''">
									{{ item.feedback }}
								</span>
							</v-row>
						</v-col>
						<v-col v-if="(!isEditFeedback && item.feedback != '') && ($store.getters['auth/getAccountId'] == item.creatorAccountId)" cols="1">
							<v-row
								no-gutters
								justify="end">
								<v-icon
									small
									style="cursor: pointer;"
									class="mt-1"
									@click.prevent="openEditFeedback(index)">
									edit
								</v-icon>
							</v-row>
						</v-col>
						<v-col
							cols="12"
							class="pt-4">
							<v-divider v-if="index <= feedbackInfo.feedback.length - 1" />
						</v-col>
					</v-row>
				</div>
				<v-row 
					v-if="isEditFeedback"
					no-gutters 
					class="pa-6 pt-3"
					justify="end">
					<v-btn 
						:disabled="callApiFeedback"
						tile
						text
						small
						class="btn__nxt mr-4" 
						color="#2f80ed"
						@click.prevent="cancelEditAddFeedback()">
						Cancelar
					</v-btn> 
					<v-btn  
						:loading="callApiFeedback"
						:disabled="callApiFeedback"
						tile
						small
						color="#2f80ed"
						class="white--text btn__nxt" 
						@click.prevent="editFeedback()">
						Guardar
					</v-btn>
				</v-row>
				<v-row 
					v-else-if="isCreateFeedback"
					no-gutters 
					class="pa-6 pt-3"
					justify="end">
					<v-btn 
						:disabled="callApiFeedback"
						tile
						text
						small
						class="btn__nxt mr-4" 
						color="#2f80ed"
						@click.prevent="feedbackInfo.feedback.length == 0 ? closeFeedbackDialog() : cancelEditAddFeedback()">
						Cancelar
					</v-btn> 
					<v-btn  
						:loading="callApiFeedback"
						:disabled="callApiFeedback"
						tile
						small
						color="#2f80ed"
						class="white--text btn__nxt" 
						@click.prevent="createFeedback()">
						Guardar
					</v-btn>
				</v-row>
				<v-row 
					v-else
					no-gutters 
					class="pa-6 pt-3"
					justify="end">
					<v-btn  
						tile
						small
						color="#2f80ed"
						class="white--text btn__nxt mt-3" 
						@click.prevent="isCreateFeedback = true, isFirstComment = false">
						Agregar
					</v-btn>
				</v-row>
			</v-card>
		</v-dialog>
		<report-sended 
			:open-dialog="openModalReportSended"
			event-close-dialog="EVENT_CLOSE_REPORT_SENDED_MODAL" />
		<report-user-modal
			:open-report-dialog="openModalReportUser"
			event-close-dialog="EVENT_CLOSE_REPORT_USER_MODAL"
			event-send-report="EVENT_SEND_USER_REPORT" />
		<snackBar :color="snackColor" :snackbar="snackbar" :text="snackText" event-hide="HIDE_SNACKBAR_MODULE_DETAILS" />
		<modal
			:open-modal="openModalInfo"
			:close-modal="closeModalEvent"
			:icon="iconModal"
			:title="titleModal"
			:info="infoModal"
			:is-persistent="isPersistentModal"
			:buttons="buttonsModal"
			:events="eventsModal"
			:modal-width="500"
			:button-colors="buttonsColorModal" /> 
		<EditAdviser
			:is-open-dialog="openEdition"
			title="Editar asesor" 
			width="350" />
		<!-- <v-dialog
			v-model="downloadInfoDialog"
			max-width="350"
			:persistent="true">
			<v-card tile class="pa-6">
				<v-row no-gutters justify="center">
					<v-progress-circular
						indeterminate
						color="#2f80ed" />
				</v-row>
				<v-row no-gutters justify="center" class="pt-3">
					<span style="text-align: center;">
						Procesando información. La descarga comenzará automáticamente
					</span>
				</v-row>
				<v-row no-gutters justify="center" class="pt-3">
					<v-btn
						color="#2F80ED"
						tile
						small
						class="white--text btn__nxt"
						@click.prevent="closeDownloadInfoDialog()">
						Aceptar
					</v-btn>
				</v-row>
			</v-card>
		</v-dialog> -->
	</v-container>
</template>
<script>
import axios from "axios";
import EditAdviser from '@/components/base/Editors/EditAdviser'
import BaseDataTable from '@/components/base/Admin/BaseDataTable'
export default {
    components:{
		BaseDataTable,
		EditAdviser
	},
	layout: "adminLayout",
	data() {
		return {
			token: '9260023c-3deb-4b2d-bb8d-bb595bbff9fc',
			openEdition:false,
			deleteDialog:false,
			students:[],
			idSelected: null,
			genderSelected:0,
			genders:[],
			periodSelected:0,
			periods:[],
			careerSelected:0,
			careers:[],
			pageSelected: 0,
			pagesOptions: [
				{
					id: 0,
					text: "Listado",
					to: "persons-list"
				},
				{
					id: 1,
					text: "Verificar",
					to: "persons-verify"
				},
				{
					id: 2,
					text: "Licencias",
					to: "persons-licenses"
				}
			],
			contactInfo: {
				name: '',
				email: '',
				phone: '',
				institutionName: '',
				institutionProfilePicutre: '',
				phoneInstitution: '',
				emailInstitution: ''
			},
			search: '',
			isEnabled:true,
			personsCsv: [],
			headers: [
				{
					text: 'Foto',
					align: 'start',
					sortable: true,
					value: 'profile_pic',
					title: 'Foto',
					dataKey: "profile_pic",
					selected: false
				},
				{
					text: 'Nombre',
					align: 'center',
					sortable: true,
					value: 'student_name',
					title: 'Nombre',
					dataKey: "name",
					selected: false
				},
				{
					text: 'Apellido',
					align: 'center',
					sortable: true,
					value: 'student_last_name',
					title: 'Apellido',
					dataKey: "student_last_name",
					selected: false
				},
				{
					text: 'Sexo',
					align: 'center',
					sortable: true,
					value: 'student_sex_id',
					title: 'Sexo',
					dataKey: "student_sex_id",
					selected: false
				},
				{
					text: 'Carrera',
					align: 'center',
					sortable: true,
					value: 'student_career',
					title: 'Nombre',
					dataKey: "student_career",
					selected: false
				},
				{
					text: 'Periodo',
					align: 'center',
					sortable: true,
					value: 'period_name',
					title: 'Periodo',
					dataKey: "period_name",
					selected: false
				},
				{
					text: 'Nombre del proyecto',
					align: 'center',
					value: 'project_name',
					title: 'Nombre del proyecto',
					dataKey: "student_name",
					selected: false
				},
				{
					text: 'Unidad economica',
					align: 'center',
					sortable: true,
					value: 'company_name',
					title: 'Empresa',
					dataKey: "company_name",
					selected: false
				},
				{
					text: 'Vigencia',
					align: 'center',
					sortable: true,
					value: 'student_status',
					title: 'Empresa',
					dataKey: "student_status",
					selected: false
				},
				{
					text: 'Acciones',
					align: 'center',
					sortable: true,
					value: 'action',
				}
			],
			radios: null,
			openModalReportUser: false,
			openModalReportSended: false,
			accountId: null,
			careAboutType: 0,
			seeAssistProfiles: 0,
			showFilters: false,
			subaccounts: [],
			selectedSubaccounts: [],
			headersSubaccounts: [
				{
					text: 'Ver todas',
					sortable: false,
					value: 'name',
				}
			],
			activatedFilters: false,
			feedbackDialog: false,
			selectedItem: {},
			feedbackInfo: {
				personName: '',
				feedback: '',
				feedbackEdit: '',
				accountId : '',
			},
			isEditFeedback: false,
			callApiFeedback: false,
			snackbar: false,
			snackText: "",
			snackColor: "",
			attendedItems: [
				{
					id: 1,
					text: 'Atendido',
				},
				{
					id: 0,
					text: 'Por atender',
				}
			],
			openModalInfo: false,
			closeModalEvent: "",
			iconModal: [],
			titleModal: "",
			titleDialog: 'Descarga',
			infoModal: "",
			isPersistentModal: true,
			buttonsModal: [],
			eventsModal: [],
			buttonsColorModal: [],
			selectedPerson: {},
			openModalPersonDetail: false,
			callApiPersonPreview: false,
			seeHelpProfiles: 0,
			seeAttendedProfiles: 0,
			indexFeedback: null,
			isCreateFeedback: false,
			indexSelectedItem: null,
			isFirstComment: false,
			totalResults: 0,
			options: {},
			limit: 15,
			offset: 0,
			loadingData: false,
			sourceCancelToken: null,
			searchKey: '',
			downloadInfoDialog: false,

			currentPage: 1,
			perPage: 15,
			totalPages: null,
			rangeAge: [16,80],
			filterGender: null,
			specialField_id: null,
			filterMinAge: 16,
			filterMaxAge: 80,
			specialFieldsServer: [],
			emailVerified: null,
		}
	},
	computed: {
		filteredStudents() {
		// Filtrar estudiantes según los filtros seleccionados
		return this.students.filter((student) => {
			return (
			(!this.careerSelected || student.career_id === this.careerSelected) &&
			(!this.periodSelected || student.period_id === this.periodSelected.period_id) &&
			(!this.genderSelected || student.student_sex_id === this.genderSelected)
			);
		});
		},
	},
	watch: {
		currentPage(value){
			this.currentPage = value
			this.getPersons()
		},
		search(key){
			this.searchKey = key
			this.sourceCancelToken.cancel('')
			// this.currentPage = 0 
			this.getPersons(false, 1, this.perPage, key, true)
		},
		options(val){
			this.getPersons(false, val.page, val.itemsPerPage, this.searchKey, false)
		},
	},
	created() {
        axios.get('http://localhost:3100/api/careers',{
            headers:{
                'authorization':`Bearer ${this.token}`
            }
        }).then((response)=>{
            if(response.status === 200){
				console.log(response.data)
                this.careers=response.data
				console.log(this.careers)
            }
            else{
            	console.log(response.status)
            }
        })  
		axios.get('http://localhost:3100/api/periods',{
            headers:{
                'authorization':`Bearer ${this.token}`
            }
        }).then((response)=>{
            if(response.status === 200){
				console.log(response.data)
                this.periods=response.data
				console.log(this.periods)
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
				console.log(response.data)
                this.genders=response.data
				console.log(this.genders)
            }
            else{
            	console.log(response.status)
            }
        })        
		axios.get('http://localhost:3100/api/student_info_admin',{
            headers:{
                'authorization':`Bearer ${this.token}`
            }
        }).then((response)=>{
            if(response.status === 200){
				console.log(response.data)
				console.log(this.persons)
                this.students=response.data
				console.log(this.students)
            }
            else{
            	console.log(response.status)
            }
        })     
    },
	methods: {
		toPage(id) {
			this.$router.push({
				name: this.pagesOptions[id].to
			})
		},
		goToProfile(item) {
			this.callApiPersonPreview = true
			this.openModalPersonDetail = true
			this.selectedItem = item

			this.$axios.$get(process.env.api +
                `/admin/persons/${item.personId}`,
			{
				headers: {
					Authorization: 'Token'
				}
			}
			).then((res) => {
				if(res.statusCode === 200) {
					this.selectedPerson = {...res.contents}
					this.callApiPersonPreview = false
				}
			}) 
		},
		toPageExpress() {
			this.$router.push({
				name: 'person-register'
			})
		},
	}
}
</script>
<style>
.v-select .v-input__slot::before {
    border-color: var(--primary-color) !important;
}
</style>
<style lang="scss" scoped>
.v-expansion-panel-content>>> .v-expansion-panel-content__wrap {
  padding-bottom: 0 !important;
}
.v-expansion-panel::before {
  box-shadow: none;
}
.custom-size >>> i {
    font-size: 18px !important;
}
.fixed {
    font-weight: normal;
    font-size: 12px;
    color: #828282;
}
.info-page {
    font-style: normal;
    font-weight: normal;
    font-size: 0.9375rem;
    color: #404350;
    line-height: 1.125rem;
}
.filters-page {
    font-style: normal;
    font-weight: normal;
    font-size: 0.9375rem;
    color: #404350;
    line-height: 1.125rem;
    cursor: pointer;
}
.contact-info-item {
    font-style: normal;
    font-weight: normal;
    font-size: 0.9375rem;
    line-height: 1.125rem;
    color: #404350;
}
.contact-info-title {
    font-style: normal;
    font-weight: 500;
    font-size: 0.9375rem;
    line-height: 1.125rem;
    color: #404350;
}
.contact-info-text {
    font-style: normal;
    font-weight: normal;
    font-size: 0.9375rem;
    line-height: 1.125rem;
    color: #404350;
}
.item-text {
    font-style: normal;
    font-weight: normal;
    font-size: 0.875rem;
    line-height: 1rem;
    color: #404350;
}
.item-text-link {
    font-style: normal;
    font-weight: normal;
    font-size: 	0.875rem;
    line-height: 1rem;
	color: #404350;
}
.item-text-link:hover {
    cursor: pointer;
    text-decoration: underline;
	color: #2f80ed;
}
.info-text {
    font-style: normal;
    font-weight: normal;
    font-size: 12px;
    color: #404350;
}
.csv-text {
    font-style: normal;
    font-weight: 500;
    font-size: 0.875rem;
    line-height: 0.9375rem;
    color: #404350;
    cursor: pointer;
}
.container-style {
    height: calc(100vh - 64px);
}
.card-general-style {
    height: calc(100vh - 170px);
}
.text-title {
    font-weight: 500 !important;
    font-size: 1.125rem !important;
    color: #404350 !important;
}
.filter-item-text {
    font-size: 0.9rem;
    color: #404350;
}
.filter-item-title {
    font-weight: 500;
    font-size: 0.9rem;
    color: #404350;
}
.chip-new {
    color: white;
    font-weight: 500;
    top: -2px;
}
.date-text{
    font-style: normal;
    font-weight: normal;
    font-size: 0.75rem;
    line-height: 0.875rem;
    color: #666666;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    word-break: break-word;
}
.contact-info-feedback {
    font-style: normal;
    font-weight: normal;
    font-size: 	0.9375rem;
    line-height: 1.125rem;
    color: #404350;
    display: block;
}
.item-text-blue {
    font-style: normal;
    font-weight: normal;
    font-size: 	0.875rem;
    line-height: 1rem;
    color: #2f80ed;
    cursor: pointer;
    text-decoration: underline;
}
</style>