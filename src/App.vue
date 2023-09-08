<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <header>
    <div class="header">
      <router-link class="link" to="/">
        <h2 class="text-3xl font-bold underline">水彩</h2>
        <h2>suisai</h2>
      </router-link>
    </div>
  </header>

  <body>
    <!--<RouterView />-->
    <div class=" container mx-auto py-10">
      <div class="border m-6   bg-white mx-auto max-w-sm shadow-lg rounded-lg overflow-hidden">
        <div class="sm:flex sm:items-center px-6 py-4">
          <img class="block h-16 sm:h-24 rounded-full mx-auto mb-4 sm:mb-0 sm:mr-4 sm:ml-0" src="https://api.adorable.io/avatars/196/abott@adorable.png" alt="">
          <div class="text-center sm:text-left sm:flex-grow">
            <div class="mb-4">
              <p class="text-xl leading-tight">Jane Doe</p>
              <p class="text-sm leading-tight text-grey-dark">Software Developer at SpongeBob LLC.</p>
            </div>
            <div class="flex flex-wrap">
              <button class=" text-xs font-semibold rounded-full px-4 py-1 mx-3  leading-normal bg-white border border-blue text-blue hover:bg-blue hover:text-white">Call</button>
              <button class="  text-xs font-semibold rounded-full px-4 py-1 leading-normal bg-white border border-purple text-purple hover:bg-purple hover:text-white">Message</button>
            </div>
          </div>
        </div>
      </div>
    </div>
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
      font-size: 18px;
      width: 100%;
      display: flex;
      flex-direction: row;
      background-color: orange;
    }
  }

</style>
