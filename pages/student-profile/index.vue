<template>
  <div class="content-style" align="center">
    <v-row align="center" class="row-style">
      <v-col cols="12">
        <v-tabs vertical>
          <v-tab>
              Mi información 
            </v-tab>
            <v-tab>
              Mi proyecto
            </v-tab>

          <v-tab-item>
            <v-card flat>
              <v-card-text>
                <h1>
                  Mi información
                </h1>
                <v-row>
                  <v-col cols="12" class="pb-0 mt-5">
                    <v-text-field 
                      outlined 
                      required
                      :rules="[v => !!v || 'Este campo es requerido']"
                      label="Nombre" />
                  </v-col>
                  <v-col cols="12" class="pb-0 mt-0 pt-0">
                    <v-text-field outlined label="Apellidos">
                    </v-text-field>
                  </v-col>
                  <v-col cols="6" class="pb-0 mt-0 pt-0">
                    <v-text-field outlined label="No. Control">
                    </v-text-field>
                  </v-col>
                  <v-col cols="6" class="pb-0 mt-0 pt-0">
                    <v-text-field outlined label="CURP">
                    </v-text-field>
                  </v-col>
                <v-col cols="12" class="pb-0 mt-0 pt-0">
                  <v-text-field outlined label="Correo">
                  </v-text-field>
                </v-col>
                <v-col cols="3" class="pb-0 mt-0 pt-0">
                  <v-text-field outlined label="Promedio">
                  </v-text-field>
                </v-col>
                <v-col cols="3" class="pb-0 mt-0 pt-0">
                  <v-text-field outlined label="Creditos acumulados">
                  </v-text-field>
                </v-col>
                <v-col cols="3" class="pb-0 mt-0 pt-0">
                  <v-text-field outlined label="Semestre">
                  </v-text-field>
                </v-col>
                <v-col cols="3" class="pb-0 mt-0 pt-0">
                  <v-text-field outlined label="Clave plan de estudio">
                  </v-text-field>
                </v-col>
                </v-row>
                <v-btn
                  block
                  outlined
                  disabled
                  color="#2CA58D"
                  class="border-rounded text-none"
                  @click="nextStep()">
                  Editar
                </v-btn>
              </v-card-text>
            </v-card>
          </v-tab-item>
          <v-tab-item>
            <v-card flat>
              <v-card-text>
                <p>
                  Morbi nec metus. Suspendisse faucibus, nunc et pellentesque egestas, lacus ante convallis tellus, vitae iaculis lacus elit id tortor. Sed mollis, eros et ultrices tempus, mauris ipsum aliquam libero, non adipiscing dolor urna a orci. Curabitur ligula sapien, tincidunt non, euismod vitae, posuere imperdiet, leo. Nunc sed turpis.
                </p>

                <p>
                  Suspendisse feugiat. Suspendisse faucibus, nunc et pellentesque egestas, lacus ante convallis tellus, vitae iaculis lacus elit id tortor. Proin viverra, ligula sit amet ultrices semper, ligula arcu tristique sapien, a accumsan nisi mauris ac eros. In hac habitasse platea dictumst. Fusce ac felis sit amet ligula pharetra condimentum.
                </p>

                <p>
                  Sed consequat, leo eget bibendum sodales, augue velit cursus nunc, quis gravida magna mi a libero. Nam commodo suscipit quam. In consectetuer turpis ut velit. Sed cursus turpis vitae tortor. Aliquam eu nunc.
                </p>

                <p>
                  Etiam ut purus mattis mauris sodales aliquam. Ut varius tincidunt libero. Aenean viverra rhoncus pede. Duis leo. Fusce fermentum odio nec arcu.
                </p>

                <p class="mb-0">
                  Donec venenatis vulputate lorem. Aenean viverra rhoncus pede. In dui magna, posuere eget, vestibulum et, tempor auctor, justo. Fusce commodo aliquam arcu. Suspendisse enim turpis, dictum sed, iaculis a, condimentum nec, nisi.
                </p>
              </v-card-text>
            </v-card>
          </v-tab-item>
          <v-tab-item>
            <v-card flat>
              <v-card-text>
                <p>
                  Fusce a quam. Phasellus nec sem in justo pellentesque facilisis. Nam eget dui. Proin viverra, ligula sit amet ultrices semper, ligula arcu tristique sapien, a accumsan nisi mauris ac eros. In dui magna, posuere eget, vestibulum et, tempor auctor, justo.
                </p>

                <p class="mb-0">
                  Cras sagittis. Phasellus nec sem in justo pellentesque facilisis. Proin sapien ipsum, porta a, auctor quis, euismod ut, mi. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nam at tortor in tellus interdum sagittis.
                </p>
              </v-card-text>
            </v-card>
          </v-tab-item>
        </v-tabs>
      </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  layout: "internalLayout",
}
</script>

<style scoped>
h1.h1-style {
  font-size: 80px;
  color:#361D2E;
}
.content-style {
  background-color: #F8F7FF;
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
}
</style>