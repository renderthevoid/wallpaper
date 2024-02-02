<script lang="ts" setup>
interface ITabsProps {
  names: []
  selectedTab: string
}

defineProps<ITabsProps>()

const emit = defineEmits(['changeTab'])

const clickOnTab = (tabName: string) => {
  emit('changeTab', tabName)
}
</script>

<template>
  <div class="tabs">
    <div
      class="tab"
      v-for="tab in names"
      :key="tab['name']"
      :class="['tab-nav__item', { selected: tab['name'] === selectedTab }]"
      @click="clickOnTab(tab['name'])"
    >
      {{ tab['label'] }}
    </div>
  </div>
  <div class="tabs__content">
    <slot />
  </div>
</template>
<style scoped lang="scss">
@import '../assets/base.scss';
.tabs {
  gap: 24px;
  @include flex(start, center, nowrap);

  &__content {
    width: 100%;
  }
  .selected {
    color: $text_color;
    border-bottom: 2px solid $btn_primary;
  }
}

.tab {
  padding: 0 0 6px;
  font-weight: 400;
  font-size: 36px;
  color: $text_color_secondary;
  cursor: pointer;
}
</style>
