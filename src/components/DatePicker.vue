<template>
  <div class="date-picker" :class="{ place: !value2 }">
    <span @click="onClick">{{ value2 ? value2 : '请选择' }}</span>
    <van-popup v-model="showPicker" round position="bottom">
      <van-datetime-picker
        v-model="currentDate"
        type="date"
        title="选择年月日"
        :min-date="minDate"
        :max-date="maxDate"
        @confirm="onConfirm" />
    </van-popup>
  </div>
</template>
<script>
import dayjs from 'dayjs';
export default {
  name: 'DatePicker',
  props: {
    value: [String, Number],
  },
  data() {
    return {
      showPicker: false,
      minDate: new Date(1960, 0, 1),
      maxDate: new Date(),
      currentDate: new Date(),
    };
  },
  computed: {
    value2: {
      get() {
        if (this.value) {
          this.setData(this.value);
        }
        return this.value;
      },
      set(value) {
        this.$emit('input', value);
      },
    },
  },
  methods: {
    setData(value) {
      this.currentDate = new Date(value);
    },
    onClick() {
      this.showPicker = true;
    },
    onConfirm(value) {
      this.value2 = dayjs(value).format('YYYY-MM-DD');
      this.showPicker = false;
    },
  },
};
</script>
<style lang="less" scoped>
.date-picker {
  width: 100%;
  text-align: right;
  font-size: 0.32rem;
  &.place {
    color: #9b9fa3;
  }
}
</style>
