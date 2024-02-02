<template>
  <div class="checkbox">
    <input
      type="checkbox"
      :id="props.id"
      :name="props.label"
      @change="changeCheckbox"
      :value="props.modelValue"
      v-bind="$attrs"
      class="checkbox__picker"
    />
    <label for="remember" class="checkbox__label">{{ props.label }}</label>
  </div>
</template>

<script setup lang="ts">
interface ICheckboxProps {
  modelValue: boolean
  label?: string
  id?: string
}
const emit = defineEmits(['update:modelValue'])

const changeCheckbox = (event: Event) => {
  emit('update:modelValue', (event.target as HTMLInputElement).checked)
}
const props = defineProps<ICheckboxProps>()
</script>

<style scoped lang="scss">
@import '../assets/base.scss';
.checkbox {
  width: 187px;
  @include flex(end, center, nowrap);
  &__picker {
    position: relative;
    opacity: 0;
    z-index: -1;
  }
  &__label {
    position: relative;
    display: inline-block;
    font-weight: 400;
    font-size: 20px;
  }
  &__picker[type='checkbox'] + &__label::after {
    content: '';
    position: absolute;
    top: 0;
    left: -30px;
    z-index: 1;
    background-color: $bg_color;
    width: 22px;
    height: 22px;
    border: 1px solid $text_color;
    @include border_radius_5;
    cursor: pointer;
  }
  &__picker[type='checkbox']:checked + &__label::after {
    background: url('../assets/checkbox.svg');
    background-color: $bg_color;
    background-repeat: no-repeat;
    background-position: 50% center;
    background-size: 70% 70%;
  }
}
</style>
