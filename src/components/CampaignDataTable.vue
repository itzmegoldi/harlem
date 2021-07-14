<template>
    <div>
        <h2>Campaign wise data table</h2>
        <v-data-table
        hide-default-footer
        fixed-header
        :headers="headers"
        :items="campaigns"
        :loading="loader"
        loading-text="Loading... Please wait"
        class="elevation-1"
        mobile-breakpoint="0"
        >
            <template v-slot:item="row" >
                <tr>
                  <td class="text-center row-item"  divider: true>
                    
                        <v-chip small :class="`${row.item.campaign.status}`">
                            {{row.item.campaign.status}}
                        </v-chip>
                    
                    <h4>{{row.item.campaign.id}}</h4>
                    <p>{{row.item.campaign.date}}</p>
                  </td>
                  <td class="text-center row-item" >{{row.item.type}}</td>
                  <td class="text-center row-item" >{{row.item.pta}}</td>
                  <td class="text-center row-item" >{{row.item.fund}}</td>
                  <td class="text-center row-item" >{{row.item.no_student}}</td>
                  <td class="text-center row-item" >{{row.item.no_shares}}</td>
                  <td class="text-center row-item" >{{row.item.video}}</td>
                  <td class="text-center row-item" > 


                    <v-chip class="chip">
                    <v-tooltip bottom>
                        <template v-slot:activator="{ on, attrs }">
                            <v-icon
                            dark
                            v-bind="attrs"
                            v-on="on"
                            class="icons"
                            color="#6B6B6B"
                            >
                            mdi-eye
                            </v-icon>
                        </template>
                        <span>view</span>
                    </v-tooltip>
                    </v-chip>

                    <v-chip class="chip">
                    <v-tooltip bottom>
                        <template v-slot:activator="{ on, attrs }">
                            <v-icon
                            dark
                            v-bind="attrs"
                            v-on="on"
                            class="icons"
                            color="#6B6B6B"
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
    name:"CampaignDataTable",
    data(){
        return {
            itemPage:10,
            page:1,
            itemPerPage:[10,15,20,25,50,100],
            pageCount:5,
            campaigns:[
                {
                    campaign:{
                        id:'wizfit2021',
                        status:'ONGOING',
                        date:"27/08/2021"
                    },
                    type:"school",
                    pta:'Test Elementry',
                    fund:2222,
                    no_student:22536,
                    video:5555,
                    no_shares:6595,

                },
                {
                    campaign:{
                        id:'wizfit2021',
                        status:'COMPLETED',
                        date:"27/08/2021"
                    },
                    type:"school",
                    pta:'Test Elementry',
                    fund:2222,
                    no_student:22536,
                    video:5555,
                    no_shares:6595,

                },
                {
                    campaign:{
                        id:'wizfit2021',
                        status:'UPCOMING',
                        date:"27/08/2021"
                    },
                    type:"school",
                    pta:'Test Elementry',
                    fund:2222,
                    no_student:22536,
                    video:5555,
                    no_shares:6595,

                },
                {
                    campaign:{
                        id:'wizfit2021',
                        status:'DRAFT',
                        date:"27/08/2021"
                    },
                    type:"school",
                    pta:'Test Elementry',
                    fund:2222,
                    no_student:22536,
                    video:5555,
                    no_shares:6595,

                }
            ],
            loader:false,
            headers: [
                {
                text: "Campaign",
                align: "center",
                sortable: false,
                value: "campaign",
                class: "grey lighten-4"
                },
                {
                text: "Campaign type",
                align: "center",
                sortable: false,
                value: "type",
                class: "grey lighten-4"
                },
                {
                sortable: false,
                text: "District/School",
                align: "center",
                value: "pta",
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
                text: "# shares",
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
      ]
        }
    }
}
</script>

<style scoped>
span.v-chip.ONGOING{
margin-top:10px;
background-color: rgba(231, 111, 0, 0.12);
color: #E76F00;
}
span.v-chip.COMPLETED{
margin-top:10px;
background-color: rgba(6, 118, 5, 0.12);
color: #067605
;
}
span.v-chip.UPCOMING{
margin-top:10px;
background-color: rgba(0, 133, 255, 0.12);
color: #0085FF;
}
span.v-chip.DRAFT{
margin-top:10px;
}
.chip.v-chip{
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

}
</style>