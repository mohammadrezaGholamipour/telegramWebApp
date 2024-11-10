<template>
  <div>
    <h1>Welcome to Telegram Mini App</h1>
    <p v-if="user">Hello, {{ user.first_name }}</p>
    <button @click="sendData">Send Data to Telegram</button>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const user = ref(null);

onMounted(() => {
  if (window.Telegram && window.Telegram.WebApp) {
    // مقداردهی اولیه API تلگرام
    window.Telegram.WebApp.ready();
    // گرفتن اطلاعات کاربر
    user.value = window.Telegram.WebApp.initDataUnsafe.user;
  }
});

const sendData = () => {
  // ارسال داده به تلگرام
  if (window.Telegram && window.Telegram.WebApp) {
    window.Telegram.WebApp.sendData("Hello from Vue 3!");
  }
};
</script>
