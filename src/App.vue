<script setup>
import { RouterLink, RouterView } from "vue-router";
import HelloWorld from "./components/HelloWorld.vue";

</script>

<template>
  <div class="container">

    <HelloWorld />
    
    <RouterView />
  </div>
</template>

<style scoped>
.container{
  max-width: 1200px;
  margin: auto;
  padding: 10px;
}
</style>
