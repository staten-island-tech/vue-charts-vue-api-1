<template>
  <div>
    <canvas ref="chartCanvas"></canvas>
  </div>
</template>

<script>
import Chart from 'chart.js/auto';

export default {
  mounted() {
    this.renderChart();
  },
  methods: {
    renderChart() {
      const ctx = this.$refs.chartCanvas.getContext('2d');
      const labels = ['2000', '2005', '2010', '2015', '2020'];
      const data = Array.from({ length: 5 }, () => Math.floor(Math.random() * 100));
      const chart = new Chart(ctx, {
        type: 'bar',
        data: {
          labels: labels,
          datasets: [{
            label: 'Squirel Sightings',
            data: data,
            backgroundColor: 'pink',
            borderColor: 'black',
            borderWidth: 1
          }]
        },
        options: {
          scales: {
            y: {
              beginAtZero: true,
              title: {
                display: true,
                text: 'Sightings'
              }
            },
            x: {
              title: {
                display: true,
                text: 'Year'
              }
            }
          }
        }
      });
    }
  }
};
</script>

<style>
canvas {
  width: 100%;
  height: 400px; /* Adjust height as needed */
}
</style>
