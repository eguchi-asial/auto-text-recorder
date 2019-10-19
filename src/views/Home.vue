<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import Component from "vue-class-component";
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default class Home extends Vue {
  msg: string = "Hello";
}
</script>
