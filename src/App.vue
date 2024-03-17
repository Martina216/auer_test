<script setup>
import { RouterLink, RouterView } from 'vue-router';
import { onMounted } from 'vue';
import chatBot from './components/ChatBot.vue';

  // 執行於元件被掛載後
  onMounted(() => {
    console.log('Component mounted');
  });

  
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
      <nav>
        <RouterLink to="/chart">圖表</RouterLink>
        <RouterLink to="/forms">報表</RouterLink>
      </nav>
    </div>
  </header>
  <chatBot/>

  <RouterView />
</template>