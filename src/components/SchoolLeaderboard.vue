<template>
    <div>
        <h3>School wise Leader board</h3>
        <v-data-table
        hide-default-footer
        :headers="headers"
        :loading="loader"
        :items="tabData"
        loading-text="Loading... Please wait"
        class="elevation-1"
        >
            <template v-slot:top>
                <v-menu offset-y>
                    <template v-slot:activator="{ on, attrs }">
                        
                        <v-icon
                        class="d-flex d-sm-none"
                        v-bind="attrs"
                        v-on="on"
                        >mdi-dots-vertical</v-icon>
                    </template>
                    <v-list>
                        <v-list-item-group>
                        <v-list-item
                        background-color="transparent"
                        color="red"
                        active-class="active-class"
                        v-for="(item,i) in tabs" 
                        :key="i" 
                        >
                        <v-list-item-title
                        v-text="item.title"
                        >
                        </v-list-item-title>
                        </v-list-item>
                        </v-list-item-group>
                    </v-list>
                </v-menu>
                <v-tabs 
                background-color="transparent"
                color="red"
                class="d-none d-sm-flex">
                    <v-tab v-for="(item,i) in tabs" 
                    :key="i" 
                    v-text="item.title"
                    style="margin-left:40px;"></v-tab>
                    
                </v-tabs>
             <b><hr style="margin-bottom:5px"></b>
            </template>

            <template v-slot:item="row" >
                <tr>
                  <td class="text-center row-item"  divider: true>
                  <div style="margin-bottom:15px;"><v-icon color="#F9A825" v-if="row.item.rank=='1st'">mdi-crown</v-icon><br>
                    {{row.item.rank}}</div>
                  </td>
                  <td class="text-center row-item" >{{row.item.school}}</td>
                  <td class="text-center row-item" >{{row.item.reg_student}}</td>
                  <td class="text-center row-item" >{{row.item.video}}</td>
                  <td class="text-center row-item" >{{row.item.shares}}</td>
                  <td class="text-center row-item" >{{row.item.fund}}</td>
                </tr>
            </template>
        
        </v-data-table>
    </div>
</template>
<script>
export default {
  name: "SchoolLeaderboard",
  data() {
    return {
        loader:false,
        headers: [
        {
          text: "Rank",
          align: "center",
          sortable: false,
          value: "rank",
          class: "grey lighten-4"
        },
        {
          text: "School",
          align: "center",
          sortable: false,
          value: "school",
          class: "grey lighten-4"
        },
        {
          sortable: false,
          text: "Registered Student",
          align: "center",
          value: "reg_student",
          class: "grey lighten-4",
          color: "dark"
        },
        {
          sortable: false,
          text: "Wizfit Video",
          align: "center",
          value: "video",
          class: "grey lighten-4"
        },
        {
          sortable: false,
          text: "Shares ",
          value: "shares",
          align: "center",
          class: "grey lighten-4"
        },

        {
          sortable: false,
          text: "Fund Raised",
          value: "fund",
          class: "grey lighten-4",
          align: "center"
        }
      ],
      tabs: [
        { title: "Most Funds Raised" },
        { title: "Top Registration" },
        { title: "Most Video Watched" },
        { title: "Most number of shares" }
      ],
      tabData: [
        {
          rank: "1st",
          school: "test elementry",
          reg_student: "23562",
          video: "244552/8000",
          shares: 2552545,
          fund: 2552255
        },
        {
          rank: "2nd",
          school: "test elementry",
          reg_student: "23562",
          video: "244552/8000",
          shares: 2552545,
          fund: 2552255
        },
        {
          rank: "3rd",
          school: "test elementry",
          reg_student: "23562",
          video: "244552/8000",
          shares: 2552545,
          fund: 2552255
        },
        {
          rank: "4th",
          school: "test elementry",
          reg_student: "23562",
          video: "244552/8000",
          shares: 2552545,
          fund: 2552255
        },
        {
          rank: "5th",
          school: "test elementry",
          reg_student: "23562",
          video: "244552/8000",
          shares: 2552545,
          fund: 2552255
        }
      ]
    };
  }
};
</script>

<style scoped>
.active-class {
  border-right: 4px solid red;
  border-radius: 4px;
}
</style>