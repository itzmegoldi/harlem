<template>
    <div>
    <v-dialog
        persistent
        v-model="CampaignDialogData.flag"
        max-width="500px"
        max-height="800px"
        >
            <v-card style="background-color:#F2F2F2;">
            <v-card-title
            class="headline darken-1"
            style="background-color:#E7E5ED;color:black;height:100px"
            
            >
            <div 
            style="margin-top:10px;margin-left:10px;width:415px;">Please provide below details <br> to 
             publish this campaign</div>
            <v-spacer></v-spacer>
            <v-icon text color="black" @click="CloseForm"  
            style="cursor:pointer;margin-right:0px;"
                >mdi-close
            </v-icon>
            </v-card-title><br><br>
            <v-card-text>
                <v-row ><p 
                style="font-size:20px;border-bottom:2px solid #2C1963;color:#2C1963;margin-left:20px;"
                >Basic Information</p></v-row>
                <v-row>
                <v-col cols="6">
                    <v-icon class="ml-1" color="red">mdi-close</v-icon>
                    <p style="float:right;margin-right:80px;color:black">Campaign Type</p>
                </v-col>
                <v-col v-if="CampaignDialogData.campaign_type=='district'" cols="6">
                    <v-icon  class="ml-1" color="red">mdi-close</v-icon>
                    <p style="float:right;margin-right:80px;color:black">Select District</p>
                </v-col>
                <v-col v-if="CampaignDialogData.campaign_type=='school'"  cols="6">
                    <v-icon class="ml-1" color="red">mdi-close</v-icon>
                    <p style="float:right;margin-right:80px;color:black">Select school</p>
                </v-col>
                <v-col  cols="6">
                    <v-icon class="ml-1" color="red">mdi-close</v-icon>
                    <p style="float:right;margin-right:100px;color:black">Host Name</p>
                </v-col>
                <v-col cols="6">
                    <v-icon class="ml-1" color="red">mdi-close</v-icon>
                    <p style="float:right;margin-right:100px;color:black">Host Email</p>
                </v-col>
                </v-row>
                <v-row>
                <p 
                style="font-size:20px;border-bottom:2px solid #2C1963;color:#2C1963;margin-left:20px;"
                >Incentives</p>
                </v-row>
                <v-row>
                <v-col cols="6">
                    <v-icon class="ml-1" color="red">mdi-close</v-icon>
                    <p style="float:right;margin-right:60px;color:black">Teacher Incentives</p>
                </v-col>
                <v-col  cols="6">
                    <v-icon class="ml-1" color="red">mdi-close</v-icon>
                    <p style="float:right;margin-right:60px;color:black">Student Incentives</p>
                </v-col>
                </v-row>
                <v-row>
                <p 
                style="font-size:20px;border-bottom:2px solid #2C1963;color:#2C1963;margin-left:20px;"
                >Timeline/Events</p>
                </v-row>
                <v-row>
                <v-col cols="6">
                    <v-icon class="ml-1" color="red">mdi-close</v-icon>
                    <p style="float:right;margin-right:5px;color:black">Graduation Celebration Day</p>
                </v-col>
                
                </v-row>
            </v-card-text>
            </v-card>
    </v-dialog>
    </div>
</template>
<script>
export default {
    name:'CampaignDialog',
    props:['CampaignDialogData'],
    data(){
        return{

        }
    },
    methods:{
        CloseForm(){
            this.CampaignDialogData.flag=false
        }
    }
}
</script>