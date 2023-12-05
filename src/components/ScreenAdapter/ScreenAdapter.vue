<template>
  <div class="screen-adapter" :style="style">
    <slot></slot>
  </div>
</template>
<script lang="ts">
  import { defineComponent, toRefs, onMounted, onUnmounted, ref, computed } from 'vue';
  import { debounceFn } from '@/utils/utils';
  export default defineComponent({
    name: 'ScreenAdapter',
    props: {
      width: {
        type: String,
        default: '1920',
      },
      height: {
        type: String,
        default: '960',
      },
    },
    setup(props) {
      const { width, height } = toRefs(props);
      const scaleRatio = ref(1);
      const style = computed(() => {
        return {
          width: width.value + 'px',
          height: height.value + 'px',
          transform: `scale(${scaleRatio.value}) translate(-50%, -50%)`,
        };
      });
      // 获取放大缩小比例 以小的为准
      const getScaleRatio = () => {
        const w = window.innerWidth / +width.value;
        const h = window.innerHeight / +height.value;
        scaleRatio.value = w < h ? w : h;
      };
      onMounted(() => {
        getScaleRatio();
        window.onresize = debounceFn(getScaleRatio);
      });
      onUnmounted(() => {
        window.onresize = null;
      });
      return {
        style,
      };
    },
  });
</script>
<style lang="scss" scoped>
  .screen-adapter {
    position: absolute;
    top: 50%;
    left: 50%;
    opacity: 1;
    transform: translate(-50%, -50%);
    transition: 0.3s;
    transform-origin: 0 0; // 变化中心改为左上角 默认是center
  }
</style>
