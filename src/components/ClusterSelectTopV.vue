<template>
  <!-- <el-switch
    v-model="swVal"
    size="default"
    active-color="#409EFF"
    inactive-color="#409EFF"
    active-text="Die1"
    inactive-text="Die0"
  /> -->
  <ClustersV :clustTotalNum="46" :text="'Die0'" />
  <ClustersV :clustTotalNum="48" :text="'Die1'" />
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import ClustersV from '@/components/ClustersV.vue';

export default defineComponent({
  name: 'ClusterSelectTopV',
  components: { ClustersV },
  setup() {
    const swVal = ref(true);

    return { swVal };
  },
});
</script>

<style lang="scss">
.el-switch__label {
  color: gray;
  font-weight: bold;
  &.is-active {
    color: black;
  }
}
</style>
