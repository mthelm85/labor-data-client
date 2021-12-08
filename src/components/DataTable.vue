<template>
    <v-container justify="center" align="center">
        <v-data-table
            :headers="headers"
            :items="values"
            :items-per-page="5"
        >
        </v-data-table>
    </v-container>
</template>
<script>
  export default {
    name: 'DataTable',
    data: () => ({
        headers: [],
        values: []
    }),

    methods: {
        sorter (a, b) {
            if (a.year !== b.year) {
                return a.year - b.year
            } else {
                return a.month - b.month
            }
        }
    },

    mounted () {
      this.$root.$on('fetching', data => {
          this.headers = []
          this.values = []
          let headers = Object.keys(data.data.series.laus[0])
          for (let i = 0; i < headers.length; i++) {
              this.headers.push({ text: headers[i], value: headers[i] })
          }
          let sorted = data.data.series.laus.sort(this.sorter)
          for (let i = 0; i < sorted.length; i++) {
              this.values.push(sorted[i])
          }
      })
    }
  }
</script>