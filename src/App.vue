<script setup lang="ts">
import { ref, watch } from 'vue'
import { RouterLink, RouterView } from 'vue-router'
import WHeader from './components/WHeader.vue'

const isLoginPage = ref(false)
</script>

<template>
  <w-header :isLoginPage="isLoginPage"></w-header>
  <nav v-if="!isLoginPage">
    <RouterLink to="/" @click="isLoginPage = false">Home</RouterLink>
    <RouterLink to="/auth" @click="isLoginPage = true">Login</RouterLink>
  </nav>

  <RouterView />
</template>

<style scoped></style>
