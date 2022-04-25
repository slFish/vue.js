<template>
<div>
  <h1>{{ msg }}</h1>
  <div v-for="(item, index) in items" :key="index">
    {{ item }}
  </div>
</div>
</template>

<script>
export default {
  name: "MyCosts",
  props: {
    msg: String,
    items: {
      type: Array,
      default: ()=>[]
    }
  },
}
</script>

<style scoped>

</style>