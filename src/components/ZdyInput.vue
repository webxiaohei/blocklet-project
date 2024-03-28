<template>
  <input class="input" type="text" placeholder="请输入" :value="value" @input="onInput" />
</template>
<script>
export default {
  name: 'ZdyInput',
  props: {
    value: [String, Number],
  },
  methods: {
    onInput(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>
<style lang="less" scoped>
.input {
  width: 100%;
  border: none;
  outline: none;
  text-align: right;
  &::placeholder {
    color: #9b9fa3;
  }
}
</style>
