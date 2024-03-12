<template>
  <div></div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

async function getsqurriel() {
  let res = await fetch('https://data.cityofnewyork.us/resource/vfnx-vebw.json')
  let data = await res.json()
  console.log(data)
}
onMounted(() => {
  getsqurriel()
})
</script>

<style lang="scss" scoped></style>
