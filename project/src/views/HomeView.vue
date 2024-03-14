<template>
  <div>
    <squrrielcard
      v-for="squrriel in squrriels"
      :key="squrriels.unique_squirrel_id"
      :squrriel="squrriel"
    ></squrrielcard>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { squrrielcard } from '../components/Squrrielcard.vue'
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
</script>

<style lang="scss" scoped></style>
