<template>
  <!-- <div class="p-8">
    <h1 class="text-4xl font-bold mb-4">Ingredients</h1>
    <router-link
      :to="{
        name: 'byIngredient',
        param: { ingredient: ingredient.idIngredient },
      }"
      v-for="ingredient of ingredients"
      :key="ingredient.idIngredient"
      class="block bg-white rounded p-3 mb-3 shadow"
    >
      <h3 class="text-2xl font-bold mb-2">{{ ingredient.strIngredient }}</h3>
      <p>{{ ingredient.strDescription }}</p>
    </router-link>
  </div> -->
  <Meals :meals="meals" />
</template>


<script setup>
import { onMounted, ref, computed } from "vue";
import axiosClient from "../axiosClient";
import { useRoute } from "vue-router";
import store from "../store";
import Meals from "../components/Meals.vue";

const ingredients = ref([]);
const route = useRoute();
const meals = computed(() => store.state.mealsByIngredient);
// grid grid-cols-1 md:grid-cols-3 gap-5
onMounted(() => {
  store.dispatch("searchMealsByIngredient", route.params.ingredient);
  // axiosClient.get("list.php?i=list").then(({ data }) => {
  //   ingredients.value = data.meals;
  //   console.log(data);
  // });
});
</script> 