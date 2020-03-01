<template lang="html">
<GChart class="Histogram"
  type="Histogram"
  :data="histogramDataNEOMagnitude"
  :options="chartOptions"
/>
</template>


<script>
import {GChart} from 'vue-google-charts'

export default {
  name:"chart",
  components: {
    GChart
  },
  props:['histogramDataNEOMagnitude'],
  data(){
    return{
      chartOptions:{
        title: 'Histogram of near earth object magnitudes from 22/02/20 to 29/02/20',
      }
    }
  }
}
</script>

<style lang="css" scoped>
.Histogram{
width:1100px;
height:1000px;

}
</style>
