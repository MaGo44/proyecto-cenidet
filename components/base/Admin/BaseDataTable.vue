<template>
	<v-card class="card-border-rounded elevation-0">
		<v-data-table
			:headers="headers"
			:items="items"
			:loading="isLoading"
			:mobile-breakpoint="0"
			:page.sync="currentPageLocal"
			:items-per-page="perPage"
			:search="search"
			:show-expand="showExpand"
			:single-expand="singleExpand"
			:item-key="itemKey"
			hide-default-footer
			:height="height"
			fixed-header>
			<slot
				v-for="slot in Object.keys($slots)"
				:slot="slot"
				:name="slot" />
			<template
				v-for="slot in Object.keys($scopedSlots)"
				:slot="slot"
				slot-scope="scope">
				<slot :name="slot" v-bind="scope" />
			</template>
			<template v-slot:no-data>
				<div
					v-if="items.length == 0"
					class="px14 font-weight-light blackPrimary--text">
					No se encontraron resultados
				</div>
			</template>
		</v-data-table>
		<div>
			<v-row
				class="mt-5 px-8"
				no-gutters
				justify="start">
				<v-col v-if="items.length > 0 && showExportPdf" cols="auto">
					<v-row v-if="isEnabled" no-gutters class="mt-3">
						<div class="text-center">
							<!-- <v-list>
								<v-list-group
									v-for="item in downloadOptions"
									:key="item.title"
									v-model="item.active"
									:append-icon="null"
									no-action>
									<template v-slot:activator>
										<v-list-item-content>
											<v-list-item-title v-text="item.title" />
										</v-list-item-content>
									</template>

									<v-list-item
										v-for="child in item.items"
										:key="child.title">
										<v-list-item-content>
											<v-list-item-title v-text="child.title" />
										</v-list-item-content>
									</v-list-item>
								</v-list-group>
							</v-list> -->
							<v-menu
								top
								outlined
								color="greyPrimary"
								content-class="elevation-0 tile"
								:close-on-click="false"
								:close-on-content-click="false"
								:value="isDownloadMenu"
								:offset-y="offset">
								<template v-slot:activator="{ on, attrs }">
									<v-btn
										:class="isDownloadMenu ? 'v-btn-download-active elevation-0' : 'v-btn-download elevation-0'"
										color="greyPrimary"
										small
										outlined
										v-bind="attrs"
										v-on="on"
										@click="isDownloadMenu=!isDownloadMenu">
										Descargar
										<v-icon
											right
											dark>
											mdi-tray-arrow-down
										</v-icon>
									</v-btn>
								</template>

								<v-list>
									<v-list-item
										v-for="(item, index) in downloadOptions"
										:key="index"
										@click="menuActionClick(item.action)">
										<v-list-item-title>{{ item.title }}</v-list-item-title>
									</v-list-item>
								</v-list>
							</v-menu>
						</div>
						<!-- <BaseExportPDF
							:is-dialog="isDialogPDF"
							:columns="headers"
							:companies="items"
							:title-export="titleExport"
							:download-pdf="downloadPdf"
							@close-export="closeExport" />
						<BaseExportCSV
							:is-dialog="isDialogCSV"
							:items="itemsCsv"
							:title-export="titleExport"
							:download-csv="downloadCsv"
							@close-export="closeExport" /> -->
					</v-row>
				</v-col>
				<v-spacer />
				<v-col
					v-if="items.length > 0 && showPagination"
					cols="auto"
					class="pa-0 ma-0 pb-3">
					<v-pagination
						v-model="currentPageLocal"
						:length="totalPages"
						:total-visible="totalVisible"
						class="custom-pagination"
						color="#40BFB4"
						@input="handlePageChange" />
				</v-col>
			</v-row>
		</div>
	</v-card>
