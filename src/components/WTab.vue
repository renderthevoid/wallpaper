<template>
  <div class="tab" :class="{ selected: props.name === props.selected }">
    {{ props.name }}
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

interface ITab {
  name: string
  selected: string
}

let activeTab = ref(0)
const emit = defineEmits(['changeTab'])
const clickOnTab = (tabName: string) => {
  emit('changeTab', tabName)
}
const props = defineProps<ITab>()
</script>
<style scoped lang="scss">
.tab {
  font-weight: 400;
  font-size: 36px;
}
.tab__active {
  border-bottom: 1px solid blue;
}
</style>
