<template>
    <v-row justify="center">
        <v-dialog
        persistent
        v-model="SchoolFormData.flag"
        max-width="500px"
        max-height="800px"
        >
        <div class="text-center" v-if="loading" style="min-height:500px;">
            <v-progress-circular
            :size="100"
            :width="10"
            style="text-align:center;padding-top:20px;padding-bottom:20px;margin-top:200px"
            color="#7253CF"
            indeterminate
            ></v-progress-circular>
        </div>

            <v-card style="background-color:#F2F2F2;" v-if="!loading">
            <v-card-title
            class="headline darken-1"
            style="background-color:#7253CF;color:white;height:100px"
            
            >
            <div class="d-none d-sm-flex">
            <img src="basketball.png" height="85" width="100">
            </div> <div v-if="SchoolFormData.type == 'add'" 
            style="margin-top:-10px;margin-left:20px">Add new school</div>
            <div v-if="SchoolFormData.type=='edit'" 
            style="margin-top:-10px;margin-left:20px">Edit school</div>
            <div v-if="SchoolFormData.type=='view'" 
            style="margin-top:-10px;margin-left:20px">School details</div>
            <v-spacer></v-spacer>
            <v-icon text color="white" @click="CloseForm"  
            style="cursor:pointer;margin-top:-80px;margin-right:-15px;"
                >mdi-close
            </v-icon>
            </v-card-title>
            <v-form>
                <v-card-text >
                    <v-row class="logo-row" style="margin-top:20px">
                        <v-col v-if="previewImage" cols="5">
                            <img
                            :src="previewImage"
                            alt=""
                            class="logo"
                            />
                        </v-col>
                        <v-col class="file-input-col" cols="5">
                        <div v-if="SchoolFormData.type=='add'" class="label-div">
                            <label for="inputId">Upload logo</label>
                        </div>
                        <div v-if="SchoolFormData.type=='edit'" class="label-div">
                            <label for="inputId">Change logo</label>
                        </div>
                        <v-file-input
                            prepend-icon
                            outlined
                            label="upload logo"
                            color="#7253CF"
                            dense
                            class="file-input"
                            id="inputId"
                            @change="onFileChange"
                            style="display:none">
                            </v-file-input>
                            
                        </v-col>
                        <p v-if="!previewImage && this.SchoolFormData.type=='add'" 
                        class="logo-des">Please upload a 
                        logo for district,file size should be less than 10 mb</p>
                    </v-row>
                    <v-row no-gutters justify="center">
                        <v-col cols="10">
                            <v-text-field
                            outlined
                            dense
                            v-model="school_name"
                            :rules="nameRules"
                            label="School name"
                            color="#7253CF"
                            :disabled="SchoolFormData.disabled">
                            </v-text-field>
                        </v-col>
                        <v-col cols="5">
                            <v-text-field
                            outlined
                            dense
                            v-model="cont_per_name"
                            label="Contact person name"
                            color="#7253CF"
                            class="left-input"
                            :disabled="SchoolFormData.disabled">
                            </v-text-field>
                        </v-col>
                        <v-col cols="5">
                            <v-text-field
                            outlined
                            dense
                            v-model="designation"
                            label="Designation"
                            color="#7253CF"
                            class="right-input"
                            :disabled="SchoolFormData.disabled"></v-text-field>
                        </v-col>      
                        <v-col cols="5">
                            <v-text-field
                            outlined
                            dense
                            :rules="contactPersonRules"
                            v-model="mobile"
                            label="Contact person phone"
                            color="#7253CF"
                            class="left-input"
                            :disabled="SchoolFormData.disabled">
                            </v-text-field>
                        </v-col>
                        <v-col cols="5">
                            <v-text-field
                            outlined
                            dense
                            :rules="roleRules"
                            v-model="email"
                            label="Contact person email"
                            color="#7253CF"
                            class="right-input"
                            :disabled="SchoolFormData.disabled"></v-text-field>
                        </v-col>
                        <v-col  cols="5">
                            <v-text-field
                            outlined
                            dense
                            v-model="city"
                            :rules="cityRules"
                            label="City"
                            color="#7253CF"
                            class="left-input"
                            :disabled="SchoolFormData.disabled">
                            </v-text-field>
                        </v-col>
                        <v-col cols="5">
                            <v-autocomplete
                            outlined
                            dense
                            :rules="stateRules"
                            v-model="state"
                            :items="states"
                            label="State"
                            color="#7253CF"
                            class="right-input"
                            :disabled="SchoolFormData.disabled">
                            </v-autocomplete >
                        </v-col>
                        <v-col cols="10">
                            <v-textarea
                            outlined
                            dense
                            v-model="shipping_address"
                            :rules="nameRules"
                            label="Shipping Address"
                            color="#7253CF"
                            class="shipping-input"
                            :disabled="SchoolFormData.disabled">
                            </v-textarea>
                        </v-col>
                        <v-col  cols="5">
                            <v-text-field
                            outlined
                            dense
                            v-model="lead_group"
                            
                            label="Lead Group"
                            color="#7253CF"
                            class="left-input"
                            :disabled="SchoolFormData.disabled">
                            </v-text-field>
                        </v-col>
                        <v-col cols="5">
                            <v-autocomplete
                            outlined
                            dense
                        
                            v-model="sales_rep"
                            
                            label="sales REP"
                            color="#7253CF"
                            class="right-input"
                            :disabled="SchoolFormData.disabled">
                            </v-autocomplete >
                        </v-col>
                        <v-col cols="5">
                            <v-btn v-if="this.SchoolFormData.type=='add'" 
                             class="submit-btn" dark color="#38227A"
                             @click="saveForm">Add school</v-btn>
                            <v-btn v-if="this.SchoolFormData.type=='edit'" 
                            class="submit-btn-edit" dark color="#38227A">save</v-btn>
                        </v-col>
                    </v-row>
                </v-card-text>
            </v-form>
            </v-card>
        </v-dialog>
    </v-row>
