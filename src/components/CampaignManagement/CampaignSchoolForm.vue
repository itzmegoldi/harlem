<template>
  <div>
    <v-row>
      <v-col>
        <v-autocomplete
          v-model="school"
          :items="schools"
          outlined
          color="#2C1963"
          dense
          label="Select School"
        ></v-autocomplete>
      </v-col>
      <v-col>
        <v-autocomplete
          v-model="sales_rep"
          :items="sales_Rep"
          outlined
          color="#2C1963"
          dense
          label="Select Sales representative"
        ></v-autocomplete>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-text-field
          v-model="host_name"
          outlined
          color="#2C1963"
          dense
          label="Host name"
        ></v-text-field>
      </v-col>
      <v-col>
        <v-text-field
          v-model="host_email"
          outlined
          color="#2C1963"
          dense
          label="Host email"
        ></v-text-field>
      </v-col>
    </v-row>
    <v-row>
      <v-col xs="12">
        <v-text-field
          outlined
          color="#2C1963"
          dense
          v-model="sub_domain"
          label="Campaign public address"
          suffix=".wizfitchallenge.com"
        ></v-text-field>
        <p style="margin-top:-20px;margin-left:5px">Ex:issaquah@wizfitchallenge.com</p>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <quillEditor
          v-model="school_special_message"
          :options="editorOptions"
        />
      </v-col>
    </v-row>
    <br /><br /><br /><br /><br />
    <v-card-title
      style="border-bottom:2px solid #2C1963;color:#2C1963;width:250px;height:50px"
    >
      Default goals
    </v-card-title>
    <hr />
    <br /><br>
    <v-row>
      <v-col cols="6">
        <v-text-field
          outlined
          dense
          label="School goal"
          color="#2C1963"
          v-model="school_goal"
        ></v-text-field>
      </v-col>
    </v-row>

    <v-card-title
      style="border-bottom:2px solid #2C1963;color:#2C1963;width:250px;height:50px"
    >
      Incentives
    </v-card-title>
    <hr />
    <br />
    <v-row>
      <v-col cols="12">
        <quillEditor v-model="teacher_incentive" :options="editorOptionsT" />
      </v-col>
    </v-row>
    <br /><br /><br /><br /><br />
    <v-row>
      <v-col cols="12">
        <quillEditor v-model="student_incentive" :options="editorOptionsS" />
      </v-col>
    </v-row>
    <br /><br /><br /><br />
    <v-card-title
      style="border-bottom:2px solid #2C1963;color:#2C1963;width:250px;height:50px"
    >
      Timeline/Events
    </v-card-title>
    <hr />
    <br /><br>
    <v-row>
      <v-col>
        <v-menu
          ref="menu1"
          v-model="menu1"
          :close-on-content-click="false"
          transition="scale-transition"
          offset-y
          max-width="290px"
          min-width="auto"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-text-field
              v-model="event_start_date"
              label="Event Start Date"
              prepend-inner-icon="mdi-calendar"
              v-bind="attrs"
              outlined
              v-on="on"
              dense
              color="#2C1963"
            ></v-text-field>
          </template>
          <v-date-picker
            v-model="event_start_date"
            no-title
            @input="menu1 = false"
          ></v-date-picker>
        </v-menu>
      </v-col>
      <v-col>
        <v-menu
          ref="menu2"
          v-model="menu2"
          :close-on-content-click="false"
          transition="scale-transition"
          offset-y
          max-width="290px"
          min-width="auto"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-text-field
              v-model="kick_off_date"
              label="Kick-Off Date"
              prepend-inner-icon="mdi-calendar"
              v-bind="attrs"
              outlined
              v-on="on"
              dense
              color="#2C1963"
            ></v-text-field>
          </template>
          <v-date-picker
            v-model="kick_off_date"
            no-title
            @input="menu2 = false"
          ></v-date-picker>
        </v-menu>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-menu
          ref="menu3"
          v-model="menu3"
          :close-on-content-click="false"
          transition="scale-transition"
          offset-y
          max-width="290px"
          min-width="auto"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-text-field
              v-model="gold_ball_giveaway"
              label="Gold ball giveaway date"
              prepend-inner-icon="mdi-calendar"
              v-bind="attrs"
              outlined
              v-on="on"
              dense
              color="#2C1963"
            ></v-text-field>
          </template>
          <v-date-picker
            v-model="gold_ball_giveaway"
            no-title
            @input="menu3 = false"
          ></v-date-picker>
        </v-menu>
      </v-col>
      <v-col>
        <v-menu
          ref="menu4"
          v-model="menu4"
          :close-on-content-click="false"
          transition="scale-transition"
          offset-y
          max-width="290px"
          min-width="auto"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-text-field
              v-model="graduation_date"
              label="Graduation celebration date"
              prepend-inner-icon="mdi-calendar"
              v-bind="attrs"
              outlined
              v-on="on"
              dense
              color="#2C1963"
            ></v-text-field>
          </template>
          <v-date-picker
            v-model="graduation_date"
            no-title
            @input="menu4 = false"
          ></v-date-picker>
        </v-menu>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="6">
        <v-menu
          ref="menu5"
          v-model="menu5"
          :close-on-content-click="false"
          transition="scale-transition"
          offset-y
          max-width="290px"
          min-width="auto"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-text-field
              v-model="event_end_date"
              label="Event end date"
              prepend-inner-icon="mdi-calendar"
              v-bind="attrs"
              outlined
              v-on="on"
              dense
              color="#2C1963"
            ></v-text-field>
          </template>
          <v-date-picker
            v-model="event_end_date"
            no-title
            @input="menu5 = false"
          ></v-date-picker>
        </v-menu>
      </v-col>
    </v-row>
    <v-card-title
      style="border-bottom:2px solid #2C1963;color:#2C1963;width:260px;height:50px"
    >
    Images & Videos Gallery
    </v-card-title>
    <hr />
    <br />
    <v-row>
      <v-file-input
        label="upload logo"
        color="#7253CF"
        dense
        class="file-input"
        id="inputId"
        style="display:none"
      >
      </v-file-input>
      <v-col cols="4">
        <div class="gallery">
          <label style="cursor:pointer;" for="inputId">
            <v-icon color="#CECECE" class="input-label" large
              >mdi-cloud-upload-outline</v-icon
            >
            <h3 style="color:#2c1963;">Upload</h3>
            <p style="color:#404040;font-size:12px">images & videos</p>
          </label>
        </div>
      </v-col>
      <v-col cols="4" v-for="(item, i) in dummy_url" :key="i">
        <div
          class="img-box"
          :style="{'background-image':'url('+`${publicPath}${item.img}`+')'}"
        >
        <div class="delete-btn">
          <v-icon  small color="red">mdi-delete</v-icon>
        </div>
        <!-- <img :src="`${publicPath}${item.img}`"> -->
            <!-- <img src="@/assets/hello.png"> -->
                    
        </div>
      </v-col>
    </v-row>
      <CampaignDialog :CampaignDialogData="CampaignDialogData" v-if="CampaignDialogData.flag"/>
  </div>
