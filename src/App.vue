<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <Calculator msg="Welcome to My Vue-Calculator" />
    <MyCosts msg="My personal costs" />
    <div>Total = {{ getFullPaymentValue }}</div>
    <MyCosts :items="getPaymentList" />
    <AddPaymentForm @addNewPayment="addPaymentData" />
    <MyPagination :cur="cur" :length="12" :n="n" @changePage="changePage" />
  </div>
</template>

<script>
import Calculator from "./components/Calculator.vue";
import MyCosts from "./components/Costs.vue";
import AddPaymentForm from "./components/AddPaymentForm.vue";
import { mapMutations, mapGetters } from "vuex";
import MyPagination from "./components/MyPagination.vue";

export default {
  name: "App",
  components: {
    Calculator,
    MyCosts,
    AddPaymentForm,
    MyPagination,
  },
  data() {
    return {
      paymentsList: [],
      cur: 1,
      n: 3,
    };
  },
  computed: {
    ...mapGetters(["getFullPaymentValue", "getPaymentList"]),
    // getFPV() {
    //   return this.$store.getters.getFullPaymentValue;
    // },
  },
  methods: {
    ...mapMutations({
      MyMutation: "setPaymentListData",
    }),
    addPaymentData(data) {
      this.paymentsList.push(data);
    },
    changePage(p) {
      this.cur = p;
      this.$store.dispatch("fetchData", p);
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
    this.$store.dispatch("fetchData", this.cur);
  },
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
