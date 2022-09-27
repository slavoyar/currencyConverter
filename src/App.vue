<script>
import ComboBox from './components/ComboBox.vue'

export default {
  components: {
    ComboBox
  },
  emits: ['update:modelValue'],
  data() {
    return {
      currencies: ['USD', 'EUR', 'RUB'],
      fromCurrency: 'USD',
      toCurrency: 'RUB'
    }
  },
  watch: {
    fromCurrency() {
      console.log(this.fromCurrency)
    }
  }
}

</script>

<template>
  <div class="container">
    <input type="text">
    <combo-box label="From" :items="currencies" v-model="fromCurrency"></combo-box>
    <button class="change-currencies-button"><img
        src="https://cdn2.iconfinder.com/data/icons/arrows-set-1/512/27-512.png" alt=""></button>
    <input type="text">
    <combo-box label="To" :items="currencies" v-model="toCurrency"></combo-box>
  </div>
</template>

<style scoped>
.container {
  width: 620px;
  margin: 30% auto;
  display: grid;
  grid-gap: 1%;
  grid-template-columns: 1fr 1fr 60px 1fr 1fr;
}

.change-currencies-button {
  height: 50px;
  width: 50px;
  padding: 0;
  margin: 35% auto 0;
}

.change-currencies-button img {
  height: 40px;
  width: 40px;
  margin: 0;
}
</style>
