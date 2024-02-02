<template>
  <div class="input-wrapper">
    <label :for="props.label" class="label">{{ props.label }}</label>
    <input
      type="text"
      :id="props.label"
      class="input"
      :value="props.modelValue"
      @input="updateInput"
      v-bind="$attrs"
      placeholder="Enter your text"
    />
    <div class="input-warn">ыыыы</div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

interface Props {
  modelValue: string
  label?: string
  name?: string
}
const props = defineProps<Props>()
const emit = defineEmits(['update:modelValue'])
const updateInput = (event: Event) => {
  emit('update:modelValue', (event.target as HTMLInputElement).value)
}
const computeWarn = computed(() => {
  return !props.modelValue.length
})

</script>

<style scoped lang="scss">
@import '../assets/base.scss';
.input {
  padding: 10px 14px 9px;
  background-color: $component_color;
  outline: none;
  border: 1px solid transparent;
  color: $text_color_secondary;
  font-weight: 400;
  width: 100%;
  font-size: 16px;
  @include border_radius_10;
  &:focus {
    border: 1px solid $btn_primary;
  }
}
.input-wrapper {
  width: 100%;
}
.label {
  margin: 8px 0;
  font-weight: 400;
  font-size: 24px;
}
</style>
