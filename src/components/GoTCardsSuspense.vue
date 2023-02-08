<script setup>
import ThronesCards from "./ThronesCards.vue";
</script>

<template>
  <Suspense>
    <template #default>
      <ThronesCards />
    </template>
    <template #fallback>
      <div class="cards spinner">
        <NSpin size="large" />
      </div>
    </template>
  </Suspense>
</template>

<style scoped>
.cards {
  height: 700px;
  background-color: rgb(27, 32, 29);
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
