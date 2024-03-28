<template>
  <ZdyCell>
    <CellItem v-for="(item, index) in userInfo" :key="index" :label="item.label" :value="item.value | formatValue" />
  </ZdyCell>
</template>
<script>
import ZdyCell from './ZdyCell.vue';
import CellItem from './CellItem.vue';
export default {
  name: 'PreviewView',
  props: {
    userInfo: {
      type: Array,
      default: () => [],
    },
  },
  components: { ZdyCell, CellItem },
  filters: {
    formatValue(value) {
      return value ? value : '--';
    },
  },
};
</script>
