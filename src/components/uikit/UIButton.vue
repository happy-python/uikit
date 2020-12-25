<template>
  <div>
    <button
      class="ui-btn"
      :class="{
        'ui-btn-large': large,
        'ui-btn-xlarge': xlarge,
        'ui-btn-small': small,
        'ui-btn-xsmall': xsmall,
        'ui-btn-tile': tile,
        'ui-btn-rounded': rounded,
        'ui-btn-circle': circle,
        'ui-btn-disabled': disabled,
      }"
      :style="`--color-tint:${TintColor}`"
      @click="onClick"
    >
      <slot>Button</slot>
    </button>
  </div>
</template>
<script lang="ts">
import { Vue, Component, Emit, Prop } from "vue-property-decorator";

@Component
export default class UIButton extends Vue {
  // 如果父组件传递了此属性，则值为true，否则为false
  @Prop(Boolean) private xlarge: boolean | undefined;
  @Prop(Boolean) private large: boolean | undefined;
  @Prop(Boolean) private xsmall: boolean | undefined;
  @Prop(Boolean) private small: boolean | undefined;
  @Prop(Boolean) private tile: boolean | undefined;
  @Prop(Boolean) private rounded: boolean | undefined;
  @Prop(Boolean) private circle: boolean | undefined;
  @Prop(Boolean) private disabled: boolean | undefined;
  @Prop(String) private color: string | undefined;

  // 计算属性
  public get TintColor(): string {
    // 没有给默认值
    return this.color ? this.color : "#2d8cf0";
  }

  @Emit("click") private btnClickEvent(event: MouseEvent) {}

  private onClick(event: MouseEvent) {
    if (!this.disabled) {
      this.btnClickEvent(event);
    }
  }
}
</script>
<style scoped lang="stylus">
resize(min-width, height, paddingLR, font-size)
    min-width width
    height height
    padding 0 paddingLR
    font-size font-size
    &.ui-btn-rounded,&.ui-btn-circle
        // 半径为高度的一半
        border-radius (@height / 2)
    &.ui-btn-circle
        // 宽度的值等于高度
        width @height
        min-width 0
        padding 0

.ui-btn
    resize(64px, 36px, 16px, 0.875rem)
    border 0 solid black
    border-radius 4px
    outline none
    font-weight 500
    letter-spacing 0.09em
    // 读取变量
    background-color var(--color-tint)
    color #17233D
    cursor pointer
    // 无法选中按钮内文本
    user-select none
    &:hover
        // 滤镜 值超过100%，图像会比原来更亮，否则会比原来更暗
        filter brightness(120%)
    &:active
        filter brightness(80%)

    &.ui-btn-large
        resize(78px, 44px, 19px, 0.875rem)

    &.ui-btn-xlarge
        resize(92px, 52px, 23px, 1rem)

    &.ui-btn-small
        resize(50px, 28px, 12px, 0.75rem)

    &.ui-btn-xsmall
        resize(36px, 20px, 9px, 0.625rem)

    // 矩形
    &.ui-btn-tile
        border-radius 0

    &.ui-btn-disabled
        background-color #f5f5f5
        color #c5c8ce
        cursor not-allowed
</style>
