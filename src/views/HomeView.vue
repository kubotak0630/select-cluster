<template>
  <ClusterSelectTopV />
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import ClusterSelectTopV from '@/components/ClusterSelectTopV.vue';

export default defineComponent({
  name: 'HomeView',
  components: { ClusterSelectTopV },
});
</script>
