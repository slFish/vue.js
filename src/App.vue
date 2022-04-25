<template>
  <img alt="Vue logo" src="./assets/logo.png">
<!--  <Calculator msg="Welcome to My Vue.js Calculator"/>-->
  <MyCosts msg="My personal costs"/>
  <MyCosts :items = "paymentsList" />
  <AddPaymentForm @addNewPayment="addPaymentData" />
</template>

<script>
// import Calculator from './components/Calculator.vue'
import MyCosts from './components/Costs.vue'
import AddPaymentForm from "@/components/AddPaymentForm";

export default {
  name: 'App',
  components: {
    // Calculator,
    MyCosts,
    AddPaymentForm
  },
  data () {
    return {
      paymentsList: []
    }
  },
  methods: {
    addPaymentData(data) {
      this.paymentsList.push(data)
    },
    fetchData() {
      return [
        {
          date: "28.03.2020",
          category: "Food",
          value: 169,
        },
        {
          date: "24.03.2020",
          category: "Transport",
          value: 360,
        },
        {
          date: "24.03.2020",
          category: "Food",
          value: 532,
        },
      ];
    },
  },
  created() {
    this.paymentsList = this.fetchData()
  }
};

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
