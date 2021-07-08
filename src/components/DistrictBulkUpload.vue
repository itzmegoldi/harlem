<template>
    <div>
        <v-card class="card">
        <v-card-title 
        ><h4 class="card-heading">STEP-1</h4>
        </v-card-title>
        <v-card-text>
            <div class="card-text">
                <h2>Download Format</h2>
                <p style="margin-top:5px">First step to download the excel sheet format. Fill up the excel sheet with the 
                district data for all the <br> required columns</p>
                <button class="btn">Download Format</button>
            </div>
            
        </v-card-text>
        </v-card>

        <v-card class="card1">
        <v-card-title 
        ><h4 class="card-heading">STEP-2</h4>
        </v-card-title>
        <v-card-text>
            <div class="card-text">
                <h2>Download Format</h2>
                <p style="margin-top:5px">First step to download the excel sheet format. Fill up the excel sheet with the 
                district data for all the <br> required columns</p>
                
                    <v-file-input
                    prepend-inner-icon="mdi-paperclip"
                    prepend-icon=""
                    outlined
                    placeholder="Upload File"
                    color="#7254CF"
                    dense>
                    </v-file-input>
                <button class="btn1">Submit</button>
            </div>
            
        </v-card-text>
        </v-card>
    </div>
</template>
<script>
export default {
    name:'DistrictBulkUpload'
}
</script>
<style scoped>
.card.v-card{
    max-height: 180px;
}
.card1.v-card{
    margin-top: 50px;
}
.btn{
    border:1px solid #38227A;
    padding: 4px;
    padding-left:10px ;
    padding-right: 10px;
    border-radius:5px;
    transition-duration: 0.4s;
    color:#38227A;
    position:relative;
    left:800px;
    bottom: 60px;
    height: 35px;
    width: 150px;
}
.btn1{
    background-color: #38227A;
    color: white;
    border-radius: 5px;
    width: 150px;
    height: 35px;
    transition-duration: 0.4s;
    position:absolute;
    left:830px;
    bottom:35px;
}
.btn1:hover{
    background-color:white;
    color:#38227A;
    border: 1px solid #38227A;
    box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2), 0 6px 20px 0 rgba(0,0,0,0.19);
}
.btn1:active{
    color:white;
    background-color: #38227A;
}
.btn:hover{
background-color:#38227A ;
color:white;
box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2), 0 6px 20px 0 rgba(0,0,0,0.19);
}
.btn:active{
    color:#38227A;
    background-color: white;
}
.card-text{
    margin-top:10px;
    color: black;
    padding: 20px;
}
.v-card__title{
    text-align: center;
    background-color:#D30024;
    color:white;
    min-height: 50px;
}
.card-heading{
   position:absolute;
   left: 450px;
}
.v-input{
    max-width: 400px;
    height: 35px;
}

@media (min-width:0px) and (max-width:600px ){
    .card-heading{
        position:absolute;
        left: 130px;
    }
    .card.v-card{
        max-height: 300px;
    }
    .btn{
        position: static;
    }
    .btn1{
        position: static;
    }
    .v-input{
        margin-bottom: 20px;
    }
}
</style>