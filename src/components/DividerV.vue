<template>
  <div class="devider" :style="{ left: posX_str }"></div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'DivederV',
  props: {
    posX: {
      type: Number,
      required: true,
    },
  },
  setup(props) {
    // widthの半分を引く
    const posX_str = `${props.posX - 1}px`;

    return { posX_str };
  },
});
</script>

<style lang="scss" scoped>
.devider {
  position: absolute;
  top: 20px;

  width: 2px;
  height: 60px;
  background-color: gray;

  // CPBCクラスタで線上でボタンをクリックさせるため
  pointer-events: none;
}
</style>