</template>
<script>
// import BaseExportPDF from "@/components/base/BaseExportPDF"
// import BaseExportCSV from "@/components/base/BaseExportCSV"
export default {
	name: "BaseDataTable",
	components: {
		// BaseExportPDF,
		// BaseExportCSV
	},
	props: {
		headers: {
			type: Array,
			required: true
		},
		items: {
			type: Array,
			required: false,
			default() {
				return []
			}
		},
		search: {
			type: String,
			required: false,
			default: null
		},
		height: {
			type: String,
			required: false,
			default: ''
		},
		isLoading: {
			type: Boolean,
			required: false,
			default: false
		},
		showPagination: {
			type: Boolean,
			required: false,
			default: false
		},
		currentPage: {
			type: Number,
			required: false,
			default: null
		},
		perPage: {
			type: Number,
			required: false,
			default: 10
		},
		isEnabled:{
			type: Boolean,
			required: false,
		},
		totalVisible: {
			type: Number,
			required: false,
			default: 8
		},
		totalPages: {
			type: Number,
			required: false,
			default: 0
		},
		showExportPdf: {
			type: Boolean,
			required: false,
			default: true
		},
		showExpand: {
			type: Boolean,
			required: false,
			default: false
		},
		singleExpand: {
			type: Boolean,
			required: false,
			default: false
		},
		itemKey: {
			type: String,
			required: false,
			default: ''
		},
		titleExport: {
			type: String,
			required: false,
			default: 'unknow'
		},
		itemsPdf: {
			type: Array,
			required: false,
			default: null
		},
		itemsCsv: {
			type: Array,
			required: false,
			default: null
		},
		downloadCsv: {
			type: String,
			required: false,
			default: ''
		},
		downloadPdf: {
			type: String,
			required: false,
			default: ''
		},

	},
	data() {
		return {
			currentPageLocal: this.currentPage,
			downloadOptions: [
				{
					title: 'Como CSV',
					action: "CSV"
				},
				{
					title: 'Como PDF',
					action: "PDF"
				},
			],
			offset: true,
			isDialogPDF: false,
			isDialogCSV: false,
			isDownloadMenu: false
		}
	},
	watch: {
		currentPage (value) {
			this.currentPageLocal = value
		},
	},
	methods: {
		handlePageChange(currentPage) {
			this.$emit('update:currentPage', currentPage)
		},
		menuActionClick(action){
			if (action === "PDF") {
				this.isDialogPDF = true
			} else if (action === "CSV") {
				this.isDialogCSV = true
			}
		},
		closeExport(){
			this.isDialogPDF=false
			this.isDialogCSV=false
			this.isDownloadMenu=false
		}
	},
}
</script>
<style scoped>
.v-data-table >>> th {
    background-color: #E07A5F !important;
}
.v-data-table  >>> th .v-data-table-header__icon {
  display: none;
}
.v-data-table >>> th > span {
    color: #FFFFFF;
    font-style: normal;
    font-weight: 500;
    font-size: 14px;
    line-height: 16px;
}
.v-data-table >>> .v-data-table__wrapper{
    border-radius: 8px 8px 0px 0px;
    background-color: #FFFFFF !important;
}
.v-data-table >>> td {
    border: none !important;
    font-weight: 500;
    font-size: 14px;
    line-height: 16px;
    color: #101820;
}
.v-menu__content.tile {
	border-radius: 5px 5px 0px 0px;
	border: 1px solid #8C8E90 !important;
	color: #8C8E90;
}
.v-btn-download{
	/* font-style: normal;
    font-weight: 400;
    font-size: 16px !important;
    line-height: 19px;
    text-align: center !important;
    padding: 0px 30px !important; */
	color: #8C8E90;
	padding: 16px !important;
	font-size: 16px !important;
	text-align: center !important;
    text-transform: none !important;
	letter-spacing: normal;
}
.v-btn-download-active{
	border-radius: 0px 0px 5px 5px;
	font-size: 16px !important;
	text-align: center !important;
	padding: 16px !important;
	letter-spacing: normal;
	color: #8C8E90;
	/* font-style: normal;
    font-weight: 400;
    font-size: 16px !important;
    line-height: 19px;
    text-align: center !important;
    padding: 0px 30px !important; */
    text-transform: none !important;
}
/* .v-btn-download.v-btn--outlined ::v-deep{
	border: 1px 0px 0px 0px solid #8C8E90 !important;
} */
.v-btn-download-active::before {
  display: none;
}
.v-btn-download-active::after {
  display: none;
}
</style>
<style lang="scss">
.v-pagination__item {
    background: white;
    border: 1px solid #C4C4C4;
    border-radius: 4px;
    box-shadow: none;
}
.v-pagination__navigation{
    background: white;
    border: 1px solid #C4C4C4;
    border-radius: 4px;
    box-shadow: none;
}
tbody tr:nth-of-type(odd) {
    background-color: #e8d8d0;
}
tbody tr:nth-of-type(even) {
    background-color: #fcf4ea;
}
</style>