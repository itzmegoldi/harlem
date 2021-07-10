<template>
    <div>
        <v-card class="card-datatable">
            <v-card-text>
                <v-row no-gutters>
                <v-col xs="6">
                <v-text-field
                outlined
                dense
                label="Search by School name"
                append-icon="mdi-magnify"
                type="text"
                color="#38227A"
                class="search-input"
                >
                </v-text-field>
                </v-col>
                <v-col class="d-flex d-sm-none" cols="2">
                    <v-menu offset-y>
                        <template v-slot:activator="{ on, attrs }">
                            <v-icon
                            v-bind="attrs"
                            v-on="on"
                            class="mobile-menu"
                            >mdi-menu</v-icon>
                        </template>
                        <v-list>
                            <v-list-item-group active-class="active-class">
                            <v-list-item
                            @click="openForm()"
                            >
                            <v-list-item-title>
                            Add School
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
                <v-spacer></v-spacer>
                <v-col class="d-none d-sm-flex" cols="2">
                     <v-btn
                    color="#38227A"
                    dark
                    @click="openForm()"
                    class="text-capitalize"
                    >
                    Add School
                    </v-btn>
                </v-col>
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
        >

            <template v-slot:item="row" >
                <tr class="text-flex">
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
                  <td class="text-center row-item" >
                        <tr>
                            <td style="font-size:14px;">{{row.item.contact_person}}</td>
                            </tr>
                            <tr>
                                <td style="font-size:10px;color:grey;">{{row.item.cont_person_email}}</td>
                            </tr>
                            <tr>
                                <td style="font-size:10px;color:grey;">{{row.item.cont_person_phone}}</td>
                            </tr>
                  
                  </td>
                  <td class="text-center row-item" >{{row.item.city}}/{{row.item.state}}</td>
                  <td class="text-center row-item" >{{row.item.lead_group}}</td>
                  <td class="text-center row-item" >{{row.item.sales_rep}}</td>
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
                    <p class="footer_p">Show</p>
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
        <SchoolCrudForm :SchoolFormData="SchoolFormData" v-if="SchoolFormData.flag" />
    </div>
</template>
<script>
import SchoolCrudForm from "./SchoolCrudForm"
export default {
    name:'SchoolDataTable',
    components:{ SchoolCrudForm},
    data(){
        return {

            headers: [
                {
                text: "School Info",
                align: "center",
                value: "school_info",
                class: "grey lighten-4"
                },
                {
                text: "Contact Person Info",
                align: "center",
                value: "contact_person",
                class: "grey lighten-4"
                },
                {
                text: "City/State",
                align: "center",
                value: "city_state",
                class: "grey lighten-4"
                },
                {
                text: "The lead group",
                align: "center",
                value: "lead_group",
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
                SchoolFormData:{
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
          {info:'Test Elementry School',sub_text:'Test elementry district',contact_person:'Prashant Yadav',
          cont_person_phone:7898123091,cont_person_email:'prashant.yadav@codenicely.in',
          lead_group:'test elementry',sales_rep:'prashant yadav' ,url:"log.png",state:'Arizona',city:'hello',},
           {info:'Test Elementry School',sub_text:'Test elementry district',contact_person:'Prashant Yadav',
          cont_person_phone:7898123091,cont_person_email:'prashant.yadav@codenicely.in',
          lead_group:'test elementry',sales_rep:'prashant yadav' ,url:"log.png",state:'Arizona',city:'hello',},
           {info:'Test Elementry School',sub_text:'Test elementry district',contact_person:'Prashant Yadav',
          cont_person_phone:7898123091,cont_person_email:'prashant.yadav@codenicely.in',
          lead_group:'test elementry',sales_rep:'prashant yadav' ,url:"log.png",state:'Arizona',city:'hello',},
           {info:'Test Elementry School',sub_text:'Test elementry district',contact_person:'Prashant Yadav',
          cont_person_phone:7898123091,cont_person_email:'prashant.yadav@codenicely.in',
          lead_group:'test elementry',sales_rep:'prashant yadav' ,url:"log.png",state:'Arizona',city:'hello',},
           {info:'Test Elementry School',sub_text:'Test elementry district',contact_person:'Prashant Yadav',
          cont_person_phone:7898123091,cont_person_email:'prashant.yadav@codenicely.in',
          lead_group:'test elementry',sales_rep:'prashant yadav' ,url:"log.png",state:'Arizona',city:'hello',},
           {info:'Test Elementry School',sub_text:'Test elementry district',contact_person:'Prashant Yadav',
          cont_person_phone:7898123091,cont_person_email:'prashant.yadav@codenicely.in',
          lead_group:'test elementry',sales_rep:'prashant yadav' ,url:"log.png",state:'Arizona',city:'hello',},
  
      ]
        }
    },
    methods:{
        openForm(){
            this.SchoolFormData.flag=true
            this.SchoolFormData.type='add'
        },
        editForm(item){
            this.SchoolFormData.flag=true
            this.SchoolFormData.type='edit'
            this.SchoolFormData.item=item
        },
        viewForm(item){
            this.SchoolFormData.flag=true
            this.SchoolFormData.disabled=true
            this.SchoolFormData.item=item
            this.SchoolFormData.type='view'
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
margin-left: 8px;
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
    
    .footer-card.v-card{
        max-height: 200px;
        align-items: center;
        text-align: center;
        }
    .footer_p{
    margin-left: 45px;
    }
    .v-input.search-input{
    width: 240px;
    
    }
    .v-icon.notranslate.mobile-menu{
    position: relative;
    left: 20px;
    bottom: 13px;
    }
    .v-data-table-header{
    display: flex;
    width: 100%;
    overflow-x: scroll;
    }
}
</style>