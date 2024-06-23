<script setup lang="ts">
import { ref } from "vue";
import { invoke } from "@tauri-apps/api/core";

const greetMsg = ref("");
const name = ref("");

const greetMsg_s = ref("");
const name_s= ref("");

async function greet_vue() {
  // Learn more about Tauri commands at https://tauri.app/v1/guides/features/command
  greetMsg.value = await invoke("greet_rust", { name: name.value });
}

async function greet_vue_s() {
  // Learn more about Tauri commands at https://tauri.app/v1/guides/features/command
  greetMsg_s.value = await invoke("greet_rust_s", { name: name_s.value });
}

</script>

<template>
  <form class="row" @submit.prevent="greet_vue">
    <input id="greet-input" v-model="name" placeholder="Enter a name..." />
    <button type="submit">Greet</button>
  </form>

  <p>{{ greetMsg }}</p>

  <form class="row" @submit.prevent="greet_vue_s">
    <input id="greet-input" v-model="name_s" placeholder="Enter a name..." />
    <button type="submit">Greet</button>
  </form>

  <p>{{ greetMsg_s }}</p>

</template>
