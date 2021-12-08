<template>
  <v-container fill-height fluid>
    <v-row
      align="center"
      justify="center"
    >
      <v-col cols=10>
        <v-card outlined>
          <Map/>
        </v-card>
      </v-col>
      <v-col cols=2>
        <v-card outlined height="600px">
          <v-card-title>County Metadata</v-card-title>
          <SideCard/>
        </v-card>
      </v-col>
    </v-row>
    <v-row>
    <v-col>
      <v-card outlined height="450px">
        <v-card-title>Labor Force Data Table</v-card-title>
        <DataTable/>
      </v-card>
    </v-col>
    <v-col>
      <v-card outlined height="450px">
        <v-card-title>Unemployment Rate Trend</v-card-title>
        <SparkLine/>
      </v-card>
    </v-col>
    </v-row>
  </v-container>
</template>

<script>
  import Map from '@/components/Map'
  import SideCard from '@/components/SideCard'
  import DataTable from '@/components/DataTable'
  import SparkLine from '@/components/SparkLine'

  export default {
    name: 'Layout',
    components: {
      Map,
      SideCard,
      DataTable,
      SparkLine
    },

    data: () => ({

    }),
  }
</script>
