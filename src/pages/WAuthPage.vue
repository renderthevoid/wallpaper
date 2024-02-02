<template>
  <!-- <label for="">{{ text }}</label>
  <w-input v-model="text"></w-input> -->
  <div class="login-page">
    <div class="login-page__wrapper">
      <div class="login-page__left">
        <img src="../assets/image.png" alt="" class="login-page__image" />
      </div>
      <div class="login-page__right">
        <w-tabs :names="tabs" :selectedTab="selectedTab" @change-tab="changeTab">
          <form class="form" v-if="selectedTab === 'auth'">
            <div class="form__inputs">
              <w-input v-model="loginValues.email" label="Email или логин">
                <p>{{ loginValues.email }}</p>
              </w-input>
              <w-input v-model="loginValues.password" label="Пароль">
                <p>{{ loginValues.password }}</p></w-input
              >
            </div>
            <div class="form__bottom">
              <w-checkbox label="Запомнить меня" id="remember" v-model="checkbox"></w-checkbox>
              <div class="form__actions">
                <w-button view="primary">Войти</w-button>
              </div>
            </div>
          </form>
          <div v-if="selectedTab === 'sign'"></div>
        </w-tabs>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import WCheckbox from '@/components/WCheckbox.vue'
import WInput from '@/components/WInput.vue'
import WTabs from '@/components/WTabs.vue'
import WButton from '@/components/WButton.vue'
import { ref } from 'vue'

interface IAuth {
  email: string
  password: string
}
interface ITabs {
  name: string
  label: string
}
const loginValues = ref<IAuth>({
  email: '',
  password: ''
})
const checkbox = ref(false)
const tabs: ITabs[] = [
  { label: 'Авторизация', name: 'auth' },
  { label: 'Регистрация', name: 'sign' }
]
const selectedTab = ref('auth')
const changeTab = (tabName: string) => {
  selectedTab.value = tabName
}
</script>

<style scoped lang="scss">
@import '../assets/base.scss';
.login-page {
  max-height: 100vh;
  overflow: hidden;
  @include flex(center, start, nowrap);
  width: 100%;
  &__wrapper {
    padding-right: 104px;
    gap: 104px;
    max-width: 1920px;
    width: 100%;
    height: 100%;
    overflow: hidden;
    @include flex(space-between, center, nowrap);
  }

  &__left {
    width: 789px;
    overflow: hidden;
  }

  &__image {
    object-fit: none;
    transition: 0.3s ease-in-out;
    &:hover {
      transform: scale(1.1);
    }
  }

  &__right {
    width: calc(100% - 789px);
    gap: 33px;
    @include flex(center, start, nowrap);
    @include flex_direction_column;
  }
}
.form {
  width: 100%;
  @include flex(center, start, nowrap);
  @include flex_direction_column;
  &__inputs {
    width: 100%;
    margin: 0 0 44px;
  }
  &__bottom {
    gap: 24px;
    @include flex(start, start, nowrap);
    @include flex_direction_column;
  }
  &__actions {
  }
}
</style>
