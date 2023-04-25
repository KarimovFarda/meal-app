<template>
  <div class="p-8 pb-0">
    <input
      type="text"
      v-model="keyword"
      class="rounded border-2 border-gray-200 w-full"
      placeholder="Search for Meals"
      @change="searchMeals"
    />
  </div>
  <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
    <MealItem v-for="meal of meals" :key="meal.idMeal" :meal="meal" />
  </div>
</template>


<script setup>
import { computed, onMounted, ref } from "vue";
import axiosClient from "../axiosClient.JS";
import store from "../store";
import { useRoute } from "vue-router";
import YoutubeButton from "../components/YoutubeButton.vue";
import MealItem from "../components/MealItem.vue";

const keyword = ref("");
const meals = computed(() => store.state.searchedMeals);
const route = useRoute();
function searchMeals() {
  if (keyword.value) {
    store.dispatch("searchMeals", keyword.value);
  } else {
    store.dispatch("setSearchedMeals", []);
  }
}

onMounted(() => {
  keyword.value = route.params.name;
  if (keyword.value) {
    searchMeals();
  }
});
</script>