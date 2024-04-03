<template>
  <div class="one">
    <h1>Squirrel population vs. Fur color</h1>
    <Chart v-if ="loaded" :data="Object.values(furstuff)" :labels="Object.keys(furstuff)"/>
    <div class="two" @change="rechart">
      <label>
          Select a Filter
          <select id="selection" v-model="agefilter">
            <option value="nothing">No Filter</option>
            <option v-for="filter in oldnessarray" :key="filter">{{ filter }}</option>
          </select>
        </label>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, reactive  } from 'vue';
import Chart from '@/components/BarChart.vue';

let oldnessarray = [];
const loaded = ref(false);
let data = reactive([]);
const furstuff = ref({});
const agefilter = ref("nothing"); //default for dropdown select

onMounted(async() => {
  const fetchAge = await fetch( //To get all the years
    "https://data.cityofnewyork.us/resource/vfnx-vebw.json?$query=SELECT%20%60age%60%20GROUP%20BY%20%60age%60"
  );
  oldnessarray = await fetchAge.json();
  oldnessarray = oldnessarray.map((age) => age.age);
  console.log(oldnessarray);
  rechart();
});

async function rechart(){
  loaded.value = false;
furstuff = {};
  console.log(agefilter.value)
  if (agefilter.value === "nothing") {
    data = await fetchDataNormal();
  } else {
    data = await fetchChartData(agefilter.value);
  }
  console.log(data);
  data.forEach((squirrel) => {
    furstuff[squirrel.primary_fur_color] ??= 0;
    furstuff[squirrel.primary_fur_color] += 1;
  });
  console.log(furstuff);
  console.log(Object.keys(furstuff));
  console.log(Object.values(furstuff));
  loaded.value = true;
}

async function fetchChartData(age){
  try {
    let res = await fetch(`
    https://data.cityofnewyork.us/resource/vfnx-vebw.json?$query=SELECT%0A%20%20%60x%60%2C%0A%20%20%60y%60%2C%0A%20%20%60unique_squirrel_id%60%2C%0A%20%20%60hectare%60%2C%0A%20%20%60shift%60%2C%0A%20%20%60date%60%2C%0A%20%20%60hectare_squirrel_number%60%2C%0A%20%20%60age%60%2C%0A%20%20%60primary_fur_color%60%2C%0A%20%20%60highlight_fur_color%60%2C%0A%20%20%60combination_of_primary_and%60%2C%0A%20%20%60color_notes%60%2C%0A%20%20%60location%60%2C%0A%20%20%60above_ground_sighter%60%2C%0A%20%20%60specific_location%60%2C%0A%20%20%60running%60%2C%0A%20%20%60chasing%60%2C%0A%20%20%60climbing%60%2C%0A%20%20%60eating%60%2C%0A%20%20%60foraging%60%2C%0A%20%20%60other_activities%60%2C%0A%20%20%60kuks%60%2C%0A%20%20%60quaas%60%2C%0A%20%20%60moans%60%2C%0A%20%20%60tail_flags%60%2C%0A%20%20%60tail_twitches%60%2C%0A%20%20%60approaches%60%2C%0A%20%20%60indifferent%60%2C%0A%20%20%60runs_from%60%2C%0A%20%20%60other_interactions%60%2C%0A%20%20%60geocoded_column%60%2C%0A%20%20%60%3A%40computed_region_efsh_h5xi%60%2C%0A%20%20%60%3A%40computed_region_f5dn_yrer%60%2C%0A%20%20%60%3A%40computed_region_yeji_bk3q%60%2C%0A%20%20%60%3A%40computed_region_92fq_4b7q%60%2C%0A%20%20%60%3A%40computed_region_sbqj_enih%60%0AWHERE%20caseless_one_of(%60age%60%2C%20%22${age}%22)`);
    let data = await res.json();
    return data
  } catch (e) {
    console.error(e);
  }
}

async function fetchDataNormal(){
  try {
    let res = await fetch(`
    https://data.cityofnewyork.us/resource/vfnx-vebw.json?$query=SELECT%0A%20%20%60x%60%2C%0A%20%20%60y%60%2C%0A%20%20%60unique_squirrel_id%60%2C%0A%20%20%60hectare%60%2C%0A%20%20%60shift%60%2C%0A%20%20%60date%60%2C%0A%20%20%60hectare_squirrel_number%60%2C%0A%20%20%60age%60%2C%0A%20%20%60primary_fur_color%60%2C%0A%20%20%60highlight_fur_color%60%2C%0A%20%20%60combination_of_primary_and%60%2C%0A%20%20%60color_notes%60%2C%0A%20%20%60location%60%2C%0A%20%20%60above_ground_sighter%60%2C%0A%20%20%60specific_location%60%2C%0A%20%20%60running%60%2C%0A%20%20%60chasing%60%2C%0A%20%20%60climbing%60%2C%0A%20%20%60eating%60%2C%0A%20%20%60foraging%60%2C%0A%20%20%60other_activities%60%2C%0A%20%20%60kuks%60%2C%0A%20%20%60quaas%60%2C%0A%20%20%60moans%60%2C%0A%20%20%60tail_flags%60%2C%0A%20%20%60tail_twitches%60%2C%0A%20%20%60approaches%60%2C%0A%20%20%60indifferent%60%2C%0A%20%20%60runs_from%60%2C%0A%20%20%60other_interactions%60%2C%0A%20%20%60geocoded_column%60%2C%0A%20%20%60%3A%40computed_region_efsh_h5xi%60%2C%0A%20%20%60%3A%40computed_region_f5dn_yrer%60%2C%0A%20%20%60%3A%40computed_region_yeji_bk3q%60%2C%0A%20%20%60%3A%40computed_region_92fq_4b7q%60%2C%0A%20%20%60%3A%40computed_region_sbqj_enih%60`);
    let data = await res.json();
    return data
  } catch (e) {
    console.error(e);
  }
}

</script>

<style scoped>
.one{
  max-width: 900px;
  max-height: 900px;
}


</style>