<template>
    <div class="container_main" style="height: 100%">
        <v-container>
        <v-row align="center" justify="center" class="margin-row container_main">
            <v-col cols="12">
                <!-- <h4 class="mt-5">
                    {{ title }}
                </h4>
                <h3 class="mt-5">
                    {{ subtitle }}
                </h3> -->
                <h1 class="primaryColor--text mb-5" align="center">
                    Registro al modelo de educación dual
                </h1>
            </v-col>
            <v-col cols="12">
                <v-stepper v-model="activeStep" class="no-border no-elevation container_main">
                    <v-stepper-header class="no-border no-elevation textfields-form-p">
                        <v-stepper-step
                            :color="'#2CA58D'"
                            :complete="activeStep > 1"
                            step="1">
                        </v-stepper-step>
                        <v-divider />
                        <v-stepper-step
                            :color="'#2CA58D'"
                            :complete="activeStep > 2"
                            step="2">
                        </v-stepper-step>
                        <v-divider />
                        <v-stepper-step
                            :color="'#2CA58D'"
                            :complete="activeStep > 3"
                            step="3">
                        </v-stepper-step>
                        <v-divider />
                        <v-stepper-step
                            :color="'#2CA58D'"
                            :complete="activeStep > 4"
                            step="4">
                        </v-stepper-step>
                    </v-stepper-header>
                    <v-stepper-items class="textfields-form">
                        <v-stepper-content step="1">
                            <StudentPeriod
                                :periods="periods"
                                event-next-step="NEXT_STEP_REGISTER_COMPANY"
                                event-previous-step="PREVIOUS_STEP_REGISTER_COMPANY"
                                @set-period="setPeriod" />
                        </v-stepper-content>
                        <v-stepper-content step="2">
                            <StudentInfo
                                ref="studentInfoComponent"
                                :careers="careers"
                                :genders="genders"
                                @set-student-info="setStudentInfo"
                                @set-student-image="submitFiles"
                                event-next-step="NEXT_STEP_REGISTER_COMPANY"
                                event-previous-step="PREVIOUS_STEP_REGISTER_COMPANY" />
                        </v-stepper-content>
                        <v-stepper-content step="3">
                            <ProjectInfo
                                :companies="companies"
                                :advisers="advisers"
                                @set-project-info="setProjectInfo"
                                event-next-step="NEXT_STEP_REGISTER_COMPANY"
                                event-previous-step="PREVIOUS_STEP_REGISTER_COMPANY" />
                        </v-stepper-content>
                        <v-stepper-content step="4">
                            <StudentDocuments
                              :student-id="registerStudentInfo.student_id"
                              event-next-step="NEXT_STEP_REGISTER_COMPANY"
                              event-previous-step="PREVIOUS_STEP_REGISTER_COMPANY" />
                        </v-stepper-content>
                    </v-stepper-items>
                </v-stepper>
            </v-col>
        </v-row>
    </v-container>
    </div>
</template>
<script>
import axios from "axios";
import StudentPeriod from "@/components/base/StudentPeriod"
import StudentInfo from "@/components/base/StudentInfo"
import ProjectInfo from "@/components/base/ProjectInfo"
import StudentDocuments from "@/components/base/StudentDocuments"

