<template>
  <div>
    <v-app-bar
      color="#FFFFFF"
    >
    <v-app-bar-nav-icon class="d-flex d-sm-none" @click="drawer = !drawer"></v-app-bar-nav-icon>
      
      <v-toolbar-title class="heading">{{barTitle}}</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn class="d-none d-sm-flex" text><v-icon left>mdi-account</v-icon> Prashant Yadav</v-btn>
      <v-menu offset-y
      >
      <template v-slot:activator="{ on, attrs }">
        
        <v-icon
        class="d-none d-sm-flex"
        v-bind="attrs"
          v-on="on"
        >mdi-chevron-down</v-icon>
      </template>
      <v-list>
        <v-list-item-group>
        <v-list-item
        >
          <v-list-item-title>
          Logout
          <v-icon right>mdi-logout</v-icon>
          </v-list-item-title>
        </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-menu>
    </v-app-bar>
      <v-tabs class="tabs" v-if="selected=='Email'">
    <v-tab>Automated email template </v-tab>
    <v-tab>Manual email template</v-tab>
    <v-tab>Bulk emails</v-tab>
  </v-tabs>
    <!--destop view nav drawer-->
    <v-navigation-drawer
      dark
      color="#2C1963"
      width="250px"
      height="1307px"
      absolute
      permanent
      hide-overlay
      class="d-none d-sm-flex"
    >
      <img src="logo.png" style="margin-left:45px;margin-top:45px" />
          <v-list nav dense>
            <v-list-item-group>
              <v-list-item 
              active-class="active-class"
              v-for="(item, i) in navLinks" :key="i"
              @click="ChangeTab(item.heading,item.select,item.url)"
              >
                <v-icon left>{{ item.icon }}</v-icon>
                <v-list-item-title>{{ item.title }}</v-list-item-title>
              </v-list-item>
              
            </v-list-item-group>
          </v-list>
    </v-navigation-drawer>
    
    <!--mobile view nav drawer-->
    <v-navigation-drawer
      v-model="drawer"
      dark
      color="#2C1963"
      width="250px"
      height="1307px"
      absolute
      temporary
      hide-overlay
      class="d-flex d-sm-none"
    >
      <img src="logo.png" style="margin-left:45px;margin-top:45px" />
          <v-list nav dense>
            <v-list-item-group>
              <v-list-item 
              active-class="active-class"
              v-for="(item, i) in navLinks" :key="i"
              @click="ChangeTab(item.heading,item.select)"
              >
                <v-icon left>{{ item.icon }}</v-icon>
                <v-list-item-title>{{ item.title }}</v-list-item-title>
              </v-list-item>
              <v-list-item class="d-sm-none">
                    <v-icon>mdi-logout</v-icon>
                    <v-list-item-title>Logout</v-list-item-title>
                </v-list-item>
            </v-list-item-group>
          </v-list>
    </v-navigation-drawer>

    <div class="maindiv"> 
        <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "NavBar",
  data() {
    return {
      navLinks: [
        { title: "Dashboard", icon: "mdi-view-dashboard", heading:"Internal Dashboard"
        ,select:"Dashboard"},
        { title: "District Management", icon: "mdi-office-building" ,heading:"District Management",
        select:"District",url:'/district'},
        { title: "School Management", icon: "mdi-school" ,heading:"School Management",
        select:"School" },
        { title: "Campaign Management", icon: "mdi-bullhorn" ,heading:"Campaign Management",
        select:"Campaign"},
        { title: "Game Management", icon: "mdi-basketball" ,heading:"Game Management" ,
        select:"Game"},
        { title: "Team Management", icon: "mdi-account-group" ,heading:"Team Management" ,
        select:"Team"},
        { title: "Student Management", icon: "mdi-account-group" ,heading:"Student Management",
        select:"Student" },
        { title: "Teacher Management", icon: "mdi-account-group" ,heading:"Teacher Management",
        select:"Teacher" },
        { title: "Donation Management", icon: "mdi-charity" ,heading:"Donation Management",
        select:"Donation" },
        { title: "Emails", icon: "mdi-mail" ,heading:"Emails", select:"Email"},
        { title: "Reports", icon: "mdi-card-account-details" ,heading:"Reports"},
        { title: "Settings", icon: "mdi-cog" ,heading:"Settings" },
      ],
      drawer:false,
      barTitle:"Internal Dashboard",
      selected:"Dashboard"
    };
  },
  methods:{
      /**
       * for changing the tabs and heading
       * param {string} title - navbar heading
       */
      ChangeTab(heading,select,url){
          this.barTitle = heading
          this.drawer=false
          this.selected=select
          this.$router.push(url)

      }
  }
};
</script>

<style scoped>
.active-class{
    border-right: 4px solid yellow;
    width: 242px;
}
.maindiv{
    margin-left:290px;
    margin-top:50px;
    margin-right:30px
}
.heading{
    margin-left:250px
}
.tabs{
  margin-left:250px;
}
@media (min-width:0px) and (max-width:600px ){
    .maindiv{
        margin-left:25px
    }
    .heading{
        margin-left: 10px;
    }
    .tabs{
      margin-left: 0px;
    }
}
</style>
