<script setup lang="ts">
import LoginForm from "@/components/LoginForm.vue";
import SignupForm from "@/components/SignupForm.vue";

import {useRoute, useRouter} from 'vue-router'
const location = useRoute();

if (localStorage.getItem('authToken') != null) useRouter().push('/dashboard');

</script>

<template>
  <main>
    <div class="w-full md:w-auto">
      <signup-form v-if="location.path == '/signup'"/>
      <login-form v-if="location.path == '/login'"/>
    </div>

  </main>
</template>
