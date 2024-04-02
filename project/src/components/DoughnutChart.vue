<template>
  <div class="two"></div>
</template>

<script>
const ongroundnum = [1000]
const abovegroundnum = [843]
async function getabovegroundnum() {
  let res = await fetch(
    "https://data.cityofnewyork.us/resource/vfnx-vebw.json?$query=SELECT%20x%2C%20y%2C%20unique_squirrel_id%2C%20hectare%2C%20shift%2C%20date%2C%20hectare_squirrel_number%2C%20age%2C%20primary_fur_color%2C%20highlight_fur_color%2C%20combination_of_primary_and%2C%20color_notes%2C%20location%2C%20above_ground_sighter%2C%20specific_location%2C%20running%2C%20chasing%2C%20climbing%2C%20eating%2C%20foraging%2C%20other_activities%2C%20kuks%2C%20quaas%2C%20moans%2C%20tail_flags%2C%20tail_twitches%2C%20approaches%2C%20indifferent%2C%20runs_from%2C%20other_interactions%2C%20geocoded_column%20WHERE%20(upper(%60location%60)%20LIKE%20'%25ABOVE%20GROUND%25')"
  )
  let data = await res.json()
  abovegroundnum.value = data.length
}
async function getongroundnum() {
  let res = await fetch(
    "https://data.cityofnewyork.us/resource/vfnx-vebw.json?$query=SELECT%20x%2C%20y%2C%20unique_squirrel_id%2C%20hectare%2C%20shift%2C%20date%2C%20hectare_squirrel_number%2C%20age%2C%20primary_fur_color%2C%20highlight_fur_color%2C%20combination_of_primary_and%2C%20color_notes%2C%20location%2C%20above_ground_sighter%2C%20specific_location%2C%20running%2C%20chasing%2C%20climbing%2C%20eating%2C%20foraging%2C%20other_activities%2C%20kuks%2C%20quaas%2C%20moans%2C%20tail_flags%2C%20tail_twitches%2C%20approaches%2C%20indifferent%2C%20runs_from%2C%20other_interactions%2C%20geocoded_column%20WHERE%20(upper(%60location%60)%20LIKE%20'%25GROUND%20PLANE%25')"
  )
  let data = await res.json()
  ongroundnum.value = data.length
}
console.log(ongroundnum, abovegroundnum)
getongroundnum()
getabovegroundnum()

export const data = {
  labels: [ongroundnum, abovegroundnum],
  datasets: [
    {
      backgroundColor: ['#f87979', '#00D8FF'],
      label: ['ongroundnum', 'abovegroundnum'],
      data: [ongroundnum, abovegroundnum]
    }
  ]
}

export const options = {
  responsive: true
}
</script>

<style scoped></style>
