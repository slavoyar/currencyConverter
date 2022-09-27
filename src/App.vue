<script>
import axios from 'axios'
import countryToCurrency from 'country-to-currency'
import ComboBox from './components/ComboBox.vue'
import TextBox from './components/TextBox.vue'

export default {
  components: {
    ComboBox,
    TextBox
  },
  data() {
    return {
      currencies: [],
      fromAmount: 1,
      toAmount: 1,
      fromCurrency: 'USD',
      toCurrency: 'EUR',
      timer: null
    }
  },
  mounted() {
    this.getCurrencies()
    const currentCountry = navigator.language.split('-')[1]
    this.fromCurrency = countryToCurrency[currentCountry]
    this.convertCurrency()
  },
  methods: {
    changeCurrencies() {
      const tempAmount = this.fromAmount
      this.fromAmount = this.toAmount
      this.toAmount = tempAmount

      const tempCurrency = this.fromCurrency
      this.fromCurrency = this.toCurrency
      this.toCurrency = tempCurrency
    },
    getCurrencies() {
      axios.get('https://api.exchangerate.host/symbols')
        .then(response => {
          this.currencies = []
          for (const item of Object.values(response.data.symbols)) {
            this.currencies.push(item.code)
          }
        })
        .catch(e => {
          console.error(e)
        })
    },
    convertCurrency() {
      const url = `https://api.exchangerate.host/convert?from=${this.fromCurrency}&to=${this.toCurrency}&amount=${this.fromAmount}`
      axios.get(url)
        .then(response => {
          this.toAmount = response.data.result
        })
        .catch(e => {
          console.error(e)
        })
    }
  },
  watch: {
    fromCurrency() {
      this.convertCurrency()
    },
    toCurrency() {
      this.convertCurrency()
    },
    fromAmount() {
      if (this.timer) {
        clearTimeout(this.timer)
        this.timer = null
      }
      this.timer = setTimeout(this.convertCurrency, 300)
    }
  }
}

</script>

<template>
  <h1>Currency converter</h1>
  <div class="container">
    <text-box label="Amount" v-model="fromAmount"/>
    <combo-box label="From" :items="currencies" v-model="fromCurrency"></combo-box>
    <button class="change-currencies-button" @click="changeCurrencies"><img
        src="https://cdn2.iconfinder.com/data/icons/arrows-set-1/512/27-512.png" alt=""></button>
    <text-box label="Amount" v-model="toAmount" :isDisabled="true" />
    <combo-box label="To" :items="currencies" v-model="toCurrency"></combo-box>
  </div>
</template>

<style scoped>
h1 {
  text-align: center;
  margin: 20% auto 50px;
  color: rgb(37, 37, 37);
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
  background-color: transparent;
  border: 0;
  cursor: pointer;
}

.change-currencies-button img {
  height: 40px;
  width: 40px;
  margin: 0;
}
</style>
