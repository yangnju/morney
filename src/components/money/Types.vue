<template>
  <div>
    <ul class="types">
<!--      如果type是-，增加selected，点击后改变type的值-->
      <li :class="type === '-' && 'selected'" @click="selectType('-')">支出</li>
      <li :class="type === '+' && 'selected'" @click="selectType('+')">收入</li>
    </ul>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
// 告诉vue export里面的内容是组件,vue-class-component包含装饰器，是一个第三方的，比官方好用，具体用法可以看vue-class-component 或 官方装饰器文档。
import Component from "vue-class-component";

@Component
export  default class Types extends Vue {
  type = '-'
  // ts中是不允许出现any类型的参数的
  selectType(type: string) {
    if(type !== '-' && type !== '+') {
      throw new Error('type is unknown')
    }
    this.type = type
  }
}
/*export default {
  name: "Types",
  data(){
    return{
      type:'-'
    }
  },
  methods:{
    selectType(type) {
      if(type !== '-' && type !== '+') {
        throw new Error('type is unknown')
      }
      this.type = type
    }
  }
}*/
</script>

<style lang="scss" scoped>
@import "~@/assets/style/helper.scss";

.types {
  background: #c4c4c4;
  display: flex;
  text-align: center;
  font-size: 24px;

  > li {
    width: 50%;
    height: 64px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;

    &.selected::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      height: 4px;
      background: #333;
    }
  }
}
</style>