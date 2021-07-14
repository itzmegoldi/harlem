<template>
    <div>
        <v-card class="card-datatable">
            <v-card-text>
                <v-row no-gutters>
                <v-col xs="6">
                <v-text-field
                outlined
                dense
                label="Search by district"
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
                            Start New Campaign
                            </v-list-item-title>
                            </v-list-item>
                            </v-list-item-group>
                        </v-list>
                    </v-menu>
                </v-col>
                <v-spacer></v-spacer>
                
                <v-col class="d-none d-sm-flex" cols="3">
                    <v-btn
                    color="#38227A"
                    dark
                    @click="openForm()"
                    class="text-capitalize"
                    >
                    Start New Campaign
                    </v-btn>
                </v-col>
                </v-row>
            </v-card-text>
        </v-card>
        <v-data-table
         hide-default-footer
        fixed-header
        :headers="headers"
        :items="campaigns"
        :loading="loader"
        loading-text="Loading... Please wait"
        class="elevation-1"
        mobile-breakpoint="0">
            <template v-slot:item="row">
                <tr class="text-flex">
                  <td class="text-center row-item"  divider: true>
                  {{row.item.district_school}}
                  </td>
                  <td class="text-center row-item" >{{row.item.campaign_type}}</td>
                  <td class="text-center row-item" v-for="(item,i) in row.item.campaign" :key="i" >
                    <tr >
                       <td>
                            <v-chip small :class="`${item.status}`">
                                {{item.status}}
                            </v-chip>
                       </td>
                    </tr>
                    <tr >
                       <td>{{item.date}}</td>
                    </tr>
                    <tr >
                       <td 
                       style="font-size:10px;color:rgba(29, 29, 29, 0.6);">{{item.id}}</td>
                    </tr>
                  </td>
                  <td class="text-center row-item" >{{row.item.fund}}</td>
                  <td class="text-center row-item" >{{row.item.no_student}}</td>
                  <td class="text-center row-item" >{{row.item.video}}</td>
                  <td class="text-center row-item" >{{row.item.no_shares}}</td>
                  <td class="text-center row-item" >
                  
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
    </div>
</template>
<script>
export default {
    name:'CampaignDataTable',

    data(){
        return{
                headers: [
                {
                text: "District/School",
                align: "center",
                sortable: false,
                value: "district_school",
                class: "grey lighten-4"
                },
                {
                text: "Campaign type",
                align: "center",
                sortable: false,
                value: "campaign_type",
                class: "grey lighten-4"
                },
                {
                sortable: false,
                text: "Campiagn",
                align: "center",
                value: "campaign",
                class: "grey lighten-4"
                },
                {
                sortable: false,
                text: "Fund Raised",
                align: "center",
                value: "fund",
                class: "grey lighten-4"
                },
                {
                sortable: false,
                text: "# students registered",
                value: "no_student",
                align: "center",
                class: "grey lighten-4"
                },
                
                {
                sortable: false,
                text: "Wizfit video",
                value: "video",
                class: "grey lighten-4",
                align: "center"
                },
                {
                sortable: false,
                text: "#Shares",
                value: "no_shares",
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
            itemPerPage:[10,15,20,25,50,100],
            itemPage:10,
            page:1,
            pageCount:4,
            loader:false,
            campaigns:[
                {
                    district_school:"Test Elementry School",
                    campaign_type:"School",
                    campaign:[
                        {status:"ONGOING",
                        date:"26/05/2021 to 26/06/2021",
                        id:"WIZFIT-01-1010"
                        }
                    ],
                    fund:203212,
                    no_student:55255,
                    video:"2122/9000",
                    no_shares:55522
                },
                {
                    district_school:"Test Elementry School",
                    campaign_type:"School",
                    campaign:[
                        {status:"UPCOMING",
                        date:"26/05/2021 to 26/06/2021",
                        id:"WIZFIT-01-1010"
                        }
                    ],
                    fund:203212,
                    no_student:55255,
                    video:"2122/9000",
                    no_shares:55522
                },
                {
                    district_school:"Test Elementry School",
                    campaign_type:"School",
                    campaign:[
                        {status:"COMPLETED",
                        date:"26/05/2021 to 26/06/2021",
                        id:"WIZFIT-01-1010"
                        }
                    ],
                    fund:203212,
                    no_student:55255,
                    video:"2122/9000",
                    no_shares:55522
                },
                {
                    district_school:"Test Elementry School",
                    campaign_type:"School",
                    campaign:[
                        {status:"DRAFT",
                        date:"26/05/2021 to 26/06/2021",
                        id:"WIZFIT-01-1010"
                        }
                    ],
                    fund:203212,
                    no_student:55255,
                    video:"2122/9000",
                    no_shares:55522
                },
            ]
        }
    },
    methods:{
        openForm(){
            this.$router.push('/start-campaign/start')
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
    position: absolute;
    right:10px;
}
.v-chip{
border-radius:4px;
margin-left: 8px;
}
.v-chip.v-chip--no-color.theme--light.v-size--small.ONGOING{
    margin-top:10px;
    background-color: rgba(231, 111, 0, 0.12);
    color: #E76F00;
    border-radius: 10px;
}
.v-chip.v-chip--no-color.theme--light.v-size--small.UPCOMING{
    margin-top:10px;
    background-color: rgba(0, 133, 255, 0.12);
    color: #0085FF;
    border-radius: 10px;
}
.v-chip.v-chip--no-color.theme--light.v-size--small.COMPLETED{
    margin-top:10px;
    background-color: rgba(6, 118, 5, 0.12);
    color: #067605;
    border-radius: 10px;
}
.v-chip.v-chip--no-color.theme--light.v-size--small.DRAFT{
    margin-top:10px;
    border-radius: 10px;
}
.footer-card.v-card{
max-height: 70px;
}
.footer-input.v-input{
width: 60px;
padding: 0%;
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
    margin-left: 60px;
    }
    .v-input.search-input{
    width: 240px;
    
    }
    .v-icon.notranslate.mobile-menu{
    position: relative;
    left: 30px;
    bottom: 13px;
    }
}
</style>