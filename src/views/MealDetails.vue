<template>
  <div class="w-[800px] mx-auto p-8">
    <h1 class="text-5xl font-bold mb-5">{{ meal.strMeal }}</h1>
    <img :src="meal.strMealThumb" :alt="meal.strMeal" class="max-w-[100%]" />
    <div class="grid grid-cols-1 sm:grid-cols-3 text-lg py-2">
      <div><strong>Category :</strong> {{ meal.strCategory }}</div>
      <div><strong>Area : </strong>{{ meal.strArea }}</div>
      <div><strong>Tags : </strong>{{ meal.strTags }}</div>
    </div>
  </div>
  <div class="my-3">{{ meal.strInstructions }}</div>
  <div class="grid grid-cols-1 sm:grid-cols-2">
    <div>
      <h2 class="text-2xl font-semibold mb-3">Ingredients</h2>
      <ul>
        <template v-for="(el, ind) of new Array(20)" :key="ind">
          <li v-if="meal[`strIngredient${ind + 1}`]">
            {{ ind + 1 }}. {{ meal[`strIngredient${ind + 1}`] }}
          </li>
        </template>
      </ul>
    </div>
    <div>
      <h2 class="text-2xl font-semibold mb-3">Measures</h2>
      <ul>
        <template v-for="(el, ind) of new Array(20)" :key="ind">
          <li v-if="meal[`strMeasure${ind + 1}`]">
            {{ ind + 1 }}. {{ meal[`strMeasure${ind + 1}`] }}
          </li>
        </template>
      </ul>
    </div>
    <div class="mt-4">
      <YoutubeButton href="meal.strYoutube">Go To Youtube</YoutubeButton>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import axiosClient from "../axiosClient";
import YoutubeButton from "../components/YoutubeButton.vue";

const meal = ref({});
const route = useRoute();

onMounted(() => {
  axiosClient.get(`lookup.php?i=${route.params.id}`).then(({ data }) => {
    meal.value = data.meals[0];
    console.log(data);
  });
});
</script>