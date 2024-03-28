<template>
  <div class="form-item">
    <div class="form-item-label" :class="{ required: required }">{{ label }}</div>
    <div class="form-item-value">
      <slot></slot>
    </div>
  </div>
</template>
<script>
export default {
  name: 'FormItem',
  props: {
    label: String,
    required: Boolean,
  },
};
</script>
<style lang="less" scoped>
.form-item {
  height: 1.12rem;
  color: #1a1d27;
  font-size: 0.32rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: relative;
  &:not(:last-child)::after {
    content: '';
    width: 100%;
    height: 1px;
    background-color: #eeeeee;
    position: absolute;
    left: 0;
    bottom: 0;
  }
  .form-item-label {
    width: 2rem;
    &.required {
      position: relative;
      &::before {
        content: '*';
        color: #f74c31;
        font-size: 0.24rem;
        position: absolute;
        left: -0.2rem;
        top: 3px;
      }
    }
  }
  .form-item-value {
    flex: 1;
  }
}
</style>
