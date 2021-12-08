<template>
    <v-container>
        <v-card flat>
          &nbsp;&nbsp;&nbsp; {{ placeName }}
            <!-- <v-card-title>
                {{ placeName }}
            </v-card-title> -->
            <v-card-subtitle>
                {{ whdOffice }} {{ whdRegion }}
            </v-card-subtitle>
            <v-card-text>
                Year: {{ qcew[0].year }}
                <br/>
                Avg Empl Level: {{ qcew[0].annual_avg_emplvl.toLocaleString("en-US") }}
                <br/>
                Avg Establishments: {{ qcew[0].annual_avg_estabs.toLocaleString("en-US") }}
                <br/>
                Avg Weekly Wage: {{ qcew[0].annual_avg_wkly_wage.toLocaleString("en-US") }}
            </v-card-text>
        </v-card>
    </v-container>
</template>
<script>
  export default {
    name: 'SideCard',
    data: () => ({
        placeName: null,
        whdOffice: null,
        whdRegion: null,
        avgEstabs: null,
        avgEmp: null,
        avgWage: null,
        qcew: null,
    }),

    mounted () {
      this.$root.$on('fetching', data => {
        this.placeName = data.data.place_name
        this.whdOffice = data.data.do_name
        this.whdRegion = data.data.region_name
        this.qcew = data.data.series.qcew
      })
    }
  }
</script>