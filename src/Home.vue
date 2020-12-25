<template>
  <div>
    <div style="height:100px">
      <UIButton
        @click="onClick"
        :xlarge="xlarge"
        :xsmall="xsmall"
        :small="small"
        :large="large"
        :disabled="disabled"
        :tile="tile"
        :rounded="rounded"
        :circle="circle"
        :color="color"
        >点我鸭</UIButton
      >
    </div>

    <div class="btn-group">
      <UIButton class="btn" @click="resize('xsmall')">超小</UIButton>
      <UIButton class="btn" @click="resize('small')">小</UIButton>
      <UIButton class="btn" @click="resize('normal')">正常</UIButton>
      <UIButton class="btn" @click="resize('large')">大</UIButton>
      <UIButton class="btn" @click="resize('xlarge')">超大</UIButton>
    </div>

    <div class="btn-group">
      <UIButton class="btn" @click="changeShape('tile')">矩形</UIButton>
      <UIButton class="btn" @click="changeShape('normal')">正常</UIButton>
      <UIButton class="btn" @click="changeShape('rounded')">半圆</UIButton>
      <UIButton class="btn" @click="changeShape('circle')">圆</UIButton>
    </div>

    <div class="btn-group">
      <UIButton class="btn" @click="changeDisabled">禁用</UIButton>
    </div>

    <div class="btn-group">
      <UIButton class="btn" @click="changeColor('#F56C6C')">Danger色</UIButton>
      <UIButton class="btn" @click="changeColor('#67C23A')">Success色</UIButton>
    </div>
  </div>
</template>
<script lang="ts">
import { Vue, Component } from "vue-property-decorator";
import UIButton from "@/components/uikit/UIButton.vue";

@Component({
  components: {
    UIButton,
  },
})
export default class Home extends Vue {
  // 颜色
  private color = "";
  // 大小
  private xsmall = false;
  private small = false;
  private large = false;
  private xlarge = false;

  // 形状
  private tile = false;
  private rounded = false;
  private circle = false;

  // 禁用
  private disabled = false;

  // 改变颜色
  private changeColor(color: string) {
    this.color = color;
  }

  // 改变禁用状态
  private changeDisabled() {
    this.disabled = !this.disabled;
  }

  // 改变形状
  private changeShape(shape: string) {
    switch (shape) {
      case "tile":
        this.tile = true;
        this.rounded = false;
        this.circle = false;
        break;
      case "rounded":
        this.tile = false;
        this.rounded = true;
        this.circle = false;
        break;
      case "circle":
        this.tile = false;
        this.rounded = false;
        this.circle = true;
        break;
      case "normal":
        this.tile = false;
        this.rounded = false;
        this.circle = false;
        break;
    }
  }

  // 改变大小
  private resize(size: string) {
    switch (size) {
      case "xsmall":
        this.xsmall = true;
        this.small = false;
        this.large = false;
        this.xlarge = false;
        break;
      case "small":
        this.xsmall = false;
        this.small = true;
        this.large = false;
        this.xlarge = false;
        break;
      case "large":
        this.xsmall = false;
        this.small = false;
        this.large = true;
        this.xlarge = false;
        break;
      case "xlarge":
        this.xsmall = false;
        this.small = false;
        this.large = false;
        this.xlarge = true;
        break;
      case "normal":
        this.xsmall = false;
        this.small = false;
        this.large = false;
        this.xlarge = false;
        break;
    }
  }

  private onClick(event: MouseEvent) {
    console.log(event);
  }
}
</script>
<style sopend lang="stylus">
.btn-group
    display flex
    justify-content center
    align-items left

.btn
    margin 6px
</style>
