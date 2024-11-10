<template>
  <div>
    <h1>Welcome to Telegram Mini App</h1>
    <p v-if="user">Hello, {{ user.first_name }}</p>
    <button @click="sendData">Send Data to Telegram</button>
  </div>
</template>

<script setup>
import { onMounted } from 'vue';

onMounted(() => {
  if (window.Telegram && window.Telegram.WebApp) {
    // مقداردهی اولیه WebApp API
    window.Telegram.WebApp.ready();
    console.log("Telegram WebApp API initialized.");
  } else {
    console.error("Telegram WebApp API not available.");
  }
});
</script>

