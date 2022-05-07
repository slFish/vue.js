<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="@/assets/logo.png" /> -->
    <Calculator msg="Welcome to My Vue-Calculator" />
    <MyCosts msg="My personal costs" />
    <div>Total = {{ getFullPaymentValue }}</div>
    <MyCosts :items="getPaymentList" />
    <br />

    <router-link
      class="shortcut"
      :to="{
        name: 'AddPaymentForm',
        params: { section: 'payment', category: 'Food' },
        query: { value: 200, show: true },
      }"
      ><button>Food 200</button></router-link
    >
    <router-link
      class="shortcut"
      :to="{
        name: 'AddPaymentForm',
        params: { section: 'payment', category: 'Transport' },
        query: { value: 50, show: true },
      }"
      ><button>Transport 50</button></router-link
    >
    <router-link
      class="shortcut"
      :to="{
        name: 'AddPaymentForm',
        params: { section: 'payment', category: 'Entertainment' },
        query: { value: 2000, show: true },
      }"
      ><button>Entertainment 2000</button></router-link
    >
    <hr />
    <AddPaymentForm @addNewPayment="addPaymentData" />
    <MyPagination :cur="cur" :length="12" :n="n" @changePage="changePage" />
  </div>
</template>

<script>
import Calculator from "@/components/Calculator.vue";
import MyCosts from "@/components/Costs.vue";
import AddPaymentForm from "@/components/AddPaymentForm.vue";
import { mapMutations, mapGetters } from "vuex";
import MyPagination from "@/components/MyPagination.vue";

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
<style scoped>
.shortcut {
  padding: 10px;
}
</style>