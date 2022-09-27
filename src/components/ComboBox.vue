<script>
export default {
  name: 'ComboBox',
  props: ['label', 'items', 'modelValue'],
  data() {
    return {
      content: this.modelValue
    }
  },
  watch: {
    content() {
      this.$emit('update:modelValue', this.content)
    },
    modelValue() {
      this.content = this.modelValue
    }
  }
}
</script>

<template>
  <div class="combobox">
    <label for="combobox-select">{{ label }}</label>
    <select id="combobox-select" v-model="content">
      <option v-for="item of items">{{ item }}</option>
    </select>
  </div>
</template>

<style>
.combobox {
  font-size: 14pt;
  width: 300px;
}

.combobox-label {
  padding: 0;
  margin: 0;
}

#combobox-select {
  width: 100%;
  font-size: 14pt;
}
</style>