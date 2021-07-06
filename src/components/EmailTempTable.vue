<template>
  <div>
    <v-simple-table>
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left grey lighten-4">
              Email Title & description
            </th>
            <th class="text-right grey lighten-4">
              Actions
            </th>
          </tr>
        </thead>
        <tbody>
          <tr >
            <td class="text-left">
            <div>
            <p style="font-size:px"><b><span style="font-size:20px">50% of goal milestone</span></b>
            <br><span>This email will be sent to parent when the student
            reaches 50% of the fundraising goal</span>
            </p>
            </div>
            </td>
            <td class="text-right">
                <v-chip>
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
            </td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </div>
</template>
<script>
export default {
  name: "EmailTempTable",
};
</script>
