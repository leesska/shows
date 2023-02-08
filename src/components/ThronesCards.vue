<script setup>
import { ref, watch } from "vue";
import axios from "axios";
import Card from "@/components/Card.vue";

const characters = ref(null);
let page = ref(1);

const characterPerPage = 8;
const response = await axios.get(
  "https://thronesapi.com/api/v2/Characters",
  {}
);

const getSubArray = (dataset, limitOfData, offset = 0) => {
  return dataset.filter((c) => c.id >= offset && c.id < offset + limitOfData);
};
characters.value = getSubArray(
  response.data,
  characterPerPage,
  characterPerPage * (page.value - 1)
);

watch(page, () => {
  characters.value = getSubArray(
    response.data,
    characterPerPage,
    characterPerPage * (page.value - 1)
  );
});

// const characters = ref(null);
// const page = ref();

// const limit = 4;

// watch(page, async () => {
//   const res = await axios.get("https://thronesapi.com/api/v2/Characters/", {});
//   characters.value = res.data;
//   console.log(res);
// });

// page.value = 0;
</script>

<template>
  <div class="container">
    <div class="cards">
      <Card
        v-for="character in characters"
        :key="character.id"
        :name="character.fullName"
        :image="character.imageUrl"
      >
        <p>
          {{ character.title }}
        </p>
      </Card>
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
  max-width: 70%;
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
