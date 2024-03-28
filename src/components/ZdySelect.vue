<template>
  <div class="select" :class="{ place: !value2 }">
    <span @click="onClick">{{ value2 ? value2 : '请选择' }}</span>
    <van-popup v-model="showPicker" round position="bottom">
      <van-picker show-toolbar :columns="columns" @cancel="showPicker = false" @confirm="onConfirm" />
    </van-popup>
  </div>
</template>
<script>
export default {
  name: 'ZdySelect',
  props: {
    value: {
      type: [String, Number],
    },
    columns: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      showPicker: false,
    };
  },
  computed: {
    value2: {
      get() {
        return this.value;
      },
      set(value) {
        this.$emit('input', value);
      },
    },
  },
  methods: {
    onClick() {
      this.showPicker = true;
    },
    onConfirm(value) {
      this.value2 = value;
      this.showPicker = false;
    },
  },
};
</script>
<style lang="less" scoped>
.select {
  width: 100%;
  text-align: right;
  font-size: 0.32rem;
  &.place {
    color: #9b9fa3;
  }
}
</style>
