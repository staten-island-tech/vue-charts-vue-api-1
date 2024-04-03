<template>
  <main>
    <Doughnut id="chart-id" :options="chartOptions" :data="chartData" />
  </main>
</template>

<script>
import { Doughnut } from "vue-chartjs";
import { Chart as ChartJS, ArcElement, Tooltip, Legend } from "chart.js";
ChartJS.register(ArcElement, Tooltip, Legend);


export default {
  name: "Donut",
  components: { Doughnut },
  props: {
    data: {
      type: Array,
      required: true,
    },
    labels: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      chartData: {
        labels: this.labels,
        datasets: [
          {
            data: this.data,
            hoverOffset: 4,
            backgroundColor: ['#f87979', '#00D8FF', '#f87947'],
          },
        ],
      },
      chartOptions: {
        responsive: true,
      },
    };
  },
};


</script>

<style scoped></style>