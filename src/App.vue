<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header class="bg-lime-600">
    <div class="header">
      <router-link class="link" to="/">
        <h2 class="text-3xl text-lime-100">水彩</h2>
        <h2 class="text-3xl text-stone-200">suisai</h2>
      </router-link>
    </div>
  </header>

  <body>
    <RouterView />
  </body>
</template>



<style scoped lang="scss">

  .link {
    display: flex;
    flex-direction: row;

    h2 {
      margin: 0 3px;
    }

  }

  header{
    width: 100%;

    div {
      padding: 4px;
      font-size: 18px;
      width: 100%;
      display: flex;
      flex-direction: row;
    }
  }

</style>
