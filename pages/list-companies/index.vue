<template>
	<v-container fluid>
		<v-row>
			<v-col cols="12">
				<h1>Unidades económicas</h1>
			</v-col>
			<v-col cols="12" class="pt-0">
				<BaseDataTable
					:headers="headers"
					:items="companies"
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
					<template v-slot:[`item.company_name`]="{ item }">
						<div class="d-flex align-center py-2">
							<!-- <v-avatar tile :size="30" class="mr-2">
								<v-img :src="profilePicturePath + item.profilePicutre" />
							</v-avatar> -->
							<span>
								<span>
									{{ item.company_name }}
								</span>
								<!-- <v-chip v-if="getDays(item) && (item.attended == 0 || item.attended == null)" class="ma-0 px-2 chip-new" x-small color="turquoisePrimary">
									Nuevo
								</v-chip> -->
							</span>
							<v-tooltip top content-class="custom-tooltip">
								<template v-slot:activator="{ on }">
									<v-avatar
										v-if="item.adminAccountId != null"
										tile
										:size="15"
										class="ml-2"
										v-on="on">
										<!-- <v-img
											:src="require('~/assets/png/pencil2.png')" /> -->
									</v-avatar>
								</template>
								<span>Registro manual desde el administrador</span>
							</v-tooltip>
						</div>
					</template>
					<!-- <template v-slot:[`item.createdAt`]="{ item }">
						<span>{{ getDate(item.createdAt) }}</span>
					</template> -->
					<template v-slot:[`item.company_email`]="{ item }">
						<div class="d-flex align-center py-2">
							{{ item.company_email }}
						</div>
					</template>
					<template v-slot:[`item.email`]="{ item }">
						<div class="d-flex align-center py-2">
							<span>{{ item.email == '' || item.email == null ? 'Correo no proporcionado' : item.email }}</span>
						</div>
					</template>
					<template v-slot:[`item.phone`]="{ item }">
						<span>{{ item.phone }}</span>
					</template>
					<template v-slot:[`item.status`]="{ item }">
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
								<template v-slot:selection="{ item }">
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
					<template v-slot:[`item.action`]="{ item }">
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
										@click.prevent="deleteCompany(item.company_id)">
										mdi-trash-can
									</v-icon>
								</template>
								<span>Eliminar</span>
							</v-tooltip>
							<v-tooltip 
								top 
								content-class="custom-tooltip">
								<template #activator="{ on }">
									<v-icon 
										v-on="on"
										@click.prevent="openOverviewDialog(item)">
										mdi-domain
									</v-icon>
								</template>
								<span>Ver unidad</span>
							</v-tooltip>
						</div>
					</template>
				</BaseDataTable>
			</v-col>
		</v-row>
		<v-dialog
			v-model="editDialog"
			width="50%"
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
		<snackBar :color="snackColor" :snackbar="snackbar" :text="snackText" event-hide="HIDE_SNACKBAR_MODULE_DETAILS" />
		<EditCompany
			:is-open-dialog="openEdition"
			:company="selectedCompany"
			:agreement_status="agreement_status"
			:studies="studies"
			:careers="careersForm"
			title="Editar unidad económica" 
			width="550"
			@close-dialog="closeDialog"
			@edit-company="editCompany" />
		<info-overview
			:is-open-dialog="openOverview"
			:company="selectedCompany"
			:agreement_status="agreement_status"
			:studies="studies"
			:careers="careersForm"
			title="Información de la unidad económica" 
			width="550"
			@close-dialog="closeDialog">
			<template #sectionContent>
				<v-col cols="12" class="pb-0 mt-5">
                    <b> Nombre de la unidad económica: </b> {{ selectedCompany.company_name }}
                </v-col>
                <v-col cols="12" class="pb-0 mt-2">
                    <b> Razón social: </b> {{ selectedCompany.company_business_name }}
                </v-col>
                <v-col cols="12" class="pb-0 mt-2">
                    <b> Dirección de la unidad económica: </b> {{ selectedCompany.company_address }}
                </v-col>
                <v-col cols="12" class="pb-0 mt-2">
                    <b> Código postal: </b> {{ selectedCompany.company_postal_code }}
                </v-col>
                <v-col cols="12" class="pb-0 mt-2">
                	<b> Colonia: </b> {{ selectedCompany.company_colony }}
                </v-col>
                <v-col cols="12" class="pb-0 mt-2">
                    <b> Localidad: </b> {{ selectedCompany.company_location }}
                </v-col>
                <v-col cols="12" class="pb-0 mt-2">
                                    <b> Municipio: </b> {{ selectedCompany.company_municipality }}
                                </v-col>
                                <v-col cols="12" class="pb-0 mt-2">
                                    <b> Estado: </b> {{ selectedCompany.company_state }}
                                </v-col>
                                <v-col cols="12" class="pb-0 mt-2">
                                    <b> Número exterior: </b> {{ selectedCompany.company_external_number }}
                                </v-col>
                                <v-col cols="12" class="pb-0 mt-2">
                                    <b> País: </b> {{ selectedCompany.company_country }}
                                </v-col>
                                <v-col cols="12" class="pb-0 mt-2">
                                    <b> Nombre del representante: </b> {{ selectedCompany.company_representative_name }}
                                </v-col>
                                <v-col cols="12" class="pb-0 mt-2">
                                    <b> Nombre del contacto: </b> {{ selectedCompany.company_contact_name }}
                                </v-col>
                                <v-col cols="12" class="pb-0 mt-2">
                                    <b> Estudios máximos: </b> {{ selectedCompany.grade_name }}
                                </v-col>
                                <v-col cols="12" class="pb-0 mt-2">
                                    <b> Cargo o puesto: </b> {{ selectedCompany.company_contact_position }}
                                </v-col>
                                <v-col cols="12" class="pb-0 mt-2">
                                    <b> Teléfono fijo: </b> {{ selectedCompany.company_contact_max_studies }}
									<div v-if="selectedCompany.company_tel_ext!=null"> <b> Extensión: </b> {{ selectedCompany.company_tel_ext }} </div>
                                </v-col>
                                <v-col cols="12" class="pb-0 mt-2">
                                    <b> Teléfono celular: </b> {{ selectedCompany.company_cel }}
                                </v-col>
                                <v-col cols="12" class="pb-0 mt-2">
                                    <b> Correo: </b> {{ selectedCompany.company_email }}
                                </v-col>
                                <v-col cols="12" class="pb-0 mt-2">
                                    <b> Segundo correo: </b>{{ selectedCompany.company_second_email }}
                                </v-col>
								<v-col cols="12" class="pb-0 mt-2">
                                    <b> Estatus del convenio: </b>{{ selectedCompany.status_name }}
                                </v-col>
								<v-col cols="12" class="pb-0 mt-2">
                                    <b > Fecha del convenio: </b>{{ selectedCompany.status_name }}
                                </v-col>
			</template>
		</info-overview>
		<success-dialog
			:is-open-dialog="isSucess"
			width="550"
			@close="closeSucessDialog()">
			<template #sectionContent>
				Unidad económica editada correctamente.
			</template>
		</success-dialog>
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
	</v-container>
