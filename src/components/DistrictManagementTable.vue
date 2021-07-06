<template>
    <div>
        <v-data-table
        fixed-header
        :headers="headers"
        :items="dummyData"
        :loading="loader"
        loading-text="Loading... Please wait"
        class="elevation-1"
        :sort-by="[district_info,no_schools,no_campaigns,fund,last_wizfit,sales_rep]"
        >
            <template v-slot:top>
            <br>
                <v-row no-gutters>
                <v-col class="ml-4" cols="12" xs="8" sm="3">
                <v-text-field
                outlined
                dense
                label="Search by district"
                append-icon="mdi-magnify"
                type="text"
                >
                </v-text-field>
                </v-col>
                <v-spacer></v-spacer>
                <v-col class="d-none d-sm-flex" cols="2">
                    <v-btn
                    text
                    style="border:1px solid #757575"
                    >
                    bulk import
                    </v-btn>
                </v-col>
                <v-col class="d-none d-sm-flex" cols="2">
                    <v-btn
                    color="#38227A"
                    dark
                    @click="openForm()"
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
                            >
                            <v-list-item-title>
                            Bulk Import
                            </v-list-item-title>
                            </v-list-item>
                            </v-list-item-group>
                        </v-list>
                    </v-menu>
                </v-col>
                </v-row>
            </template>
            <template v-slot:item="row" >
                <tr>
                  <td class="text-center row-item"  divider: true>
                  <v-avatar size="40" color="indigo">
                    <v-icon dark>
                        mdi-account-circle
                    </v-icon>
                    </v-avatar>
                  {{row.item.info}}
                  </td>
                  <td class="text-center row-item" >{{row.item.no_school}}</td>
                  <td class="text-center row-item" >{{row.item.no_campaigns}}</td>
                  <td class="text-center row-item" >{{row.item.fund}}</td>
                  <td class="text-center row-item" >{{row.item.last}}</td>
                  <td class="text-center row-item" >{{row.item.saleRep}}</td>
                  <td class="text-center row-item" > 


                    <v-chip class="mr-2">
                    <v-tooltip bottom>
                        <template v-slot:activator="{ on, attrs }">
                            <v-icon
                            dark
                            v-bind="attrs"
                            v-on="on"
                            class="icons"
                            color="black"
                            >
                            mdi-eye
                            </v-icon>
                        </template>
                        <span>view</span>
                    </v-tooltip>
                    </v-chip>

                    <v-chip class="mr-2">
                    <v-tooltip bottom>
                        <template v-slot:activator="{ on, attrs }">
                            <v-icon
                            dark
                            v-bind="attrs"
                            v-on="on"
                            class="icons"
                            color="black"
                            >
                            mdi-pencil
                            </v-icon>
                        </template>
                        <span>Edit</span>
                    </v-tooltip>
                    </v-chip>
                    <v-menu offset-y>
                    <template v-slot:activator="{ on, attrs }">
                        
                        <v-chip>
                        <v-icon
                        v-bind="attrs"
                        v-on="on"
                        >mdi-dots-horizontal</v-icon>
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
            </template>
        </v-data-table>
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
                align: "last_wizfit",
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
      DistrictFormData:{
          flag:false,
          loading:false,
          disabled:false
      },

      dummyData:[
          {info:'lousiana school district',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav"},
          {info:'lousiana school district',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav"},
          {info:'lousiana school district',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav"},
          {info:'lousiana school district',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav"},
          {info:'lousiana school district',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav"},
          {info:'lousiana school district',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav"},
          {info:'lousiana school district',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav"},
          {info:'lousiana school district',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav"},
          {info:'lousiana school district',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav"},
          {info:'lousiana school district',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav"},
          {info:'lousiana school district',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav"},
          {info:'lousiana school district',no_school:35,no_campaigns:65,fund:325625,last:"26/04/2021",
          saleRep:"Prashant Yadav"},
      ]
        }
    },
    methods:{
        openForm(){
            this.DistrictFormData.flag=true
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
</style>