<template>
  <div>
    <h1>Welcome to Telegram Mini App</h1>
    <p v-if="user">Hello, {{ user.first_name }}</p>
    <button v-if="isTelegramAvailable" @click="sendData">Send Data to Telegram</button>
    <p v-else>Telegram WebApp API is not available.</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const user = ref(null);
const isTelegramAvailable = ref(false);

onMounted(() => {
  // بررسی اینکه API تلگرام در دسترس است
  if (window.Telegram && window.Telegram.WebApp) {
    // مقداردهی اولیه Telegram WebApp API
    window.Telegram.WebApp.ready();
    isTelegramAvailable.value = true;
    user.value = window.Telegram.WebApp.initDataUnsafe.user;
    console.log("Telegram WebApp API initialized. User data:", user.value);
  } else {
    console.error("Telegram WebApp API not available.");
  }
});

// تابعی برای ارسال داده به تلگرام
const sendData = () => {
  if (window.Telegram && window.Telegram.WebApp) {
    window.Telegram.WebApp.sendData("Hello from Vue 3!");
  }
};
</script>

<style>
/* استایل‌های اختیاری */
</style>
