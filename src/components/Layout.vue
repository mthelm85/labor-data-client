<template>
  <v-container fluid>
    <v-row
      align="center"
      justify="center"
    >
      <v-col cols=9>
        <v-card outlined>
          <Map/>
        </v-card>
      </v-col>
      <v-col cols=3>
        <v-card outlined :height="height">
          <v-card-title>County Metadata</v-card-title>
          <SideCard/>
        </v-card>
      </v-col>
    </v-row>
    <v-row>
    <v-col>
      <v-card outlined :height="bottomHeight">
        <v-card-title>Labor Force, Employed, Unemployed</v-card-title>
        <DataTable/>
      </v-card>
    </v-col>
    <v-col>
      <v-card outlined :height="bottomHeight">
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

    computed: {
      height () {
        switch (this.$vuetify.breakpoint.name) {
          case 'xs': return '250px'
          case 'sm': return '350px'
          case 'md': return '300px'
          case 'lg': return '400px'
          case 'xl': return '500px'
          default: return '400px'
        }
      },
      bottomHeight () {
          switch (this.$vuetify.breakpoint.name) {
            case 'xs': return '450px'
            case 'sm': return '450px'
            case 'md': return '450px'
            case 'lg': return '450px'
            case 'xl': return '550px'
            default: return '450px'
        }
      }
    }
  }
</script>
