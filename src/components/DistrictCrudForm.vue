<template>
    <v-row justify="center">
        <v-dialog
        persistent
        v-model="DistrictFormData.flag"
        max-width="500px"
        max-height="800px"
        >
            <v-card style="background-color:#F2F2F2;" v-if="!loading">
            <v-card-title
            class="headline darken-1"
            style="background-color:#7253CF;color:white;height:100px"
            
            >
            Add new district
            <v-spacer></v-spacer>
            <v-icon  text color="white" @click="CloseForm" large style="cursor"
                >mdi-close
            </v-icon>
            </v-card-title>
            <v-form>
                <v-card-text >
                    <v-row justify="center" style="margin-top:20px">
                        
                        <v-col cols="4">
                            <v-file-input
                            prepend-icon
                            outlined
                            label="upload logo"
                            color="#7253CF"
                            dense>
                            </v-file-input>
                        </v-col>
                        <p style="font-size:12px;margin-top:-35px">Please upload a logo for district,file size should be less than 10 mb</p>
                    </v-row>
                    <v-row justify="center">
                        <v-col cols="10">
                            <v-text-field
                            outlined
                            dense
                            label="District name">
                            </v-text-field>
                        </v-col>
                    </v-row>
                    <v-row justify="center">
                        <v-col cols="5">
                            <v-text-field
                            outlined
                            dense
                            label="City">
                            </v-text-field>
                        </v-col>
                        <v-col cols="5">
                            <v-autocomplete
                            outlined
                            dense
                            label="State">
                            </v-autocomplete>
                        </v-col>
                    </v-row>
                    <v-row justify="center">
                        <v-col cols="5">
                            <v-text-field
                            outlined
                            dense
                            label="Contact person name">
                            </v-text-field>
                        </v-col>
                        <v-col cols="5">
                            <v-text-field
                            outlined
                            dense
                            label="Role"></v-text-field>
                        </v-col>
                    </v-row>
                    <v-row justify="center">
                        <v-col cols="5">
                            <v-text-field
                            outlined
                            dense
                            label="Email">
                            </v-text-field>
                        </v-col>
                        <v-col cols="5">
                            <v-text-field
                            outlined
                            dense
                            label="Mobile"></v-text-field>
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
    name:"DistrictCrudForm.vue",
    props:['DistrictFormData'],
    methods:{
        CloseForm(){
            this.DistrictFormData.flag=false
        }
    }
}
</script>