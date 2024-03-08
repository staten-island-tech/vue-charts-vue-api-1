<template>
  <div></div>
</template>

<script setup>
import { ref, Created } from 'vue'
const squrriel = ref('')
async function getsqurriel() {
  let res = await fetch('https://data.cityofnewyork.us/resource/vfnx-vebw.json')
  let data = await res.json()
  squrriel.value = data.results
}
Created(() => {
  getsqurriel()
})
</script>

<style lang="scss" scoped></style>
