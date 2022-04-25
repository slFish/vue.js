<template>
  <button @click="show=!show">Add</button>
<div v-if="show">
  <input v-model="date" placeholder="Date">
  <input v-model="category" placeholder="Category">
  <input v-model="value" placeholder="Value">
  <button @click="onClickSave">ADD +</button>
</div>
</template>

<script>
export default {
  name: "AddPaymentForm",
  emits: ["addNewPayment"],
  data() {
    return {
      date: '',
      category:'',
      value:'',
      show: false,
    }
  },
  computed: {
    getCurrentDate(){
      const today = new Date()
      const todayFormated = new Intl.DateTimeFormat('ru').format(today)
      return todayFormated
      // const d = today.getDate()
      // const m = today.getMonth()+1
      // const y = today.getFullYear()
      // return `${d}.${m}.${y}`
    },

  },
  methods: {
    onClickSave() {
      const data = {
        date: this.date || this.getCurrentDate,
        category: this.category,
        value: this.value
      }
      this.$emit('addNewPayment', data)
    },
  }
}
</script>

<style scoped>

</style>