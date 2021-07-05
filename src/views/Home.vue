<template>
  <div>
    <OverviewKpi/>
    <CampaignDataTable/><br>
    <leaderboard/>
  </div>
</template>

<script>
  import OverviewKpi from "../components/OverviewKpi.vue"
  import CampaignDataTable from "../components/CampaignDataTable.vue"
  import Leaderboard from "../components/SchoolLeaderboard.vue"
  export default {
    name: 'Home',

    components: {
      OverviewKpi,
      CampaignDataTable,
      Leaderboard
    },
  }
</script>
