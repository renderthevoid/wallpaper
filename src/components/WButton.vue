<template>
  <button type="button" class="btn" :class="classList" :disabled="disabled">
    <span class="btn__wrapper" :style="{ justifyContent: center ? 'center' : '' }">
      <a class="btn__href" v-if="addHref" :href="addHref" target="_blank"></a>
      <template v-if="before.length && !before.includes('.svg')">
        <span class="btn__before" v-html="before"> </span>
      </template>
      <template v-else-if="before.length && before.includes('.svg' || '.png')">
        <img :src="before" alt="icon" class="btn__before" />
      </template>
      <span class="btn__text">
        <slot></slot>
      </span>
      <span class="btn__after" v-if="after.length" v-html="after"></span>
    </span>
  </button>
</template>

<script setup lang="ts">
import { ref } from 'vue'

interface IButtonProps {
  view: string
  mode?: string
  buttonType?: string
  before?: string
  after?: string
  addHref?: string
  disabled?: boolean
  center?: boolean
  stretch?: boolean
  interactive?: boolean
}
const props = withDefaults(defineProps<IButtonProps>(), {
  buttonType: 'button',
  mode: '',
  before: '',
  after: '',
  addHref: '',
  disabled: false,
  center: false,
  stretch: false,
  interactive: false
})
const emit = defineEmits(['click'])
const classList = ref([
  props.view,
  props.addHref ? 'link' : '',
  props.disabled ? 'disabled' : '',
  props.interactive ? 'interactive' : '',
  props.before && props.after && !props.stretch ? 'icons-mode' : '',
  props.before && !props.after && !props.stretch ? 'icon-mode' : '',
  props.after && !props.before && !props.stretch ? 'icon-mode' : '',
  props.mode.length ? `${props.view}-${props.mode}` : '',
  props.stretch ? 'btn-stretch' : ''
])
</script>

<style lang="less" scoped>
@import url('@/assets/base.less');
.btn {
  display: inline-block;
  padding: 0;
  font-size: 13px;
  font-style: normal;
  font-weight: 400;
  line-height: 20px;
  min-height: @ui_btn_height;
  min-width: @ui_btn_width;
  cursor: pointer;
  .border_radius_4;

  &-stretch {
    width: 100%;
    .btn__wrapper {
      justify-content: center;
      gap: 8px;
    }
  }
  &.link {
    position: relative;
  }
  &.disabled {
    opacity: 0.6;
  }
  &.interactive {
    transition: 0.3s ease-in-out;
  }
  &.positive {
    color: @white;
    &-primary {
      background-color: @ui_btn_positive_green;
      border: 1px solid @ui_btn_positive_green;
      &:not([disabled]):hover {
        background-color: @ui_btn_positive_green_hover;
      }
    }
    &-secondary {
      background-color: @ui_btn_positive_orange;
      border: 1px solid @ui_btn_positive_orange;
      &:not([disabled]):hover {
        background-color: @ui_btn_positive_orange_hover;
      }
    }
  }
  &.accent {
    background-color: @ui_btn_accent;
    color: @text_color;
    &-primary {
      border: 1px solid @ui_btn_accent_border_primary;
    }
    &-secondary {
      border: 1px solid @ui_btn_accent_border_secondary;
    }
    &:not([disabled]):hover {
      background-color: @ui_btn_accent_hover;
    }
  }
  &.variable {
    background-color: @ui_btn_variable;
    color: @white;
    border: 1px solid @ui_btn_variable;
    &:not([disabled]):hover {
      background-color: @ui_btn_variable_hover;
    }
  }
  &.negative {
    background-color: @ui_btn_negative;
    color: @white;
    border: 1px solid @ui_btn_negative;
    &:not([disabled]):hover {
      background-color: @ui_btn_negative_hover;
    }
  }

  &__wrapper {
    display: flex;
    align-items: center;
    justify-content: space-around;
    height: 100%;
    padding: 0 16px;
  }
  &.icons-mode {
    min-width: @ui_btn_with_icons_width;
  }
  &.icon-mode {
    min-width: @ui_btn_with_icon_width;
    .btn__wrapper {
      gap: 8px;
    }
  }
  &-before,
  &-after {
    width: @ui_btn_svg_size;
    height: @ui_btn_svg_size;
    svg {
      width: @ui_btn_svg_size;
      height: @ui_btn_svg_size;
    }
  }
  img.btn__before,
  img.btn__before {
    width: @ui_btn_svg_size;
    height: @ui_btn_svg_size;
  }
  &__href {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    .border_radius_4;
  }
}
</style>
