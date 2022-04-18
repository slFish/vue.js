<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    {{ error }}
    <br>
    <input v-model.number="operand1" :class="picked"/>
    и
    <input v-model.number="operand2" :class="picked"/>
    =
    {{ result }}
    <hr>
    <button @click="add">+</button>
    <button @click="substract">-</button>
    <button @click="divide">/</button>
    <button @click="multiply">x</button>
    <button @click="pow">Степень</button>

    <br>

    <input type="checkbox" id="checkbox" v-model="numPad">
    <label for="checkbox">Показать панель</label>

    <div v-if="picked == 'operand1'">
      <div v-if="numPad">
        <button
            @click="edit1(num)"
            :title="num"
            v-for="num in nums"
            :key="num"
        > {{ num }}
        </button>
        <button @click="del1">Del</button>
        <div>
          <input type="radio" id="one" value="operand1" v-model="picked" >
          <label for="one">Один</label>
          <input type="radio" id="two" value="operand2" v-model="picked" >
          <label for="two">Два</label>
        </div>
      </div>
    </div>
    <div v-else>
      <div v-if="numPad">
        <button
            @click="edit2(num)"
            :title="num"
            v-for="num in nums"
            :key="num"
        > {{ num }}
        </button>
        <button @click="del2">Del</button>
        <div>
          <input type="radio" id="one" value="operand1" v-model="picked" >
          <label for="one">Один</label>
          <input type="radio" id="two" value="operand2" v-model="picked" >
          <label for="two">Два</label>
        </div>
      </div>
    </div>
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
      numPad: true,
      nums: [1,2,3,4,5,6,7,8,9,0],
      picked:'operand1',
      test:'',
    }
  },
  methods: {
    add () {
      this.result = +this.operand1 + +this.operand2
    },
    substract () {
      this.result = this.operand1 - this.operand2
    },
    divide () {
      if (this.operand2 !== 0) {
        this.result = this.operand1 / this.operand2
      } else {
        this.error = 'Нельзя делить на ноль!'
      }
      setTimeout(() => {this.error = ''}, 2000) // Убрали инфу об ошибке
    },
    multiply () {
      this.result = this.operand1 * this.operand2
    },
    pow () {
      this.result = this.operand1 ** this.operand2
    },
    edit1(num) {
      this.test = String(this.operand1)
      this.operand1 = this.test.padEnd(this.operand1.length + 1,num)
      console.log(typeof this.operand1)
    },
    del1() {
      this.test = String(this.operand1)
      this.operand1 = this.test.slice(0,-1)
      console.log(typeof this.operand1)
    },
    edit2(num) {
      this.test = String(this.operand2)
      this.operand2 = this.test.padEnd(this.operand2.length + 1,num)
    },
    del2() {
      this.test = String(this.operand2)
      this.operand2 = this.test.slice(0,-1)
    },
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
