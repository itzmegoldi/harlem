<template>
    <div>
        <h2>Overview</h2>

        <v-row>
         <v-col cols="12" xs="10" sm="6" md="3" v-for="(item,i) in kpiData" :key="i">
            <v-card
                max-height="180"
                max-width="350"
                >
                <v-list>
                        <v-list-item>
                            <v-list-item-icon>
                                <v-sheet 
                                class="text-center"
                                rounded
                                height="50" width="50" :color="item.backColor">
                                <v-icon class="mt-2" :style="{color:item.iconColor}" large v-text="item.icon"></v-icon>
                                </v-sheet>
                                
                            </v-list-item-icon>
                            <v-list-item-content>
                            <v-list-item-title>
                                566555
                            </v-list-item-title>
                            </v-list-item-content>
                        </v-list-item>
                        <v-list-item>
                            <v-list-item-content>
                                <v-list-item-title :style="{color:item.iconColor}" v-text="item.title">
                                </v-list-item-title>
                            </v-list-item-content>
                        </v-list-item>
                    
                </v-list>
                </v-card>
         </v-col>
        </v-row>

    </div>
</template>
<script>
export default {
    name:"OverviewKpi",

    data(){
        return {
            kpiData:[
            {icon:"mdi-basketball",iconColor:'#D30024',backColor:"rgba(211, 0, 36, 0.12)",
            title:"Total Campaign"},
            {icon:"mdi-account-group",iconColor:'#E76F00',backColor:"rgba(231, 111, 0, 0.12)",
            title:"#Students Reg"},
            {icon:"mdi-cash-multiple",iconColor:'#067605',backColor:"rgba(6, 118, 5, 0.12)",
            title:"Total Fund Raised"},
            {icon:"mdi-video-check",iconColor:'#0085FF',backColor:"rgba(0, 133, 255, 0.12)",
            title:"# Videos Watched"},
        ],
       
        }
    }
}
</script>
<style scoped>
.title{
margin-top: 0px;
font-size: 10px;
}

</style>