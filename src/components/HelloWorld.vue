<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    {{ error }}
    <br>
    <input v-model.number="operand1"/>
    и
    <input v-model.number="operand2"/>
    =
    {{ result }}
    <hr>
    <button @click="sum">+</button>
    <button @click="minus">-</button>
    <button @click="sub">/</button>
    <button @click="multiply">x</button>
    <button @click="pow">Степень</button>
<!--возведение в степень-->
<!--    не делим на ноль-->


  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      result: '',
      operand1: '',
      operand2: '',
      error: '',
    }
  },
  methods: {
    sum () {
      this.result = this.operand1 + this.operand2
    },
    minus () {
      this.result = this.operand1 - this.operand2
    },
    sub () {
      if (this.operand2 !== 0)
      this.result = this.operand1 / this.operand2
      else (this.error = 'Нельзя делить на ноль!')
      setTimeout(() => {this.error = ''}, 2000) // Убрали инфу об ошибке
    },
    multiply () {
      this.result = this.operand1 / this.operand2
    },
    pow () {
      this.result = this.operand1 ** this.operand2
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
button {
  margin: 5px;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
