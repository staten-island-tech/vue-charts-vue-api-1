<template>
  <Doughnut :data="data" :options="options" />
</template>

<script lang="js">
import { Chart as ChartJS, ArcElement, Tooltip, Legend } from 'chart.js'
import { Doughnut } from 'vue-chartjs'

ChartJS.register(ArcElement, Tooltip, Legend)

export default {
  name: 'App',
  components: {
    Doughnut
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
