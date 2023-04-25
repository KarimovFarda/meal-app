<template>
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
onMounted(() => {
  store.dispatch("searchMealsByIngredient", route.params.ingredient);
});
</script> 