<template>
  <ClustersV :clustTotalNum="46" />
  <ClustersV :clustTotalNum="48" />
  <ClustersV :clustTotalNum="40" />
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import ClustersV from '@/components/ClustersV.vue';

export default defineComponent({
  name: 'ClusterSelectTopV',
  components: { ClustersV },
});
</script>
