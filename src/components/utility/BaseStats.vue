<script lang="ts">
import {
  Chart as ChartJS,
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
  Title,
  Tooltip,
  Legend
} from 'chart.js'
import { Line } from 'vue-chartjs'

ChartJS.register(
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
  Title,
  Tooltip,
  Legend
)


export default {
  name: 'BaseStats',
  props: {
    pokemon: Object
  },
  components: {
    // eslint-disable-next-line vue/no-reserved-component-names
    Line
  },
  data() {
    const labels = this.pokemon.additionalData && this.pokemon.additionalData.stats ?
      this.pokemon.additionalData.stats.map(e => e.stat.name) :
      [];

    const stats = this.pokemon.additionalData && this.pokemon.additionalData.stats ?
      this.pokemon.additionalData.stats.map(e => e.base_stat) :
      [];

    const data = {
      labels,
      datasets: [
        {
          label: 'Base Stats',
          backgroundColor: '#f87979',
          data: stats
        }
      ]
    }

    const options = {
      responsive: true,
      maintainAspectRatio: false
    }
    return { data, options }; // Dies gibt die definierten Daten und Optionen zurück
  }
}

</script>

<template>
  <div class="chart-wrapper">
    <Line :data="data" :options="options" />
  </div>
</template>

<style scoped lang="scss">
.chart-wrapper {
  width: 100%;
  height: 100%;
  background-color: hsl(0, 0%, 100%);
}
</style>