<template>
  <div>
    <button @click="show = !show">Add</button>
    <div v-if="show">
      <input v-model="date" placeholder="Date" />
      <select v-model="category" v-if="categoryList">
        <option v-for="(value, idx) in categoryList" :key="idx">
          {{ value }}
        </option>
      </select>
      <!-- <input v-model="category" placeholder="Category" /> -->
      <input v-model.number="value" placeholder="Value" />
      <button @click="onClickSave">ADD +</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddPaymentForm",
  data() {
    return {
      date: "",
      category: "",
      value: "",
      show: false,
    };
  },
  computed: {
    getCurrentDate() {
      const today = new Date();
      const todayFormated = new Intl.DateTimeFormat("ru").format(today);
      return todayFormated;
      // const d = today.getDate()
      // const m = today.getMonth()+1
      // const y = today.getFullYear()
      // return `${d}.${m}.${y}`
    },
    categoryList() {
      return this.$store.getters.getCategoryList;
    },
  },
  methods: {
    onClickSave() {
      const data = {
        date: this.date || this.getCurrentDate,
        category: this.category,
        value: this.value,
      };
      this.$store.commit("addDataToPaymentsList", data);
    },
  },
};
</script>

<style scoped>
</style>