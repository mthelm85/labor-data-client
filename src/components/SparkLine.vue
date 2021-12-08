<template>
    <v-container fill-height fluid>
        <v-row justify="center" height="100%">
            <v-sparkline
            :value="values"
            auto-draw
            ></v-sparkline>
        </v-row>
    </v-container>
</template>
<script>
  export default {
    name: 'DataTable',
    data: () => ({
        values: []
    }),

    mounted () {
      this.$root.$on('fetching', data => {
          this.values = []
          for (let i = 0; i < data.data.series.laus.length; i++) {
              this.values.push(data.data.series.laus[i].unemployment_rate)
          }
      })
    }
  }
</script>