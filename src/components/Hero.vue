<script setup>
import { defineProps, defineEmits } from "vue";
const { isGoT } = defineProps(["isGoT"]);
const emit = defineEmits(["selectShow"]);

const emitSelectedShow = () => {
  emit("selectShow");
};
</script>

<template lang="">
  <div class="hero">
    <h1>{{ isGoT ? "Game of Thrones" : "Rick and Morty" }}</h1>
    <p @click="emitSelectedShow">
      {{ isGoT ? "Rick and Morty" : "Game of Thrones" }}
    </p>
  </div>
</template>

<style scoped>
.hero {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  flex-direction: column;
}
.hero img {
  position: absolute;
  height: 700px;
  opacity: 0.1;
}
.hero h1 {
  font-size: 100px;
  font-weight: bold;
}
.hero p {
  cursor: pointer;
}
</style>