</template>

<script>
import "quill/dist/quill.snow.css";
import { quillEditor } from "vue-quill-editor";
import CampaignDialog from "./CampaignDialog"
export default {
  name: "CampaignSchoolForm",
  components: {
    quillEditor,
    CampaignDialog
  },
  data() {
    return {
      publicPath: process.env.BASE_URL,
      menu1: false,
      menu2: false,
      menu3: false,
      menu4: false,
      menu5: false,
      school: "",
      schools: ["test elementry", "test elementry 1"],
      sales_rep: "",
      sales_Rep: ["Prashant Yadav"],
      host_name: "",
      host_email: "",
      sub_domain: "",
      school_special_message: "",
      teacher_incentive: "",
      student_incentive: "",
      editorOptions: {
        debug: "info",
        placeholder: "School special message",
        readOnly: true,
        theme: "snow"
      },
      editorOptionsT: {
        debug: "info",
        placeholder: "Teacher Incentive",
        readOnly: true,
        theme: "snow"
      },
      editorOptionsS: {
        debug: "info",
        placeholder: "Student Incentive",
        readOnly: true,
        theme: "snow"
      },
      school_goal: null,
      event_start_date: "",
      kick_off_date: "",
      gold_ball_giveaway: "",
      graduation_date:"",
      event_end_date:"",
      CampaignDialogData:{
        flag:false,
        campaign_type:''
      },

      dummy_url: [
        { img: 'logo.png', title: "hello how are you" },
        { img: "logo.png", title: "hello how are you" },
        { img: "logo.png", title: "hello how are you" },
        { img: "logo.png", title: "hello how are you" },
        { img: "logo.png", title: "hello how are you" },
      ],
    };
  },
  methods:{
    submitForm(value){
      this.CampaignDialogData.campaign_type=value
      if(this.school && this.host_name && this.host_email && this.teacher_incentive && this.student_incentive && this.graduation_date)
      {
        console.log('ready to publish')
      }
      else{
        this.CampaignDialogData.flag=true
      }
    }
  },
  
  
};
</script>
<style scoped>
.quill-editor {
  height: 150px;
}
.ql-toolbar.ql-snow {
  color: #2c1963;
}
.gallery {
  width: 186px;
  height: 150px;
  border: 2px dotted #2c1963;
  text-align: center;
  margin: 10px;
  border-radius: 10px;
}
.input-label {
  margin-top: 15%;
}
.img-box {
  width: 180px;
  height: 150px;
  border: 2px solid #2c1963;
  text-align: center;
  margin: 10px;
  border-radius: 4px;
  background-position: center;
  
}
.delete-btn{
margin-left:150px;
background-color: white;
cursor: pointer;
height: 20px;
width: 20px;
border-radius: 50%;
}
.v-input{
margin-top:-20px;
}
</style>
