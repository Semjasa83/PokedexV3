<script lang="ts">
import {
  Chart as ChartJS,
  RadialLinearScale,
  PointElement,
  LineElement,
  Filler,
  Tooltip,
  Legend
} from 'chart.js'
import { Radar } from 'vue-chartjs'
import * as chartConfig from './chartConfig.js'

ChartJS.register(
  RadialLinearScale,
  PointElement,
  LineElement,
  Filler,
  Tooltip,
  Legend
)

export default {
  name: 'App',
  components: {
    Radar
  },
  data() {
    return chartConfig
  }
}
</script>

<template>
  <div class="chart-wrapper">
    <Radar :data="data" :options="options" />
  </div>
</template>

<style scoped lang="scss">
  .chart-wrapper {
    width: 100%;
    height: 100%;
    background-color: hsl(0, 0, 100%);
  }

</style>