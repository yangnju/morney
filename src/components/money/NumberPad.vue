<template>
  <div class="numberPad">
    <div class="output">{{ output }}</div>
    <div class="buttons">
      <!--inputContent可以不传参数，是因为vue会自动传给函数一个event事件-->
      <button @click="inputContent">1</button>
      <button @click="inputContent">2</button>
      <button @click="inputContent">3</button>
      <button @click="remove">删除</button>
      <button @click="inputContent">4</button>
      <button @click="inputContent">5</button>
      <button @click="inputContent">6</button>
      <button @click="clear">清空</button>
      <button @click="inputContent">7</button>
      <button @click="inputContent">8</button>
      <button @click="inputContent">9</button>
      <button @click="ok" class="ok">OK</button>
      <button @click="inputContent" class="zero">0</button>
      <button @click="inputContent">.</button>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import {Component} from 'vue-property-decorator';

@Component
export default class NumberPad extends Vue {
  // 因为'0'就是字符串，所以不需要在output后面再加 : string
  output = '0';

  // 使用vue自动传递的event事件，事件类型要根据mdn来，自己查
  inputContent(event: MouseEvent) {
    // target可能有很多种，所以会因为情况没有写全而报错，as HTMLButtonElement 作用是强制规定是button，避免报错
    const button = (event.target as HTMLButtonElement);

    // !表示的是不为空（null、undefined)，在这里相当于 as string
    const input = button.textContent as string;

    // 超过16位就不再增加数字
    if (this.output.length === 16) {
      return;
    }

    if (this.output === '0') {
      // 如果input的值是0123456789
      if ('0123456789'.indexOf(input) >= 0) {
        this.output = input;
      } else {
        // 否则就加在后面
        this.output += input;
      }
      return;
    }

    // 如果input中有了'.'  或者就是 '.'
    if (this.output.indexOf('.') >= 0 && input === '.') {
      return;
    }
    this.output += input;
  }

  remove() {
    // 如果只有一位，点击删除直接显示0
    if (this.output.length === 1) {
      this.output = '0';
    } else {
      // 否则删除末尾一位
      this.output = this.output.slice(0, -1);
    }
  }

  clear() {
    this.output = '0';
  }

  ok() {
    this.$emit('update:value', this.output);
    this.$emit('submit', this.output);
  }

}

</script>

<style lang="scss" scoped>
@import "~@/assets/style/helper.scss";

.numberPad {
  .output {
    @extend %clearFix;
    @extend %innerShadow;
    font-size: 36px;
    font-family: Consolas, monospace;
    padding: 9px 16px;
    text-align: right;
  }

  .buttons {
    @extend %clearFix;

    > button {
      width: 25%;
      height: 64px;
      float: left;
      background: transparent;
      border: none;

      &.ok {
        height: 64*2px;
        float: right;
      }

      &.zero {
        width: 25*2%;
      }

      $bg: #f2f2f2;

      &:nth-child(1) {
        background: $bg;
      }

      &:nth-child(2), &:nth-child(5) {
        background: darken($bg, 4%);
      }

      &:nth-child(3), &:nth-child(6), &:nth-child(9) {
        background: darken($bg, 4*2%);
      }

      &:nth-child(4), &:nth-child(7), &:nth-child(10) {
        background: darken($bg, 4*3%);
      }

      &:nth-child(8), &:nth-child(11), &:nth-child(13) {
        background: darken($bg, 4*4%);
      }

      &:nth-child(14) {
        background: darken($bg, 4*5%);
      }

      &:nth-child(12) {
        background: darken($bg, 4*6%);
      }
    }
  }
}
</style>