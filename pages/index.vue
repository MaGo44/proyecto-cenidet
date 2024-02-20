<template>
    <div class="content-style" align="center">
          <v-row class="mb-5 mt-7" justify="center">
            <v-col cols="12">
              <h1 class="h1-style">Selecciona tu perfil:</h1>
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="6">
              <v-card class="card-style" @click="goToPage('login-student')">
                <v-col align="center" class="mt-5">
                  <v-row justify="center"> 
                    <div>
                      Soy estudiante
                    </div>
                  </v-row>
                  <v-icon size="250">
                      mdi-account-school
                  </v-icon>
                </v-col>
              </v-card>
            </v-col>
            <v-col cols="6">
              <v-card class="card-style" @click="goToPage('login-admin')">
                <v-col align="center" class="mt-5">
                  <v-row justify="center">
                    <div>
                      Soy administrador
                    </div>
                </v-row>
                  <v-icon size="250">
                      mdi-account
                  </v-icon>
                </v-col>
              </v-card>
            </v-col>
          </v-row>
    </div>
</template>

<script>
export default {
  name: 'IndexPage',
  layout: 'default',
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
h1.h1-style {
  font-size: 27px;
  color:#361D2E;
}
.content-style {
  height: 100%;
}
.row-style{
    margin: 0 10%;
}
.primaryColor--text{
  color:#E07A5F;
}
.secondaryColor--text{
  color:#2CA58D;
}
.card-style{
  width: 400px;
  height:300px;
  display: flex;
  justify-content: center; /* Centrar horizontalmente */
  align-items: center;
}
</style>