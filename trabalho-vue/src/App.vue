<script setup>
import { useRoute } from "vue-router"
import HelloWorld from "@/components/icons/IconCommunity.vue"


const route = useRoute()





</script>



<template>



<nav v-if="route.path !== '/'">
    <RouterLink to="/">Login</RouterLink>
    <RouterLink to="/home">Home</RouterLink>
    <RouterLink to="/about">About</RouterLink>
  </nav>
  <RouterView></RouterView>


<HelloWorld v-if="route.path !== '/'"/>







</template>


<style></style>