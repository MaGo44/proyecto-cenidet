<template>
	<v-app style="overflow: auto" light>
		<v-navigation-drawer
			v-model="drawer"
			:clipped="true"
			style="box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.15);"
			app
			:mini-variant.sync="miniVariant"
			:permanent="$vuetify.breakpoint.mdAndUp"
			expand-on-hover>
			<v-list dense>
				<v-subheader class="justify-center mt-5 mb-5">
					<img
						v-show="!miniVariant"
						:src="logoColorSiga"
						:aspect-ratio="16 / 9"
						:height="$vuetify.breakpoint.sm && platform != 'TP' && platform != 'TN' ? 50 : platform != 'TP' && platform != 'TN' ? 50 : 42">
					<img
						v-show="miniVariant"
						:src="logoOnlySiga"
						:aspect-ratio="16 / 9"
						:height="$vuetify.breakpoint.sm && platform != 'TP' && platform != 'TN' ? 50 : platform != 'TP' && platform != 'TN' ? 50 : 42">
				</v-subheader>
				<v-list-group
					v-for="item in items"
					:key="item.text"
					color="colorPrimary"
					:append-icon="item.actions != undefined && item.actions.length > 0 ? '$vuetify.icons.expand' : ''"
					no-action
					@click.prevent="toPage(item.to)">
					<template v-slot:prependIcon>
						<v-icon :class="{ 'colorPrimary--text': $route.name == 'dashboard' && item.text == 'Dashboard' }">
							{{ item.icon }}
						</v-icon>
					</template>
					<template v-slot:activator>
						<v-list-item-content>
							<v-list-item-title
								:class="{ 'colorPrimary--text': $route.name == 'dashboard' && item.text == 'Dashboard' }">
								{{ item.text }}
							</v-list-item-title>
										</v-list-item-content>
									</template>
									<v-list-item
										v-for="subItem in item.actions"
										:key="subItem.name"
										:style="listItemSelected"
										:class="{ 'opacity-blue': $route.name == subItem.to }"
										@click="subItem.to[0] == '#' ? toDashboard(subItem.to) : toPage(subItem.to) , $vuetify.breakpoint.mdAndDown ? drawer = !drawer : ''">
										<v-list-item-content>
											<v-list-item-title
												class="px14 font-weight-light greyPrimary--text">
								{{ subItem.name }}
							</v-list-item-title>
						</v-list-item-content>
					</v-list-item>
				</v-list-group>
				<NuxtLink to="/">
					Cerrar sesion
				</NuxtLink>
			</v-list>
			<v-btn
				v-show="$vuetify.breakpoint.xsOnly"
				depressed
				class="text-none"
				style="font-size:13px"
				color="#fff"
				@click.prevent="signOut()">
				<v-icon class="mr-9" color="#757575">
					exit_to_app
				</v-icon>
				Cerrar sesion
			</v-btn>
		</v-navigation-drawer>
		<v-app-bar
			v-if="$vuetify.breakpoint.smAndDown"
			:clipped-left="$vuetify.breakpoint.smAndDown"
			app
			:color="primaryColorToolbar"
			elevation="0"
			class="content-card__elevationNav"
			dark>
			<v-toolbar-title
				v-if="$vuetify.breakpoint.smAndDown"
				style="width: 50px"
				class="ml-0 pl-4">
				<v-app-bar-nav-icon color="colorPrimary" @click.stop="drawer = true" />
			</v-toolbar-title>
			<img
				v-show="$vuetify.breakpoint.smAndUp"
				:src="logoColorSiga"
				:aspect-ratio="16 / 9"
				class="ml-5"
				:height="$vuetify.breakpoint.sm && platform != 'TP' && platform != 'TN' ? 35 : platform != 'TP' && platform != 'TN' ? 42 : 42">
			<v-spacer />
			<v-tooltip top content-class="custom-toolti">
				<template v-slot:activator="{ on}">
					<v-avatar
						:size="$vuetify.breakpoint.mdAndUp ? 35 : 25"
						:class="{'mr-1': accountsManager.length == 0}"
						v-on="on">
						<img
							class="border-img">

						<v-btn
							v-show="$vuetify.breakpoint.smAndUp"
							class="ml-5 mr-8 pr-6"
							icon
							v-on="on"
							@click.prevent="signOut()">
							<v-icon color="colorPrimary">
								exit_to_app
							</v-icon>
						</v-btn>
					</v-avatar>
				</template>
				<span>Cerrar sesión</span>
			</v-tooltip>
		</v-app-bar>
		<v-content class="content-style">
			<v-container
				:style="{minWidth: minWidthContainer}"
				fluid
				class="u-no-mxh px-5 background">
				<nuxt />
			</v-container>
		</v-content>
		<v-overlay
			:absolute="false"
			:value="callApi">
			<v-progress-circular
				indeterminate
				size="64" />
		</v-overlay>
	</v-app>
