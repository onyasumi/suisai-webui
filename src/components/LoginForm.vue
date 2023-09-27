<script setup lang="ts">

import type {Ref} from "vue";
import {ref} from "vue";

const emailError: Ref<string> = ref("");
const passwdError: Ref<string> = ref("");

let email: string = "";
let password: string = "";

function checkEmail(): string {

  if(email.length == 0) return "Please enter your email";
  else if(email.match(/.+@.+\..+/g) == null) return "Invalid email";
  else return "";

}

function checkPassword(): string {

  if(password.length == 0) return "Please enter your password";
  else return "";

}

</script>

<template>
  <div class="flex min-h-full flex-col justify-center px-6 py-12 lg:px-8">
    <div class="sm:mx-auto sm:w-full sm:max-w-sm">
      <h2 class="mt-10 text-center text-2xl font-bold leading-9 tracking-tight text-gray-900">Sign in to your account</h2>
    </div>

    <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
      <div class="space-y-6">
        <div>
          <label for="email" class="label text-sm font-medium leading-6 text-gray-900">
            Email address
            <span class="label-text-alt text-error" v-show="emailError.length != 0">{{emailError}}</span>
          </label>
          <div class="mt-2">
            <input type="text" placeholder="akira@karatsubalabs.com" class="input input-bordered focus:input-secondary w-full" :class="{'input-error': emailError.length}" v-model="email" @focusin="emailError = ''" @focusout="emailError = checkEmail()" />
          </div>
        </div>

        <div>
          <label for="password" class="label text-sm font-medium leading-6 text-gray-900">
            Password
            <span class="label-text-alt text-error" v-show="passwdError.length != 0">{{passwdError}}</span>
          </label>
          <div class="mt-2">
            <input type="password" placeholder="••••••••" class="input input-bordered focus:input-secondary w-full" :class="{'input-error': passwdError}" v-model="password" @focusin="passwdError = ''" @focusout="passwdError = checkPassword()" />
          </div>
        </div>

        <div>
          <button class="btn btn-primary btn-block">Sign In</button>
        </div>
      </div>

      <p class="mt-10 text-center text-sm text-gray-500">
        Not a member?
        <a href="/signup" class="font-semibold leading-6 text-lime-600 hover:text-lime-500">Sign up</a>
      </p>
    </div>
  </div>
</template>