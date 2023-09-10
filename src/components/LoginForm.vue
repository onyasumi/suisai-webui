<script setup lang="ts">
</script>

<template>
  <div class="flex min-h-full flex-col justify-center px-6 py-12 lg:px-8">
    <div class="sm:mx-auto sm:w-full sm:max-w-sm">
      <h2 class="mt-10 text-center text-2xl font-bold leading-9 tracking-tight text-gray-900">Sign in to your account</h2>
    </div>

    <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
      <form class="space-y-6" action="#" method="POST">
        <div>
          <label for="email" class="block text-sm font-medium leading-6 text-gray-900">Email address</label>
          <div class="mt-2">
            <input type="text" placeholder="akira@karatsubalabs.com" class="input input-bordered focus:input-secondary w-full " />
          </div>
        </div>

        <div>
          <label for="password" class="block text-sm font-medium leading-6 text-gray-900">Password</label>
          <div class="mt-2">
            <input type="password" placeholder="********" class="input input-bordered focus:input-secondary w-full" />
          </div>
        </div>

        <div>
          <button class="btn btn-primary btn-block">Sign In</button>
        </div>
      </form>

      <p class="mt-10 text-center text-sm text-gray-500">
        Not a member?
        <a href="/signup" class="font-semibold leading-6 text-lime-600 hover:text-lime-500">Sign up</a>
      </p>
    </div>
  </div>
</template>