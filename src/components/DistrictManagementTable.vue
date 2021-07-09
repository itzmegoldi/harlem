<template>
    <div>
        <v-card class="card-datatable">
            <v-card-text>
                <v-row no-gutters>
                <v-col  cols="12" xs="8" sm="3">
                <v-text-field
                outlined
                dense
                label="Search by district"
                append-icon="mdi-magnify"
                type="text"
                color="#38227A"
                >
                </v-text-field>
                </v-col>
                <v-spacer></v-spacer>
                <v-col class="d-none d-sm-flex" cols="2">
                    <v-btn
                    text
                    style="border:1px solid #38227A"
                    class="text-capitalize"
                    @click="route"
                    >
                    bulk import
                    </v-btn>
                </v-col>
                <v-col class="d-none d-sm-flex" cols="2">
                    <v-btn
                    color="#38227A"
                    dark
                    @click="openForm()"
                    class="text-capitalize"
                    >
                    Add district
                    </v-btn>
                </v-col>
                <v-col class="d-flex d-sm-none" cols="1">
                    <v-menu offset-y>
                        <template v-slot:activator="{ on, attrs }">
                            <v-icon
                            v-bind="attrs"
                            v-on="on"
                            >mdi-menu</v-icon>
                        </template>
                        <v-list>
                            <v-list-item-group active-class="active-class">
                            <v-list-item
                            @click="openForm()"
                            >
                            <v-list-item-title>
                            Add District
                            </v-list-item-title>
                            </v-list-item>
                            <v-list-item
                            @click="route">
                            <v-list-item-title>
                            Bulk Import
                            </v-list-item-title>
                            </v-list-item>
                            </v-list-item-group>
                        </v-list>
                    </v-menu>
                </v-col>
                </v-row>
            </v-card-text>
        </v-card>
        <v-data-table
        fixed-header
        hide-default-footer
        :headers="headers"
        :items="dummyData"
        :loading="loader"
        loading-text="Loading... Please wait"
        class="elevation-1"
        mobile-breakpoint="0"
        :sort-by="[district_info,no_schools,no_campaigns,fund,last_wizfit,sales_rep]"
        >

            <template v-slot:item="row" >
                <tr>
                  <td class="text-center row-item"  divider: true>
                    
                    <tr>
                        <v-avatar size="40">
                                <v-img :src="row.item.url"></v-img>
                        </v-avatar>
                        <td>
                            <tr>
                            <td style="font-size:14px;">{{row.item.info}}</td>
                            </tr>
                            <tr>
                                <td style="font-size:10px;color:grey;text-align:left">{{row.item.sub_text}}</td>
                            </tr>    
                        </td>
                    </tr>
                    
                  </td>
                  <td class="text-center row-item" >{{row.item.no_school}}</td>
                  <td class="text-center row-item" >{{row.item.no_campaigns}}</td>
                  <td class="text-center row-item" >{{row.item.fund}}</td>
                  <td class="text-center row-item" >{{row.item.last}}</td>
                  <td class="text-center row-item" >{{row.item.saleRep}}</td>
                  <td class="text-center row-item" > 
                    
                    <tr>
                        <td>
                            <v-chip small @click="viewForm(row.item)">
                            <v-tooltip bottom>
                                <template v-slot:activator="{ on, attrs }">
                                    <v-icon
                                    dark
                                    v-bind="attrs"
                                    v-on="on"
                                    class="icons"
                                    color="#6B6B6B"
                                    small
                                    >
                                    mdi-eye
                                    </v-icon>
                                </template>
                                <span>view</span>
                            </v-tooltip>
                            </v-chip>

                            <v-chip small @click="editForm(row.item)">
                            <v-tooltip  bottom>
                                <template v-slot:activator="{ on, attrs }">
                                    <v-icon
                                    dark
                                    v-bind="attrs"
                                    v-on="on"
                                    class="icons"
                                    color="#6B6B6B"
                                    small
                                    >
                                    mdi-pencil
                                    </v-icon>
                                </template>
                                <span>Edit</span>
                            </v-tooltip>
                            </v-chip>
                            <v-menu offset-y>
                            <template v-slot:activator="{ on, attrs }">
                                
                                <v-chip small
                                v-bind="attrs"
                                v-on="on">
                                <v-icon
                                color="#6B6B6B" small>mdi-dots-horizontal</v-icon>
                                </v-chip>
                            </template>
                            <v-list>
                                <v-list-item-group>
                                <v-list-item
                                >
                                <v-list-icon><v-icon>mdi-bullhorn</v-icon></v-list-icon>
                                <v-list-item-title>
                                Start a New Campaign
                                </v-list-item-title>
                                </v-list-item>
                                <v-list-item
                                >
                                <v-list-icon><v-icon>mdi-file-find</v-icon></v-list-icon>
                                <v-list-item-title>
                                View Campaigns
                                </v-list-item-title>
                                </v-list-item>
                                </v-list-item-group>
                            </v-list>
                        </v-menu>
                        </td>
                    </tr>
                  </td>
                </tr>
            </template>
        </v-data-table>
        <v-card class="footer-card">
            <v-card-text>
                <v-row  no-gutters>
                <v-col cols="12" xs="12" sm="6" md="6">
                    <div style="display:flex">
                    <p class="footer_p">show</p>
                    <p><v-autocomplete
                    class="footer-input"
                    :items="itemPerPage"
                    dense
                    color="#38227A"
                    v-model="itemPage"
                    ></v-autocomplete> </p> 
                    
                    <p style="margin-left:25px;margin-right:15px;margin-top:8px;color:black;"
                    >1-{{itemPage}} of 2020</p>   
                    </div>
                </v-col>
                <v-spacer></v-spacer>
                <v-col cols="12" xs="12" sm="4" md="3">
                <div><v-pagination
                v-model="page"
                :length="pageCount"
                color="#EE1F51"
                >
                </v-pagination></div>
                </v-col>
                </v-row>
            </v-card-text>
        </v-card>
        <district-crud-form :DistrictFormData="DistrictFormData" v-if="DistrictFormData.flag"/>
    </div>
