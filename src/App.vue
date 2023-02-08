<script setup>
import { ref } from "vue";
import GoTCardsSuspense from "./components/GoTCardsSuspense.vue";
import RickAndMortyCards from "./components/RickAndMortyCards.vue";
import Hero from "./components/Hero.vue";

const isGoT = ref(true);
</script>

<template>
  <main>
    <Hero :isGoT="isGoT" @selectShow="isGoT = !isGoT" />
    <KeepAlive>
      <Component :is="isGoT ? GoTCardsSuspense : RickAndMortyCards" />
    </KeepAlive>
  </main>
</template>

<style scoped></style>
