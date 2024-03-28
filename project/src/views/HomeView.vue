<template>
  <div>
    <h1>Squrriels by their id</h1>
    <CardList
      class="card"
      v-for="card in squrriels"
      :key="squrriels.unique_squirrel_id"
      :card="card"
    />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import CardList from '@/components/SqurrielCard.vue'
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

<style lang="css">
body * {
  box-sizing: border-box;
  font-size: 110%;
  margin: 0;
  padding: 0;
}
h1 {
  text-align: center;
  font-size: 3rem;
}
.CardList {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  background-color: #fec89a;
  border: black solid;
}
.name {
  width: 30rem;
  margin: 1rem auto;
  border-radius: 2rem;
  object-fit: cover;
  border-radius: 2rem;
  justify-content: space-around;
  text-align: center;
}
</style>
