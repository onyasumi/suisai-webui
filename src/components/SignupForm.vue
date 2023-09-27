<script setup lang="ts">

import type {Ref} from "vue";
import {ref} from "vue";
import {apiPrefix} from "@/config";
import {useRouter} from "vue-router";

const emailError: Ref<string> = ref("");
const passwdError: Ref<string> = ref("");
const passwdConfirmError: Ref<string> = ref("");

let email: string = "";
let password: string = "";
let confirm: string = "";

function checkEmail() {

  if(email.length == 0) emailError.value = "Please enter your email";
  else if(email.match(/.+@.+\..+/g) == null) emailError.value = "Invalid email";
  else emailError.value = "";

}

function checkPassword() {

  if(password.length == 0) passwdError.value = "Please provide a password";
  else passwdError.value = "";

}

function confirmPassword() {

  if(password != confirm) passwdConfirmError.value = "Passwords do not match";
  else passwdConfirmError.value = "";

}

function signup() {

  checkEmail()
  checkPassword()
  confirmPassword()

  if(emailError.value.length != 0 || passwdError.value.length != 0 || passwdConfirmError.value.length != 0) {
    console.log("Input Error")
    return
  }

  const requestOptions = {
    method: 'POST',
    headers: {'Content-Type': 'application/json'},
    body: JSON.stringify({
      email: email,
      password: password
    })
  }

  fetch(apiPrefix + '/auth/signup', requestOptions)
      .then(response => {

        if(response.ok) {
          response.json().then(result => {
            localStorage.setItem('authToken', result)
            useRouter().push('/dashboard');
          })
        }
        else if(response.status == 409) emailError.value = "Email taken"
        else alert("Registration failed: " + response.status)

      })

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
            <span class="label-text-alt text-error" v-show="emailError.length != 0">{{emailError}}</span>
          </label>
          <div class="mt-2">
            <input type="text" placeholder="akira@karatsubalabs.com" class="input input-bordered focus:input-secondary w-full" :class="{'input-error': emailError.length}" v-model="email" @focusin="emailError = ''" @focusout="checkEmail()" />
          </div>
        </div>

        <div>
          <label for="password" class="label text-sm font-medium leading-6 text-gray-900">
            Password
            <span class="label-text-alt text-error" v-show="passwdError.length != 0">{{passwdError}}</span>
          </label>
          <div class="mt-2">
            <input type="password" placeholder="••••••••" class="input input-bordered focus:input-secondary w-full" :class="{'input-error': passwdError}" v-model="password" @focusin="passwdError = ''" @focusout="checkPassword()" />
          </div>
        </div>

        <div>
          <label for="confirm-password" class="label text-sm font-medium leading-6 text-gray-900">
            Confirm Password
            <span class="label-text-alt text-error" v-show="passwdConfirmError.length != 0">{{passwdConfirmError}}</span>
          </label>
          <div class="mt-2">
            <input type="password" placeholder="••••••••" class="input input-bordered focus:input-secondary w-full" :class="{'input-error': passwdConfirmError}" v-model="confirm" @focusin="passwdConfirmError = ''" @focusout="confirmPassword()" />
          </div>
        </div>

        <div>
          <button class="btn btn-primary btn-block" @click="signup()">Register</button>
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