export default {
    components: {
    StudentPeriod,
    StudentInfo,
    ProjectInfo,
    StudentDocuments
  },
  layout: "internalLayout",
  data() {
    return {
      token: '9260023c-3deb-4b2d-bb8d-bb595bbff9fc',
      periods:[],
      careers:[],
      genders:[],
      companies:[],
      advisers:[],
      title: "Ayúdanos con algunos datos",
      subtitle: "Completa tu registro",
      textButton: "Crear empresa",
      textButtonFinish: "Guardar información",
      registerStudentInfo: {},
      registerStudentProject: {
        project_period:'',
        student_id:null
      },
      activeStep: 1,
      step1: "Información de la empresa",
      step2: "Responsable",
      step3: "Documentación",
      step4: "Logotipo",
      step5: "Términos y condiciones",
      isLoadingBtnNext: false,
    }
  },

//   watch: {
//     activeStep(val) {
//       this.$store.commit("api/post/accounts/companies/setStepOnStepper", val)
//     },
//   },

  created() {
    axios.get('http://localhost:3100/api/periods',{
            headers:{
                'authorization':`Bearer ${this.token}`
            }
        }).then((response)=>{
            if(response.status === 200){
                this.periods=response.data
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
                this.careers=response.data
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
                this.genders=response.data
            }
            else{
            	console.log(response.status)
            }
        })

        axios.get('http://localhost:3100/api/company_info',{
            headers:{
                'authorization':`Bearer ${this.token}`
            }
        }).then((response)=>{
            if(response.status === 200){
                this.companies=response.data
            }
            else{
            	console.log(response.status)
            }
        })

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
      
    this.$nuxt.$on("NEXT_STEP_REGISTER_COMPANY", (_) => {
      this.activeStep++
    })
    this.$nuxt.$on("PREVIOUS_STEP_REGISTER_COMPANY", (_) => {
      this.activeStep--
    })
    // this.activeStep = this.$store.getters["api/post/accounts/companies/getCurrentStepOnStepper"]
  },
  beforeDestroy() {
    this.$nuxt.$off("NEXT_STEP_REGISTER_COMPANY")
    this.$nuxt.$off("PREVIOUS_STEP_REGISTER_COMPANY")
  },
  methods: {
    setPeriod(period){
      this.registerStudentProject.project_period=period
      console.log(this.registerStudentProject)
    },
    async setStudentInfo(studentInfo){
      this.registerStudentInfo=studentInfo
      await axios.post('http://localhost:3100/api/student_info', this.registerStudentInfo,{
        headers:{
          'authorization':`Bearer ${this.token}`,
          'content-type': 'application/json'
        }
        }).then((response)=>{
          if(response.status===200){
            console.log(response.data.student_id);
            this.registerStudentInfo=response.data
            console.log(this.registerStudentInfo.student_id);
            this.$refs.studentInfoComponent.submitFiles(this.registerStudentInfo.student_id);
          } 
          else{
            console.log(response.status);
          }
        })
      console.log(this.registerStudentInfo,'hola')
    },
    async setProjectInfo(projectInfo){
      this.registerStudentProject.student_id=this.registerStudentInfo.student_id
      for (const property in projectInfo) {
        this.registerStudentProject[property] = projectInfo[property]
      }
      await axios.post('http://localhost:3100/api/student_project', this.registerStudentProject,{
               headers:{
                   'authorization':`Bearer ${this.token}`,
                   'content-type': 'application/json'
               }
           }).then((response)=>{
               if(response.status==="200"){
                  console.log('Todo bien');
               }
               else{
                console.log(response.status);
               }
           })
      console.log(this.registerStudentProject)
    },
    nextStep() {
      this.activeStep += 1
    },
    trimEmail() {
      this.registerForm.email = this.registerForm.email.trim()
    },
  },
}
</script>
<style lang="scss" scoped>
.margin-row {
  margin: 0 5%;
}
.textfields-form {
  margin: 0 15%;
}
.textfields-form-p {
  padding: 0 27%;
}
.justify-content-center {
  justify-content: center;
}
.container_main {
  background-color: #F8F7FF;
}
h4 {
  font-weight: 400;
  font-size: 12px;
  line-height: 14px;
  text-align: center;
  text-transform: uppercase;
  color: #40484c;
}
h3 {
  font-weight: 600;
  font-size: 24px;
  line-height: 28px;
  text-align: center;
  color: #1a1c1e;
}
.no-border {
  border: none !important;
}

.no-elevation {
  box-shadow: none !important;
}
</style>