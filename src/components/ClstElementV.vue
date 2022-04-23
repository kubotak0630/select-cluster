<template>
  <div>
    <div
      class="cluster"
      :class="{ pushed: pushed, 'is-cpbc': isCpbc }"
      :style="{ width: rectWidth }"
      @click="onClickBtn"
    >
      {{ clstIdx }}
    </div>
    <div v-if="isCpbc" class="under-line" :style="{ width: underLineWidth }"></div>
  </div>
</template>

<script lang="ts">
import { computed } from '@vue/reactivity';
import { defineComponent, ref, watch, onMounted } from 'vue';

export default defineComponent({
  name: 'ClstElementV',
  components: {},
  emits: ['emit-pushed'],
  props: {
    clstIdx: {
      type: Number,
      required: true,
    },
    isCpbc: {
      type: Boolean,
      default: false,
      required: false,
    },
    resetToggle: {
      type: Boolean,
      required: true,
    },
    selectToggle: {
      type: Boolean,
      required: true,
    },
    rectWidth: {
      type: String,
      required: true,
    },
  },
  setup(props, context) {
    const pushed = ref(false);

    const onClickBtn = () => {
      pushed.value = !pushed.value;
      context.emit('emit-pushed', props.clstIdx, pushed.value);
    };

    watch(
      () => props.resetToggle,
      () => {
        pushed.value = false;
      }
    );

    watch(
      () => props.selectToggle,
      () => {
        pushed.value = true;
      }
    );

    const underLineWidth = `${parseInt(props.rectWidth) * 0.8}px`;

    return { pushed, onClickBtn, underLineWidth };
  },
});
</script>

<style lang="scss" scoped>
.cluster {
  box-sizing: border-box;
  // width: 24px;
  height: 24px;
  border: solid 1px gray;
  border-radius: 5px;
  margin: 0 0px;
  text-align: center;
  line-height: 24px;
  font-size: 16px;
  background-color: #ffebcd;

  &.pushed {
    color: white;
    background-color: #eb6100;
    border-color: red;
  }

  &:hover {
    opacity: 0.7;
    cursor: pointer;
  }
}

.under-line {
  margin-left: 3px;
  height: 3px;
  background-color: darkblue;
}
</style>
