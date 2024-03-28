<template>
  <div class="cell-item">
    <div class="cell-item-label">{{ label }}</div>
    <div class="cell-item-value">{{ value }}</div>
  </div>
</template>
<script>
export default {
  name: 'CellItem',
  props: {
    label: String,
    value: [String, Number],
  },
};
</script>
<style lang="less" scoped>
.cell-item {
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
  .cell-item-label {
  }
  .cell-item-value {
  }
}
</style>
