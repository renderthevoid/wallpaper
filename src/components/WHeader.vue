<template>
  <header class="header" :class="props.isLoginPage ? 'header__fixed' : ''">
    <div class="header__container" :class="props.isLoginPage ? 'header__container-full-width' : ''">
      <RouterLink to="/">
        <div class="logo">
          <icon-main class="logo__icon"></icon-main>
          <div class="logo__text">
            <div class="logo__text-top">Wallone</div>
            <div class="logo__text-bottom">#Бесконечно..</div>
          </div>
        </div>
      </RouterLink>
      <template v-if="!isLoginPage">
        <div class="header__search">
          <w-input v-model="headerInputValue"></w-input>
          <div class="header__tags">
            <p class="header_tag">#Popular</p>
            <p class="header_tag">#Oldest</p>
            <p class="header_tag">#Oldestr</p>
          </div>
        </div>
        <div class="header__lang">
          <div class="header__lang-item">RU</div>
          <div class="header__lang-item">EN</div>
        </div>
        <div class="user">
          <icon-user class="user__icon"></icon-user>
          <div class="user__actions">
            <div class="user__actions-wrapper">
              <div class="user__actions-item">Войти</div>
              <div class="user__actions-item">Регистрация</div>
            </div>
          </div>
        </div>
      </template>
    </div>
  </header>
</template>

<script setup lang="ts">
import type { Ref } from 'vue'
import { ref } from 'vue'
import { RouterLink } from 'vue-router'
import WInput from './WInput.vue'
import IconMain from './icons/IconMain.vue'
import IconUser from './icons/IconUser.vue'

interface HeaderProps {
  isLoginPage: boolean
}

const props = defineProps<HeaderProps>()
const headerInputValue: Ref<string> = ref('')
</script>

<style scoped lang="scss">
@import "../assets/base.scss";
.header {
  &__fixed {
    position: fixed;
    z-index: 100;
    width: 100%;
  }
  &_tag {
  }

  &__container {
    @include flex(space-between, center, nowrap);
    max-width: 1440px;
    margin: 0 auto;
    padding: 0 162px;
    &-full-width {
      max-width: 1920px;
      padding: 38px 52px 0;
    }
  }

  &__search {
  }

  &__tags {
  }

  &__lang {
  }

  &__lang-item {
  }
}
.logo {
  @include flex(center, start, nowrap);
  gap: 16px;
  &__icon {
  }

  &__text {
  }

  &__text-top {
    font-family: 'Fredoka', sans-serif;
    font-size: 22px;
    font-style: normal;
    font-weight: 400;
    line-height: normal;
    letter-spacing: 0.44px;
  }

  &__text-bottom {
    text-decoration: none;
    font-size: 16px;
    font-style: normal;
    font-weight: 400;
    line-height: normal;
  }
}
.user {
  &__icon {
  }

  &__actions {
  }

  &__actions-wrapper {
  }

  &__actions-item {
  }
}
</style>
