<template>
    <div>
        <v-row>
            <v-col cols="12" xs="12" sm="4" md="4">
                <v-row>
                    <v-col cols="12" v-for="(item,i) in cardData" :key="i">
                        <v-card 
                        max-width="200"
                        max-height="110"
                        >
                        <v-list>
                            <v-list-item style="margin-top:-10px;">
                                <v-list-item-icon>
                                <v-sheet 
                                class="text-center"
                                rounded
                                height="40" width="40" :color="item.backColor">
                                <v-icon class="mt-2" 
                                :style="{color:item.iconColor}" 
                            
                                v-text="item.icon"></v-icon>
                                </v-sheet>
                                
                            </v-list-item-icon>
                            <v-list-item-content>
                            <v-list-item-title>
                                566555
                            </v-list-item-title>
                            </v-list-item-content>
                        </v-list-item>
                        <v-list-item style="margin-top:-20px;">
                            <v-list-item-content>
                                <v-list-item-title :style="{color:item.iconColor}" v-text="item.title">
                                </v-list-item-title>
                            </v-list-item-content>
                        </v-list-item>
                        </v-list>

                        </v-card>
                    </v-col>
                </v-row>
            </v-col>
        </v-row>
    </div>
</template>
<script>
export default {
    name:"CardAndGraphs",
    data(){
        return {
            cardData:[
            {icon:"mdi-basketball",iconColor:'#D30024',backColor:"rgba(211, 0, 36, 0.12)",
            title:"Total Campaign"},
            {icon:"mdi-account-group",iconColor:'#E76F00',backColor:"rgba(231, 111, 0, 0.12)",
            title:"#Students Reg"},
        ],
       
        }
    }
}
</script>