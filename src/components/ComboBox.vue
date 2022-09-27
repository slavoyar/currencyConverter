<script>
export default {
  name: 'ComboBox',
  props: ['label', 'items', 'modelValue'],
  emits: ['update:modelValue'],
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
  width: 100%;
}

#combobox-select {
  width: 100%;
  height: 50px;
  font-size: 12pt;
}
</style>