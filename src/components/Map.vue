<template>
    <div id="map" :style="{ height: height }">
    </div>
</template>
<script>
  import axios from 'axios'
  import L from 'leaflet'
  import usaMap from '@/assets/counties.json'

  export default {
    name: 'Map',
    components: {

    },
    data: () => ({
      map: null,
      baseLayer: null,
      marker: null,
      icon: null,
      jsonLayer: null,
      jsonLayerGroup: null
    }),

    methods: {
        async fetchData (fips) {
            const res = await axios.get(`https://warm-cliffs-95292.herokuapp.com/county/${fips}`)
            this.$root.$emit('fetching', res.data)
        },

        highlightFeature (e) {
            let layer = e.target

            layer.setStyle({
                weight: 5,
                color: '#666',
                dashArray: '',
                fillOpacity: 0.7
            })

            if (!L.Browser.ie && !L.Browser.opera && !L.Browser.edge) {
                layer.bringToFront();
            }
        },

        resetHighlight (e) {
            this.jsonLayer.resetStyle(e.target)
        },

        onEachFeature (feature, layer) {
            layer.on({
                mouseover: this.highlightFeature,
                mouseout: this.resetHighlight,
                click: () => { this.fetchData(layer.feature.id.toString().padStart(5, '0')) }
            })
        }
    },

    mounted () {
        this.map = L.map('map', { zoomControl: true, attributionControl: false, scrollWheelZoom: true }).setView([40.0, -97.0], 5)
        this.map.createPane('labels')
        this.map.getPane('labels').style.zIndex = 5
        this.baseLayer = L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        maxZoom: 19
        }).addTo(this.map)
        L.control.zoom({ position: 'topright' }).addTo(this.map)
        this.jsonLayer = L.geoJSON(
            usaMap, {
                style: {
                    'fillColor': '',
                    'fillOpacity': 0.0,
                    'color': 'grey',
                    'weight': 1,
                    'opacity': 0.2
                },
                onEachFeature: this.onEachFeature
            }
        ).addTo(this.map)
        // this.jsonLayerGroup.addLayer(this.jsonLayer)
    },

    computed: {
      height () {
        switch (this.$vuetify.breakpoint.name) {
          case 'xs': return '200px'
          case 'sm': return '300px'
          case 'md': return '400px'
          case 'lg': return '500px'
          case 'xl': return '600px'
          default: return '400px'
        }
      },
    }
  }
</script>
<style lang="css" scoped>
@import "~leaflet/dist/leaflet.css";
</style>