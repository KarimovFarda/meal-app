<template>
  <div class="flex justify-center gap-2 mt-2">
    <router-link
      :to="{ name: 'byLetter', params: { letter } }"
      v-for="letter of letters"
      :key="letter"
    >
      {{ letter }}</router-link
    >
  </div>
  <Meals :meals="meals" />
</template>

<script setup>
import { computed, onMounted, watch } from "vue";
import store from "../store";
import { useRoute } from "vue-router";
import MealItem from "../components/MealItem.vue";
import Meals from "../components/Meals.vue";

const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("");
const meals = computed(() => store.state.mealsByLetter);
const route = useRoute();

// <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
//   <MealItem v-for="meal of meals" :key="meal.idMeal" :meal="meal" />
// </div>

watch(route, () => {
  store.dispatch("searchMealsByLetter", route.params.letter);
});

onMounted(() => {
  store.dispatch("searchMealsByLetter", route.params.letter);
});
</script>