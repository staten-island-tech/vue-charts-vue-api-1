<template>
  <div></div>
  <Bar id="my-chart-id" :options="chartOptions" :data="chartData" />
</template>

<script>
import { ref, onMounted } from 'vue'
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
const squrriels = ref('')
async function getsqurriel() {
  let res = await fetch('https://data.cityofnewyork.us/resource/vfnx-vebw.json')
  let data = await res.json()
  squrriels.value = data
  console.log(squrriels)
}
onMounted(() => {
  getsqurriel()
})
export default {
  name: 'BarChart',
  components: { Bar },
  data() {
    return {
      chartData: {
        labels: [squrriels.unique_squirrel_id],
        datasets: [{ data: [40, 20, 12, 30] }]
      },
      chartOptions: {
        responsive: true
      }
    }
  }
}
</script>

<style lang="scss" scoped></style>
