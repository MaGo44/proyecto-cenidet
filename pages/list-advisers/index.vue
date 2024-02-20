<template>
	<v-container fluid>
		<v-row>
			<v-col cols="12">
                <v-row>
                    <h1>Listado de asesores internos</h1>
                    <v-spacer/>
					<v-select 
						v-model="careerSelected"
						:items="careers"
						item-value="career_id"
                        item-text="career_name"
						style="max-width:206px"
                        :menu-props="{ openOnHover: true }"
						dense
                        outlined
                        single-line>
					</v-select>
                </v-row>
			</v-col>
			<v-col cols="12" class="pt-0">
				<BaseDataTable
					:headers="headers"
					:items="advisers"
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
									:color="primaryColor"
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
										@click="openDialog(item)">
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
										@click.prevent="deleteAdviser(item.internal_adviser_id)">
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
		<snackBar :color="snackColor" :snackbar="snackbar" :text="snackText" event-hide="HIDE_SNACKBAR_MODULE_DETAILS" />
		<EditAdviser
			:is-open-dialog="openEdition"
			:adviser="selectedAdviser"
			:genders="genders"
			:studies="studies"
			:careers="careersForm"
			title="Editar asesor" 
			width="550" />
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
			openEdition:false,
			advisers:[],
            careerSelected:0,
			careers:[
				{
					career_id:0,
					career_name:'Todas las carreras'
				},
				{
					career_id:1,
					career_name:'Industrial'
				},
				{
					career_id:2,
					career_name:'Sistemas computacionales'
				},
			],
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
			persons: [
                {
                    internal_name:'Santiago Robles',
					career_name:'Industrial',
					internal_email:'santi@gmail.com',
					internal_phone:'6574848896'
                },
				{
                    internal_name:'Pamela Rodriguez',
					career_name:'Sistemas computacionales',
					internal_email:'pam@gmail.com',
					internal_phone:'5567895706'
                }
            ],
			personsCsv: [],
			headers: [
				{
					text: 'Nombre',
					align: 'start',
					sortable: true,
					value: 'internal_name',
					title: 'Nombre',
					dataKey: "name",
					selected: false
				},
				{
					text: 'Carrera de adscripción',
					align: 'start',
					sortable: true,
					value: 'career_name',
					title: 'Nombre',
					dataKey: "internal_adscription_career",
					selected: false
				},
				{
					text: 'Correo electronico',
					align: 'start',
					value: 'internal_email',
					title: 'Nombre del proyecto',
					dataKey: "internal_email",
					selected: false
				},
				{
					text: 'Telefono',
					align: 'start',
					sortable: true,
					value: 'internal_phone',
					title: 'Empresa',
					dataKey: "internal_phone",
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
			token: "9260023c-3deb-4b2d-bb8d-bb595bbff9fc",
			selectedAdviser:{},
			genders:[],
			studies:[],
			careersForm:[]
		}
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
        this.getAdvisers()
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
                this.careersForm=response.data
            }
            else{
            	console.log(response.status)
            }
        })
    },
	methods: {
		openDialog(adviser){
			console.log(adviser,'adviser')
			this.selectedAdviser=adviser
			this.openEdition=true
		},
		getAdvisers(){
			axios.get('http://localhost:3100/api/internal_adviser_info',{
				headers:{
					'authorization':`Bearer ${this.token}`
				}
			}).then((response)=>{
				if(response.status === 200){
					this.advisers=response.data
				}
				else{
					console.log(response.status)
				}
			})     
		},
		deleteAdviser(id){
			axios.delete(`http://localhost:3100//api/internal_adviser_info/${id}`, {
				headers:{
					'authorization':`Bearer ${this.token}`
				}
			}).then((response)=>{
				if(response.status === 204){
					this.getAdvisers()
				}
				else{
					console.log(response.status)
				}
			}) 
		},
		toPage(id) {
			this.$router.push({
				name: this.pagesOptions[id].to
			})
		},
		// openContactInfoDialog(item) {
		// 	this.contactInfo.name = item.name
		// 	this.contactInfo.email = item.email
		// 	this.contactInfo.phone = item.phone
		// 	this.contactInfo.institutionProfilePicutre = item.profilePicutre
            
		// 	this.contactInfoDialog = true
		// },
		// closeContactInfoDialog() {
		// 	this.contactInfoDialog = false
		// },
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