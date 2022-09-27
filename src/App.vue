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
  }
}

</script>

<template>
  <combo-box label="From" :items="currencies" v-model="fromCurrency"></combo-box>
  <combo-box label="To" :items="currencies" v-model="toCurrency"></combo-box>
</template>

<style scoped>

</style>
