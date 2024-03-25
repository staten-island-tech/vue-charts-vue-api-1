<template>
  <div>
    <canvas ref="chartCanvas"></canvas>
  </div>
</template>

<script>
import Chart from 'chart.js/auto';

export default {
  mounted() {
    this.fetchDataAndRenderChart();
  },
  methods: {
    async fetchDataAndRenderChart() {
      try {
        const years = [2018, 2019, 2020];

        const dataPromises = years.map(async year => {
          const response = await fetch(`https://data.cityofnewyork.us/resource/vfnx-vebw.json?date=${year}`);
          const data = await response.json();
          return { year, data };
        });

        const results = await Promise.all(dataPromises);

        const datasets = results.map(result => {
          const totalSightings = result.data.length;
          return {
            label: `Squirrel Sightings in ${result.year}`,
            data: [totalSightings],
            backgroundColor: 'pink',
            borderColor: 'black',
            borderWidth: 1
          };
        });

        this.renderChart(datasets);
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    },
    renderChart(datasets) {
      const ctx = this.$refs.chartCanvas.getContext('2d');
      const chart = new Chart(ctx, {
        type: 'bar',
        data: {
          labels: datasets.map(dataset => dataset.label),
          datasets: datasets
        },
        options: {
          scales: {
            y: {
              beginAtZero: true,
              title: {
                display: true,
                text: 'Number of Sightings in Millions'
              },
            },
            x: {
              title: {
                display: true,
                text: 'Years',
                padding: {
                  top: 20, 
                  bottom: 0,
                  left: 0,
                  right: 0
                }
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
