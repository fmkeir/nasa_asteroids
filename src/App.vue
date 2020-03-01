<template>
  <div id="app">
    <neo-histogram :histogramDataNEOMagnitude="histogramDataNEOMagnitude"/>
  </div>
</template>

<script>
import config from './api_config.js'
import NEOHistogram from './components/NEOHistogram.vue'

export default {
  name: 'App',
  data() {
    return {
      apiKey: config.apiKey,
      startDate: '2020-02-22',
      endDate: '2020-02-29',
      near_earth_objects: [],
      histogramDataNEOMagnitude: []
    }
  },
  components: {
    "neo-histogram": NEOHistogram
  },
  mounted(){
    let url = `https://api.nasa.gov/neo/rest/v1/feed?start_date=${this.startDate}&end_date=${this.endDate}&api_key=${this.apiKey}`
    fetch(url)
    .then(response => response.json())
    .then(data => {
      this.near_earth_objects = data["near_earth_objects"]
      this.histogramDataNEOMagnitude = this.absoluteMagnitudeAllAsteroids()
    })
  },
  methods: {
    absoluteMagnitudeAllAsteroids() {
       let all_NEO = Object.values(this.near_earth_objects).reduce((all_NEO, dated_NEO) => {
        return all_NEO.concat(dated_NEO)
      }, [])
      let formattedMagnitudes = all_NEO.map(NEO => {
        return [NEO.name, NEO.absolute_magnitude_h]
      })
      formattedMagnitudes.unshift(["near_earth_object", "magnitude"])
      return formattedMagnitudes
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
