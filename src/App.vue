<script>
import ComboBox from './components/ComboBox.vue'
import TextBox from './components/TextBox.vue'

export default {
  components: {
    ComboBox,
    TextBox
  },
  emits: ['update:modelValue'],
  data() {
    return {
      currencies: ['USD', 'EUR', 'RUB'],
      fromAmount: 10,
      toAmount: 20,
      fromCurrency: 'USD',
      toCurrency: 'RUB'
    }
  },
  mounted() {
    
  },  
  methods: {
    changeCurrencies() {
      const tempAmount = this.fromAmount
      this.fromAmount = this.toAmount
      this.toAmount = tempAmount

      const tempCurrency = this.fromCurrency
      this.fromCurrency = this.toCurrency
      this.toCurrency = tempCurrency
    }
  }
}

</script>

<template>
  <h1>Currency converter</h1>
  <div class="container">
    <text-box label="Amount" v-model="fromAmount" />
    <combo-box label="From" :items="currencies" v-model="fromCurrency"></combo-box>
    <button class="change-currencies-button" @click="changeCurrencies"><img
        src="https://cdn2.iconfinder.com/data/icons/arrows-set-1/512/27-512.png" alt=""></button>
    <text-box label="Amount" v-model="toAmount" :isReadonly="true"/>
    <combo-box label="To" :items="currencies" v-model="toCurrency"></combo-box>
  </div>
</template>

<style scoped>
h1 {
  text-align: center;
  margin: 20% auto 50px;
  
}
.container {
  width: 620px;
  margin: 0 auto;
  display: grid;
  grid-gap: 1%;
  grid-template-columns: 3fr 2fr 60px 3fr 2fr;
}

.change-currencies-button {
  height: 50px;
  width: 50px;
  padding: 0;
  margin: 35% auto 0;
  background-color: white;
  border: 0;
  cursor: pointer;
}

.change-currencies-button img {
  height: 40px;
  width: 40px;
  margin: 0;
}
</style>
