<template>
  <div class="container">
    <ClstElementV v-for="(n, i) in 24" :key="i" :clstNo="i" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import ClstElementV from '@/components/ClstElementV.vue';

export default defineComponent({
  name: 'NandClusterV',
  components: { ClstElementV },
});
</script>

<style lang="scss" scoped>
.container {
  display: flex;
}
</style>
