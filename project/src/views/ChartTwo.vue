<template>
  <h1>Squrriels above ground VS on ground</h1>
  <Doughnut v-if="loaded" :data="Object.values(sqe)" :labels="Object.keys(sqe)" />
</template>

<script lang="js" setup>
import Doughnut from "../components/DoughnutChart.vue";
import { onMounted, ref, reactive } from "vue";
const loaded = ref(false);
let d = reactive([]);
let sqe = reactive ({});

async function Chart(){
  loaded.value = false;
  console.log(d);
  d.forEach((sq)=> {
  sqe[sq.location] ??= 0;
  sqe[sq.location] += 1;}
  )
  loaded.value = true;
}

onMounted(async () => {
  const fetched = await fetch('https://data.cityofnewyork.us/resource/vfnx-vebw.json')
  const jsondata = await fetched.json();
  d = jsondata
  await Chart();
});



</script>
<style scoped></style>