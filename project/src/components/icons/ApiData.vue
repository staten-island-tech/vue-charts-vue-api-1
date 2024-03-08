<template>
  <div></div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
const squrriel = ref('')
async function getdata() {
  let res = await fetch('https://data.cityofnewyork.us/resource/vfnx-vebw.json')
  let data = await res.json()
  squrriel.value = data.result
  console.log(squrriel.data)
}
onMounted(() => {
  getdata()
})
</script>

<style lang="scss" scoped></style>
