<template>
  <div>
    <el-button type="primary" @click="onClickClearBtn">Reset</el-button>
    <el-button type="primary" @click="onClickAllSelectBtn">All Select</el-button>
    <div class="clusters-wrapeer" :style="{ 'min-width': clustersMinWidth }">
      <div class="pg-wrapper">
        <div class="pg-type lo-page" :style="{ width: pgRectWidth }">Lowera</div>
        <div class="pg-type mid-page" :style="{ width: pgRectWidth }">Middle</div>
        <div class="pg-type upper-page" :style="{ width: pgRectWidth }">Upper</div>
      </div>

      <div class="pl-wrapper-top">
        <div class="pl-wrapper">
          <div v-for="n in 4" :key="n" class="pl lo-page" :style="{ width: plRectWidth }">
            PL{{ n - 1 }}
          </div>
        </div>
        <div class="pl-wrapper">
          <div v-for="n in 4" :key="n" class="pl mid-page" :style="{ width: plRectWidth }">
            PL{{ n - 1 }}
          </div>
        </div>
        <div class="pl-wrapper">
          <div v-for="n in 4" :key="n" class="pl upper-page" :style="{ width: plRectWidth }">
            PL{{ n - 1 }}
          </div>
        </div>
      </div>
      <div class="el-container">
        <ClstElementV
          v-for="(n, i) in clustTotalNum"
          :key="i"
          :clstIdx="i"
          :isCpbc="i === 7"
          :resetToggle="resetToggle"
          :selectToggle="allSelToggle"
          :rectWidth="clstWidth"
          @emit-pushed="onEmitPushed"
        />
      </div>
      <DivederV v-for="n in 11" :key="n" :posX="n * CLST_STD_WIDTH * 4" />
    </div>

    {{ clstList }}
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, Ref, computed } from 'vue';
import ClstElementV from '@/components/ClstElementV.vue';
import DivederV from '@/components/DividerV.vue';

export default defineComponent({
  name: 'ClustersV',
  components: { ClstElementV, DivederV },
  props: {
    clustTotalNum: {
      type: Number,
      required: true,
    },
  },
  setup(props) {
    const CLST_STD_WIDTH = 28; //C48の1clstのサイズ 描画のXサイズはこの値に連動する
    const resetToggle = ref(false);
    const allSelToggle = ref(false);
    const clstList: Ref<number[]> = ref([]);

    const onClickClearBtn = () => {
      resetToggle.value = !resetToggle.value;
      clstList.value.length = 0;
    };

    const onEmitPushed = (clstNo: number, pushed: boolean) => {
      console.log(`onEmitPushed ${clstNo}`);
      if (pushed) {
        clstList.value.push(clstNo);
      } else {
        clstList.value = clstList.value.filter((n) => n !== clstNo);
      }
    };

    const onClickAllSelectBtn = () => {
      allSelToggle.value = !allSelToggle.value;
      clstList.value = [];
      for (let i = 0; i < props.clustTotalNum; i++) {
        clstList.value.push(i);
      }
    };

    const clstWidth = computed(() => {
      return `${(48.0 / props.clustTotalNum) * CLST_STD_WIDTH}px`;
    });

    const plRectWidth = `${CLST_STD_WIDTH * 4}px`;
    const pgRectWidth = `${CLST_STD_WIDTH * 4 * 4}px`;
    const clustersMinWidth = `${CLST_STD_WIDTH * 48 + 10}px`;

    return {
      onClickClearBtn,
      resetToggle,
      allSelToggle,
      onEmitPushed,
      clstList,
      onClickAllSelectBtn,
      clstWidth,
      plRectWidth,
      pgRectWidth,
      clustersMinWidth,
      CLST_STD_WIDTH,
    };
  },
});
</script>

<style lang="scss" scoped>
.clusters-wrapeer {
  position: relative;
  // background-color: yellow;
  margin: 20px 20px;

  .el-container {
    display: flex;
    margin-top: 4px;
  }
}

.pg-wrapper {
  display: flex;
  .pg-type {
    text-align: center;
    box-sizing: border-box;
    font-size: 15px;
    line-height: 20px;
    // width: 480px;
    height: 20px;
    border: solid 1px gray;
    &.lo-page {
      background-color: #a1e8ff;
    }
    &.mid-page {
      background-color: #dda0dd;
    }

    &.upper-page {
      background-color: lightgreen;
    }
  }
}

.pl-wrapper-top {
  display: flex;

  .pl-wrapper {
    display: flex;
    .pl {
      text-align: center;
      font-size: 15px;
      line-height: 20px;
      box-sizing: border-box;
      // width: 120px;
      height: 20px;
      border: solid 1px gray;

      &.lo-page {
        background-color: #a1e8ff;
      }

      &.mid-page {
        background-color: #dda0dd;
      }

      &.upper-page {
        background-color: lightgreen;
      }
      // background-color: skyblue;
    }
  }
}
</style>
