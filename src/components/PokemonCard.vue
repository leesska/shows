<script setup>
import { ref, watch } from "vue";
import axios from "axios";
import Card from "../components/Card.vue";

const characters = ref(null);
const page = ref();

const limit = 4;

watch(page, async () => {
  const res = await axios.get(
    `https://pokeapi.co/api/v2/pokemon/?limit=${limit}&offset=${
      page.value * limit
    }`
  );
  characters.value = res.data.results;
  console.log(characters.value);
});

page.value = 0;
</script>

<template>
  <div class="container">
    <div class="cards">
      <Card
        v-for="character in characters"
        :key="character.name"
        :name="character.name"
      />
      {{ characters }}
    </div>
    <div class="button-container">
      <button @click="page--">&lt;</button>
      <button @click="page++">></button>
    </div>
  </div>
</template>

<style scoped>
.container {
  background-color: rgb(27, 26, 26);
  padding: 30px;
}
.cards {
  max-width: 1000px;
  margin: 0 auto;
  display: flex;
  flex-wrap: wrap;
  height: 700px;
}
.cards h3 {
  font-weight: bold;
}
.cards p {
  font-size: 10px;
}
.jobs {
  display: flex;
  flex-wrap: wrap;
}
.button-container {
  display: flex;
  justify-content: center;
  padding-top: 30px;
}
.button-container button {
  border: none;
  width: 50px;
  height: 50px;
  border-radius: 100%;
  margin: 0 5px;
  cursor: pointer;
}
.spinner {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
