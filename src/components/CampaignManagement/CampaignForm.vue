<template>
  <div>
    <v-card>
      <v-container>
        <v-col cols="8">
        <v-card-title style="border-bottom:2px solid #2C1963;color:#2C1963;width:250px;height:50px">
          Basic Information  
        </v-card-title>
        <hr>
        </v-col>

        <v-card-text>
          <v-from>
            <v-row no-gutters>
              <v-col cols="8" xs="12">
                <v-row>
                  <v-col cols="4">
                     <p style="color:rgba(0, 0, 0, 0.6);font-size:17px">campaign type</p>
                    <v-radio-group small v-model="campaign_type" row>
                      <v-radio color="#2C1963" label="School" value="school"></v-radio>
                      <v-radio color="#2C1963" label="District" value="district"></v-radio>
                    </v-radio-group>
                  </v-col>
                </v-row>
           <v-row v-if="this.campaign_type == 'school'">
                <campaign-school-form ref="school_form"/>
           </v-row>
           <v-row v-if="this.campaign_type=='district'">
              <CampaignDistrictForm ref="district_form"/>
           </v-row>
              </v-col>
            </v-row>
          </v-from>
        </v-card-text>
        <br><br><br><br>
        <v-row>
              <div class="footer-sbt">
              <v-btn class="p-btn" @click="submitForm(campaign_type)">Publish</v-btn>
              <v-btn class="s-btn">Save as draft</v-btn>
              </div>
              </v-row>
      </v-container>
      
    </v-card>
    <br>
  </div>
</template>
<script>
import  CampaignSchoolForm from "./CampaignSchoolForm.vue"
import CampaignDistrictForm from "./CampaignDistrictForm.vue"
export default {
    name:"CampaignForm",
    components:{
      CampaignSchoolForm,
      CampaignDistrictForm
    },
    data(){
        return{
            campaign_type:'school',
            
        }
    },
    methods:{
        submitForm(campaign_type){
          if(campaign_type=='school'){
            this.$refs.school_form.submitForm(this.campaign_type)
          }else{
            this.$refs.district_form.submitForm(this.campaign_type)
          }
        }
    }
}
</script>
<style scoped>
.footer-sbt{
width: 100%;
height: 80px;
background-color: #E7E5ED;
float:right;
}
.v-btn{
float: right;
margin-right: 20px;
margin-top:20px;
}
.v-btn.p-btn{
color: white;
background-color: #38227A;
}
.v-btn.s-btn{
color:#38227A;
border: 0.5px solid #38227A;
background-color: white;
}

</style>