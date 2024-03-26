<template>
  <Bar id="my-chart-id" :options="chartOptions" :data="chartData" />
</template>

<script>
import { Bar } from 'vue-chartjs'
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale
} from 'chart.js'

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

export default {
  name: 'BarChart',
  components: { Bar },
  props: {
    data: Array,
    labels: Array
  },
  data() {
    return {
      chartData: {
        labels: this.labels,
        datasets: [
          {
            backgroundColor: '#f87979',
            label: 'Number of squirrels with this fur color',
            data: this.data
          }
        ]
      },
      chartOptions: {
        responsive: true
      }
    }
  }
}
</script>

<style scoped>
bar {
  max-width: 800px;
  max-height: 800px;
}
</style>
