/* 
    Descripcion:
    Componente de encabezado.
*/
<template>
        <div>
            <!-- Barra para las opciones -->
            <v-toolbar color="black">
                <!-- Enlace hacia la pagina de tareas -->
                <NuxtLink to="/">
                    <button class="ml-2">
                        <v-img width="150px" :src="require('@/assets/png/logofooter.png')"/>
                    </button>
                </NuxtLink>
                <v-spacer />
                <div v-for="link in links" :key="link.name" class="mr-4">
                    <NuxtLink :to="link.url">
                        <button class="mr-2">
                            <v-toolbar-title class="white--text"> {{ link.name }} </v-toolbar-title>
                        </button>
                    </NuxtLink>
                </div>
                <v-icon color="white"> mdi-magnify </v-icon>
            </v-toolbar>
            <!-- Barra para las opciones -->
                <div v-if="userType=='admin'">
                    <v-navigation-drawer class="white" width="100">
                        <div class="text-center mt-5"> 
                            <v-btn>
                                hola
                                <v-icon>mdi-account-circle</v-icon>
                            </v-btn>
                        </div>
                        <div class="text-center mt-5"> 
                            <v-btn>
                                hola
                                <v-icon>mdi-account-circle</v-icon>
                            </v-btn>
                        </div>
                    </v-navigation-drawer>
                </div>
            <v-toolbar v-else color="white">
                <v-row v-if="userType=='student'" justify="center">
                    <div v-for="btn in navButtons" :key="btn.name" class="mr-4">
                        <NuxtLink :to="btn.url">
                            <button class="mr-2">
                                <v-toolbar-title class="secondaryColor--text"> {{ btn.name }} </v-toolbar-title>
                            </button>
                        </NuxtLink>
                    </div>
                        <v-col cols="auto">
                                <v-menu v-model="mn" open-on-hover :left="true" offset-y>
                                    <template #activator="{ on }">
                                        <div class="ma-0 pa-0" v-on="on">
                                            <v-avatar :size="32">
                                                <v-img
                                                    :src="require('@/assets/png/accountImage.png')"
                                                    :lazy-src="require('@/assets/png/accountImage.png')" />
                                            </v-avatar>
                                            <v-icon small color="lightPrimary" class="ml-1">
                                                mdi-chevron-down
                                            </v-icon>
                                        </div>
                                    </template>
                                    <v-card class="card-border-rounded" elevation="1" style="max-width: 260px;">
                                        <v-list-item @click="goToPage('student-profile')">
                                            <v-list-item-avatar size="32">
                                                <v-img :src="require('@/assets/png/accountImage.png')" />
                                            </v-list-item-avatar>
                                            <v-list-item-content>
                                                <v-list-item-title class="px16 blackPrimary--text font-weight-medium">
                                                    Mi información
                                                    <v-spacer />
                                                </v-list-item-title>
                                            </v-list-item-content>
                                            <v-list-item-action class="my-auto">
                                                <v-icon color="lightPrimary">
                                                    mdi-chevron-right
                                                </v-icon>
                                            </v-list-item-action>
                                        </v-list-item>
                                        <v-list tile dense elevation="0">
                                            <v-list-item-group>
                                                <!-- ITEM FOR CHANGE COUNTRY -->
                                                <v-list-item @click="goToPage('reports')">
                                                    <v-list-item-title class="px16 blackPrimary--text font-weight-medium">
                                                    Mi progreso
                                                    <v-spacer />
                                                </v-list-item-title>
                                                    <v-list-item-action class="my-auto">
                                                        <v-icon color="lightPrimary">
                                                            mdi-chevron-right
                                                        </v-icon>
                                                    </v-list-item-action>
                                                </v-list-item>
                                                <v-list-item-title disabled>
                                                  <v-divider />
                                                </v-list-item-title>
                                                <!-- ITEM FOR CHANGE COUNTRY -->
                                                <!-- <v-list-item
                                                    v-for="(item, index) in menuMexicoSiga"
                                                    :key="index"
                                                    :class="{ 'div-item px-0': item.title == 'divider' }"
                                                    :disabled="item.title == 'divider'"
                                                    @click.prevent="item.id != 0 ? menuLinks(item.id) : ''">
                                                    <v-list-item-title v-if="item.title == 'divider'" disabled>
                                                        <v-divider />
                                                    </v-list-item-title>
                                                    <v-list-item-title
                                                        v-else
                                                        :class="item.title == 'Cerrar sesión'
                                                            ? 'px16 error--text font-weight-medium'
                                                            : 'px16 blackPrimary--text font-weight-medium'
                                                        "
                                                        nuxt>
                                                        {{ item.title }}
                                                    </v-list-item-title>
                                                </v-list-item> -->
                                            </v-list-item-group>
                                        </v-list>
                                    </v-card>
                                </v-menu>
                            </v-col>
                </v-row>
                <v-row v-else>
                    <div>
                        <NuxtLink to="/login-admin">
                            <button class="mr-2">
                                <v-toolbar-title class="secondaryColor--text"> Acceso de administrador </v-toolbar-title>
                            </button>
                        </NuxtLink>
                    </div>
                </v-row>
            </v-toolbar>
        </div>
</template>
<script>
    export default {
        props:{
            userType:{
                type: String,
                required:false,
                default:"visitor"
            },
        },
        data() {
            return{
                title:"Logo Mexico",
                links:[
                    {
                        name: 'Gobierno',
                        url: ''
                    },
                    {
                        name: 'Participa',
                        url: ''
                    },
                    {
                        name: 'Datos',
                        url: ''
                    }
                ],
                navButtons:[
                    {
                        name: 'Inicio',
                        url: '/dashboard'
                    },
                    {
                        name: 'Descargables',
                        url: '/downloads'
                    },
                    // {
                    //     name: 'Empresas',
                    //     url: ''
                    // },
                    {
                        name: 'Registro al PED',
                        url: '/student-register'
                    },
                ]
            }
        },
        created(){
        },
        methods:{
            goToPage(page) {
			this.$router.push({
				name: page
			})
		
            }
        }
}
</script>
<style scoped>
.secondaryColor--text{
  color:#2CA58D;
}
</style>