</template>
<script>
import axios from "axios";
import EditCompany from '@/components/base/Editors/EditCompany';
import InfoOverview from '@/components/dialogs/InfoOverview';
import BaseDataTable from '@/components/base/Admin/BaseDataTable';
import SuccessDialog from '@/components/dialogs/SuccessDialog';
export default {
    components:{
		BaseDataTable,
		EditCompany,
		SuccessDialog,
		InfoOverview
	},
	layout: "adminLayout",
	data() {
		return {
			companies:[],
			agreement_status:[],
			studies:[],
			pageSelected: 0,
			search: '',
			isEnabled:true,
			personsCsv: [],
			headers: [
				{
					text: 'Nombre',
					align: 'start',
					sortable: true,
					value: 'company_name',
					title: 'Nombre',
					dataKey: "company_name",
					selected: false
				},
				{
					text: 'Nombre del contacto',
					align: 'center',
					sortable: true,
					value: 'company_contact_name',
					title: 'Fecha de registro',
					dataKey: "company_contact_name",
					selected: false
				},
				{
					text: 'Correo electronico',
					align: 'center',
					value: 'company_email',
					title: 'Ayuda',
					dataKey: "company_email",
					selected: false
				},
				{
					text: 'Telefono',
					align: 'center',
					sortable: true,
					value: 'company_tel',
					title: 'Fecha de registro',
					dataKey: "company_tel",
					selected: false
				},
				{
					text: 'Vacantes',
					align: 'center',
					sortable: true,
					value: 'company_vacants_number',
					title: 'Fecha de registro',
					dataKey: "company_vacants_number",
					selected: false
				},
				{
					text: 'Vigencia',
					align: 'center',
					sortable: true,
					value: 'status_name',
					title: 'Fecha de registro',
					dataKey: "company_status",
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
			token:"9260023c-3deb-4b2d-bb8d-bb595bbff9fc",
			selectedCompany:{},
			openEdition:false,
			openOverview:false,
			isSucess:false
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
        this.getCompanies()
		axios.get('http://localhost:3100/api/agreement_status',{
            headers:{
                'authorization':`Bearer ${this.token}`
            }
        }).then((response)=>{
            if(response.status === 200){
                this.agreement_status=response.data
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
                this.careersForm=response.data
            }
            else{
            	console.log(response.status)
            }
        })
    },
	methods: {
		openDialog(company){
			console.log(this.openEdition,'company')
			this.selectedCompany=company
			this.openEdition=true
			console.log(this.openEdition,'company')
		},
		openOverviewDialog(company){
			console.log(this.openEdition,'company')
			this.selectedCompany=company
			this.openOverview=true
			console.log(this.openEdition,'company')
		},
		closeSucessDialog(){
			this.isSucess=false
		},
		closeDialog(){
			this.openEdition=false
			this.openOverview=false
			console.log(this.openEdition,'company')
		},
		getCompanies(){
			axios.get('http://localhost:3100/api/company_info',{
				headers:{
					'authorization':`Bearer ${this.token}`
				}
			}).then((response)=>{
				if(response.status === 200){
					console.log(response.data)
					this.companies=response.data
					console.log(this.companies)
				}
				else{
					console.log(response.status)
				}
			}) 
		},
		deleteCompany(id){
			axios.delete(`http://localhost:3100/api/company_info/${id}`, {
				headers:{
					'authorization':`Bearer ${this.token}`
				}
			}).then((response)=>{
				if(response.status === 204){
					console.log('Eliminada')
					this.getCompanies()
				}
				else{
					console.log(response.status)
				}
			}) 
		},
		editCompany(company){
			console.log('info',company)
			axios.patch(`http://localhost:3100/api/company_info/${company.company_id}`, company, {
				headers:{
					'authorization':`Bearer ${this.token}`
				}
			}).then((response)=>{
				console.log('Compania editada',response.status)
				if(response.status === 200){
					this.getCompanies()
					this.isSucess=true;
				}
				else{
					console.log(response.status)
				}
			}) 
		},
		// toPage(id) {
		// 	this.$router.push({
		// 		name: this.pagesOptions[id].to
		// 	})
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