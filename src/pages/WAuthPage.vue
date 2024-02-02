<template>
  <!-- <label for="">{{ text }}</label>
  <w-input v-model="text"></w-input> -->
  <div class="login-page">
    <div class="login-page__wrapper">
      <div class="login-page__left">
        <img src="../assets/image.png" alt="" class="login-page__image" />
      </div>
      <div class="login-page__right">
        <w-tabs :names="tabs" :selectedTab="selectedTab" @changeTab="changeTab">
          <form class="form" v-if="selectedTab === 'auth'">
            <w-input v-model="loginValues.email" label="Email или логин"></w-input>
            <w-input v-model="loginValues.password" label="Пароль"></w-input>
            <input type="checkbox" id="remember" name="Запомнить меня" />
            <label for="remember">Запомнить меня</label>
            <div class="form__buttons">
              <button type="button">Войти</button>
            </div>
          </form>
          <div v-if="selectedTab === 'sign'">
            <div>хай</div>
          </div>
        </w-tabs>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import WInput from '@/components/WInput.vue'
import WTabs from '@/components/WTabs.vue'
import { ref } from 'vue'

interface IAuth {
  email: string
  password: string
}
interface ITabs {
  name: string
  label: string
}
const tabs: ITabs[] = [
  { label: 'Авторизация', name: 'auth' },
  { label: 'Регистрация', name: 'sign' }
]
const selectedTab = ref('auth')

const changeTab = (tabName: string) => {
  selectedTab.value = tabName
}
const loginValues = ref<IAuth>({
  email: '',
  password: ''
})
</script>

<style scoped lang="scss">
@import '../assets/base.scss';
.login-page {
  height: 100%;
  overflow: hidden;
  &__wrapper {
    padding-right: 104px;
    gap: 104px;
    max-width: 1920px;
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
  @include flex(center, center, nowrap);
  @include flex_direction_column;
  &__buttons {
  }
}
</style>
