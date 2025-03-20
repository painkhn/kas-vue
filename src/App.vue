<script setup lang="ts">
import Layout from '@/layouts/MainLayout.vue';
import { ref } from 'vue';
import HomeGuest from '@/Pages/Home/HomeGuest.vue';
import HomeAuth from '@/Pages/Home/HomeAuth.vue';
const user = ref(null);

// Пример функции для аутентификации (замените на вашу логику)
const authenticateUser = async () => {
    // Здесь может быть запрос к API для аутентификации
    const response = await fetch('/api/auth/user');
    const data = await response.json();
    user.value = data.user;
};

// Вызов функции аутентификации при загрузке компонента
authenticateUser();
</script>

<template>

  <Layout>
    <HomeGuest v-if="!user" />
    <HomeAuth v-if="user" />
  </Layout>
</template>

<style scoped>
.h-main {
  height: calc(100vh - 150px);
}
</style>
