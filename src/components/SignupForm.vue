<script setup lang="ts">

import type {Ref} from "vue";
import {ref} from "vue";

const emailError: Ref<boolean> = ref(false);
const passwdError: Ref<boolean> = ref(false);
const passwdConfirmError: Ref<boolean> = ref(false);

let email: string = "";

function checkEmail(): boolean {

  if(email.length == 0) return true;
  else return email.match(/.+@.+\..+/g) == null;

}

</script>



<template>
  <div class="flex min-h-full flex-col justify-center px-6 py-12 lg:px-8">
    <div class="sm:mx-auto sm:w-full sm:max-w-sm">
      <h2 class="mt-8 text-center text-2xl font-bold leading-9 tracking-tight text-gray-900">Create an account</h2>
    </div>

    <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
      <div class="space-y-6">
        <div>
          <label for="email" class="label text-sm font-medium leading-6 text-gray-900">
            Email address
            <span class="label-text-alt text-error">Bottom Right label</span>
          </label>
          <div class="mt-2">
            <input type="text" placeholder="akira@karatsubalabs.com" class="input input-bordered focus:input-secondary w-full" :class="{'input-error': emailError}" v-model="email" @focusin="emailError = false" @focusout="emailError = checkEmail()"/>
          </div>
        </div>

        <div>
          <label for="password" class="label text-sm font-medium leading-6 text-gray-900">
            Password
            <span class="label-text-alt text-error">Bottom Right label</span>
          </label>
          <div class="mt-2">
            <input type="password" placeholder="••••••••" class="input input-bordered focus:input-secondary w-full" :class="{'input-error': passwdError}" />
          </div>
        </div>

        <div>
          <label for="confirm-password" class="label text-sm font-medium leading-6 text-gray-900">
            Confirm Password
            <span class="label-text-alt text-error">Bottom Right label</span>
          </label>
          <div class="mt-2">
            <input type="password" placeholder="••••••••" class="input input-bordered focus:input-secondary w-full" :class="{'input-error': passwdConfirmError}" />
          </div>
        </div>

        <div>
          <button class="btn btn-primary btn-block">Register</button>
        </div>
      </div>

      <p class="mt-10 text-center text-sm text-gray-500">
        Already a member?
        <a href="/login" class="font-semibold leading-6 text-lime-600 hover:text-lime-500">Sign in</a>
      </p>
    </div>
  </div>
</template>



<style scoped lang="scss">

.label {
  padding: 0;
}

</style>