</template>
<script>
import DistrictCrudForm from "./DistrictCrudForm.vue"
export default {
    name:'DistrictManagementTable',
    components:{DistrictCrudForm},
    data(){
        return {

            headers: [
                {
                text: "District Info",
                align: "center",
                value: "district_info",
                class: "grey lighten-4"
                },
                {
                text: "#Schools",
                align: "center",
                value: "no_schools",
                class: "grey lighten-4"
                },
                {
                text: "#Campaigns",
                align: "center",
                value: "no_campaigns",
                class: "grey lighten-4"
                },
                {
                text: "Total Fund Raised",
                align: "center",
                value: "fund",
                class: "grey lighten-4"
                },
                {
                text: "LastWizfit",
                value: "no_student",
                align: "center",
                class: "grey lighten-4"
                },
                
                {
                text: "salesREP",
                value: "sales_rep",
                class: "grey lighten-4",
                align: "center"
                },
                {
                sortable: false,
                text: "Actions",
                value: "icon",
                class: "grey lighten-4",
                align: "center"
                },
            ],
                loader:false,
                DistrictFormData:{
                    flag:false,
                    loading:false,
                    disabled:false,
                    type:'add',
                    item:[]
                },
                itemPerPage:[10,15,20,25,50,100],
                itemPage:10,
                page:1,
                pageCount:4,

      dummyData:[
          {info:'lousiana school district',sub_text:'hi i am sub text',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav",url:"basketball.png",state:'Arizona',city:'hello',
           contact_person:"Prashant Yadav",role:"Admin",email:'prashant.yadav@codenicely.in',
           mobile:7898123091},
          {info:'lousiana school district',sub_text:'hi i am sub text',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav",url:"basketball.png"},
          {info:'lousiana school district',sub_text:'hi i am sub text',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav",url:"basketball.png"},
          {info:'lousiana school district',sub_text:'hi i am sub text',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav",url:"basketball.png"},
          {info:'lousiana school district',sub_text:'hi i am sub text',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav",url:"basketball.png"},
          {info:'lousiana school district',sub_text:'hi i am sub text',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav",url:"basketball.png"},
          {info:'lousiana school district',sub_text:'hi i am sub text',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav",url:"basketball.png"},
          {info:'lousiana school district',sub_text:'hi i am sub text',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav",url:"basketball.png"},
          {info:'lousiana school district',sub_text:'hi i am sub text',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav",url:"basketball.png"},
          {info:'lousiana school district',sub_text:'hi i am sub text',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav",url:"basketball.png"},
          {info:'lousiana school district',sub_text:'hi i am sub text',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav",url:"basketball.png"},
          {info:'lousiana school district',sub_text:'hi i am sub text',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav",url:"basketball.png"},
      ]
        }
    },
    methods:{
        openForm(){
            this.DistrictFormData.flag=true
            this.DistrictFormData.type='add'
        },
        editForm(item){
            this.DistrictFormData.flag=true
            this.DistrictFormData.type='edit'
            this.DistrictFormData.item=item
        },
        viewForm(item){
            this.DistrictFormData.flag=true
            this.DistrictFormData.disabled=true
            this.DistrictFormData.item=item
            this.DistrictFormData.type='view'
        },
        route(){
            this.$router.push('/upload')
        }
    }
}
</script>
<style scoped>
.active-class{
    border-right:4px solid #38227A;
    border-left:4px solid #38227A;
    border-radius: 4px;
}
.card-datatable.v-card{
    max-height: 70px;
    margin-bottom: -2px;
    display: flex;
}
.text-capitalize.v-btn{
    width:150px;
}
.v-chip{
border-radius:4px;
margin-left: 5px;
}
.footer-input.v-input{
width: 60px;
padding: 0%;

}
.footer-card.v-card{
max-height: 70px;
}
.footer_p{
margin-left:25px;
margin-right:15px;
margin-top:8px;
color:black
}
@media (min-width:0px) and (max-width:600px ){
    .card-datatable.v-card{
        max-height: 150px;
    }
    .footer-card.v-card{
        max-height: 200px;
        align-items: center;
        text-align: center;
        }
    .footer_p{
    margin-left: 45px;
    }
}
</style>