</template>

<script>
export default {
	data: () => ({
		callApi: false,
		accountsManager: [],
		dialog: false,
		drawer: false,
		perc: undefined,
		isIntersecting: false,
		picturePerson: '',
		namePerson: '',
		lastNamePerson: '',
		nameInstitution: '',
    miniVariant: true,
		items: [
			{
				icon:'mdi-view-dashboard-outline',
				text: 'Dashboard',
				to: 'dashboard',
				actions: []
			}
		],
	}),
	computed: {
		minWidthContainer() {
			if (this.$vuetify.breakpoint.xl) return '1500px'
			else return ''
		},
		listItemSelected() {
			return {
				"--color-list-item-selected": this.colorListItemSelected
			}
		}
	},
	created() {
			this.items.push({
				icon:'mdi-school-outline',
				text: 'Estudiantes',
				to: '',
				actions: [
					{
						name: 'Listado',
						to: 'list-student'
					},
					{
						name: 'Reportes',
						to: 'list-student-report'
					},
					{
						name: 'Registro',
						to: 'company-register'
					},
				]
			})

			this.items.push({
				icon:'mdi-domain',
				text: 'Empresas',
				to: '',
				actions: [
					{
						name: 'Listado',
						to: 'list-companies'
					},
					{
						name: 'Registro',
						to: 'register-company'
					},
				]
			})

			this.items.push({
				icon:'mdi-account-outline',
				text: 'Asesores',
				to: '',
				actions: [
					{
						name: 'Listado',
						to: 'list-advisers'
					},
					{
						name: 'Registro',
						to: 'register-internal-adviser'
					},
				]
			})
	},
	methods: {
    toPage(page) {
			this.$router.push({
				name: page
			})
		},
	}
}
</script>
<style scoped>
.name-person-text {
    font-style: normal;
    font-weight: normal;
    font-size: 1rem;
    line-height: 1.0625rem;
    color: #404350 !important;
}
.name-person-text-sm {
    font-style: normal;
    font-weight: normal;
    font-size: 0.8rem;
    line-height: 1.0625rem;
    color: #404350 !important;
}
.name-institution-text {
    font-style: normal;
    font-weight: 500;
    font-size: 1rem;
    line-height: 1.0625rem;
    color: #404350 !important;
}
.name-institution-text-sm {
    font-style: normal;
    font-weight: 500;
    font-size: 0.8rem;
    line-height: 1.0625rem;
    color: #404350 !important;
}
.item-selected {
    background-color: var(--color-list-item-selected);
}
.item-color {
    color: #0038A8;
}
.subaccount {
    cursor: pointer;
}
.text-change-account {
    text-align: left;
    color: #404350;
    font-weight: 400;
    font-size: 16px;
    letter-spacing: 1px;
}
</style>
<style>
.v-list-item__action, .v-list-item__avatar, .v-list-item__icon {
    display: inline-flex !important;
    min-width: 10px !important;
    padding-top: 5px !important;;
    margin-bottom: 8px !important;;
}
.content-style {
    background-color: #F8F7FF;
    }
</style>