<template>
  <div class="form">
    <FormItem v-for="(item, index) in userInfo" :key="index" :label="item.label" :required="item.required">
      <ZdyInput v-if="item.type === 'input'" v-model="item.value" />
      <ZdySelect v-if="item.type === 'select'" :columns="item.columns" v-model="item.value" />
      <DatePicker v-if="item.type === 'datePicker'" v-model="item.value" />
    </FormItem>
  </div>
</template>
<script>
import FormItem from './FormItem.vue';
import ZdyInput from './ZdyInput.vue';
import ZdySelect from './ZdySelect.vue';
import DatePicker from './DatePicker.vue';
export default {
  name: 'ZdyForm',
  props: {
    userInfo: {
      type: Array,
      default: () => [],
    },
  },
  components: { FormItem, ZdyInput, ZdySelect, DatePicker },
};
</script>
<style lang="less" scoped>
.form {
  padding: 0 0.56rem;
}
</style>
