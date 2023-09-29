<script setup lang="ts">

import type {Ref} from "vue";
import {ref} from "vue";
import {apiPrefix} from "@/config";
import {useRouter} from "vue-router";

const emailError: Ref<string> = ref("");
const passwdError: Ref<string> = ref("");
const genericError: Ref<string> = ref("");

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

function login() {

  genericError.value = ""

  checkEmail()
  checkPassword()

  if(emailError.value.length != 0 || passwdError.value.length != 0) {
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

  fetch(apiPrefix + '/auth/login', requestOptions)
      .then(response => {

        if(response.ok) {
          response.json().then(result => {
            localStorage.setItem('authToken', result)
            useRouter().push('/dashboard');
          })
        }
        else if(response.status == 401) genericError.value = "Incorrect email or password"
        else genericError.value = ("Login failed: " + response.status)

      })

}

function sendFocus(id: string) {
  (document.activeElement as HTMLElement).blur()
  document.getElementById(id)!.focus()
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
            <input type="text" placeholder="akira@karatsubalabs.com" class="input input-bordered focus:input-secondary w-full" :class="{'input-error': emailError.length}" v-on:keyup.enter="sendFocus('inputPasswd')" v-model="email" @focusin="emailError = ''" @focusout="emailError = checkEmail()" />
          </div>
        </div>

        <div>
          <label for="password" class="label text-sm font-medium leading-6 text-gray-900">
            Password
            <span class="label-text-alt text-error" v-show="passwdError.length != 0">{{passwdError}}</span>
          </label>
          <div class="mt-2">
            <input type="password" placeholder="••••••••" class="input input-bordered focus:input-secondary w-full" :class="{'input-error': passwdError}" id="inputPasswd" v-on:keyup.enter="(e) => {(e.target as HTMLElement).blur(); login()}" v-model="password" @focusin="passwdError = ''" @focusout="passwdError = checkPassword()" />
          </div>
        </div>

        <div>
          <p class="text-center text-error" v-show="genericError.length != 0">{{genericError}}</p>
        </div>

        <div>
          <button class="btn btn-primary btn-block" id="btnLogin" @click="login()">Sign In</button>
        </div>
      </div>

      <p class="mt-10 text-center text-sm text-gray-500">
        Not a member?
        <a href="/signup" class="font-semibold leading-6 text-lime-600 hover:text-lime-500">Sign up</a>
      </p>
    </div>
  </div>
</template>