<template>
  <div>
    <PieChart :chartData="chartData" />
  </div>
</template>

<script>
import { Pie } from 'vue-chartjs'
import { Chart as ChartJS, Title, Tooltip, Legend } from 'chart.js'
ChartJS.register(Title, Tooltip, Legend)

export default {
  name: 'PieChart',
  components: { Pie },
  data() {
    return {
      chartData: {
        labels: [],
        datasets: [{
          backgroundColor: ['#007bff', '#28a745', '#dc3545', '#ffc107'],
          data: []
        }]
      }
    }
  },
  mounted() {
    this.fetchChartData()
  },
  methods: {
    async fetchChartData() {
      try {
        const response = await fetch('https://data.cityofnewyork.us/resource/vfnx-vebw.json')
        const data = await response.json()
        
        // Assuming the response contains an array of objects with 'month' and 'value' properties
        const labels = data.map(entry => entry.month)
        const values = data.map(entry => entry.value)

        this.chartData.labels = labels
        this.chartData.datasets[0].data = values
      } catch (error) {
        console.error('Error fetching chart data:', error)
      }
    }
  }
}
</script>

<style lang="scss" scoped>
</style>

