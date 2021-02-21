<template>
  <div class="layout-wrapper" :class="classPrefix && `${classPrefix}-wrapper`">
    <div class="content" :class="classPrefix && `${classPrefix}-content`   ">
      <slot></slot>
    </div>
    <Nav/>
  </div>
</template>

<script lang="ts">
export default {
  props: ['classPrefix'],
  name: 'Layout'
};
</script>

<style lang="scss" scoped>
.layout-wrapper {
  display: flex;
  //纵向排列
  flex-direction: column;
  //容器只能有一个屏幕的高度
  height: 100vh;
}

.content {
  //让内容可以滚动，不然高度还是很高，不是一屏
  overflow: auto;
  //尽量把所有的高度都给content，nav占剩下的,这是flex的优势，一下就占满了，很方便
  flex-grow: 1;
}
</style>