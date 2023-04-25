<template>
  <div class="p-8">
    <h1 class="text-4xl font-bold mb-4">Ingredients</h1>
    <router-link
      :to="{
        name: 'byIngredient',
        params: { ingredient: ingredient.strIngredient },
      }"
      v-for="ingredient of computedIngredients"
      :key="ingredient.idIngredient"
      class="block bg-white rounded p-3 mb-3 shadow"
    >
      <h3 class="text-2xl font-bold mb-2">{{ ingredient.strIngredient }}</h3>
      <p>{{ ingredient.strDescription }}</p>
    </router-link>
    <!-- <MealItem v-for="meal of meals" :key="meal.idMeal" :meal="meal" /> -->
  </div>
  <!-- <div v-if="!meals.length" class="flex justify-center">There are no meals</div> -->
</template>


<script setup>
import { onMounted, ref, computed } from "vue";
import axiosClient from "../axiosClient";
import { useRoute } from "vue-router";
import store from "../store";

const ingredients = ref([]);
const route = useRoute();
const meals = computed(() => store.state.mealsByIngredient);
const keyword = ref("");
const computedIngredients = computed(() => {
  if (!computedIngredients) return ingredients;
  return ingredients.value.filter((i) =>
    // i.strDescription.toLowerCase().includes(keyword.value.toLowerCase()) ||
    i.strIngredient.toLowerCase().includes(keyword.value.toLowerCase())
  );
});

// grid grid-cols-1 md:grid-cols-3 gap-5
onMounted(() => {
  // store.dispatch("searchMealsByIngredient", route.params.ingredient);
  axiosClient.get("list.php?i=list").then(({ data }) => {
    ingredients.value = data.meals;
  });
});
</script>