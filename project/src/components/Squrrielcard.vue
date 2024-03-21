<template>
  <div>
    <div class="CardList">
      <h2 class="name">{{ card.unique_squirrel_id }}</h2>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  card: Object
})
</script>

<style lang="scss"></style>