</template>
<script>
export default {
    name:"SchoolCrudForm.vue",
    props:['SchoolFormData'],
    data(){
        return {
            states:[
                "Alabama","Alaska","American Samoa","Arizona","Arkansas","California","Colorado",
                "Connecticut","Delaware","District Of Columbia","Federated States Of Micronesia",
                "Florida","Georgia","Guam","Hawaii","Idaho","Illinois","Indiana","Iowa","Kansas",
                "Kentucky","Louisiana","Maine","Marshall Islands","Maryland","Massachusetts","Michigan",
                "Minnesota","Mississippi","Missouri","Montana","Nebraska","Nevada","New Hampshire",
                "New Jersey","New Mexico","New York","North Carolina","North Dakota",
                "Northern Mariana Islands","Ohio","Oklahoma","Oregon","Palau","Pennsylvania","Puerto Rico",
                "Rhode Island","South Carolina","South Dakota","Tennessee","Texas","Utah","Vermont",
                "Virgin Islands","Virginia","Washington","West Virginia","Wisconsin","Wyoming"
            ],
            loading:false,
            previewImage:null,
            school_name:'',
            nameRules: [
                v => !!v || 'Required',
            ],
            city:'',
            cityRules:[
                v=> !!v || 'Required'
            ],
            state:'',
            stateRules:[
                v => !!v || 'Required'
            ],
            cont_per_name:'',
            contactPersonRules:[
                v => !!v || 'Required'
            ],
            designation:'',
            role:'',
            roleRules:[
                v => !!v || 'Required'
            ],
            email:'',
            emailRules:[
                v => !!v || 'Required',
                v => /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail must be valid'
            ],
            mobile:null,
            mobileRules:[
                v => !!v || "Required",
                v => /^\(?(\d{3})\)?[- ]?(\d{3})[- ]?(\d{4})$/.test(v) || 'Mobile Number must be valid'
            ],
            shipping_address:'',
            lead_group:'',
            sales_rep:[]

        }
    },
    methods:{
        CloseForm(){
            this.SchoolFormData.flag=false
            this.SchoolFormData.type=''
            this.SchoolFormData.item=[]
            this.SchoolFormData.disabled=false
            this.district_name='',
            this.previewImage=null,
            this.city='',
            this.state='',
            this.cont_per_name='',
            this.role='',
            this.email='',
            this.mobile=null

        },
        onFileChange(payload) {
            //const file = payload.target.files[0]; // use it in case of normal HTML input
            const file = payload; // in case vuetify file input
            if (file) {
                this.previewImage = URL.createObjectURL(file);
                URL.revokeObjectURL(file); // free memory
            } else {
                this.previewImage =  null
            }
        },
        editDataOnload(){
            console.log('hello',this.SchoolFormData.item)
            
            this.previewImage=this.SchoolFormData.item.url
            this.district_name=this.SchoolFormData.item.info
            this.city=this.SchoolFormData.item.city
            this.state=this.SchoolFormData.item.state
            this.cont_per_name=this.SchoolFormData.item.contact_person
            this.role=this.SchoolFormData.item.role
            this.email = this.SchoolFormData.item.email
            this.mobile = this.SchoolFormData.item.mobile
        },
        saveForm(){
            this.loading=true
            setTimeout(()=>{
                this.loading=false
            },2000)
        }
    },
    mounted(){
        if (this.SchoolFormData.type=='view' || this.SchoolFormData.type=='edit'){
            this.editDataOnload()
        }
            
        }
}
</script>
<style scoped>
.v-input.left-input{
width: 180px;
}
.v-input.right-input{
width:180px;
margin-left:10px;
}
.v-input.shipping-input{
width: 400px;
}
.logo-preview{
height: 100px;
width: 200px;
position: relative;
bottom: 30px;
}
.logo-des{
font-size:12px;
margin-top:-10px;
margin-left: 50px;
}
.row.logo-row{
min-height: 100px;
margin-bottom: 10px;
}
.file-input-col{
margin-left:40px
}
.label-div{
width: 110px;
height: 30px;
border:1px solid #38227A;
border-radius: 10px;
text-align: center;
color:#38227A ;
padding: 4px;
margin-top:20px
}
.label-div:hover{
background-color: #38227A;
color:white;
}
.label-div:active{
background-color:white;
color:#38227A;
}
img.logo{
margin-left:40px;
max-width: 180px;
max-height: 80px;
}
.v-btn.submit-btn{
margin-left:150px;
margin-bottom: 25px ;
}
.v-btn.submit-btn-edit{
margin-left:215px;
margin-bottom: 25px ;
}
@media (min-width:0px) and (max-width:600px ) {
    .v-input.right-input{
        margin-left:10px;
        width:110px
    }
    .v-input.left-input{
        width: 110px;
    }
    .v-btn.submit-btn{
    margin-left:80px;
    width: 120px;
    }
    .v-btn.submit-btn-edit{
    margin-left: 120px;
    }
}
</style>