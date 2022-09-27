<script>
import { readonly } from 'vue';

export default {
  name: 'TextBox',
  props: ['modelValue', 'label', 'isDisabled'],
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
  <div class="textbox">
    <label for="textbox-input">{{ label }}</label>
    <input id="textbox-input" type="number" min="0" v-model="content" :disabled="isDisabled"/>
  </div>
</template>

<style>
.textbox {
  width: 100%;
}

#textbox-input {
  width: 100%;
  height: 46px;
  padding: 0;
  font-size: 12pt;
}
</style>