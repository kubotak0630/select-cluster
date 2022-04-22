<template>
  <div class="clst">
    <el-button type="primary">{{ clstNo }}</el-button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'ClstElementV',
  components: {},
  props: {
    clstNo: {
      type: Number,
      required: true,
    },
  },
});
</script>

<style lang="scss" scoped>
.clst {
  margin: 0 2px;
}
</style>
