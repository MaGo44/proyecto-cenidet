<template>
    <div class="content-style" align="center">
        <v-row align="center" class="row-style">
            <v-col cols="6">
            <v-card class="card-style" @click="goToPage('login-student')">
              <v-col align="center">
                <v-row class="text-center"> 
                Soy estudiante
              </v-row>
                <v-icon size="250">
                    mdi-account
                </v-icon>
              </v-col>
            </v-card>
            </v-col>
            <v-col cols="6">
            <v-card class="card-style" @click="goToPage('login-admin')">
              <v-col align="center">
                <v-row class="text-center">
                Soy administrador
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
  font-size: 80px;
  color:#361D2E;
}
.content-style {
  background-color: #F8F7FF;
  height: 500px;
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
  width: 500px;
}
</style>